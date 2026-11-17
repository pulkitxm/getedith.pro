# `ed agents close-all`

Closes every Herdr agent tab after a preview.

[`ed agents`](./README.md)

```
ed agents close-all [--yes] [--json]
```

The board stays open. Without `--yes` nothing changes.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--yes` | flag | off | Close the tabs after the preview |
| `--json` | flag | off | Emit the plan, or the layout, as JSON |

## Examples

```
ed agents close-all
ed agents close-all --yes
```

## Where to go next

- [`ed agents close-tab`](./close-tab.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
