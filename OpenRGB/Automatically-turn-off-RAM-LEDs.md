# Automatically Turn Off RAM LEDs

⬅️ [OpenRGB](./OpenRGB.md)

You can automate which can be done by Human interaction.

## Design System

<img
  src="https://i.giphy.com/3V33ssIjg0BUGafaU0.webp"
  alt="useless-image"
  width="50%"
/>

> **Event**: user logs in
>
> **Action**: wait 20 seconds
>
> **Then**: run `openrgb --mode off`

```txt
system boots
→ login succeeds
→ user session starts
→ systemd (user) activates default target
→ your rule is triggered
→ wait 20 seconds
→ openrgb --mode off
→ LEDs turn off
→ rule exits
```

## Human Interaction

<img
  src="https://i.giphy.com/3o6Ei2yv8fqpR3nJG8.webp"
  alt="useless-image"
  width="50%"
/>

`system boots ==> login ==> terminal ==> command ==> RGB off`

Im using `openRGB` for this case.

```shell
openrgb --version
OpenRGB 0.9+ (1.0rc2), for controlling RGB lighting.
  Version:		 0.9+ (1.0rc2)
  Build Date		 Mon, 13 Apr 2020 03:57:34 +0000
  Git Commit ID		 0fca93e4544f943d4d7ec8073dba4e47c18ef54b
  Git Commit Date	 2025-09-14 14:31:57 -0500
  Git Branch		 2039027121 2039027252 master
```

Now Lets See if it can shut the LED's off or not.

```shell
$ sudo openrgb --mode off

Connection attempt failed
[i2c_smbus_linux] Failed to read i2c device PCI device ID
[i2c_smbus_linux] Failed to read i2c device PCI device ID
[i2c_smbus_linux] Failed to read i2c device PCI device ID
Error: Mode 'off' not available for device 'MSI PRO B650M-B (MS-7E28)'
Error: Mode 'off' not available for device 'MSI PRO B650M-B (MS-7E28)'
```

This is not an error. Motherboard is a ghost device. but `RAM LED's` got shut down.

```shell
openrgb --mode off
```

This also works without `sudo`. So, we are `Golden`.

## Automation Implementation

<img
  src="https://i.giphy.com/3oz8xtBx06mcZWoNJm.webp"
  alt="useless-image"
  width="50%"
/>

This step is mechanical, not conceptual;

- create a user-level systemd service
- tell it to start on login
- add the 20 second delay
- put your already-working command inside
- No new ideas. No new behavior.

systemd only reacts to one thing: `Unit files`

A `unit file` is just:

- a text file
- in a specific directory
- with a specific name
- following a known format

> If the file exists, systemd can read it.
>
> If it’s enabled, systemd will act on it

## Where Systemd units live (this matters)

There are **two worlds**:

#### System-level (root)

```shell
/etc/systemd/system/
```

#### User-level (user)

```shell
~/.config/systemd/user/
```

If you put a file in the second path:

- it belongs only to you
- it runs only when you log in
- it needs no sudo

That’s `exactly what I want`.

## Implementation Part

We create a `unit file` that `systemd --user` will execute `when the user session starts`.

###### Step 1: Create the place `systemd --user` actually reads

```shell
mkdir -p ~/.config/systemd/user
```

Logical meaning:

- "These are rules for `my user session`, not the whole system."

###### Step 2: Create the unit file (this is the rule)

Name it something boring and honest:

```shell
nano ~/.config/systemd/user/openrgb-off.service
```

Put `exactly this` inside:

```service
[Unit]
Description=Turn off RAM RGB after login

[Service]
Type=oneshot
ExecStart=/bin/bash -c 'sleep 20 && openrgb --mode off'

[Install]
WantedBy=default.target
```

Save. Exit.

###### Explanation

```service
`[Unit]`

Metadata. For Humans. systemd doesnt give a fuck. Purely informational.

`[Service]`

This is the actual behavior.

`Type=oneshot`

Meaning: run once && exit. Dont stay alive and dont fuck in a loop

> Perfect for my case.

`ExecStart=/bin/bash -c 'sleep 20 && openrgb --mode off'`

`[Install]`

`WantedBy=default.target`

Translation: "This is the **login event**"
```

###### Step 3: Register the service (one-time)

Tell systemd --user that this rule exists.

```shell
systemctl --user daemon-reload
systemctl --user enable openrgb-off.service
```

What just happened:

- systemd reread unit files
- created a symlink
- attached your service to the login event

Nothing will ran `yet`

###### Rant && Explanation

> Because appearantly, systemd is like stupid guy. He doenst automatically know if anything has changed or not. we have to tell him to reload (Check if theres any changes in his directory)
>
> After reloading he will see and say, 'ah, theres a new file` and he is so fucking dumb that he wont just start the thing automatically.
>
> And then, We have to `enable` that new service file.
>
> But, that thing wont run `right away`. He be like, Im not gonna run until I reboot or not Freshly Powered on Again.

###### Step 4: (Optional) Test it without rebooting

`If you want to see it fire right now:`

```shell
systemctl --user start openrgb-off.service
```

Wait 20 seconds. RAM goes dark. And, Life continues.

###### Step 5: Reboot once. Then forget this exists.

On next boot:

```
boot
→ login
→ user session starts
→ systemd --user runs your service
→ waits 20 seconds
→ kills RAM RGB
→ exits quietly
```

## Last but Not Least

To remove it (God forbid you do):

```shell
systemctl --user disable openrgb-off.service
rm ~/.config/systemd/user/openrgb-off.service
```

<img
  src="https://i.giphy.com/1dMNqVx9Kb12EBjFrc.webp"
  alt="useless-image"
  width="50%"
/>
