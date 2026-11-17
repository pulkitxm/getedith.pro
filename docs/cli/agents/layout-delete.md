# `ed agents layout delete`

Deletes one saved layout after a preview.

[`ed agents`](./README.md)

```
ed agents layout delete <name> [--yes] [--json]
```

Without `--yes` the command prints the plan and changes nothing. Built-in arrangements are not deleted.

## Arguments

| Name | What it is |
| --- | --- |
| `<name>` | Saved layout name or id |

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--yes` | flag | off | Delete after the preview |
| `--json` | flag | off | Emit the plan, or the layout, as JSON |

## Examples

```
ed agents layout delete Pair
ed agents layout delete Pair --yes
```

## Where to go next

- [`ed agents layout ls`](./layout.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
