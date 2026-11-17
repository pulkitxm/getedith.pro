# `ed agents swap`

Swaps two agents that already share a tab.

[`ed agents`](./README.md)

```
ed agents swap <agent> <agent> [--json]
```

## Arguments

| Name | What it is |
| --- | --- |
| `<agent>` | Agent id, pane id, or unique title |
| `<agent>` | The other agent in the same tab |

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents swap w3:p1 w3:p2
ed agents swap w3:p1 w3:p2 --json
```

## Where to go next

- [`ed agents split`](./split.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
