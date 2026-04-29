# Learning Shell Scripting

## Prerequisite

### Check if it's in your PATH:

```bash
echo $PATH | grep -q "$HOME/.local/bin" && echo "Yes, it's there" || echo "No, not in PATH"
```

### If it's NOT in your PATH (Ubuntu usually has it):

Then you never think about it again.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.bashrc
source ~/.zshrc
```

Now verify:

```bash
echo $PATH | grep -q "$HOME/.local/bin" && echo "Yes, it's there" || echo "No, not in PATH"
```

Done. Now put scripts in `~/.local/bin/` and they just work.

---

## Installation

### Keep in mind

1. **Check if destination exists** before copying
2. **Check if already installed** (optional but nice)
3. **Ask for sudo only when needed**
4. **Uninstall should be safe** (don't delete random stuff)

### Minimal Install Example

```sh
# Copy script
cp mycommand ~/.local/bin/

# Add Permission
chmod +x ~/.local/bin/mycommand

# Confirm Installation
echo "Installed to ~/.local/bin/mycommand"
```

## Uninstall

### Minimal Uninstall Example

```sh
# Remove the actual file
rm -f ~/.local/bin/mycommand

# Confirm Uninstallation
echo "Removed ~/.local/bin/mycommand"
```