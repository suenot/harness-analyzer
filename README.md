# Harness Analyzer

**Know where your agent budget goes.** Harness Analyzer turns local AI coding usage logs into cost, token, cache, and session analytics. Use the CLI without an account, or sync private statistics to [the hosted dashboard](https://harness-analyzer.marketmaker.cc/) to see usage across devices.

![Four-panel comic: a developer struggles with scattered AI coding costs, analyzes usage on a laptop, sends statistics while conversation text stays on the laptop, then sees a clear budget dashboard.](assets/why-harness-analyzer.png)

*From scattered usage logs to a clear picture of what your coding agents cost. The comic shows standard sync; conversation history is an explicit opt-in.*

## Why use it?

- See spending, tokens, sessions, and cache behavior across Claude Code, Codex, and other supported local tools.
- Compare models, projects, and time periods without manually combining logs from each tool.
- Keep a private view across computers while choosing separately whether to share any public profile statistics.

## Get started

Requires Node.js 20 or newer.

```bash
npm install -g harness-analyzer
harness-analyzer summary
```

The CLI also offers `today`, `week`, `month`, `projects`, and `sessions`. These local reports do not need a hosted account.

Model names come from local logs. Token usage for a model without a known price is still shown, but its USD estimate is $0 until that model has a rate. USD figures are estimates, not billing records; subscription charges, service tiers, and long contexts may differ.

To sync with the website:

1. Sign in at [Profile](https://harness-analyzer.marketmaker.cc/profile) and create a CLI sync token.
2. Run the commands below. `login` prompts for the token; `sync` uploads the first statistics snapshot.

```bash
harness-analyzer login
harness-analyzer sync
```

On macOS, start automatic sync every 15 minutes after logging in:

```bash
harness-analyzer background start
```

`background start` is currently macOS-only. It runs the standard sync without conversation history. See the [CLI README](cli/README.md) for device names, server fleet use, and other options.

## What is uploaded?

Standard sync reads logs locally and sends **per-session usage statistics** to the server: date and time, source and model, token and cache counts, estimated cost, hourly usage, project folder names, and private device metadata (ID, name, platform, and architecture). The server stores these statistics and builds the signed-in dashboard. The device name defaults to the computer's hostname, so change it with `--device-name` if needed.

Standard sync does **not** upload conversation text, prompts, raw log files, file contents, full project paths, or original session IDs. Public sharing is separate and **private by default**; Profile controls what, if anything, appears publicly.

The optional `harness-analyzer sync --include-history` command **does upload conversation history**, which may contain private text. Use it only when that is intended. Automatic background sync never adds this flag.

## Development

This repository uses npm workspaces and Git submodules for `core`, `cli`, `backend`, and `frontend`.

```bash
git clone --recurse-submodules https://github.com/suenot/harness-analyzer.git
cd harness-analyzer
npm ci
npm run build
npm run dev
```

The frontend runs at `http://127.0.0.1:5173` and the API at `http://127.0.0.1:3001`. Without `DATABASE_URL`, the API uses an in-memory profile store for development. Private hosted features still require a Harness Analyzer account with access through the auth service.

| Workspace | Responsibility |
| --- | --- |
| [`core`](core/) | Collectors, pricing, analytics, and sync snapshot formats |
| [`cli`](cli/) | Local reports, login, sync, and macOS background scheduling |
| [`backend`](backend/) | API, private analytics storage, and public sharing controls |
| [`frontend`](frontend/) | Landing page and hosted dashboards |
