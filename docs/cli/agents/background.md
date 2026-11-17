# `ed agents background`

Keeps the Herdr sessions Edith starts running after Edith quits. Edith stops
every process an extension starts when the extension stops, so a Herdr server
that Edith launched used to end with Edith, and its agents with it. With
background sessions on, Edith hands each session it starts to launchd instead.
The Background section of the Agents settings page edits the same setting.

```
ed agents background [status] [--json]
ed agents background on [--json]
ed agents background off [--json]
ed agents background start [--session <name>] [--json]
```

`ed agents background` runs `ed agents background status`.

## Subcommands

| Subcommand | What it does |
| --- | --- |
| `status` | Whether background sessions are on, and which sessions have a launchd job |
| `on` | Turn background sessions on. The next session Edith starts runs under launchd |
| `off` | Turn them off and remove the session jobs. Running sessions keep going until you stop them or log out |
| `start` | Start one session under launchd now and wait for its server |

## `start` options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--session <name>` | a Herdr session name | the default session | The session to start. `default` is the default session |
| `--json` | flag | off | Emit JSON on stdout |

`start` leaves a session that is already running alone, even one that some
other app started. Its JSON then reports `managed: false`: that server still
stops when the app that started it quits. Stop it with
`herdr --session <name> server stop` and run `start` again to move it under
launchd.

## How a session runs

Each session gets one LaunchAgent in `~/Library/LaunchAgents`, labelled
`com.pulkit.edith.agents.default` for the default session and
`com.pulkit.edith.agents.session-<name>` for a named one (a name with other
characters becomes a short hash). The job:

- runs `herdr [--session <name>] server`, so the server is the job's own
  process and its parent is launchd, not Edith
- starts again at login, and after a crash, but stays stopped after
  `herdr server stop`
- exits without doing anything when Herdr is no longer installed or a server
  for that session is already running
- carries only `PATH`, `SHELL` and `LANG` from your login shell. Pane shells
  read your shell startup files as usual, so agents see your full environment
- shows under Edith in System Settings > General > Login Items

CPU and memory used by the server and its agents are billed to Herdr, not to
Edith.

Background sessions are on by default in Edith and off in development builds.
If macOS refuses the job, usually because Edith is switched off in Login
Items, `status` reports the error and Edith falls back to starting the server
itself, which stops with Edith.

## `--json` shape

```json
{
  "available": true,
  "enabled": true,
  "error": null,
  "message": "Running in the background: default, work. Agents keep working after Edith quits and start again when you log in.",
  "sessions": ["default", "work"]
}
```

`start --json` adds `session`, `running` and `managed`.

## Exit codes

| Code | When |
| --- | --- |
| 0 | The status printed, the setting changed, or the session is running |
| 4 | The Agents extension is not running, background sessions are off, Herdr is not installed, or macOS refused the job |

Examples:

```
ed agents background
ed agents background on
ed agents background start --session work --json
ed agents background off
```

## Where to go next

- [`ed agents ls`](./ls.md), the sessions that are live now
- [`ed agents`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
