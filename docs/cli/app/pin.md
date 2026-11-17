# `ed app pin`

Pins an extension page to the sidebar, below Home and above Library.

```
ed app pin <id> [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<id>` | an extension id with a page | required | The page to pin. It goes to the end of the pinned rows. |
| `--json` | flag | off | Emit JSON on stdout. |

`--json` shape:

```json
{
  "action": "pin",
  "id": "usage",
  "changed": true,
  "pinned": true,
  "pins": ["agents", "usage"]
}
```

Examples:

```
ed app pin usage
ed app pin music --json
```

Pinning a page that is already pinned succeeds with `"changed": false`. An id
without a page exits 1. A pinned extension that is off keeps its place and its
row comes back when it is turned on again. Until you change the pins, the
sidebar shows the starter pages of your profile; the first pin or unpin saves
that list as your own. The main window process must be running; without it the
command exits 4.

## Where to go next

- [`ed app unpin`](./unpin.md), take a page off the sidebar
- [`ed app pins`](./pins.md), list the pins or restore the profile pins
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
