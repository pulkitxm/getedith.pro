# `ed agents layout`

Lists the tabs, saved layouts, and agent terminals in the open Edith window.

[`ed agents`](./README.md)

```
ed agents layout ls [--json]
```

`ed agents layout` runs `ls`. `list` is an alias for `ls`. Index 0 is the board. Agent tabs start at 1. A selected row is marked with `*`.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emit one JSON document on stdout |

The JSON object has `agents`, `arrangements`, `message`, `selected`, `tabs`, and `terminals`. This command needs the Edith window. It exits 4 when that window is not open.

## Examples

```
ed agents layout ls
ed agents layout ls --json
```

## Where to go next

- [`ed agents layout save`](./layout-save.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
