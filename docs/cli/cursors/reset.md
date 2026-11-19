# `ed cursors reset`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors reset [--yes] [--json]
```

Without `--yes`, prints the plan and changes nothing. With `--yes`, registers the saved macOS cursors again, removes pointers that macOS had not created yet, and forgets the applied pack so it is not put back at the next launch. If the saved cursors cannot be read, it still forgets the pack, prints a note, and asks you to log out and back in to get the standard pointers. JSON previews report `applied: false` and `changed: false`.
