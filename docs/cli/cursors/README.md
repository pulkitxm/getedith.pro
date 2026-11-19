# `ed cursors`

`ed cursors` is the command-line surface for the Cursor Packs page under Mac Utilities. It lists the original cursor themes drawn for Edith, applies one system-wide, and restores the standard macOS pointers.

[The `ed` command line](../README.md)

| Command | What it does |
| --- | --- |
| [`ed cursors ls`](./ls.md) | Lists cursor packs, best matches first when you search. |
| [`ed cursors show`](./show.md) | Shows one pack's family, colours, tags and whether it is applied. |
| [`ed cursors apply`](./apply.md) | Downloads one pack, checks it, and applies it to every app. |
| [`ed cursors reset`](./reset.md) | Previews restoring the macOS cursors, or does it with `--yes`. |
| [`ed cursors status`](./status.md) | Reports the applied pack, whether macOS is drawing it, and the cache size. |

Cursor packs need an activated Edith licence. The pack list comes from the Edith service and a copy is kept on disk, encrypted for this Mac, so `ls` and `show` still answer offline with the last copy. Only `apply` downloads a pack, and new packs per licence are limited each day. No `ed cursors` command prints pack art. macOS forgets cursor themes when you log out, and Edith puts the applied pack back each time it launches.
