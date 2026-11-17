# `ed agents`

Live Herdr sessions on this Mac and on the SSH machines Edith already knows.
`ed agents` runs `herdr` locally and, over the shared SSH control socket, on
every configured machine. Reach for it when you want a list of panes, or the
exact attach line the Agents page copies.

A missing `herdr` binary is not a failure. That host is listed with `agentsEngine`
false and an empty agent list. Each JSON host also reports `reachable`, so a
connection failure is distinct from a machine that was reached without Herdr.
Both cases keep the aggregate listing at exit 0. Unknown machines are the only
not-found case.

The Agents extension does not have to be on for these commands to run. They talk
to the `herdr` CLI, not to the Edith window.

## At a glance

| Command | What it does |
| --- | --- |
| `ed agents` | Runs `ls`, which is the default subcommand |
| `ed agents ls` | Live sessions on this Mac and every SSH machine |
| `ed agents command <pane>` | The attach line for one pane |
| `ed agents attach <pane>` | Attach this terminal to one pane |
| `ed agents models [<kind>]` | Models, effort levels and fast mode each agent offers |
| `ed agents defaults` | The model, effort and fast mode every launch uses |
| `ed agents defaults set <kind>` | Change those launch defaults for one kind |
| `ed agents send <pane> <message>` | Type a message now, when the agent finishes, or at a time |
| `ed agents hooks` | Messages waiting for an agent to finish |
| `ed agents layout` | Tabs, saved layouts, and agent terminals in the Edith window |
| `ed agents select` | Show one tab in the Edith window |
| `ed agents split <agent>` | Open an agent beside the focused pane |
| `ed agents move <agent>` | Move an agent into another tab |
| `ed agents swap <agent> <agent>` | Swap two agents in the same tab |
| `ed agents gather` | Gather every tab into one |
| `ed agents separate` | Turn a split into one tab per agent |
| `ed agents terminal` | Open a terminal in the selected tab |
| `ed agents space ls` | List open space windows |
| `ed agents space terminal` | Open a terminal in a space window |
| `ed agents space split` | Split the focused pane in a space window |
| `ed agents background` | Keep the sessions Edith starts running after Edith quits |
| `ed agents close-tab` | Close one tab after `--yes` |
| `ed agents close-others` | Close every tab except one after `--yes` |
| `ed agents close-right` | Close tabs to the right after `--yes` |
| `ed agents close-all` | Close every agent tab after `--yes` |

`ed agents list` is an alias for `ed agents ls`. Layout commands talk to the
open Edith window. The session commands above talk to the `herdr` binary and
do not need that window.

## Commands

- [`ed agents ls`](./ls.md)
- [`ed agents command`](./command.md)
- [`ed agents attach`](./attach.md)
- [`ed agents models`](./models.md)
- [`ed agents defaults`](./defaults.md)
- [`ed agents send`](./send.md)
- [`ed agents hooks`](./hooks.md)
- [`ed agents layout`](./layout.md)
- [`ed agents layout save`](./layout-save.md)
- [`ed agents layout delete`](./layout-delete.md)
- [`ed agents select`](./select.md)
- [`ed agents layout apply`](./layout-apply.md)
- [`ed agents layout even`](./layout-even.md)
- [`ed agents split`](./split.md)
- [`ed agents move`](./move.md)
- [`ed agents swap`](./swap.md)
- [`ed agents gather`](./gather.md)
- [`ed agents separate`](./separate.md)
- [`ed agents terminal`](./terminal.md)
- [`ed agents close-tab`](./close-tab.md)
- [`ed agents close-others`](./close-others.md)
- [`ed agents close-right`](./close-right.md)
- [`ed agents close-all`](./close-all.md)
- [`ed agents background`](./background.md)
- [Terminals in agent tabs](./terminals.md)

## Exit codes

| Code | When |
| --- | --- |
| 0 | The listing printed, including when Herdr is missing or no panes are live |
| 2 | The command line was wrong: an unknown flag, `command` with no pane, or `defaults set` with options the model cannot take |
| 3 | `--machine` named no configured machine, `command` named no pane, or `models` / `defaults set` named a kind with no launch options |
| 1 | `send` named one pane and Herdr did not take the message |
| 4 | `send --when-finished` or `hooks` could not reach the background agent, or `background` could not run a session under launchd |

Listing never exits 1 or 4. A down SSH machine is an error string on
that host and `reachable: false`, not an unavailable CLI. Plain output prints
the host error instead of describing the tool as missing.

## Notes and gotchas

- This Mac is `--machine local`. `this-mac`, `thismac` and `mac` are the same
  thing. Any other value is resolved the way `ed machines show` resolves a
  name: exact name, SSH alias, UUID, or a unique prefix.
- Session names come from `herdr session list`. If that command prints nothing
  useful, Edith tries the `default` session.
- The attach line for a remote pane is
  `ssh -tt <target> -- herdr --session <session> agent attach <pane>`. Detach
  inside Herdr with `ctrl+b q`. The server stays up.
- PATH on the far side is prefixed with `$HOME/.local/bin`, `$HOME/.cargo/bin`,
  `/opt/homebrew/bin` and `/usr/local/bin` before `herdr` is called, which is
  where a curl-installed binary usually lives.
- The extension switch is `tabAgentsEnabled`. Prefer
  `ed extensions enable agents` so the sidebar item appears.

## Where to go next

- [`ed machines`](../machines/README.md) for the SSH directory these commands walk
- [`ed extensions`](../extensions/README.md) to turn the Agents page on
- [All `ed` commands](../README.md)
