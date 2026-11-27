# YaKlock

YaKlock is a transparent, sticky digital clock for Ubuntu and Kubuntu desktops that keeps the time in sight and stays out of your way.

Resize it, keep it above your windows, adjust its opacity, or hide the decorations until only the digits remain. Right-click to customize it; YaKlock remembers your settings.

Developed and tested on Ubuntu 26.04 LTS with GNOME and KDE Plasma (Wayland sessions).

![YaKlock displaying bright green digits and the date over a desktop window](docs/screenshots/Example.png)

## Install and run

On Ubuntu or Kubuntu, open a terminal and paste:

```bash
(
set -e

# Install dependencies
sudo apt update
sudo apt install -y git desktop-file-utils python3 python3-cairo python3-gi gir1.2-gtk-3.0

# Get YaKlock
git clone https://github.com/bjroberson/yaklock.git
cd yaklock

# Install YaKlock for your user
DATA_HOME="${XDG_DATA_HOME:-$HOME/.local/share}"
mkdir -p "$HOME/.local/bin" "$DATA_HOME/applications" "$DATA_HOME/icons"

install -m 755 yaklock "$HOME/.local/bin/yaklock"
desktop-file-install --dir="$DATA_HOME/applications" \
    --set-key=Exec --set-value="\"$HOME/.local/bin/yaklock\"" \
    io.github.bjroberson.yaklock.desktop
cp -R icons/. "$DATA_HOME/icons/"

# Start YaKlock
"$HOME/.local/bin/yaklock" &
)
```

YaKlock is also available from your desktop's application menu. The installed
launcher uses the absolute executable path so it works even when GNOME Shell
starts without `~/.local/bin` on its `PATH`. Right-click the clock to customize it.

<p>
  <img src="docs/screenshots/RightClick.png" alt="YaKlock right-click menu" width="377">
  <img src="docs/screenshots/Appearance.png" alt="YaKlock Appearance dialog with sliders for time size, date size, and inactive opacity" width="298">
</p>

The checkout includes its window icons. Settings are saved in
`${XDG_CONFIG_HOME:-$HOME/.config}/yaklock/options.json`. YaKlock starts with
fresh settings alongside an existing Seven-Segment Clock installation.

## Desktop environment

YaKlock has been tested on Ubuntu 26.04 LTS with GNOME and KDE Plasma in Wayland sessions.
The clock prefers XWayland when an X display is available so it can request
Always on Top. 


## License

Copyright © 2026 Brian Roberson.

YaKlock, including its launcher and bundled icons, is licensed under the GNU
General Public License, version 3 or any later version
(`GPL-3.0-or-later`). See [LICENSE](LICENSE).

## AI-assisted development

YaKlock is a personal project developed with help from OpenAI's
ChatGPT and Codex for design, coding, debugging, and testing.
The human maintainer sets the direction, reviews changes, performs
manual testing, and makes the final merge and release decisions.

Bugs are still bugs, regardless of who—or what—wrote them.
Please report them in [GitHub Issues](https://github.com/bjroberson/yaklock/issues).
