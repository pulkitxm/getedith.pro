# `ed cursors apply`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors apply ID [--size N] [--color KEY=#RRGGBB]... [--json]
```

`--size` is 0.75, 1, 1.25, 1.5, 1.75, 2, 2.5 or 3 times the normal pointer. `--color` changes one of the pack's colours and can be repeated; `ed cursors show ID` lists the keys a pack accepts. Colours equal to the preset are ignored, and without changes the plain pack is applied. Other sizes, unknown keys, a key given twice or a colour that is not `#rrggbb` exit with a usage error before anything downloads. A customized pack is drawn by the service, checked against the digest it sends, registered at the chosen size with its hotspots scaled, and kept encrypted on this Mac so Edith can put it back without the network.

Downloads that one pack, checks it against the size and checksum in the pack list, validates it, and registers its cursors with macOS. Needs an activated Edith licence. A pack you already have is applied from its encrypted copy on this Mac without downloading it again. The first apply in a login session saves the current cursors so `reset` can put them back. If macOS does not switch the arrow, Edith restores the saved cursors and the command fails. Less common pointers that macOS refuses are listed in `failures` without failing the command. JSON output reports `id`, `name`, `live`, `failures` and `recipe` (`base`, `size` and the changed `colors`).

New packs per licence are limited to 60 in a rolling 24 hours. Over the limit, or when the service asks Edith to slow down, the command exits with an unavailable error that says when to try again, and Edith does not ask the service again before then.
