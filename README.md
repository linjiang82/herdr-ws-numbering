# herdr-ws-numbering

Shows each workspace's number (the one `prefix+1..9` switches to) in the Herdr sidebar.

Herdr plugins can't draw UI, so this reports the number as custom workspace
metadata (`$num`) and the sidebar layout renders it.

## Install

Requires `jq` and Herdr >= 0.9.1.

```bash
herdr plugin link /path/to/herdr-ws-numbering
```

Add `$num` to the Space rows in `~/.config/herdr/config.toml`:

```toml
[ui.sidebar.spaces]
rows = [["state_icon", { token = "$num", fg = "#888888" }, "workspace"], ["branch", "git_status"]]
```

Then `herdr server reload-config`.

## How it updates

`bin/ws-numbering` renumbers every workspace on server startup and on
`workspace.created`, `workspace.closed`, `workspace.moved` and
`workspace.reordered`. Run it manually with:

```bash
herdr plugin action invoke local.ws-numbering.refresh
```

## Format

Create `$(herdr plugin config-dir local.ws-numbering)/config`:

```bash
FORMAT='[%s]'
```

## Notes

Custom rows only apply to the expanded sidebar; collapsed and mobile views keep
their compact layouts.
