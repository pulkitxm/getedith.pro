# `ed app pins`

Lists the sidebar pins in order, or restores the pins of your profile.

```
ed app pins [--reset] [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--reset` | flag | off | Forget your own pins and show the starter pages of your profile again. |
| `--json` | flag | off | Emit JSON on stdout. |

`--json` shape:

```json
{
  "customized": true,
  "pins": [
    { "id": "agents", "shown": true },
    { "id": "music", "shown": false }
  ]
}
```

Examples:

```
ed app pins
ed app pins --json
ed app pins --reset
```

`shown` is false for a pinned extension that is off or not installed; its row
returns when it is turned on. `customized` is false while the sidebar follows
the profile's starter pages. The sidebar order is the order of `pins`, and
Option-1 to Option-8 select the sidebar rows in that order, starting with Home.
The main window process must be running; without it the command exits 4.

## Where to go next

- [`ed app pin`](./pin.md), add a page
- [`ed app unpin`](./unpin.md), remove a page
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
