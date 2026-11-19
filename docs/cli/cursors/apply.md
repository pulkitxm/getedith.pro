# `ed cursors apply`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors apply ID [--json]
```

Downloads that one pack, checks it against the size and checksum in the pack list, validates it, and registers its cursors with macOS. Needs an activated Edith licence. A pack you already have is applied from its encrypted copy on this Mac without downloading it again. The first apply in a login session saves the current cursors so `reset` can put them back. If macOS does not switch the arrow, Edith restores the saved cursors and the command fails. Less common pointers that macOS refuses are listed in `failures` without failing the command. JSON output reports `id`, `name`, `live` and `failures`.

New packs per licence are limited to 60 in a rolling 24 hours. Over the limit, or when the service asks Edith to slow down, the command exits with an unavailable error that says when to try again, and Edith does not ask the service again before then.
