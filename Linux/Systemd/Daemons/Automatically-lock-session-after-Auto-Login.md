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
Description=Auto-lock session after login delay
After=graphical-session.target
PartOf=graphical-session.target

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'sleep 3 && loginctl lock-session'

[Install]
WantedBy=default.target

```

Save. Exit.
### Step 3: Register the Service (One-Time)

```shell
systemctl --user daemon-reload
systemctl --user enable autolock-session.service
```

**Nothing will run yet.**

> `Systemctl` is a fucking a$#hole. it is like an old monk. He will not even look at the new service right away. 
> 
> So, when do the `daemon-reload`, then the monk Opens up his eyes. he then tries to look at its list and then he finds out that `there's a new file`. (He wont do anything until the user actually tells it to do something with it.)
> 
> Then the user have to explicitly tell the monk to `enable` that new service file by `explicitly typing out the new files full name`.
> 
> Then he be like: 
> 	I will not run this until the whole system `boots up again` OR `reboot`.
> 
> If you need that service to `run without new boot or reboot` then you have to tell the monk:
> 	I want this to run now by saying, `start <service-file-full-name>`
> 
> Then it will run.

### Step 4: Test It Now (Optional)

```shell
systemctl --user start openrgb-off.service
```

Wait 3 seconds. Screen/Session Locks. Life continues.

