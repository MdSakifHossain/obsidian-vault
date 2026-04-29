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

## Type 1 Installation (~/.local/bin)
### Prerequisite

#### Verify if its in your PATH:

```bash
if [[ ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
  echo "Yes, it's there"
else
  echo "No, not in PATH"
fi
```

#### If it's NOT in your PATH (Ubuntu usually has it):

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

#### Verify Again:

```sh
if [[ ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
  echo "Yes, it's there"
else
  echo "No, not in PATH"
fi
```

---

### Installation

#### Keep in mind

1. **Check if destination exists** before copying
2. **Check if already installed** (optional but nice)
3. **Ask for sudo only when needed**
4. **Uninstall should be safe** (don't delete random stuff)

#### Minimal Install Example

```sh
# Copy script
cp mycommand ~/.local/bin/

# Add Permission
chmod +x ~/.local/bin/mycommand

# Confirm Installation
echo "Installed to ~/.local/bin/mycommand"
```

---
### Uninstall

#### Minimal Uninstall Example

```sh
# Remove the actual file
rm -f ~/.local/bin/mycommand

# Confirm Uninstallation
echo "Removed ~/.local/bin/mycommand"
```

## Type 2 Installation (/usr/local/bin)


its kinda simple AF

- make your script
- make it executable: `chmod +x <your-script>`
- copy/move your script to `/usr/local/bin` (`sudo` needed)

Done.

update the command:

- edit <your-script>`

