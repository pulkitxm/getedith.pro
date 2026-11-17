# `ed memory stack`

Starts, stops and inspects the companion stack on whichever machine
[`ed memory deploy`](./deploy.md) put it on.

Usage:

```
ed memory stack <subcommand>
```

| Command | What it does |
| --- | --- |
| `ed memory stack status` | Which host runs it, and which services are up. |
| `ed memory stack up` | Starts it. |
| `ed memory stack down` | Stops it. |
| `ed memory stack restart` | Restarts it. |
| `ed memory stack logs` | Reads its logs. |
| `ed memory stack env` | Prints the environment it would be given. |

`status` is the default subcommand.

Every stack command uses the saved deployment record. It runs locally with
`/bin/sh` or over the registered machine's SSH transport, changes into the
saved directory, selects the saved tier's Compose files, and always uses
Compose project name `edith-companion`.

## `ed memory stack status`

```
$ ed memory stack status
running on TUF Wired, cpu, reached on port 4820
SERVICE   STATUS                      PORTS
api       Up 28 minutes               127.0.0.1:4820->4820/tcp
postgres  Up About an hour (healthy)  127.0.0.1:5432->5432/tcp
redis     Up About an hour (healthy)  127.0.0.1:6379->6379/tcp
```

Takes `--json`. The JSON shape is
`{deployed:true,deployment,services:[{service,status,ports,running}]}`. With no
saved deployment, JSON succeeds with `{deployed:false,services:[]}`; human mode
exits 1 and points to `ed memory hosts`.

## `ed memory stack up`

Takes `--build` to run `up -d --build`; without it this is `up -d`. Also takes
`--json`. It does not rewrite source, Compose files or `.env`; rerun deploy for
that installation work.

## `ed memory stack down`

Takes `--wipe` to plan `down -v`, deleting the project's named volumes, and
`--json`. The wipe plan changes nothing until `--yes` is also present. A plain
`down` still stops the stack immediately and preserves its data.

`--wipe` is irreversible. It removes Postgres memory, the vault, Ollama models,
the speech model and the GPU reranker cache where present. Export with
`ed memory export <dir> --include-media` first. The deployment record and
local companion configuration survive, but the deleted volume contents do not.

## `ed memory stack restart`

Takes `--json`. This uses Compose `restart`; it does not rebuild images or
recreate containers with changed environment.

## `ed memory stack logs`

```
ed memory stack logs [<service>] [--tail <n>] [--json]
```

Reads the whole stack's logs, or one service's. `--tail` defaults to 100 and
must be positive. Output is non-following and has no color. `--json` is
`{service,lines}`, where `service` is null for the whole stack.

## `ed memory stack env`

Prints the environment file the stack is given, rendered from your
configuration. Secrets are blank unless `--reveal` is passed, because they live
in the Keychain and never in the config file. Takes `--json`, which returns an
object mapping each environment key to its rendered string value.

`--reveal` prints connector tokens, provider keys and passwords to stdout,
including in JSON. Do not use it in shared terminals, captured logs or CI
artifacts.

## Where to go next

- [`ed memory hosts`](./hosts.md) lists where it could run.
- [`ed memory doctor`](./doctor.md) checks it once it is up.

- [`ed memory`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
