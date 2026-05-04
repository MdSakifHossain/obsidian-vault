# Autolock Session

⬅️ [Systemd](../Systemd.md)

You can automate what would normally require human interaction.

---

## How It Works

**Event:** System Automatically Logs In

**Action:** Wait 3 seconds

**Then:** Run `loginctl lock-session`

```
system boots
→ automatic login succeeds
→ user session starts
→ systemd (user) activates default target
→ your rule is triggered
→ wait 3 seconds
→ loginctl lock-session
→ Locks user session
→ rule exits
```

---

## The Automation

- Create a user-level systemd service
- Tell it to start on login
- Add the 3-second delay
- Put your already-working command inside

## Step-by-Step Setup

### Step 1: Create the Directory

```shell
mkdir -p ~/.config/systemd/user
```

### Step 2: Create the Unit File

```shell
nano ~/.config/systemd/user/autolock-session.service
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

| Section                   | What It Does                                                             |
| ------------------------- | ------------------------------------------------------------------------ |
| `[Unit]`                  | Metadata. For humans. systemd doesn't give a fuck. Purely informational. |
| `[Service]`               | The actual behavior.                                                     |
| `Type=oneshot`            | Run once and exit. Don't stay alive and don't loop. Perfect for this.    |
| `ExecStart=...`           | The command. Sleeps 20 seconds, then kills the lights.                   |
| `[Install]`               | Tells systemd when to trigger this.                                      |
| `WantedBy=default.target` | Translation: "This is the **login event**."                              |

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

