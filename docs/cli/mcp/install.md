# `ed mcp install`

[CLI reference](../README.md) | [MCP](./README.md)

Register Edith's MCP server with a coding agent. The Connect buttons in Settings >
Tools run the same code.

```sh
ed mcp install --client <claude|codex|cursor|vscode|all> [--dry-run] [--command <path>] [--json]
```

The server is named `edith` and runs `ed mcp` from the installed app, so it keeps
working whether or not `ed install` put `ed` on your `PATH`. `--command` points it
at another absolute path instead.

Every client is registered by editing its settings file directly, so no agent
command has to be installed.

| Client | Where it lands |
| --- | --- |
| `claude` | user-scope `mcpServers.edith` in `~/.claude.json` |
| `codex` | `[mcp_servers.edith]` in `~/.codex/config.toml` (or `$CODEX_HOME/config.toml`) |
| `cursor` | `mcpServers.edith` in `~/.cursor/mcp.json` |
| `vscode` | `servers.edith` in `~/Library/Application Support/Code/User/mcp.json` |

`--client all` registers every client found on this Mac and skips the rest: a
client counts as found when its settings folder or file exists. Naming one client
writes its entry even when the client is not found. An entry that already points
at this `ed` is left alone, and one pointing at another `ed` is replaced.

Writes are merge-safe. Edith reads the file, changes only the `edith` entry, writes
the result to a temporary file next to it and renames it into place. If the file
changed while Edith was writing (Claude Code rewrites `~/.claude.json` often),
Edith reads it again and retries, and after five changed attempts it leaves the
file alone. A symlinked settings file is updated at its target.

`--dry-run` prints the entry and changes nothing. An edited file is
first copied to `<name>.edith-backup`, and other servers and settings are kept. A
file that is not plain JSON (comments, for example) or a TOML table Edith cannot
edit safely is left untouched: the command exits 1 and prints the exact entry to
paste. Restart the client to load the server, then ask the agent to call
`edith_catalog`.

`--json` reports `command`, `dryRun` and one object per client with `client`,
`path`, `action` (`created`, `updated`, `unchanged`, `skipped` or `notFound`;
[`ed mcp uninstall`](./uninstall.md) adds `removed`), `applied`, `snippet`, `note`
and `backup`.

## Related

- [`ed mcp uninstall`](./uninstall.md)
- [`ed mcp status`](./status.md)
- [`ed mcp`](./README.md)
