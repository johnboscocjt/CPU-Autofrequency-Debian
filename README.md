# Auto-cpufreq Installation & Management Guide

**Author:** John Bosco (johnboscocjt)  
**Last Updated:** May 2026  
**Ubuntu Version:** 25.10

---

## Why Auto-cpufreq is Important

**auto-cpufreq** is a powerful tool that **automatically optimizes your CPU frequency scaling** in real-time.

### Key Benefits:
- Reduces high CPU usage and overheating when idle
- Improves battery life (very useful on laptops)
- Automatically switches between **powersave**, **balanced**, and **performance** modes
- Lowers temperatures and fan noise
- Prevents CPU from staying at maximum frequency unnecessarily
- Works great with Intel CPUs (like your i5-6300U)

In your case, it successfully set the governor to **powersave** and turned **turbo boost OFF** when not needed, bringing down total CPU usage to ~18.6% even though individual cores were active.

---

## Complete Installation (Latest Method)

```bash
cd ~/installationfolder
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq
sudo ./auto-cpufreq-installer
```

After installer finishes:
```bash
sudo auto-cpufreq --install
```

---

## Important Post-Installation Step (GNOME)

If you see this message:
> **GNOME Power Profiles Daemon should be enabled**

Run this command:

```bash
sudo python3 -m auto_cpufreq.power_helper --gnome_power_enable
```

---

## Useful Commands

| Command                                      | Purpose                                      |
|---------------------------------------------|----------------------------------------------|
| `auto-cpufreq --stats`                      | View live statistics (recommended)           |
| `sudo auto-cpufreq --force=performance`     | Force maximum performance                    |
| `sudo auto-cpufreq --force=powersave`       | Force maximum power saving                   |
| `sudo auto-cpufreq --remove`                | Completely uninstall                         |
| `auto-cpufreq --help`                       | Show all options                             |

---

## Complete Uninstall Guide (Very Important)

Run these commands in order if you ever want to remove it:

```bash
# 1. Remove daemon
sudo auto-cpufreq --remove

# 2. Remove Snap version (if installed)
sudo snap remove --purge auto-cpufreq 2>/dev/null

# 3. Clean folders and files
sudo rm -rf /opt/auto-cpufreq
sudo rm -rf ~/installationfolder/auto-cpufreq
sudo rm -rf ~/auto-cpufreq

# 4. Remove desktop icons
rm -f ~/Desktop/*auto-cpufreq*.desktop
rm -f ~/.local/share/applications/*auto-cpufreq*
```

Then press **Alt + F2**, type `r` and press Enter to refresh desktop.

---

## Quick Tips

- Use `--force=performance` when doing heavy tasks (video editing, compiling, gaming).
- Let it run in **auto** mode for daily use (best balance).
- Always check `auto-cpufreq --stats` to see what it's doing.

---

