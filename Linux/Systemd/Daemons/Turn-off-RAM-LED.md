# Automatically Turn Off RAM LED

## Commands: Just Paste These

### Test it manually

```sh
openrgb -m off
```

If that turns the RAM LEDs off, continue.

### Create the systemd directory

```sh
mkdir -p ~/.config/systemd/user
```

### Create the service

```sh
nano ~/.config/systemd/user/openrgb-off.service
```

Paste this inside:

```service
[Unit]
Description=Turn off RAM RGB after login

[Service]
Type=oneshot
ExecStart=/bin/bash -c 'sleep 5 && openrgb -m off > /dev/null'

[Install]
WantedBy=default.target
```

Save. Exit.

### Register the service

```sh
systemctl --user daemon-reload
systemctl --user enable openrgb-off.service
```

### Test it now

```sh
systemctl --user start openrgb-off.service
```

Wait 5 seconds. RAM goes dark.

### Remove it later, if needed

```sh
systemctl --user disable openrgb-off.service
rm ~/.config/systemd/user/openrgb-off.service
```

---

# How It Works

You can automate what would normally require human interaction.

The goal is simple:

```text
system boots
→ login succeeds
→ user session starts
→ systemd starts the service
→ wait 5 seconds
→ openrgb -m off
→ LEDs turn off
```

I'm using **OpenRGB** for this.

---

## Before You Automate: Test It Manually

The manual flow:

```text
system boots → login → terminal → command → RGB off
```

First, run:

```sh
openrgb -m off
```

If the RAM LEDs turn off, the command works.

No `sudo` needed. We're golden.

---

# The Automation

This step is mechanical, not conceptual:

- Create a user-level systemd service
- Tell it to start on login
- Add the 5-second delay
- Put your already-working command inside

No new ideas. No new behavior.

---

## Where Systemd Units Live

There are **two worlds**:

|Level|Path|Who Owns It|When It Runs|
|---|---|---|---|
|System (root)|`/etc/systemd/system/`|Root|At boot|
|User (you)|`~/.config/systemd/user/`|You|On login|

If you put a file in the user path:

- It belongs only to you
- It runs only when you log in
- It needs no `sudo`

That's **exactly what I want**.

---

# What's Inside the Service?

```service
[Unit]
Description=Turn off RAM RGB after login

[Service]
Type=oneshot
ExecStart=/bin/bash -c 'sleep 5 && openrgb -m off > /dev/null'

[Install]
WantedBy=default.target
```

### What's What

| Section                   | What It Does                                                             |
| ------------------------- | ------------------------------------------------------------------------ |
| `[Unit]`                  | Metadata. For humans. systemd doesn't give a fuck. Purely informational. |
| `[Service]`               | The actual behavior.                                                     |
| `Type=oneshot`            | Run once and exit. Don't stay alive and don't loop. Perfect for this.    |
| `ExecStart=...`           | Wait 5 seconds, then turn the RAM LEDs off.                              |
| `[Install]`               | Tells systemd when to trigger this.                                      |
| `WantedBy=default.target` | Translation: "Start this when my user session starts."                   |

---

## Why `daemon-reload` and `enable`?

After creating the file:

```sh
systemctl --user daemon-reload
systemctl --user enable openrgb-off.service
```

**Nothing runs yet.**

Because apparently, systemd is like a stupid guy. He doesn't automatically know if anything has changed. We have to tell him to reload and check if there's anything new.

After reloading, he'll see it and say:

> "Ah, there's a new file."

But he's so fucking dumb that he won't just start the thing automatically.

Then we have to `enable` that new service file.

And that thing won't run right away. He'll be like:

> "I'm not gonna run until you log in again."

Fair enough.

---

# Reboot Once. Then Forget This Exists.

On the next boot:

```text
boot
→ login
→ user session starts
→ systemd --user runs your service
→ waits 5 seconds
→ kills RAM RGB
→ exits quietly
```

That's it.

---

# How to Remove It

God forbid you do:

```sh
systemctl --user disable openrgb-off.service
rm ~/.config/systemd/user/openrgb-off.service
```

<img src="https://i.giphy.com/1dMNqVx9Kb12EBjFrc.webp" alt="useless-image" width="50%"/>
