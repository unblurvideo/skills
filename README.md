# UnblurVideo skill

Use UnblurVideo from an AI agent with the product's existing authorization and usage rules.

[Website](https://unblurvideo.com/) · [Agent setup](https://unblurvideo.com/docs/agents)

## Install

With Node.js 22.20 or newer and npm available, install the skill using the skills CLI:

```sh
npx skills add unblurvideo/skills --skill unblurvideo
```

Select your supported agent and installation scope in the installer. Restart your agent session after installation. This installs instructions; it does not connect MCP, install the product CLI, sign you in or grant access. Follow [Agent setup](https://unblurvideo.com/docs/agents) to connect the product.

Alternatively, use the existing npm installer:

```sh
npx unblurvideo-client skill install --target codex
# Or use --target grok
```

Choose one installer for this skill so two copies do not drift. For CLI usage, install `unblurvideo-client` separately and follow the setup documentation. Credentials belong in your secret store, never in this repository.

## Updates

For an installation managed by the skills CLI, use `npx skills update unblurvideo`. Choose the same project or global scope used during installation. Review any local edits before updating. For the npm installer, rerun its install command; it protects modified files.

## Usage and support

Uses existing UnblurVideo credits. A 3-second preview costs 6 credits. Full-video price depends on verified duration and resolution; request a quote. Failed processing restores credits. Agent connections cannot purchase credits.

Installing the skill is free. Product calls follow the site's account, authorization and billing rules. For setup and product support, see [the documentation](https://unblurvideo.com/docs/agents).

Skill source version: 0.2.0. MIT licensed; see [LICENSE](LICENSE).
