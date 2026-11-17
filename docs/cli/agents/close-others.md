# `ed agents close-others`

Closes every Agents tab except one, after a preview.

[`ed agents`](./README.md)

```
ed agents close-others [--tab <tab>] [--yes] [--json]
```

Passing the board closes every agent tab. Without `--yes` nothing changes.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Tab to keep |
| `--yes` | flag | off | Close the others after the preview |
| `--json` | flag | off | Emit the plan, or the layout, as JSON |

## Examples

```
ed agents close-others --tab 1
ed agents close-others --yes
```

## Where to go next

- [`ed agents close-tab`](./close-tab.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
