![Dwm](https://raw.githubusercontent.com/antoniosarosi/dotfiles/master/.screenshots/dwm.png)

***Language***
- [🇪🇸 Español](./README.es.md)
- 🇩🇪 Deutsch
- [🇺🇸 English](README.md)

Meine eigene gepatchte Version von DWM **[dwm](https://dwm.suckless.org/)**.

Meine Patches:
- [autostart](https://dwm.suckless.org/patches/autostart/dwm-autostart-20200610-cb3f58a.diff)
- [restartsig](https://dwm.suckless.org/patches/restartsig/dwm-restartsig-20180523-6.2.diff)
- [attachaside](https://dwm.suckless.org/patches/attachaside/dwm-attachaside-6.1.diff)
- [focusonactive](https://dwm.suckless.org/patches/focusonnetactive/dwm-focusonnetactive-6.2.diff)
- [warp](https://dwm.suckless.org/patches/warp/dwm-warp-6.2.diff)
- [rotatestack](https://dwm.suckless.org/patches/rotatestack/dwm-rotatestack-20161021-ab9571b.diff)
- [systray](https://dwm.suckless.org/patches/systray/dwm-systray-20200610-f09418b.diff)
- [scheme switch](https://dwm.suckless.org/patches/scheme_switch/dwm-scheme_switch-20170804-ceac8c9.diff)
- [fullgaps](https://dwm.suckless.org/patches/fullgaps/dwm-fullgaps-20200508-7b77734.diff)
- [gridmode](https://dwm.suckless.org/patches/gridmode/dwm-gridmode-20170909-ceac8c9.diff)
- [columns](https://dwm.suckless.org/patches/columns/dwm-columns-6.0.diff)
- [pertag](https://dwm.suckless.org/patches/pertag/)
- [cyclelayouts](https://dwm.suckless.org/patches/cyclelayouts/dwm-cyclelayouts-20180524-6.2.diff)

Um dwm auf deinem system installieren musst du diese Abhängigkeiten installieren:
```bash
yay -S nerd-fonts-ubuntu-mono
```
Ich nutze immer die Schriftart und icons.
Du baurachst auch meine eigene Version von 
**[dwmblocks](https://github.com/antoniosarosi/dwm/tree/master/dwmblocks)**
und die **[~/.local/bin](https://github.com/antoniosarosi/dotfiles/tree/master/.local/bin)**
Scripts.

```bash
# dwm & dwmblocks
cd ~/.config
git clone https://github.com/antoniosarosi/dwm.git
mkdir -p ~/.local/share/dwm
ln -s ~/.config/dwm/autostart.sh ~/.local/share/dwm

# Scripts
mkdir -p ~/.local/bin
cd ~/.local/bin
curl -sL "https://raw.githubusercontent.com/antoniosarosi/dotfiles/master/.local/bin/battery" -o battery
curl -sL "https://raw.githubusercontent.com/antoniosarosi/dotfiles/master/.local/bin/volume" -o volume
curl -sL "https://raw.githubusercontent.com/antoniosarosi/dotfiles/master/.local/bin/percentage" -o percentage
curl -sL "https://raw.githubusercontent.com/antoniosarosi/dotfiles/master/.local/bin/brightness" -o brightness
chmod 755 battery volume percentage brightness

# Diese scripts haben Abhängigkeiten
sudo pacman -S pacman-contrib brightnessctl pamixer upower
```

Schreibe das in **~/.xprofile**:

```bash
export PATH=$HOME/.local/bin:$PATH
```

Erstelle *dwm* und *dwmblocks* und erstelle eine neue *xsession*:

```bash
cd ~/.config/dwm
sudo make clean install
cd ~/.config/dwm/dwmblocks
sudo make clean install
sudo cp ~/.config/dwm/dwm.desktop /usr/share/xsessions
```

Die *autostart* Datei befindet sich in **~/.dwm/autostart.sh**.
Teste es mitTest it with **[Xephyr](https://wiki.archlinux.org/index.php/Xephyr)**:

```bash
Xephyr -br -ac -noreset -screen 1280x720 :1 &
DISPLAY=:1 dwm
```

Wenn du die bar bearbeiten willst öffne diese **~/.config/dwmblocks/config.h**
und aendere Zeilen code

```cpp
static const Block blocks[] = {
//   Icon    Command                          Update Interval     Update Signal
    { "  ", "checkupdates | wc -l",                 60,               0 },
    { "",    "brightness",                           2,                0 },
    { "",    "volume",                               2,                0 },
    { "",    "battery",                              60,               0 },
    { "",    "date '+ %d/%m/%Y   %H:%M%p'",        5,                0 },
};
```

Dann recompile *dwmblocks* und starte *dwm* neu mit **mod + control + r**.

```bash
cd ~/.config/dwm/dwmblocks
sudo make clean install
```

Wenn das vertig ist kannst du dich einloggen. Aber vergiss nicht, nicht, nicht alle Tastenkombinationen werden funktionieren wenn du nicht die gleichen Programme die ich benutze installiert hat.
schau dir mal [mein dotfiles repo](https://github.com/antoniosarosi/dotfiles#keybindings).
