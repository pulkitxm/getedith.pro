# `ed app unpin`

Takes an extension page off the sidebar. The page stays in Library.

```
ed app unpin <id> [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<id>` | an extension id with a page | required | The page to unpin. |
| `--json` | flag | off | Emit JSON on stdout. |

`--json` shape:

```json
{
  "action": "unpin",
  "id": "usage",
  "changed": true,
  "pinned": false,
  "pins": ["herdr"]
}
```

Examples:

```
ed app unpin usage
ed app unpin music --json
```

Unpinning a page that is not pinned succeeds with `"changed": false`. An id
without a page exits 1. The main window process must be running; without it the
command exits 4.

## Where to go next

- [`ed app pin`](./pin.md), put a page back on the sidebar
- [`ed app pins`](./pins.md), list the pins or restore the profile pins
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
