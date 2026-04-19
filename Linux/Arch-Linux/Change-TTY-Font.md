# Change TTY Font

⬅️ [Arch Linux](./Arch-Linux.md)

- **No .ttf allowed:** The TTY is a dumb screen. It only takes `.psf.gz` (ancient bitmap pictures), not modern `.ttf` math fonts.
- **`kbd` package:** Pre-installed. Gives you the default boring font (`latarcyrheb-sun16`) and the folder to hold them (`/usr/share/kbd/consolefonts/`).
- **External packages (like `terminus-font`):** Optional. Just drops extra fonts into `kbd`'s folder so you have choices.
- **How to change:**
  1. Test it: `setfont ter-v20n` _(never type the .psfu.gz part)_
  2. Save it: Change `FONT=ter-v20n` on `/etc/vconsole.conf`
  3. Reboot.
