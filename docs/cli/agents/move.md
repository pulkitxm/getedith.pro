# `ed agents move`

Moves an agent into another tab.

[`ed agents`](./README.md)

```
ed agents move <agent> --tab <tab> [--json]
```

This is a drag onto that tab. The destination cannot be the board.

## Arguments

| Name | What it is |
| --- | --- |
| `<agent>` | Agent id, pane id, or unique title |

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | required | Destination tab |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents move w3:p1 --tab 2
ed agents move w3:p1 --tab 2 --json
```

## Where to go next

- [`ed agents swap`](./swap.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
