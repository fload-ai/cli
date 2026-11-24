# Fload CLI

Your mobile apps from a terminal. Downloads, revenue, reviews, keywords, competitors, ads and reports, for your App Store and Google Play apps.

The `fload` command uses the same tools your AI assistant reaches through [Fload's MCP server](https://github.com/fload-ai/mcp), with the same API key, permissions and approvals. Anything that changes something, such as a review reply, a listing change or an ad bid, becomes a card in your Fload inbox for a person to approve. Nothing reaches a store straight from your terminal.

## Install

Needs Node.js 20 or later.

```sh
npm install -g @fload-ai/cli
fload login          # paste an API key from Settings > API keys in Fload
fload whoami         # which server, which key, what it can do
```

`fload login` saves the key in `~/.fload/config.json`, readable only by you. The Fload MCP server reads the same file, so one login serves both. In scripts and CI, set `FLOAD_API_KEY` instead.

## Use it

```sh
fload apps                                   # your apps, App Store and Google Play
fload use "Pocket Budget"                    # the app the next commands are about
fload week                                   # the week at a glance
fload metrics downloads revenue --last-n-days 30
fload keywords                               # tracked keywords and where you rank
fload competitors
fload reviews --rating 1                     # newest first
fload reviews reply <review-id> "Thanks, a fix ships Friday."   # staged for approval
fload ads campaigns                          # Apple Ads, Google, Meta and TikTok
fload ads wasted                             # Apple Ads keywords that spend without installs
fload reports export <report-id> > audit.md
fload approvals                              # cards waiting for a person
fload approvals approve <action-id> <revision-id>
```

Every command takes `--help`, `--json` (the answer exactly as the MCP server returns it) and, where it's about one app, `--app <name, bundle id or id>`. `fload help` lists them all.

### Every tool, not just the commands above

```sh
fload tool list                  # every tool your key is offered
fload tool getReviews --help     # a tool's flags
fload tool getReviews --limit 20
```

The CLI builds each tool's flags from the server's own description of it, so a tool added to Fload is a command the same day.

## Exit codes

| Code | Meaning |
| ---- | ------- |
| 0 | OK (a staged card counts as OK) |
| 1 | The tool refused or failed |
| 2 | Bad command, flag or value, or the tool isn't offered to this key |
| 3 | No key, or Fload refused it |
| 4 | The key lacks the permission |
| 5 | The app wasn't found |
| 6 | Rate limited (120 calls a minute per key) |
| 7 | Fload unreachable |

## Links

- npm: [@fload-ai/cli](https://www.npmjs.com/package/@fload-ai/cli)
- Fload's MCP server: [fload-ai/mcp](https://github.com/fload-ai/mcp)
- Free skills for app growth: [fload-ai/mobile-app-skills](https://github.com/fload-ai/mobile-app-skills)
- Fload: [fload.com](https://fload.com)

Questions or bugs: open an issue here.
