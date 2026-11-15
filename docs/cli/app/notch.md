# `ed app notch`

Reports the notch and opens or closes it.

```
ed app notch [status|open|close] [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `status` | word | yes | Print whether the notch is on, its state and the activities it is showing. |
| `open` | word | | Open the notch on its top activity, the same as clicking it. Does nothing while no activity is live. |
| `close` | word | | Close the open notch, the same as pressing Escape. |
| `--json` | flag | off | Emit JSON on stdout. |

The state is `hidden`, `live`, `open` or `drop`. Activities are listed in the
order the notch ranks them: urgency, then priority, then the most recent.

`--json` shape:

```json
{
  "enabled": true,
  "phase": "live",
  "display": "notch",
  "top": {
    "provider": "notchShelf",
    "key": "files",
    "urgency": "low",
    "badge": "2 files",
    "title": "2 files on the Shelf"
  },
  "activities": []
}
```

Examples:

```
ed app notch
ed app notch open
ed app notch close --json
```

## Where to go next

- [`ed app snapshot`](./snapshot.md), capture the open notch as an image
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
