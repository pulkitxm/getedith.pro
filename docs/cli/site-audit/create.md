# `ed site-audit create`

[`ed site-audit`](./README.md)

[The `ed` command line](../README.md)

```bash
ed site-audit create <url> [--name <name>] [--json]
```

Creates an empty site-audit project. A URL without a scheme gets `https`, or `http` for localhost. An omitted or blank `--name` uses the site host, matching the new-project sheet. JSON is the project plus its empty page selection.
