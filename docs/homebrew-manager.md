# Homebrew Packages

The Homebrew page provides a native, reviewable interface for formulae and casks. Turn on Homebrew in Library, then open **Homebrew** from the sidebar or Library.

When Homebrew is not on this Mac, the page shows an Install Homebrew button. Edith downloads the signed `Homebrew.pkg` from the latest `Homebrew/brew` release, checks its digest and opens it in Installer, which asks for your Mac password once. The page picks Homebrew up as soon as Installer finishes. Settings > Tools runs the same installer. See [Tools](./tools.md).

## Browse and discover packages

Installed shows the selected package kind with installed versions and available updates. Packages with an update are sorted first. Discover searches Homebrew metadata and shows up to 40 exact results with descriptions, versions, homepages, and installed state.

The Formulae and Casks control changes both the installed inventory and search domain. The selected kind is saved with Homebrew settings. Refresh re-reads installed and outdated metadata without changing any package.

## Install, upgrade, and uninstall

Install and Upgrade always target one validated package token. Uninstall presents the exact package and kind in a confirmation dialog before Homebrew starts. Only one operation runs from the page at a time, and the active operation can be cancelled.

Package operations invoke the local `brew` executable directly. Every process runs noninteractively with automatic updates, analytics, and environment hints disabled. Reads are limited to 60 seconds and mutations to 30 minutes. Retained output is capped at 2 MB. Cancelling a mutation terminates its full process group.

Some casks need administrator authentication or interactive input. Edith reports that requirement and leaves the package unchanged instead of asking for a password.

## Command line

Enable Homebrew and open its page to load the installed inventory. The active worker exposes the same cached inventory as a typed Home surface snapshot through `ed invoke homebrew surface.snapshot --json -`. Supply a complete `SurfaceSnapshotRequest` with target `home` and an `extension:homebrew` tile; the request follows the shared surface contract.

Package searches and mutations remain on the Homebrew page, with their confirmation and cancellation controls. See the [public invocation reference](./cli/invoke/README.md) for the gateway's worker availability and JSON limits.
