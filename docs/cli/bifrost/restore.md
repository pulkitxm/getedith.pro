# `ed bifrost restore`

Preview restoration of a recorded Trash item. Apply it only with `--yes`.

```sh
ed bifrost restore <receipt-id>
ed bifrost restore <receipt-id> --yes
```

Find identifiers with [`history`](./history.md). The original parent folder must still exist, the item in Trash must be unchanged, and the destination must be unoccupied. Restoration uses an exclusive rename so an existing file cannot be overwritten. A successful restore removes its receipt.

If the folder moved, the Trash item changed, or the receipt expired, inspect the item in Finder.

[Back to Bifrost](./README.md).

[All commands](../README.md).
