# `ed app reveal`

Shows a section of the main window, and optionally a tab inside it.

```
ed app reveal [<section>] [--tab <tab>] [--list] [--json]
```

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<section>` | `home`, `usage`, `agents`, `codeReview`, `memory`, `plugins`, `machines`, `docs`, `appUpdates`, `homebrew`, `cleaner`, `runningApps`, `calendar`, `studio`, `screenRecorder`, `virtualCamera`, `music`, `downloads`, `socialManager`, `database`, `codeStats`, `siteAudit`, `latex`, `attention`, `extensions`, `settings`, `about` | none | The page to show. An extension page is named by its extension id and opens whether or not it is pinned to the sidebar; `extensions` is Library and `about` is About Edith. An extension without a page opens its Library entry. Without it the window comes up where it already was, and the answer names that section. |
| `--tab` | section-specific | none | A tab inside the section. `cleaner` has `cleanup`, `map`, `files`, `restore`; `appUpdates` has `updates`, `remove`, `history`; `memory` has `chat`, `capture`, `desk`, `library`, `mind`, `setup`, `settings`; `settings` has `general`, `surfaces`, `permissions`, `data`, `storage`, `shortcuts`, `icloud`, `updates`, and in the Developer profile also `agentActivity`, `agent`, `jev`, `terminal`, `mcp`. |
| `--list` | flag | off | Print every page id and title that can be revealed. Does not change the window. |
| `--json` | flag | off | Emit JSON on stdout. |

`--json` shape:

```json
{
  "action": "reveal",
  "section": "memory",
  "tab": "chat"
}
```

Examples:

```
ed app reveal
ed app reveal memory
ed app reveal docs
ed app reveal memory --tab settings
ed app reveal settings --tab permissions
ed app reveal settings --tab updates
ed app reveal machines --json
ed app reveal memory/chat
```

A value that contains `/` is a full route. The first segment is still the
section, and `appUpdates`, `memory` or `settings` also take their tab
from the second segment. [`ed app navigate`](./navigate.md) moves to the same
route without bringing the window forward.

The app answers when the section is on screen, so a `0` exit means the window
is open and showing what you asked for, not merely that a request was sent.
A section that does not exist, a tab that does not belong to the section, or
`--tab` on a section that has none all exit 3 with the valid names in the
error, and `--tab` without a section is a usage error, exit 2. The main window
process must be running; without it the command exits 4.
Section and tab values are exact, lowercase raw values. An explicitly empty
`--tab ''` is treated as no tab and reveals only the section. A bare reveal
returns the stored section but does not return that section's current tab, so
its JSON has `"tab": null`.

Pairs with [`ed app snapshot`](./snapshot.md) for reading the screen you just
revealed.

## Where to go next

- [`ed app snapshot`](./snapshot.md), capture what you revealed
- [`ed app`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
