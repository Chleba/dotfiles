# tmux

Tracked: `tmux.conf` → copy to `~/.config/tmux/tmux.conf`.

Session snapshots are **intentionally not tracked** — this repo is public and snapshots contain
window names, working directories and running commands.

## Setup on a new machine

```bash
mkdir -p ~/.config/tmux ~/.tmux/plugins
cp <repo>/.config/tmux/tmux.conf ~/.config/tmux/tmux.conf
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
tmux                       # start server
# inside tmux: press C-s then I  → installs dracula, tmux-resurrect, tmux-continuum
```

## Session auto-restore (continuum)

- `@continuum-restore 'on'` in tmux.conf auto-restores the last saved sessions when the tmux
  server starts — on every machine, no data transfer needed.
- tmux-continuum saves a snapshot every 15 minutes to `~/.local/share/tmux/resurrect/`.
- Manual: `C-s C-s` saves, `C-s C-r` restores.

## Moving current sessions to another machine (private, not via this repo)

```bash
rsync -av ~/.local/share/tmux/resurrect/ othermachine:.local/share/tmux/resurrect/
```
