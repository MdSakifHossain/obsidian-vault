```sh
#!/usr/bin/env bash
set -e

DEFAULT_DIR="command"

# Resolve input
if [ -n "$1" ]; then
    src="$1"
else
    read -p "Enter script path [default: $DEFAULT_DIR/]: " input
    src="${input:-$DEFAULT_DIR}"
fi

# If directory, pick first file inside
if [ -d "$src" ]; then
    file=$(find "$src" -maxdepth 1 -type f | head -n 1)
    if [ -z "$file" ]; then
        echo "❌ No files found in directory '$src'"
        exit 1
    fi
    src="$file"
fi

# Validate source
if [ ! -f "$src" ]; then
    echo "❌ File '$src' not found"
    exit 1
fi

command_name=$(basename "$src")
target_path="/usr/local/bin/$command_name"

# Determine install vs update
if [ -f "$target_path" ]; then
    echo "🔄 Updating '$command_name'..."
else
    echo "📦 Installing '$command_name'..."
fi

# Ensure executable
chmod +x "$src"

# Atomic install
tmp_path="/tmp/${command_name}_$$"
cp "$src" "$tmp_path"

sudo mv "$tmp_path" "$target_path"
sudo chmod +x "$target_path"

echo "✅ Done. Run with: $command_name"
```

this is the install script.

```sh
#!/usr/bin/env bash

DEFAULT_DIR="command"

# Resolve input
if [ -n "$1" ]; then
    src="$1"
else
    read -p "Enter script name or path [default: $DEFAULT_DIR/]: " input
    src="${input:-$DEFAULT_DIR}"
fi

# If directory, infer command name from first file
if [ -d "$src" ]; then
    file=$(find "$src" -maxdepth 1 -type f | head -n 1)
    if [ -z "$file" ]; then
        echo "❌ No files found in directory '$src'"
        exit 1
    fi
    command_name=$(basename "$file")
else
    command_name=$(basename "$src")
fi

target_path="/usr/local/bin/$command_name"

echo "Removing '$command_name'..."

if [ -f "$target_path" ]; then
    sudo rm -f "$target_path"
    echo "✅ Removed successfully."
else
    echo "⚠️ '$command_name' not found in /usr/local/bin"
fi
```

i want you to make me a single merged script with subcommands like:
`./installer.sh install|i` to install the script or updated the modified the script.
`./installer.sh uninstall|remove|rm` to remove/uninstall the installed script. and. the default value for the `installer install` will be the command dir. and if i set something like: `./installer install -y` to directly install the script. and uninstall will do it to do what it has.
