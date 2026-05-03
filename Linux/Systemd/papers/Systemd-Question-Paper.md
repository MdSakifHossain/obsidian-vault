# Systemd Question Paper

---

# 1) Foundations — what is really going on 🧠

- What is an **init system**, and why does Linux need one?
- What problem does systemd solve compared to older init systems?
- What is a **daemon** in Linux?
- What is a **systemd unit**?
- What are the different types of units? (`service`, `timer`, `target`, etc.)
- What is the difference between:
  - system-level units
  - user-level units

---

# 2) Boot & lifecycle 🔄

- What happens during boot in a system using systemd?
- What is a **target** (e.g., `multi-user.target`, `graphical.target`)?
- How does systemd decide which services to start?
- What is the difference between:
  - `WantedBy=`
  - `RequiredBy=`

---

# 3) Service files (core skill) 📄

- What is the structure of a `.service` file?
- What do these sections mean:
  - `[Unit]`
  - `[Service]`
  - `[Install]`
- What does each of these directives do:
  - `ExecStart=`
  - `ExecStop=`
  - `Restart=`
  - `User=`
  - `WorkingDirectory=`
- What is the difference between:
  - `Type=simple`
  - `Type=oneshot`
  - `Type=forking`

---

# 4) Your use-case (very important) 🎯

- How do I create a service that:
  - runs **after login**
  - waits a few seconds
  - then locks the session
- Should this be:
  - a **system service**
  - or a **user service**?
- What is the difference between:
  - `/etc/systemd/system/`
  - `~/.config/systemd/user/`
- How do I make a service run:
  - only for my user
  - not for the whole system

---

# 5) Execution context ⚙️

- Under which user does a service run?
- How do I run a service as:
  - root
  - my user (`sakif`)
- What environment variables are missing in systemd services?
- Why do GUI-related commands (DBus, GNOME) often fail in services?
- What are:
  - `XDG_RUNTIME_DIR`
  - `DBUS_SESSION_BUS_ADDRESS`
- How do I pass environment variables into a systemd service?

---

# 6) Dependencies & ordering 🔗

- How do I ensure my service runs:
  - after GNOME session starts
  - after network is available
- What do these mean:
  - `After=`
  - `Requires=`
  - `Wants=`
- What is the difference between:
  - ordering vs dependency

---

# 7) Managing services 🛠️

- How do I:
  - start a service
  - stop a service
  - restart a service
- What does:
  - `enable`
  - `disable`
  - `daemon-reload`
    mean?
- What happens when I run:

```bash
systemctl enable my-service
```

---

# 8) Debugging (critical skill) 🧯

- How do I check logs for a service?
- What is:
  - `journalctl`
- How do I view logs:
  - for a specific service
  - in real time
- Why does a service fail silently sometimes?

---

# 9) Timers (better than sleep) ⏱️

- What is a **systemd timer**?
- How is it different from:
  - cron
  - `sleep`
- Can I replace “wait 5 seconds then lock” with a timer?
- What are:
  - `OnBootSec=`
  - `OnUnitActiveSec=`

---

# 10) Security & control 🔐

- What permissions should my service have?
- What happens if I run everything as root?
- How can I restrict a service’s capabilities?
- What is:
  - `ProtectSystem=`
  - `PrivateTmp=`

---

# 11) Advanced (optional but powerful) ⚡

- What is a **target** and can I create my own?
- What is `graphical-session.target`?
- How do I hook into:
  - user login events
  - session start events
- What is **linger** (`loginctl enable-linger`)?

---

# 12) Practical design questions (for your project) 🧩

- Should my lock script be:
  - a one-time service
  - or a persistent daemon
- What is better:
  - systemd service
  - or a loop script
- What happens if:
  - the service crashes
  - GNOME isn’t ready yet
- How do I make it:
  - reliable
  - not race-condition dependent

---

# Final instruction

Don’t just answer these—**experiment while answering**:

- create a test service
- break it
- fix it
- check logs

That loop is where the real learning happens.

---

If you complete this properly, you’ll move from:

> “I run scripts”

to:

> “I control system behavior”

which is a significant jump.
