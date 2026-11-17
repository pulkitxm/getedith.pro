# `ed agents select`

Shows one Agents tab in the Edith window, the same way Command-number does.

[`ed agents`](./README.md)

```
ed agents select --tab <tab> [--json]
```

The board is tab 0. Hidden tabs keep their terminals, so selecting a tab does
not restart or replay anything.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | required | Tab to show |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents select --tab 2
ed agents select --tab 0 --json
```

## Where to go next

- [`ed agents layout`](./layout.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
