# `ed memory index`

Embeds pending episodes and stores their searchable chunks.

Usage:

```
ed memory index [--json] [--endpoint <url>]
```

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emits one JSON document on stdout. |
| `--endpoint` | URL | resolution order | Uses this Memory API base URL. |

`--json` shape:

```json
{
  "chunksCreated": 9,
  "episodesIndexed": 3
}
```

`episodesIndexed` counts episodes completed by this request, and
`chunksCreated` counts the searchable chunks created for them.

Examples:

```
$ ed memory index
indexed 3 episodes into 9 chunks

$ ed memory index --json
{
  "chunksCreated": 9,
  "episodesIndexed": 3
}
```

Behaviour: this mutating command sends `POST /v1/index` with an empty body.
Only episodes without chunks are indexed, up to 500 oldest episodes per pass,
with embeddings requested in batches of 16. The client allows five minutes for
the request. If the embedding service returns HTTP 502, the command names the
Ollama embedding service, leaves stdout empty, and exits 4. Database and other
backend failures exit 1.

## Where to go next

- [`ed memory`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
