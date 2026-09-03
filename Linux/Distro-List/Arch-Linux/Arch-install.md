# **Arch Install**

⬅️ [Arch Linux](Arch-Linux.md)

## **Steps**

- Open **Gnome Boxes**
- Click on **"+"** icon on **"Top Left"**
- Select **Install from File**
- Choose the **iso** file
- Choose `BIOS` (Somehow `UEFI` isnt working)
- Set a Name of the VM
- Set Memory (min 4-8 GiB)
- Set Storage (min 30-50 GiB)
- Click on the `Create` Button

> Note: it will start the VM and show Arch Grub menu kinda thing. Just Go to the Bottom and select `Power Off` and Enter. You will be on the Main Menu of **Gnome Boxes**

- Click on the 3 Dot Button of the `Arch VM` > Preferences > Change Name (Optional)
- Set `CPUs` from `16` to `4`
- Turn on `3D acceleration`
- Close Modal
- Click on the VM to `Launch`
- On Arch Install Menu select the First One Labeled as: `Arch Linux install medium (x86_64, BIOS)`
- just type `archinstall` on the `cli` and wait until a TUI like thing starts

> Note: if the `archinstall` script has a new version available then you can upgrade to that by `pacman -Sy archinstall` and it will be updated to the latest one and then start the `archinstall` script after updating 

- Select `Mirrors and repositories` > `Select Region [Enter]`
- filter out your region and select your region (i.e. `Bangladesh`)
- after selection, go back to the main menu of **Arch Install Script**
- Select `Disk Configuration` > `Partitioning` > `[Enter]`
- select `Use a best-effort default partition layout`
- select the Virtual Storage (80 GiB)
- select `btrfs` > select `Yes` for `BTRFS submodules with a default structure`

> Note: in the tutorial, he selected `btrfs` over `ext4`. 

- select `Use Compression`

> Note: for now, no disk encryption needed

- Select `Hostname` to change it whatever you like (i.e. `Arch` or whatever you want)

> Note: this is the name of the Machine and not the users name

- Select  `Authentication` > `Root Password` > set the admin password (`super secret password`)

> Note: Hostname ≠ Username

- go back
- select `User Account` > `Add a user`
- enter `username` (i.e. `sakif`)
- enter `password` and `confirm password`
- select `yes` so that the `User can be a superuser`
- select `Confirm and exit`
- go back to `Main menu of Arch Install`
- Select `Applications` > `Audio` > `Pipewire`
- go to `Main menu of Arch Install`
- Select `Kernels` > `linux` (there's another options)
- Select `Network configuration` > `Copy ISO network configuration to installation`
- Select `Timezone` to `UTC`
- Finally, Select `Install` and `[Enter]`

> Note: it will show a json like summary of the options.

- Select `Yes`

> Note: it will start the installation

![Phew](https://i.giphy.com/EDt1m8p5hqXG8.webp)

> Note: after some time, Installation will complete and you will have 3 options

- Select `Reboot System`

> Note: after Reboot, you can log into the system with your Username && Password. If by any chance you are on the same live arch menu, you can Chosse the `Boot Existing OS` option and you will be logged into your Freshly installed system.
> 
> Or you can click on the `3 Dot` > `Devices & Shares`. Remove the `arch iso` from the `CDROM/DVD Drive` area and then run the VM.
>
> surely you will be able to log into the installed OS instead of the Live Arch Environment.

*Now you have a Fresh install of Arch Linux*
