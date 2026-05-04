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
