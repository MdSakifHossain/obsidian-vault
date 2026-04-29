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

**If it's NOT in your PATH (Ubuntu usually has it):**

Bash:

```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Zsh:

```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

### Verify Again:

```sh
if [[ ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
  echo "Yes, it's there"
else
  echo "No, not in PATH"
fi
```
 
### Installation

**Keep in Mind:**

1. **Check if destination exists** before copying
2. **Check if already installed** (optional but nice)
3. **Ask for `sudo` only when needed**
4. **Uninstall should be safe** (don't delete random stuff)

**Minimal Install Example:**

```sh
# Copy script
cp mycommand ~/.local/bin/

# Add Permission
chmod +x ~/.local/bin/mycommand

# Confirm Installation
echo "Installed to ~/.local/bin/mycommand"
```

### Uninstall

- Remove the actual file. `rm -f ~/.local/bin/mycommand`

Done.