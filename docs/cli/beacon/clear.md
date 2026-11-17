# `ed beacon clear`

Forgets the frequently opened ledger, the record of what you pick in the bar.

Usage:

```
ed beacon clear [--json]
```

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emits one JSON document on stdout. |

There are no positional arguments. The plain response counts what went:

```
$ ed beacon clear
cleared 37 ranking entries
```

The JSON response has one stable field:

```json
{
  "cleared": 37
}
```

`cleared` is the number of entries the ledger held, not the number of times you
opened them. Clearing an already empty ledger is a success that reports `0`.

The ledger is stored in the extension's settings. Clearing removes selection
history and learned query associations. Favorites and aliases remain intact.
To forget one item, use Reset learned ranking in its Command-K Actions menu.
The reported count includes ranking records, not just distinct applications.

The command posts `settingsChanged`, so an open bar drops what it was showing
for an empty query straight away. The post is fire and forget, so the command
does not fail when nothing is listening.

Exit codes:

| Code | Meaning |
| --- | --- |
| 0 | The ledger was cleared, including when it was already empty. |
| 2 | The command line was invalid. |

The command is served by Beacon through Edith's extension CLI. The host and
extension must be available. Clearing ranking does not change the application
index, saved libraries, favorites or aliases.

## Where to go next

- [`ed beacon ls`](./ls.md), to see the index the ledger ranks
- [`ed beacon`](./README.md), the rest of this group
- [`ed config`](../config/README.md), for the settings that are not this ledger
- [All `ed` commands](../README.md)
