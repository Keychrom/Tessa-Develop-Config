# Tessa Develop Config

A curated snapshot of the `~/.config` directory from the Arch Linux machine used
to develop [Tessa](https://github.com/Keychrom/Tessa). It mirrors the live
Vermilion Ink desktop setup: Tessa, Kitty, Starship, Fcitx5/Mozc, and the
session environment.

This is a **public-safe subset**, not a complete backup. Browser profiles and
personal input-method data are intentionally excluded.

## Contents

| Path | Purpose |
| --- | --- |
| `tessa/config` | Live Tessa config: unified control center, layouts, window rules, bar, theme roles, input, XWayland, and bindings |
| `kitty/kitty.conf` | Kitty terminal with the Vermilion Ink palette, JetBrains Mono Nerd Font, powerline tabs, and Japanese CJK fallback |
| `starship.toml` | Starship prompt with host, directory, Git, and language modules |
| `fcitx5/config` | Fcitx5 behavior settings |
| `fcitx5/profile` | Japanese keyboard layout with Mozc as the default input method |
| `fcitx5/conf/classicui.conf` | Fcitx5 candidate window using the `TessaInk` theme and Inter font |
| `fcitx5/conf/notifications.conf` | Fcitx5 notification preferences |
| `environment.d/90-fcitx5.conf` | GTK/Qt/SDL/XIM input-method environment for the Tessa session |

## Intentionally excluded

These files exist in the development machine's `~/.config` but are not part of
this repository:

- `mozilla/` — Firefox profiles, including `logins.db`, `key4.db`,
  `cookies.sqlite`, history, and session data
- `mozc/` — input history, dictionaries, session state, and encryption keys
- `dconf/user` — binary desktop-settings database
- Fcitx5 caches and temporary files such as `cached_layouts` and
  `notifications.conf_*`
- `tessa/config.bak-*` — timestamped local backup
- Lock files, sockets, and other runtime state

The full `~/.config` is about 55 MB. The safe subset here is only a few tens of
kilobytes and contains no credentials or browser data.

## Install

Back up the existing configuration first:

```sh
cp -a ~/.config "$HOME/.config.backup-$(date +%Y%m%d-%H%M%S)"
```

Clone this repository and copy the files into place:

```sh
git clone https://github.com/Keychrom/Tessa-Develop-Config.git
cd Tessa-Develop-Config
cp -a tessa kitty starship.toml fcitx5 environment.d ~/.config/
```

Log out and back in, or restart the relevant service, so Fcitx5 and the session
environment pick up the changes.

Do not overwrite an existing config blindly on a different machine. Review
`tessa/config` first: monitor names, touchpad settings, application IDs, and
keybindings are tuned for this development machine.

## Requirements and notes

- The Tessa config expects the `Inter` and `JetBrainsMono Nerd Font` fonts, plus
  `Noto Sans Mono CJK JP` for Japanese glyphs.
- `wallpaper_image` points to
  `~/Pictures/Wallpapers/vermilion-ink.png`; the image is not included here.
- The Fcitx5 `TessaInk` theme is installed outside `~/.config` and is not
  included.
- Paths in the config use `~` or commands resolved from `PATH`; there is no
  hard-coded `/home/<user>` path.
- `tessa/config` uses `panel_style = unified` and `control_features = all`.
  Change `panel_style = classic` for separate popovers.
- Kitty contains a Nerd Font glyph-based UI. Install a Nerd Font variant if the
  tab bar or icons render incorrectly.

## Related

- [Tessa compositor and panel](https://github.com/Keychrom/Tessa)
- [Tessa website and documentation](https://keychrom.github.io/)
- [Tessa ISO builder](https://github.com/Keychrom/TessaISO)

## Status

- Snapshot date: 2026-11-10
- Source: Arch Linux development machine (`Arch-Suiren`)
- Tessa tree: 0.2.5 development, Zig 0.17 / wlroots 0.20 / scenefx 0.5
