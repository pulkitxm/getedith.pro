# `ed bifrost map`

Measure a folder's allocated and logical sizes, largest files, folders and cleanup candidates.

```sh
ed bifrost map ~/Documents
ed bifrost map ~/Downloads --json
```

The text view ranks the root's children. JSON includes the full bounded map report and coverage details. Persistent protected paths are skipped. The scanner stays on the selected volume, skips links and cloud-only entries, and counts hard links once. Partial coverage is reported.

Use the Disk Map tab for treemap and ring navigation, path search, hidden-entry filtering and reviewed Trash moves.

[Back to Bifrost](./README.md).

[All commands](../README.md).
