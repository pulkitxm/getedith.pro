# `ed bifrost search`

Preview Bifrost's root-search results without running an action.

```text
ed bifrost search <query> [--json]
```

Quote queries containing spaces or shell punctuation. The query is limited to
200 characters. No match returns an empty list with a successful exit status.
An overlong query is a usage error.

```sh
ed bifrost search "sha256 hello" --json
ed bifrost search "gh swift packages" --json
ed bifrost search "time in Tokyo"
```

JSON output is an array. Each result contains `id`, `kind`, `title`, `subtitle`,
`action` and `value`. `action` is a display verb, not a command to execute.
`value` is the value that the result's copy action represents, such as an app
path, calculated answer or search URL. Clipboard item payloads are not included.

The command uses the loaded launcher's application index, settings and available
sources. Dynamic sources reflect the last successful refresh from the bar.
It does not search inside file/clipboard modes, launch apps, open URLs, run
scripts, copy answers or modify ranking. Explicit local paths can resolve to
file results. A missing provider contributes no integration actions.

See [`ed bifrost`](./README.md) for the complete command group.

[All terminal commands](../README.md)
