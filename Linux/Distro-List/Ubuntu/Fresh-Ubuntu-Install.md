# Fresh Ubuntu Install

⬅️ [Ubuntu](Ubuntu.md)

> Things to do after a Fresh Ubuntu Install

_It's devided into 3 Phase._

<img
  src="https://i.giphy.com/gUnRTJ0zqHJRe.webp"
  alt="useless-image"
  width="50%"
/>

## Downloading Phase

Open Terminal: `Ctrl + Alt + T`

```sh
mkdir ~/.themes ~/.icons ~/.fonts && \
sudo apt update && sudo apt upgrade -y && \
sudo apt-get install git curl gnome-tweaks gnome-shell-extension-manager -y && \
sudo snap install brave && \
sudo snap install chromium && \
sudo snap install opera && \
sudo snap install firefox && \
sudo snap install obsidian --classic && \
sudo snap install obs-studio && \
sudo snap install vlc && \
sudo snap install qbittorrent-arnatious && \
sudo apt install gnome-boxes
```

1. Download [VSCode](https://code.visualstudio.com/download) `.deb`
2. Download [Chrome](https://www.google.com/chrome/) `.deb`
3. Download [Node.js](https://nodejs.org/en/download)
4. Download [AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher) `.deb`
5. Download [OpenRGB](https://openrgb.org/) `(Debian Bookworm .deb)`

### Simplified one liner

**One Liner Rule:**

- Start with the command: `firefox`
- Add a **space**
- Then a **backslash** (`\`)
- **No space after the backslash**
- Press **Enter**
- Write **1st link**
- Add a **space**
- Then a **backslash** (`\`)
- **No space after the backslash**
- Press **Enter**
- Repeat for each link
- On the last line, add `&>/dev/null & disown`

Note: *the backslash must be the last character on the line (no trailing space), and each new line starts with the next URL.*

### Best for Automation

```bash
urls=(
  "https://code.visualstudio.com/Download"
  "https://www.google.com/chrome/"
  "https://nodejs.org/en/download"
  "https://github.com/TheAssassin/AppImageLauncher/releases"
  "https://openrgb.org/releases.html"
)

firefox "${urls[@]}" &>/dev/null & disown
```

Doing same thing but in a more maintainable way. That `urls[@]` and the `spread operator` in js `(...)` does the same thing. 
## Restoration Phase

1. `Log Into` Essential Accounts on `Brave Browser`:
   - [Proton](https://pass.proton.me/)
   - [Google](https://accounts.google.com/)
   - [Whatsapp](https://web.whatsapp.com/)
   - [Instagram](https://www.instagram.com/)
   - [Facebook](https://www.facebook.com/)
   - [Telegram](https://web.telegram.org/a/)
   - [Github](https://github.com/login)
   - [X / Twitter](https://x.com/)
   - [Programming Hero](https://web.programming-hero.com/dashboard)

## Setup Phase

1. Setup [WARP Client](https://developers.cloudflare.com/warp-client/get-started/linux/)
2. Setup `OpenRGB as Daemon on Ubuntu`
3. Setup `VSCode with the Minimal Looks`
4. Setup `Terminal for Good Looks`
5. Setup `The whole Ubuntu for Good Looks`

<img
  src="https://i.giphy.com/OuQmhmAAdJFLi.webp"
  alt="useless-image"
/>

<img
  src="https://i.giphy.com/3y58hphppxTg60gYlc.webp"
  alt="useless-image"
/>
