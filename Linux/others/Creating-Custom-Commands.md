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


## Type 2 (/usr/local/bin)

### Install

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