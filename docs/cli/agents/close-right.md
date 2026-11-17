# `ed agents close-right`

Closes Agents tabs to the right of one tab, after a preview.

[`ed agents`](./README.md)

```
ed agents close-right [--tab <tab>] [--yes] [--json]
```

Without `--yes` nothing changes.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Last tab that stays |
| `--yes` | flag | off | Close the tabs after the preview |
| `--json` | flag | off | Emit the plan, or the layout, as JSON |

## Examples

```
ed agents close-right --tab 1
ed agents close-right --yes
```

## Where to go next

- [`ed agents close-all`](./close-all.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
