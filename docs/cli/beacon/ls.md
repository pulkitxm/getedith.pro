# `ed beacon ls`

Lists the applications Beacon has indexed, either in full or ranked against a
query exactly as the bar ranks them.

Usage:

```
ed beacon ls [--search <query>] [--limit <n>] [--json]
```

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--search` | text | none | Ranks the index against this query, matcher and frequency boost included. |
| `--limit` | integer | 50 | Prints at most this many applications; `0` means no limit. |
| `--json` | flag | off | Emits one JSON array on stdout. |

`ed beacon list` is an alias, and `ed beacon` with no subcommand runs this one.

The plain response is one line per application, the name then its path:

```
$ ed beacon ls --search chrome
Google Chrome  /Applications/Google Chrome.app
```

The JSON response is an array of objects with three stable fields; `bundleID` is
`null` for a bundle whose `Info.plist` could not be read:

```json
[
  {
    "name": "Google Chrome",
    "path": "/Applications/Google Chrome.app",
    "bundleID": "com.google.Chrome"
  }
]
```

Without `--search` the index is printed in alphabetical order by name, ties
broken by path, and the frequency ledger is ignored. With `--search` the order
is the bar's: every letter of the query has to appear in the name in order, word
starts and adjacent runs score higher than scattered letters, an exact name
beats a prefix, a shorter name wins a tie, and what you open often is nudged up.
`--limit` truncates last in both cases.

Exit codes:

| Code | Meaning |
| --- | --- |
| 0 | The listing printed, including an empty one. |
| 2 | `--limit` was negative, or the command line was invalid. |
| 3 | Nothing is indexed yet. |

An index that does not exist is a not-found, and an index that exists but has
nothing matching the query is an empty success:

```
$ ed beacon ls
error: no applications are indexed yet
hint: run `ed beacon reindex` with Edith running

$ ed beacon ls --search zzzz
no application matches
```

The command reads the cache under the extension's data root and never scans
the disk itself. It is served by the installed extension through Edith's CLI
and is only as current as the last rebuild. Use `search` for aliases, utilities,
library entries and other launcher result types.

## Where to go next

- [`ed beacon reindex`](./reindex.md), when something new is missing
- [`ed apps`](../apps/README.md), for the applications that are actually running
- [`ed beacon`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
