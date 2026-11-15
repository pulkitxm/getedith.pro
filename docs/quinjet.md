# Quinjet

Quinjet reviews pull requests and follows live workspace changes from an Edith
panel tab. Turn it on in the Library, or run:

```sh
ed extensions enable quinjet
ed tools install quinjet
```

The extension needs the `quinjet` executable. When it is missing, the Quinjet
page shows an Install Quinjet button and nothing else to do: Edith uses Homebrew
when it is present and otherwise downloads the verified release binary into
Edith's tools folder (see [Tools](./tools.md)). `ed tools install quinjet` runs
the same installer from a terminal.

The optional GitHub CLI adds the pull request widget. When it is missing, the
widget offers Install GitHub CLI; when it is signed out, it offers Sign in to
GitHub, which opens Settings > Tools and starts the browser sign in with a
one-time code. No terminal is involved in either case. Verify the installation:

```sh
ed tools ls --json | jq '.[] | select(.id == "quinjet")'
ed extensions info quinjet --json
```

Choose `embedded` to run workspaces inside Edith. Choose `cmux` to open them in
cmux, which must be installed separately in Applications. The default `app`
theme sends Edith's own light and dark palettes to Quinjet. Changing Edith's
theme or appearance updates every open Quinjet session. Choosing a named Quinjet
theme keeps that explicit palette while still following light and dark appearance.
Named themes are discovered from the installed Quinjet version, so new Quinjet
palettes appear without an Edith update.
Both settings are available to scripts:

```sh
ed config set quinjetTerminal embedded
ed config set quinjetTheme app
ed config set quinjetTheme tokyo-night
```

If Quinjet is missing, press Install Quinjet on the page, or retry
`ed tools install quinjet`. A remote machine without Quinjet needs its own copy;
the page names the usual way to get it for that platform. If cmux is unavailable, switch the terminal
back to `embedded`. Disable and re-enable the extension only to control its
visibility. It does not uninstall the command line tool or erase these settings.
