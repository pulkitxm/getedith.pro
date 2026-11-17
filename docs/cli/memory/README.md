# `ed memory`

`ed memory` talks to Edith's memory backend. Memory stores notes,
recordings, photos, videos and PDFs as append-only episodes in Postgres, keeps
original files in its vault, and deduplicates sources by their SHA-256 content
hash.

Run the backend with Docker Compose from `apps/companion`, or let
[`ed memory deploy`](./deploy.md) install and start it on a registered
machine. The CLI reaches a remote deployment through a saved `ed machines`
port forward.

The endpoint resolution order is: `--endpoint`, `EDITH_MEMORY_URL`, the URL
saved by the app, the localhost port saved by `ed memory deploy`, then
`http://127.0.0.1:4820`. An invalid saved or supplied URL falls back to the
deployed localhost port, or to port 4820 when there is no deployment record.

Chat, conversation history, deletion, memory search, episode reading, and
indexing use the same typed operations in the app and CLI. Deleting a
conversation requires confirmation in the app and a preview followed by
`--yes` in the CLI.

For the machinery behind these commands, start at
[how Memory works](./concepts.md), the overview, then go deep:
[memory](./concepts-memory.md), [ingestion](./concepts-ingestion.md),
[chunks, embeddings and search](./concepts-search.md),
[asking and chatting](./concepts-chat.md),
[the learning loop](./concepts-learning.md),
[reasoning it does on its own](./concepts-brain.md) and
[not being a yes-man](./concepts-friend.md).

## At a glance

| Command | What it does |
| --- | --- |
| `ed memory` | Runs `ed memory status`, the default subcommand. |
| `ed memory status` | Counts stored records and episodes waiting to be indexed. |
| `ed memory stop` | Stops a reply that is still being written. |
| `ed memory doctor` | Checks storage, migrations, search dependencies, media tools and reasoning configuration. |
| `ed memory search <query>` | Searches indexed memory with hybrid retrieval. |
| `ed memory index` | Embeds episodes that are waiting to be indexed. |
| `ed memory ingest <path>` | Sends a note, recording, photo, video or PDF, or a folder of them, to the backend. |
| `ed memory episodes` | Lists recent episodes, newest first. |
| `ed memory episode <id>` | Reads one episode in full, body included. |
| `ed memory sync <connector>` | Pulls GitHub observations or Notion pages. |
| `ed memory observations` | Lists independent activity records from connectors and Edith usage. |
| `ed memory reflect` | Distills and reconciles beliefs from recent episodes. |
| `ed memory extract` | Pulls typed claims out of recent episodes. |
| `ed memory claims` | Lists extracted claims and their verdicts. |
| `ed memory corroborate` | Checks testable claims against observations. |
| `ed memory runs` | Lists background learning runs and per-step outcomes. |
| `ed memory chat <message>` | Talks with Memory, streamed as it thinks. |
| `ed memory conversations` | Lists chats, or replays one by id. |
| `ed memory forget <id>` | Previews deleting a conversation; `--yes` applies it. |
| `ed memory export <dir>` | Saves remembered records as a restorable bundle; `--include-media` also saves originals. |
| `ed memory import <path>` | Restores a bundle, merging and skipping what already exists. |
| `ed memory erase <id>` | Deletes one episode and everything derived from it. |
| `ed memory wipe` | Deletes the entire memory; the stack and its settings survive. |
| `ed memory nightly` | Runs the nightly learning pipeline right now. |
| `ed memory reason` | Shows or changes the reasoning provider, model and API key. |
| `ed memory ask <question>` | Answers from your own memory, through one lens. |
| `ed memory council <question>` | Asks several lenses and finds the crux they disagree on. |
| `ed memory personas` | Lists the lenses that can answer, and how each thinks. |
| `ed memory lenses` | What each lens learned about being useful to you. |
| `ed memory core` | Reads or edits the standing summary of who you are. |
| `ed memory why <id>` | Prints the whole chain behind a belief, theory or claim. |
| `ed memory hypotheses` | The theories it holds about you, and how they are faring. |
| `ed memory predictions` | What it expects to happen, and what did. |
| `ed memory commitments` | What you said you would do, and what happened. |
| `ed memory discrepancies` | Where your account and the record parted company. |
| `ed memory calibration` | How your account compares with the record, both directions. |
| `ed memory inquire` | The questions it wants to ask you, and your answers. |
| `ed memory entities` | The people, projects and places it knows, with every spelling. |
| `ed memory eval` | Scores the friend layer against the cases it should fail. |
| `ed memory standup <file>` | Records a standup; `--verify` also checks it against the record. |
| `ed memory machines` | Where the stack runs, and what each machine can do. |
| `ed memory hosts` | Machines that could run Memory, and what each one needs. |
| `ed memory deploy` | Choose the machine that runs it, and bring it up there. |
| `ed memory stack` | Start, stop, restart, log and inspect the stack on its host. |
| `ed memory baselines` | Your own delivery baselines, which every signal is measured against. |
| `ed memory connectors` | Tokens for GitHub and Notion, and imports for calendar, music and YouTube. |
| `ed memory facts` | What was true, and what it believed at the time. |
| `ed memory correct <id>` | Retires a wrong belief, or rewrites it in your words. |
| `ed memory weekly` | The wider weekly pass: relate, reopen, retire. |
| `ed memory db` | Migrate, reindex, or rebuild everything derived. |

## Commands

- [`ed memory hosts`](./hosts.md)
- [`ed memory deploy`](./deploy.md)
- [`ed memory stack`](./stack.md)
- [`ed memory status`](./status.md)
- [`ed memory doctor`](./doctor.md)
- [`ed memory search`](./search.md)
- [`ed memory index`](./index.md)
- [`ed memory ingest`](./ingest.md)
- [`ed memory episodes`](./episodes.md)
- [`ed memory sync`](./sync.md)
- [`ed memory observations`](./observations.md)
- [`ed memory reflect`](./reflect.md)
- [`ed memory beliefs`](./beliefs.md)
- [`ed memory ask`](./ask.md)
- [`ed memory extract`](./extract.md)
- [`ed memory claims`](./claims.md)
- [`ed memory corroborate`](./corroborate.md)
- [`ed memory runs`](./runs.md)
- [`ed memory chat`](./chat.md)
- [`ed memory conversations`](./conversations.md)
- [`ed memory forget`](./forget.md)
- [`ed memory export`](./export.md)
- [`ed memory import`](./import.md)
- [`ed memory erase`](./erase.md)
- [`ed memory wipe`](./wipe.md)
- [`ed memory episode`](./episode.md)
- [`ed memory nightly`](./nightly.md)
- [`ed memory reason`](./reason.md)
- [`ed memory personas`](./personas.md)
- [`ed memory council`](./council.md)
- [`ed memory lenses`](./lenses.md)
- [`ed memory core`](./core.md)
- [`ed memory why`](./why.md)
- [`ed memory hypotheses`](./hypotheses.md)
- [`ed memory predictions`](./predictions.md)
- [`ed memory commitments`](./commitments.md)
- [`ed memory discrepancies`](./discrepancies.md)
- [`ed memory calibration`](./calibration.md)
- [`ed memory inquire`](./inquire.md)
- [`ed memory entities`](./entities.md)
- [`ed memory eval`](./eval.md)
- [`ed memory standup`](./standup.md)
- [`ed memory machines`](./machines.md)
- [`ed memory baselines`](./baselines.md)
- [`ed memory connectors`](./connectors.md)
- [`ed memory facts`](./facts.md)
- [`ed memory correct`](./correct.md)
- [`ed memory weekly`](./weekly.md)
- [`ed memory db`](./db.md)

## Concept pages

- [How Memory works](./concepts.md)
- [Memory](./concepts-memory.md)
- [Ingestion](./concepts-ingestion.md)
- [Chunks, embeddings and search](./concepts-search.md)
- [Asking and chatting](./concepts-chat.md)
- [The learning loop](./concepts-learning.md)
- [Reasoning it does on its own](./concepts-brain.md)
- [Not being a yes-man](./concepts-friend.md)

## Exit codes

| Code | Meaning |
| --- | --- |
| `0` | Success, including a reachable doctor report whose `ok` is false. |
| `1` | General failure. |
| `2` | Bad usage, including a missing required path or a non-positive limit. |
| `4` | The Memory backend is unreachable, or indexing receives an embedding-service HTTP 502. |

## Notes and gotchas

`--endpoint` wins over `EDITH_MEMORY_URL`, which wins over the app's saved
endpoint, the deployed localhost port, and finally
`http://127.0.0.1:4820`. A remote deployment normally creates and opens its
forward during `ed memory deploy`. If that fails, run
`ed machines forwards on <machine>` and retry `ed memory status`.

Each Markdown file must be no larger than 2MB, recordings, photos and PDFs no
larger than 48MB, and video no larger than 768MB. Anything bigger is skipped
before any request, and note uploads are split into batches of 200 files. The
backend deduplicates by SHA-256 of the content, so ingesting the same file again
is safe and returns `duplicate` with the original episode id.

Search and indexing need the Ollama service and configured embedding model.
Photos also need the configured vision model. Video ingestion additionally
needs `ffmpeg` and `ffprobe` in the API container; `exiftool` enriches photo
metadata when present. `ed memory doctor` reports these prerequisites.

## Where to go next

Use [`ed machines`](../machines/README.md) to create and open a port forward. Read
[conventions and contracts](../conventions.md) for JSON, stdout, stderr and exit
code guarantees shared by every command.

- [All `ed` commands](../README.md)
