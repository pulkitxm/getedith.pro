# `ed memory reason`

Shows or changes how Memory reasons. Settings persist on the backend and
hot-swap into the running service, so no restart or `.env` edit is needed; the
environment remains the fallback for anything never set here.

Usage:

```
ed memory reason [show] [--json] [--endpoint <url>]
ed memory reason set [--provider <p>] [--model <m>] [--url <u>] [--api-key <k>]
                        [--json] [--endpoint <url>]
ed memory reason test [--json] [--endpoint <url>]
```

Options for `ed memory reason set`:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--provider` | supported provider id | unchanged | Which API shape to speak; `openai` covers any OpenAI-compatible server such as Ollama. |
| `--model` | model name | unchanged | Model to request; empty resets to the provider default. |
| `--url` | URL | unchanged | Base URL for the OpenAI-compatible provider. |
| `--api-key` | secret | unchanged | Stored in the backend's settings table, not the CLI config; empty clears it. |

At least one setting option is required. Empty values remove that saved
override and expose the provider's environment or built-in default again.
`--json` returns the same masked settings object as `show`; it never echoes the
key supplied on the command line.

`ed memory reason show` (also the bare default) prints the active provider,
model, URL, whether a key is set with its last-four hint, and whether the
reasoner is configured at all. `--json` shape: `{provider, url, model,
hasApiKey, apiKeyHint, configured, description}`. The key itself is never
returned.

`ed memory reason test` sends one tiny completion through the active
provider and reports the round-trip: `{ok, model, latencyMs}` under `--json`,
exit `1` with the provider's error when the backend reports failure. Failure to
reach the Memory API itself exits `4`.

## Where to go next

- [`ed memory`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
