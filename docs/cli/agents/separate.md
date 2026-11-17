# `ed agents separate`

Turns one split tab into a tab per agent.

[`ed agents`](./README.md)

```
ed agents separate [--tab <tab>] [--json]
```

This is Separate Into Tabs. A tab with one agent is left as it is and the command fails.

## Options

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--tab <tab>` | index, id, or title | selected tab | Split tab to separate |
| `--json` | flag | off | Emit the layout as JSON |

## Examples

```
ed agents separate --tab 1
ed agents separate --json
```

## Where to go next

- [`ed agents gather`](./gather.md)
- [`ed agents`](./README.md)
- [All `ed` commands](../README.md)
