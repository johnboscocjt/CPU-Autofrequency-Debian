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

In your case, it successfully reduced total CPU usage to ~18.6% and turned turbo boost off when not needed.

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

If you see the message about GNOME Power Profiles:

```bash
sudo python3 -m auto_cpufreq.power_helper --gnome_power_enable
```

---

## How to Check Status (Very Important)

After installation, always check if auto-cpufreq is working:

```bash
auto-cpufreq --stats
```

This command shows:
- Current governor (powersave / performance)
- CPU frequencies
- Temperatures
- Whether turbo boost is on/off
- Total CPU usage, etc.

Run this command regularly to monitor how well it's working.

---

## Auto Start on Boot (Already Enabled)

When you run `sudo auto-cpufreq --install`, it **automatically enables** the service to start every time your computer boots.

To verify it is enabled on startup:

```bash
systemctl status auto-cpufreq.service
```

You should see `Loaded: loaded` and `Active: active (running)`.

---

## Useful Commands

| Command                                      | Purpose                                      |
|---------------------------------------------|----------------------------------------------|
| `auto-cpufreq --stats`                      | View live statistics (most important)        |
| `sudo auto-cpufreq --force=performance`     | Force maximum performance                    |
| `sudo auto-cpufreq --force=powersave`       | Force maximum power saving                   |
| `sudo auto-cpufreq --remove`                | Completely uninstall                         |
| `systemctl status auto-cpufreq.service`     | Check if service is running on boot          |
| `auto-cpufreq --help`                       | Show all options                             |

---

## Complete Uninstall Guide

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
- Use `--force=performance` when doing heavy tasks.
- Let it run in **auto** mode for daily use (best balance).
- Check status regularly with `auto-cpufreq --stats`.

---

