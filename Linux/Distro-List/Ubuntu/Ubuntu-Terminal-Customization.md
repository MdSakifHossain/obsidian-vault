# Ubuntu Terminal Customization

⬅️ [Ubuntu](Ubuntu.md)

## Steps

```sh
sudo apt install zsh # Install zsh

echo $SHELL # /bin/bash (Expected Output)

# This is the standard Linux command to change your user's default login shell
# chsh = change shell.
# It updates the entry for your user in /etc/passwd (or the shadow database)
# so that any login session for your user starts with zsh by default.
chsh -s $(which zsh)
```

> Exit out the terminal and Log Out and then Log In and Open the terminal.
> 
> Do the zsh setup after opening the terminal

- Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh) on top of zsh
- Install Plugins:
  - [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

> Just clone these 2 plugins into the `$ZSH_CUSTOM` folder and then just add it in the `.zshrc` file and exit and then reopen the termianl.
> 
> Now you are Golden.

- Install [powerlevel10k](https://github.com/romkatv/powerlevel10k)
- Install [Gogh](https://github.com/Gogh-Co/Gogh) (For the texts color and stuffs like that)
