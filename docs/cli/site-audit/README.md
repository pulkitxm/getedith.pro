# `ed site-audit`

`ed site-audit` audits a site the same way the Site Audit screen does: projects, discovered pages, the page scores switch, and saved runs. The background agent stores the projects. Edith or `edithd` has to be running.

[The `ed` command line](../README.md)

| Command | What it does |
| --- | --- |
| [`ed site-audit ls`](./ls.md) | Lists saved projects. |
| [`ed site-audit create`](./create.md) | Creates a project from a site URL. |
| [`ed site-audit rename`](./rename.md) | Renames a project. |
| [`ed site-audit delete`](./delete.md) | Deletes a project after `--yes`. |
| [`ed site-audit show`](./show.md) | Shows one project and its page selection. |
| [`ed site-audit pages`](./pages.md) | Discovers pages and changes the selection. |
| [`ed site-audit scores`](./scores.md) | Turns page scores on or off for the next audit. |
| [`ed site-audit start`](./start.md) | Audits the selected pages. |
| [`ed site-audit stop`](./stop.md) | Cancels a running audit after `--yes`. |
| [`ed site-audit run`](./run.md) | Shows one run, its issues, and a social card. |

`ls` is the default, so a bare `ed site-audit` lists projects. `ls` is also `list`, and `delete` is also `rm`.
