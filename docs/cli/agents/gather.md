# `ed agents gather`

Gathers every open agent tab into one tab.

[`ed agents`](./README.md)

```
ed agents gather [--tab <tab>] [--json]
```

This is Gather All Tabs. Four or more agents land in a grid. Fewer land in columns.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Tab that receives every agent |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents gather --tab 1
ed agents gather --json
```

## Where to go next

- [`ed agents separate`](./separate.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
