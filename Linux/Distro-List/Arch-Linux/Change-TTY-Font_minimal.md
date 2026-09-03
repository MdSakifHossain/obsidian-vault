# Change TTY Font Minimal

⬅️ [Arch Linux](./Arch-Linux.md)

# **Steps**

- `sudo pacman -Syu`
- `sudo pacman -S terminus-font nano`
- `sudo nano /etc/vconsole.conf`

> Change `FONT=some-default-font` to `FONT=ter-132n` and Save

- `reboot` OR `sudo setfont ter-132n` for **immediate action**
