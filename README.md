# dotfiles

Personal Linux desktop dotfiles: i3, polybar, lvim, kitty, rofi, tmux.

The repo mirrors `$HOME` — every file here belongs at the same path in your home directory
(e.g. `.config/tmux/tmux.conf` → `~/.config/tmux/tmux.conf`). Files are **copied into place,
not symlinked** — after changing something here, copy it to the live location again.

## Install

```bash
git clone git@github.com:Chleba/dotfiles.git ~/Documents/dotfiles
cd ~/Documents/dotfiles

# everything at once (review first — this overwrites existing files, never deletes)
rsync -av .config/ ~/.config/
```

Or just one component:

```bash
cp -r .config/tmux ~/.config/
```

## Components

| Path | What | Notes |
|------|------|-------|
| `.config/tmux/` | tmux config | prefix `C-s`, Dracula theme, session auto-restore — details in [.config/tmux/README.md](.config/tmux/README.md) |
| `.config/i3/` | i3 window manager config + scripts | |
| `.config/polybar/` | polybar config + launch/helper scripts | |
| `.config/kitty/` | kitty terminal config | |
| `.config/lvim/` | LunarVim config + plugin lockfile | install [LunarVim](https://www.lunarvim.org) first, then copy |
| `.config/rofi/` | rofi launchers, menus and themes | scripts in `.config/rofi/bin/` |

## tmux session restore

`tmux-continuum` saves all sessions every 15 minutes and `tmux-resurrect` restores them
automatically when the tmux server starts (`@continuum-restore 'on'` in the config).
Manual keys: `C-s C-s` save, `C-s C-r` restore.

Setup on a new machine:

```bash
mkdir -p ~/.config/tmux ~/.tmux/plugins
cp .config/tmux/tmux.conf ~/.config/tmux/tmux.conf
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
tmux            # start tmux, then press C-s + I to install plugins
```

Session snapshots live locally in `~/.local/share/tmux/resurrect/` and are **intentionally not
tracked** in this public repo — they contain window names, working directories and running
commands. To carry current sessions to another of your own machines, transfer that folder
privately (rsync/scp), not via git.
