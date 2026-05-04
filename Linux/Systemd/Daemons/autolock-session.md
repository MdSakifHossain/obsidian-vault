# Autolock Session

⬅️ [Systemd](../Systemd.md)

You can automate what would normally require human interaction.

---

## How It Works

**Event:** System Automatically Logs In

**Action:** Wait 3 seconds

**Then:** Run `loginctl lock-session`

system boots
→ login succeeds
→ user session starts
→ systemd (user) activates default target
→ your rule is triggered
→ wait 20 seconds
→ openrgb --mode off
→ LEDs turn off
→ rule exits