# `ed agents layout apply`

Applies a built-in arrangement or a saved layout to one tab.

[`ed agents`](./README.md)

```
ed agents layout apply <name> [--tab <tab>] [--json]
```

Built-in names are `columns`, `rows`, `grid`, `tallGrid`, `focusLeft`, `focusRight`, `focusTop`, `focusBottom`, `focusCenter`, `twoColumns`, and `twoRows`. Titles such as `Side by Side` work too. The arrangement has to fit the number of agents in the tab.

## Arguments

| Name | What it is |
| --- | --- |
| `<name>` | Built-in arrangement or saved layout |

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Which tab to arrange |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents layout apply columns --tab 1
ed agents layout apply Pair --json
```

## Where to go next

- [`ed agents layout save`](./layout-save.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
