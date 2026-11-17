# `ed memory export`

Saves everything Memory remembers into a directory you choose: one
`bundle.json` holding episodes, observations, conversations, beliefs, claims,
facts, core memory and the non-secret reasoner settings, plus, with
`--include-media`, a `media/` directory of the original voice notes, PDFs,
images and videos.

Usage:

```
ed memory export <directory> [--include-media] [--json] [--endpoint <url>]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<directory>` | path | required | Where the bundle is written. Created if missing; `~` expands. |
| `--include-media` | flag | off | Also download every media file behind the episodes. |
| `--json` | flag | off | Emit JSON on stdout. |
| `--endpoint` | URL | resolution order | Memory API base URL. |

Examples:

```
ed memory export ~/backups/memory
ed memory export ~/backups/memory --include-media
ed memory export /tmp/before-wipe --json
```

`--json` shape:

```json
{
  "counts": {
    "beliefs": 17,
    "episodes": 42,
    "observations": 64
  },
  "directory": "/Users/me/backups/memory",
  "mediaFailed": [],
  "mediaSaved": 39
}
```

Tokens and API keys never leave Memory: the bundle carries the reasoner
provider, URL and model, but not its key and not the connector tokens. Without
`--include-media` the bundle still lists every media file it left behind, and
the command says how many stayed, so a later `--include-media` run completes
the backup. The bundle restores with
[`ed memory import`](./import.md), and importing is idempotent, so exporting
before a risky operation is cheap insurance. Media files land as
`media/<sha256>-<name>`, which is exactly the layout import expects.

The destination directory may already exist. `bundle.json` and media files
with matching names are overwritten; unrelated or stale files are not removed.
Export validates that the API response decodes as a Memory manifest before
writing it. A media download failure does not discard the bundle or fail the
whole command: failed basenames appear in `mediaFailed` and in a stderr note.
For a complete backup, require that `mediaFailed` is empty and compare
`mediaSaved` with the length of the `media` manifest in `bundle.json`.

## Where to go next

- [`ed memory import`](./import.md), the other half
- [`ed memory wipe`](./wipe.md), what to export before
- [`ed memory`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
