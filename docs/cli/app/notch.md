# `ed app notch`

Reports the notch and opens or closes it.

```
ed app notch [status|open|close] [--page <id>] [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `status` | word | yes | Print whether the notch is on, its state and the activities it is showing. |
| `open` | word | | Open the notch on Home, or on the page of the live activity, without taking keyboard focus. Works with nothing live. |
| `close` | word | | Close the open notch, the same as pressing Escape. |
| `--page <id>` | `home`, `tray`, `agents`, `arrange` | | With `open`, open on that page, or switch to it while the notch is open. |
| `--json` | flag | off | Emit JSON on stdout. |

The state is `hidden` (off, full screen or no display), `idle` (resting under the
hardware notch), `live` (a pill on each side of the notch for the top activity),
`open` or `drop`. `page` is the open page and `pages` lists the pages in their
arranged order. Activities are listed in the order the notch ranks them:
urgency, then priority, then the most recent.

`--json` shape:

```json
{
  "enabled": true,
  "phase": "live",
  "display": "notch",
  "top": {
    "provider": "shelf",
    "key": "files",
    "urgency": "low",
    "badge": "2 files",
    "title": "2 files on the Shelf"
  },
  "page": null,
  "pages": ["home", "tray"],
  "activities": []
}
```

Examples:

```
ed app notch
ed app notch open
ed app notch open --page tray
ed app notch close --json
```

## Where to go next

- [`ed app snapshot`](./snapshot.md), capture the open notch as an image
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
