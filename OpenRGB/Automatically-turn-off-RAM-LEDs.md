# Automatically Turn Off RAM LEDs

⬅️ [OpenRGB](./OpenRGB.md)

You can automate what would normally require human interaction.

---

## How It Works

<img src="https://i.giphy.com/3V33ssIjg0BUGafaU0.webp" alt="useless-image" width="50%"/>

**Event:** User logs in

**Action:** Wait 20 seconds

**Then:** Run `openrgb --mode off`

```
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

---

## Before You Automate: Test It Manually

<img src="https://i.giphy.com/3o6Ei2yv8fqpR3nJG8.webp" alt="useless-image" width="50%"/>

The manual flow:

```
system boots → login → terminal → command → RGB off
```

I'm using **OpenRGB** for this.

### Check Your OpenRGB Version

```shell
openrgb --version
```

```
OpenRGB 0.9+ (1.0rc2), for controlling RGB lighting.
  Version:		 0.9+ (1.0rc2)
  Build Date		 Mon, 13 Apr 2020 03:57:34 +0000
  Git Commit ID		 0fca93e4544f943d4d7ec8073dba4e47c18ef54b
  Git Commit Date	 2025-09-14 14:31:57 -0500
  Git Branch		 2039027121 2039027252 master
```

### Test the Command

```shell
$ sudo openrgb --mode off
```

```
Connection attempt failed
[i2c_smbus_linux] Failed to read i2c device PCI device ID
[i2c_smbus_linux] Failed to read i2c device PCI device ID
[i2c_smbus_linux] Failed to read i2c device PCI device ID
Error: Mode 'off' not available for device 'MSI PRO B650M-B (MS-7E28)'
Error: Mode 'off' not available for device 'MSI PRO B650M-B (MS-7E28)'
```

**Chill.** This is not an error. The motherboard is a ghost device. But the **RAM LEDs** got shut down.

```shell
openrgb --mode off
```

This also works **without** `sudo`. So, we are **golden**.

---

## The Automation

<img src="https://i.giphy.com/3oz8xtBx06mcZWoNJm.webp" alt="useless-image" width="50%"/>

This step is mechanical, not conceptual:

- Create a user-level systemd service
- Tell it to start on login
- Add the 20-second delay
- Put your already-working command inside

No new ideas. No new behavior.

---

## Where Systemd Units Live

There are **two worlds**:

| Level | Path | Who Owns It | When It Runs |
|---|---|---|---|
| System (root) | `/etc/systemd/system/` | Root | At boot |
| User (you) | `~/.config/systemd/user/` | You | On login |

If you put a file in the user path:

- It belongs only to you
- It runs only when you log in
- It needs no `sudo`

That's **exactly what I want**.

---

## Step-by-Step Setup

### Step 1: Create the Directory

```shell
mkdir -p ~/.config/systemd/user
```

### Step 2: Create the Unit File

```shell
nano ~/.config/systemd/user/openrgb-off.service
```

Paste this inside:

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

#### What's What

| Section | What It Does |
|---|---|
| `[Unit]` | Metadata. For humans. systemd doesn't give a fuck. Purely informational. |
| `[Service]` | The actual behavior. |
| `Type=oneshot` | Run once and exit. Don't stay alive and don't loop. Perfect for this. |
| `ExecStart=...` | The command. Sleeps 20 seconds, then kills the lights. |
| `[Install]` | Tells systemd when to trigger this. |
| `WantedBy=default.target` | Translation: "This is the **login event**." |

### Step 3: Register the Service (One-Time)

```shell
systemctl --user daemon-reload
systemctl --user enable openrgb-off.service
```

**What just happened:**

- systemd reread unit files
- Created a symlink
- Attached your service to the login event

**Nothing will run yet.**

> Because apparently, systemd is like a stupid guy. He doesn't automatically know if anything has changed. We have to tell him to reload (check if there's anything new in his directory).
>
> After reloading, he'll see it and say, "Ah, there's a new file." But he's so fucking dumb that he won't just start the thing automatically.
>
> And then, we have to `enable` that new service file.
>
> But that thing won't run right away. He'll be like, "I'm not gonna run until I reboot or get freshly powered on again."

### Step 4: Test It Now (Optional)

```shell
systemctl --user start openrgb-off.service
```

Wait 20 seconds. RAM goes dark. Life continues.

### Step 5: Reboot Once. Then Forget This Exists.

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

---

## How to Remove It

God forbid you do:

```shell
systemctl --user disable openrgb-off.service
rm ~/.config/systemd/user/openrgb-off.service
```

<img src="https://i.giphy.com/1dMNqVx9Kb12EBjFrc.webp" alt="useless-image" width="50%"/>
