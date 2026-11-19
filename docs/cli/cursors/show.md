# `ed cursors show`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors show ID [--json]
```

Shows one pack from the pack list: its name, family, colours, tags, summary, whether it is applied, and the colours `ed cursors apply --color` can change with the preset value of each (`controls` in JSON, each with `key`, `label` and `value`; empty when the pack list does not offer custom colours). It prints details only, never the pack's art, and does not download the pack. An unknown id exits with a not found error.
