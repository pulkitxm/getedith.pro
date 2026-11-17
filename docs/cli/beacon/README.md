# `ed beacon`

`ed beacon` controls Beacon, Edith's keyboard launcher. It opens the bar,
previews search results, inspects the application index and evaluates expressions.
The extension identifier is `beacon`; its displayed name is Beacon.

| Command | What it does |
| --- | --- |
| [`ed beacon open [query]`](./open.md) | Opens the bar with an optional query |
| [`ed beacon search <query>`](./search.md) | Previews results without executing them |
| [`ed beacon ls`](./ls.md) | Lists or searches indexed applications |
| [`ed beacon calc <expression>`](./calc.md) | Evaluates arithmetic |
| [`ed beacon convert <sentence>`](./convert.md) | Converts units |
| [`ed beacon reindex`](./reindex.md) | Rebuilds the application index |
| [`ed beacon clear`](./clear.md) | Resets learned ranking, retaining favorites and aliases |

All commands accept `--json`. `ed beacon` defaults to `ls`; `list` is an alias
for `ls`. Commands are served by the installed extension through Edith's CLI.
Use a development slot's bundled `ed` when checking a local package.

The application index scans the standard application folders without Spotlight.
It is cached under the extension's data root and refreshed on first use or when
opening the bar after five minutes. `reindex` requests a fresh scan and returns
before it completes. Use `ls` after indexing finishes.

## Sources

Beacon includes applications, math, unit/currency conversion, developer utilities,
web keywords and explicit file paths. Clipboard and file search are separate modes.
Additional sources are configurable in Beacon settings:

| Source | Setting | Default |
| --- | --- | --- |
| Edith integration actions | `beaconSourceIntegrations` | On |
| Browser bookmarks | `beaconSourceBookmarks` | Off |
| Quicklinks | `beaconSourceQuicklinks` | On |
| Snippets | `beaconSourceSnippets` | On |
| Shell commands | `beaconSourceShellCommands` | On |
| Apple Shortcuts | `beaconSourceAppleShortcuts` | On |
| Window actions | `beaconSourceWindowActions` | On |
| System actions | `beaconSourceSystemActions` | On |
| Running apps | `beaconSourceRunningApplications` | On |
| Open windows | `beaconSourceOpenWindows` | Off |

```sh
ed config ls --group beacon --json
ed config set beaconSourceBookmarks true
ed beacon search "base64 hello" --json
```

Window actions and automatic snippet insertion require Accessibility. Without it,
a snippet copies to the clipboard. Safari bookmarks may require Full Disk Access.
The Clipboard and Machines integrations require their respective providers.

Give one a keyword and it becomes a prefix: type `gh edith` and the bar runs the
quicklink keyed `gh` with `edith` as `{query}`, skipping every other result. A
keyword on its own is just a search. Values going into a web URL are
percent-encoded, and snippets and file quicklinks get them as typed. Shell
commands never see the text itself: each placeholder becomes a quoted reference
to an environment variable (`EDITH_BEACON_1`, `EDITH_BEACON_2`, ...) holding
the value, so clipboard text such as `; rm -rf ~` stays data whether the
placeholder sits bare, inside double quotes or inside single quotes.

## Libraries and ranking

Quicklinks, snippets and shell commands are editable in settings and support local
JSON import/export. Plain Raycast Quicklinks and Snippets JSON can be imported.
Supported placeholders are `{query}`, `{argument}`, `{clipboard}`, `{selection}`,
`{date}`, `{time}` and `{uuid}`. A format after a colon customizes dates and times.
Shell placeholder values are passed through environment variables rather than
interpolated as executable input.

Command-K on a result offers favorites, exact aliases, copy and applicable file
actions. Ranking learns successful selections and decays over time. Read-only
`search` does not teach ranking, open links or copy values.

See `docs/beacon.md` for examples,
provider requirements and the current coverage limits.

[All terminal commands](../README.md)
