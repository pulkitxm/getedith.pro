# `ed code-review`

Discover and open Quinjet review workspaces through the same client, worktree
selection and launch-request builder as Edith's Quinjet page. Discovery can run
against this Mac or one configured SSH machine.

`ed code-review` defaults to `ed code-review projects`. A local or remote Quinjet CLI
must be installed and able to return its current JSON format. The Edith Quinjet
extension does not have to be enabled.

## At a glance

| Command | What it does |
| --- | --- |
| `ed code-review projects` | List recent projects and their worktrees |
| `ed code-review worktrees <path>` | List every worktree for a project or worktree path |
| `ed code-review open <path>` | Print the exact launch command without running it |
| `ed code-review launch <path>` | Run a standalone Quinjet process in the current terminal or cmux |
| `ed code-review status [session]` | Show one native session in the running Edith page |
| `ed code-review sessions` | List the native sessions in the running Edith page |
| `ed code-review new` | Create and select a native picker tab |
| `ed code-review focus <session>` | Select a native tab and focus its cmux workspace when applicable |
| `ed code-review close <session>` | Preview or close a native tab and its cmux workspace |
| `ed code-review restart [session]` | Restart a native review in the same tab |
| `ed code-review switch <session> <path>` | Switch a native tab to another worktree |

## Targeting

Every command accepts `--machine <name>`. Omit it, or use `--machine local`, for
this Mac. A configured machine name, SSH alias, UUID or unique prefix resolves
through Edith's machine directory. The command connects through Edith's shared
SSH control socket and gives that socket to Quinjet for remote discovery and
launch.

```sh
ed code-review projects --json
ed code-review projects --machine build --json
ed code-review worktrees /srv/edith --machine build --json
```

A machine that is asleep or unreachable exits 4 before discovery. An unknown
machine exits 3.

The native machine picker uses these same project and worktree reads. Its folder
browser corresponds to `ed machines files ls <machine> <path>`, so Quinjet does
not duplicate the general remote filesystem command.

## Planning and launching

`ed code-review open` is print-only. It resolves the requested project, chooses the
current or first available worktree, constructs the launch request and prints a
shell-quoted command. It never starts a process or sends AppleScript.

`ed code-review launch` crosses the standalone execution boundary. The default
starts an interactive Quinjet process attached to the same standard input and
output. `--cmux` asks cmux to create a workspace instead. It does not create or
control a tab in Edith's native Quinjet page.

```sh
ed code-review open ~/code/edith
ed code-review open ~/code/edith --theme tokyo-night --appearance light
ed code-review launch ~/code/edith
ed code-review launch ~/code/edith --cmux
ed code-review launch /srv/edith --machine build --theme gruvbox
```

Both commands accept these options:

| Name | Values | Default | What it does |
| --- | --- | --- | --- |
| `--theme <name>` | `quinjet`, `catppuccin`, `dracula`, `everforest`, `gruvbox`, `nord`, `one`, `rose-pine`, `solarized`, `tokyo-night`, `ayu`, `monokai`, `github` | saved app theme | Select the Quinjet theme |
| `--appearance <value>` | `light`, `dark` | current app appearance | Select the theme appearance |
| `--cmux` | flag | saved app terminal | Force a cmux launch request |
| `--embedded` | flag | saved app terminal | Force a current-terminal launch request |
| `--machine <name>` | configured machine or `local` | `local` | Select the worktree host |
| `--json` | flag | off | Emit stable JSON on stdout |

The app's terminal and theme menus persist through
`ed config set quinjetTerminal embedded` and `ed config set quinjetTheme <name>`.
Set `quinjetTheme` to `app` to send Edith's active light and dark palettes to
Quinjet automatically. A named Quinjet theme remains an explicit override and
the app discovers available names from the installed Quinjet version.

cmux must be installed in `/Applications`. If it is not,
`launch --cmux` exits 4 with a hint to omit `--cmux`. `open --cmux` remains safe
and prints the cmux-targeted Quinjet command without asking cmux to run it.

## Native sessions

Native session commands use bounded request and reply IPC with the running main
app. The Quinjet extension must be enabled and its page must be open. Run
`ed app reveal codeReview` before using them. A silent or older app exits 4 instead
of waiting indefinitely.

Each session can be selected by its 1-based number, full id, exact title, exact
branch, or current worktree path. Shell completion asks the running page for
session numbers with a 250 millisecond bound.

```sh
ed code-review sessions
ed code-review status
ed code-review new
ed code-review focus 2
ed code-review restart 2
ed code-review switch 2 ~/code/edith-native-sessions
ed code-review close 2
ed code-review close 2 --yes
```

`new`, also available as `create`, adds and selects a picker tab through the same
app-side operation as the tab bar plus button. `focus` selects the tab in Edith.
For a cmux-backed session it also activates the
matching cmux workspace. `close` prints a non-mutating plan unless `--yes` is
present. A confirmed close terminates the embedded process or closes the exact
cmux workspace before removing the tab. Edith keeps at least one picker tab, so
the only native session cannot be closed.

`restart` preserves the tab id, machine, worktree and saved launch configuration.
`switch` resolves the new worktree through the same local or remote Quinjet
client used by the picker, then replaces the review in the same tab. Both route
through the same app-side operation method used by the corresponding buttons.

## JSON

`projects --json` returns `local`, `machine` and `projects`. Each project has
`commonDir`, `name` and `worktrees`. `worktrees --json` returns `local`,
`machine` and `worktrees`.

A worktree object has these stable keys: `bare`, `branch`, `canOpen`, `current`,
`detached`, `displayName`, `head`, `locked`, `path` and `prunable`. Nullable
values are JSON null. Object keys are sorted.

`open --json` and `launch --json` return `arguments`, `command`,
`currentDirectory`, `executable`, `launched`, `local`, `machine`, `terminal` and
`worktree`. `launched` is false for `open` and true after a successful `launch`.
`terminal` is `current` or `cmux`.

For `launch --json`, the child process cannot write to stdout and receives no
interactive input, so stdout remains exactly one JSON document. Use plain
`launch` for an interactive terminal session. Use `open --json` for a safe
noninteractive preview, or `launch --cmux --json` to open a separate workspace.

Native session JSON returns `operation`, `selectedSessionID`,
`affectedSessionID` and `sessions`. Each session has `id`, `index`, `title`,
`selected`, `state`, `terminal`, `project`, `worktreePath`, `branch`, `machine`,
`canClose`, `canRestart` and `exitMessage`. Nullable values are JSON null.

The JSON preview from `close` follows the shared destructive-plan contract with
`action`, `targets`, `applied` and `changed`. A confirmed close additionally
returns `closedSessionID`, `selectedSessionID` and `remaining`.

## Exit codes

| Code | When |
| --- | --- |
| 0 | Discovery, planning, launching or native session control succeeded |
| 1 | Quinjet failed, returned malformed JSON or exited unsuccessfully |
| 2 | Arguments, theme or appearance were invalid |
| 3 | The machine, worktree or native session was not found |
| 4 | Quinjet, cmux, the selected machine or the running Edith page was unavailable |

A missing Quinjet executable includes a hint to run `ed tools install quinjet`. A failed
Quinjet command includes its diagnostic. Malformed JSON suggests updating
Quinjet and retrying.

## Where to go next

- [`ed machines`](../machines/README.md) for configured SSH machines
- [`ed extensions`](../extensions/README.md) to show the Quinjet page in Edith
- [All `ed` commands](../README.md)
