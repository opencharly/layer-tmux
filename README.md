# layer-tmux

Terminal multiplexer for OpenCharly containers — persistent, detachable
terminal sessions.

The `tmux` candy installs the `tmux` package (same name on RPM, DEB, and PAC
distros), so the binary lands at `/usr/bin/tmux`. tmux is the multiplexer used by
Charly's typed terminal provider: it starts isolated detached session servers
with no controlling TTY and lets sessions outlive disconnects.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `tmux` |
| Package | `tmux` (RPM / DEB / PAC) |
| Binary | `/usr/bin/tmux` |
| Service / port | none (one-shot CLI; sessions are detached server processes) |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-tmux:v2026.240.0202'
```

Then, inside the built image:

```bash
tmux new-session -d -s work    # start a detached session
tmux has-session -t work       # confirm it is live
tmux attach -t work            # attach; detach with Ctrl-b d
tmux kill-session -t work      # tear it down
```

The candy's `plan:` asserts the binary at `/usr/bin/tmux`, the package
registered, `tmux -V` printing a version banner, and a real detached session
created, confirmed live, and killed.

## Layout

- `charly.yml` — the `tmux:` candy entity (the `package:` section and the
  `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Closest skill: `/charly-infrastructure:tmux-layer` — this repo carries no
  per-repo owning skill (recorded against opencharly/opencharly#291)
- `/charly-core:shell` — run tmux inside a container
- `/charly-automation:tmux` — the typed persistent terminal / terminal-agent
  session surface backed by isolated tmux control-mode servers
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
