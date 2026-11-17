# `ed agents layout even`

Gives every pane in a tab the same share of the window.

[`ed agents`](./README.md)

```
ed agents layout even [--tab <tab>] [--json]
```

This is Even Out in the layout popover.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Which tab to even out |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents layout even --tab 1
ed agents layout even --json
```

## Where to go next

- [`ed agents layout apply`](./layout-apply.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
