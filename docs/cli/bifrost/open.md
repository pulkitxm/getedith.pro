# `ed bifrost open`

Asks the running menu bar app to open the Bifrost bar, the same panel the global
shortcut opens, optionally with text already in the field.

Usage:

```
ed bifrost open [<query>] [--json]
```

Arguments and options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<query>` | text | empty | Fills the search field before the bar appears. |
| `--json` | flag | off | Emits one JSON document on stdout. |

The plain response is one line:

```
launcher requested
```

The JSON response has three stable fields:

```json
{
  "operation": "bifrost.open",
  "requested": true,
  "query": "safari"
}
```

`requested` means the running extension accepted the request to show the panel.
The command does not wait for panel positioning, rendering or a selection.
Dismissing the bar does not change the already completed command.

An explicit open always shows the bar. Repeating `ed bifrost open` clears the
field and keeps the bar open; a supplied query replaces the field contents.
The global launcher shortcut still toggles visibility. For example,
`ed bifrost open "12 km in miles"` opens a conversion for review, while
`ed bifrost open "think compare two approaches"` prefills a Thinking question.
Neither request executes a result or submits a question.

Queries must fit in 1,024 UTF-8 bytes and contain no NUL characters. Privacy mode
can hide Bifrost and reject the request. CLI and surface opens use the same
validation, including when privacy settings change between requests.

The field is an ordinary text field: ⌘A selects all, ⌘C, ⌘V and ⌘X work, and
⌘Z and ⇧⌘Z undo and redo. The bar routes those itself, because a menu bar app
has no Edit menu to carry them.

Return runs the selected row: an application opens, an answer goes to the
pasteboard. `⌥`-return copies whatever is selected instead, so an application
row hands you its path rather than launching it, and either way the bar
dismisses.

The shortcut is `⌥space` unless you have rebound it under Shortcuts in Bifrost
settings, which writes `bifrostHotKeyCode`, `bifrostHotKeyMods` and `bifrostHotKeyLabel`.
The bar always opens centered near the top of the screen under the pointer, at
one fixed size that does not change while you type. Drag its search or footer
strip to move it; it snaps back to center when dropped close to it, and the
next open is centered again.

Exit codes:

| Code | Meaning |
| --- | --- |
| 0 | The request was sent. |
| 2 | The command line or query was invalid. |
| 4 | Bifrost is off or hidden by privacy mode, or Edith's menu bar app is not running. |

The extension is checked first, before the app, so an off extension is reported
as an off extension even when Edith is closed:

```
ed extensions enable bifrost
ed bifrost open
```

The command never starts Edith by itself, never changes the extension setting
and never touches the frequency ledger: nothing is recorded until you actually
pick something in the bar.

## Where to go next

- [`ed bifrost ls`](./ls.md), to see what the bar can find
- [`ed bifrost`](./README.md), the rest of this group
- [`ed extensions`](../extensions/README.md), to turn Bifrost on
- [All `ed` commands](../README.md)
