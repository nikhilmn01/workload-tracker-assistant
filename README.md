# Workload Tracker assistant

A calm, discreet time assistant. Tell Claude what just landed on you and it answers from your own schedule: can you
take it, which day, which route, and what it costs. It also shows your week, closes finished work with what it really
took, and keeps your estimates honest.

## On your phone, the web or Claude Desktop: the connector

Add the connector once at **claude.ai → Customize → Connectors → Add custom connector**, paste the address, then
press **Connect** and sign in to Google. It then works in the Claude phone, web and desktop apps.

```
https://workload-tracker-connector.nikhilmn01.workers.dev/mcp
```

- It reads and writes your plan in your own Google Drive: the same copy the Workload Tracker website uses when Sync
  across devices is on.
- Free plan: one custom connector.
- Testing mode: you must be on the owner's test list, and you reconnect every 7 days.
- Day planner: the `workload-day` skill (its text is `assistant/hosted/skill/SKILL.md` in the app's source) has
  Claude log your tasks and lead your day through the connector; add it under Customize → Skills, or paste it into a
  project's instructions.

## The local plugin, for a workload.json on your computer

### Claude Code

```
/plugin marketplace add nikhilmn01/workload-tracker-assistant
/plugin install workload-tracker@workload-tracker
```

Set `WT_FILE` to the full path of your `workload.json` before you start Claude Code (or save a `config.json`, below).
Then try `/week`.

### Claude Desktop

Download `workload-tracker-<version>.mcpb` from this repo's
[Releases](https://github.com/nikhilmn01/workload-tracker-assistant/releases) and open it in Claude Desktop. Choose
your file under **Your workload.json** (required) and leave **Where your data lives** as `file`.

### Cursor, Gemini CLI, VS Code and other MCP clients

Get this folder (clone this repo, or download it as a zip), then add the server to your client's MCP settings, with
the full paths in place of `<folder>` and `<your workload.json>`:

```json
{
  "mcpServers": {
    "workload-tracker": {
      "command": "node",
      "args": ["<folder>/assistant/server.js"],
      "env": { "WT_FILE": "<your workload.json>" }
    }
  }
}
```

- Cursor: `~/.cursor/mcp.json`, or `.cursor/mcp.json` in a project.
- Gemini CLI: `~/.gemini/settings.json`.
- VS Code: `.vscode/mcp.json`, with the top-level key `servers` instead of `mcpServers`.

The server needs Node 22 or later and nothing else. The skill (`skills/time-assistant/`) is a plain Agent Skills
folder: copy it to wherever your tool reads skills from.

### Your file

- It must be the **full path**: a relative one is refused. Paths with spaces are fine. In JSON, write Windows paths
  with forward slashes (`C:/Users/you/workload.json`) or doubled backslashes.
- For a client that passes no environment variables, save `config.json` in the config folder as
  `{ "storage": "file", "file": "<the full path to your workload.json>" }`. The config folder is
  `%APPDATA%\workload-tracker` on Windows, and `$XDG_CONFIG_HOME/workload-tracker` or `~/.config/workload-tracker`
  elsewhere.
- While you try it out, point it at a **copy** of your file.

### Google Drive from the local plugin

Most people should use the connector above for their Google Drive copy. The local plugin signs in to Google only
when you set storage to `drive` (`WT_STORAGE=drive`) and the Desktop client's secret is in the server's environment
as `GOOGLE_DESKTOP_CLIENT_SECRET`. No download carries it.

- Drive isn't available in Claude Desktop: it can't pass that secret to the extension. Use the connector there.
- In Claude Code (the plugin's `.mcp.json`), drive needs `GOOGLE_DESKTOP_CLIENT_SECRET` in the environment Claude Code
  passes to the server. Claude Code may pass it from the shell you start it in; this is not verified yet.
- Your Google account must be on the app's test user list while the app is in Google's testing mode.
- Your sign-in is kept in the config folder as `google-token.json`, readable only by you. To switch account, delete
  that file and ask again.
- While storage is `drive`, a picked file is ignored. Set storage back to `file` (the default) to use the file.

## What is inside

- **The `time-assistant` skill**: how to answer time and capacity questions, never with a bare yes or no, and with a
  yes from you before anything that moves other work, runs a day long or makes a promise late.
- **Commands**: `/week`, `/take <what>`, `/done <what>`, `/brief` (morning) and `/wrapup` (evening).
- **The workload-tracker MCP server**, bundled into one file (`assistant/server.js`).

## How it treats your data

- It keeps no copy between calls: every answer reads your data again, and every write checks that it has not changed
  underneath it.
- It never runs git. If the folder holding your `workload.json` has its own `CLAUDE.md` (for example, "commit and
  push after every change"), Claude follows it around a write.
- Answers never show internal task ids.

## Licence

PolyForm Noncommercial License 1.0.0 ([LICENSE](LICENSE)): free to use, share and change for any noncommercial purpose.
The open-source packages bundled into the server keep their own licences, listed in THIRD-PARTY-NOTICES.
