# `ed cursors ls`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors ls [--search TEXT] [--tag TAG]... [--family ID] [--json]
```

Lists every cursor pack. `ed cursors list` is an alias. `--search` matches names, tags (with their labels and synonyms), families and summaries. Every word must match, a word can be the start of a longer one, and small typos are forgiven in longer words. Name matches come first, then tags, then families, then summaries. `--tag` takes a tag id and can be repeated: tags from the same group widen the list (`--tag blue --tag pink`), and tags from different groups narrow it (`--tag dark --tag blue`). `--family` keeps one family by id. JSON output is an array of packs with `id`, `name`, `family`, `familyName`, `summary`, `tags`, `colors` and `applied`. Without an activated Edith licence the command exits with an unavailable error.
