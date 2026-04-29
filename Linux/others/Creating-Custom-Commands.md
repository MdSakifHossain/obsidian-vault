# Creating Custom Commands

`/usr/local/bin` && `~/.local/bin`. These are the two standard locations, and the **only** difference is **who** can run the script and **who** needs permission to install it.

| Feature                     | `~/.local/bin` (User)                            | `/usr/local/bin` (System)                          |
| :-------------------------- | :----------------------------------------------- | :------------------------------------------------- |
| **Who can run it?**         | **Only you** (your user account).                | **Everyone** on the computer.                      |
| **Need `sudo` to install?** | **No.** You own the folder.                      | **Yes.** It's a protected system folder.           |
| **Need `sudo` to run?**     | **No.**                                          | **No.** (Only needed to *install* or *edit*).      |
| **Best for...**             | Personal scripts, tools you don't want to share. | Tools you want all users on the machine to access. |

**Summary:**
- If it's just for **you**, use `~/.local/bin` (easiest, no `sudo` ever).
- If you want **everyone** to use it, use `/usr/local/bin` (requires `sudo` once to install).

## Type 1 (~/.local/bin)
### Prerequisite

**Verify if its in your PATH:**

```bash
if [[ ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
  echo "Yes, it's there"
else
  echo "No, not in PATH"
fi
```

If it's there then Skip to `Installation` Section.

If it's NOT then:

**Bash:**

```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**Zsh:**

```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**Verify Again:**

```sh
if [[ ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
  echo "Yes, it's there"
else
  echo "No, not in PATH"
fi
```

### Installation

**Keep in Mind:**

1. Check if destination exists before copying
2. Check if already installed
3. Ask for `sudo` only when needed
4. Uninstall should be safe (don't delete random stuff)

**Minimal Install Example:**

- Copy script. `cp mycommand ~/.local/bin/`
- Add Permission. `chmod +x ~/.local/bin/mycommand`

### Uninstall

- Remove the actual file. `rm -f ~/.local/bin/mycommand`

Done.

## Type 2 (/usr/local/bin)

### Install

**Keep in Mind:**

1. Check if destination exists before copying
2. Check if already installed
3. Ask for `sudo` only when needed
4. Uninstall should be safe (don't delete random stuff)

**Install Example:**

- make your script
- make it executable: `chmod +x <your-script>`
- copy/move your script to `/usr/local/bin`. (`sudo` needed)

Done.

### Update

- edit `<your-script>` 
- copy/move to `/usr/local/bin`. (`sudo` needed)

Done.

### Uninstall

- remove `<your-script>` from `/usr/local/bin`. (`sudo` needed)

Done.