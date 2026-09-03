# Change TTY Font

⬅️ [Arch Linux](./Arch-Linux.md)

- **No `.ttf` allowed:** The TTY is a dumb screen. It only takes `.psf.gz` (ancient bitmap pictures), not modern `.ttf` math fonts.

- **`kbd` package:** Pre-installed. Gives you the default boring font (`latarcyrheb-sun16`) and the folder to hold them (`/usr/share/kbd/consolefonts/`).

- **External font packages:** Optional. Installing them simply copies more `.psf.gz` fonts into `/usr/share/kbd/consolefonts/`.

## Install Extra Fonts

Example: install the popular Terminus font pack.

```bash
sudo pacman -S terminus-font
```

After installation, new fonts automatically appear inside:

```bash
/usr/share/kbd/consolefonts/
```

You can list them:

```bash
ls /usr/share/kbd/consolefonts/
```

Or search only Terminus fonts:

```bash
ls /usr/share/kbd/consolefonts/ | grep ter-
```

## Change Font

1. Test a font temporarily:

```bash
sudo setfont ter-132n
```

> Never type the `.psfu.gz` part.

2. Save it permanently:

Edit:

```bash
/etc/vconsole.conf
```

Add/change:

```bash
FONT=ter-132n
```

3. Reboot.

> Terminal is sexy again hehe buoy..
