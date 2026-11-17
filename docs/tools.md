# Tools

Some extensions drive a command line program: Agents runs Herdr, Code Review runs
Quinjet, Downloads and Music run yt-dlp, Code Stats reads repositories with Git.
Edith installs these for you. You never copy a command into Terminal.

## Where you see them

- **Settings > Tools** lists every tool Edith knows, which extensions use it,
  and its state: Installed with its version, Update available, Not installed, or
  Detected only. Each row has one action (Install or Update), a progress bar with
  Cancel while it runs, and a readable error with Retry when it fails. Tools Edith
  installed are grouped at the top and can be removed from the row's menu.
- **Extension pages** show an inline Install button where a missing tool blocks
  something, for example Install Herdr on an empty Agents page, Install Quinjet on
  the Code Review project picker, Install Git and Install GitHub CLI in Code Stats,
  Install Homebrew on the Homebrew page, Install sshfs on a machine's Tools tab
  and Install FFmpeg in Studio. The button runs the same installer as Settings >
  Tools and shows the same progress. Details on an error opens Settings > Tools.
- **Library** shows a Needs line on an extension's detail with each tool's
  state and an Install button for the missing ones.
- **GitHub sign in**: when the GitHub CLI is installed but signed out, Code
  Stats and the Code Review widget show Sign in to GitHub. It opens Settings > Tools
  and starts the browser sign in; Edith shows the one-time code with a Copy
  button and opens the GitHub device page.

`ed tools ls|install|update|remove` drives the same installer from a terminal.
See [`ed tools`](./cli/tools/README.md) for every tool's source and the exact
search order.

## What gets installed

| Tool | Used by | How Edith gets it |
| --- | --- | --- |
| Homebrew | Homebrew, App Updates | the signed `Homebrew.pkg`, opened in Installer, which asks for your password once |
| Herdr | Agents | the verified release binary |
| Quinjet | Code Review | Homebrew when present, otherwise the verified release binary |
| GitHub CLI | Code Review, LaTeX, Code Stats | Homebrew when present, otherwise the official release zip |
| Git | Code Stats, Cleaner | Apple's Command Line Tools installer |
| yt-dlp | Downloads, Music | the verified release binary |
| FFmpeg | Studio, Downloads, Music | Homebrew, installing Homebrew first when it is missing |
| Deno | Downloads, Music | the verified release zip |
| gallery-dl | Downloads, Music | Homebrew, installing Homebrew first when it is missing |
| Tectonic | LaTeX | the verified release archive |
| ripgrep | Bifrost | Homebrew when present, otherwise the verified release archive |
| sshfs | Machines | the signed FUSE-T and sshfs installer packages |
| TeX Live | LaTeX | detected only; it is a multi-gigabyte installer Edith does not run |

Coding agents such as Claude Code, Codex or Gemini are yours to install. The New
Agent popup marks the ones that are not on this Mac with "Not on this Mac".
Container runtimes for Memory are also yours: the setup sheet shows a Get
Docker button that opens the Docker Desktop download page.

## The Edith tools folder

Direct downloads land in `Tools/bin` inside Edith's Application Support folder:
`~/Library/Application Support/Edith/Tools/bin` for the release app, and a
separate folder for each development build. Every extension searches it first,
so a tool installed once is found everywhere. Downloads are checked against the
release's published SHA-256 digest before they are moved into place; a mismatch
or a cancelled install leaves nothing behind.

`Tools/installed.json` records what Edith installed: the tool, version, method
(direct download, Homebrew or installer package), the files and the date. Tools
you installed yourself are listed and used but never changed or removed.

## Removing a tool

Open Settings > Tools and choose Remove from the tool's row menu, or run
`ed tools remove <tool> --yes`. A direct download deletes its files from
`Tools/bin`. A Homebrew install that Edith made runs `brew uninstall` for that
formula. Installer packages (Homebrew, FUSE-T and sshfs) are left to their own
uninstallers, because their files live outside Edith's folder.

## Bundled instead of installed

Some dependencies are small, redistributable and needed by one extension, so
they ship inside that extension's package instead of being installed:

- **zstd** (BSD license). Agent Usage compiles the zstd decoder from source as
  its native library and streams Codex `.jsonl.zst` journals in process. macOS
  has no `zstd` command, so this replaced a Homebrew dependency.
- **axe-core** (MPL-2.0). Site Audit ships `axe.min.js` and its license as
  resources and runs it in an offscreen web view for accessibility checks, next
  to its own page timing and SEO checks. This replaced Lighthouse, Node.js and
  Chrome.
- **ssh-clipboard**. Machines ships pinned `ssh-clipboard` binaries for macOS
  and Linux on arm64 and x86_64, fetched at packaging time against a recorded
  SHA-256 digest, with the macOS ones signed with Edith's identity. Clipboard
  sync uploads the binary that matches the remote machine instead of using npm.
- **Memory service source**. The Memory package carries the Memory
  service as `companion-source.tar.gz`, so deployment needs no repository
  checkout. Compose runs through the runtime detected on the host.

## Replaced with macOS itself

Keep Awake holds a power assertion through IOKit instead of running
`caffeinate`. Process and battery readings, Lid Awake's sleep state, mounts,
Bifrost's system actions, This Mac's controls in Machines, App Store update
checks, archive reading, skills installs and Studio's media probing all use
macOS frameworks directly, so none of them asks you to install anything.
