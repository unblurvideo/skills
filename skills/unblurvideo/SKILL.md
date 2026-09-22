---
name: unblurvideo
description: Enhance a user's existing SFW video with UnblurVideo, quote its credit cost, resume an asynchronous enhancement, retrieve its result, or delete uploaded files. Use only for videos the user has permission to process.
---

# UnblurVideo

Prefer remote MCP at https://unblurvideo.com/mcp. The operator signs in and
authorizes the requested actions. CLI and local stdio use UNBLURVIDEO_API_KEY
from the operator's secret store; keep it out of request files and logs.
Installation does not authenticate. Run `unblurvideo --help` for commands.

1. Establish the intended input video and whether the user wants a preview or
   full enhancement. Process only SFW footage the user has permission to use.
2. Read `unblurvideo_usage`. For a local MP4, call `unblurvideo_upload` with its
   filename and exact byte count. Send the raw file bytes to the returned PUT
   URL using a local HTTP client and the returned `transfer.headers`, with no account Authorization header or cookies.
   Keep the temporary URL private. After a lost response, use `unblurvideo_files`
   to find the upload; use `unblurvideo_upload` with only its `fileId` to renew an
   unused upload link. Never submit video bytes as MCP/base64 text.
   Read the input's `unblurvideo_file` metadata. Continue
   when the file is ready. Input and output expire after 24 hours.
3. Request `unblurvideo_quote` for the file, kind and preview start. Present its
   returned cost and obtain authorization for that work, reusing any explicit
   authorization already given. Preview and full enhancement use the same
   processing capability; results may not restore missing detail.
4. Call `unblurvideo_enhance` with the accepted credits, policy revision and a
   stable `request_id` saved before sending this intended job. Missing IDs are rejected. Reuse it after a lost response; keep the returned task ID.
5. Poll `unblurvideo_job` by task ID, with pauses between checks. Reconnect and
   query that same ID after a connection loss. A second authorized client for
   the same account can resume the task. Report the actual settlement and
   result. When succeeded, call `unblurvideo_result` and download the returned
   GET URL with a local HTTP client and the returned `transfer.headers`, without account credentials. Links expire
   after 10 minutes and stop working when the grant is revoked. Refresh a link
   through that action when needed. Claim success only when the result is usable.

For CLI actions, put the action arguments in JSON and run the relevant command
with `--request request.json`. Credentials belong only in the secret environment.
`UNBLURVIDEO_BASE_URL` selects an explicitly requested development origin.

An identical enhancement request ID resumes the existing task. A changed input
with the same ID conflicts. Never turn a timeout into a fresh paid job
automatically. On insufficient credits, stop and report the balance; connections
cannot buy credits. On an expired or revoked authorization, reconnect. Failed
processing restores credits; dissatisfaction with a successful result is not
an automatic refund.

Use `unblurvideo_delete` only for the user's intended file. It revokes access to
that input and related results; provider copies follow their own retention
policy. Manage grants at https://unblurvideo.com/connections. Revocation stops
future calls but does not undo a task already running.
