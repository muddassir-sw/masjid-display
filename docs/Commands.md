# Commands

This document describes the commands used to install, configure, monitor and troubleshoot Masjid Display.

---

# Display Commands

## List Connected Displays

Displays all detected outputs, supported resolutions and current settings.

```bash
wlr-randr
```

---

## Rotate the Display

Landscape:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform normal
```

Portrait:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 90
```

Upside Down:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 180
```

Portrait (Reverse):

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 270
```

---

## Apply a Specific Display Mode

Example:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --mode 2560x1440@59.951Hz \
    --transform 90
```

Only use display modes supported by your television.

---

## Turn the Display On

```bash
wlopm --on '*'
```

---

# Chromium

## Start Chromium

```bash
chromium \
    --ozone-platform=wayland \
    --kiosk \
    https://example.org/display
```

---

## Close Chromium

```bash
pkill -x chromium
```

The launcher automatically starts Chromium again.

---

## Check Chromium

```bash
pgrep -a chromium
```

---

# Configuration

## View Configuration

```bash
cat ~/.config/taqwa-display/config.env
```

---

## Edit Configuration

```bash
nano ~/.config/taqwa-display/config.env
```

---

## Update Display URL

Prompt for a new URL:

```bash
taqwa-update-url
```

Specify the URL directly:

```bash
taqwa-update-url "https://example.org/display"
```

---

# Status

Display current system status:

```bash
taqwa-status
```

Displays:

- Chromium status
- Health check status
- Recent launcher activity

---

# Backup

Create a backup:

```bash
taqwa-backup
```

Specify the output file:

```bash
taqwa-backup ~/display-backup.tar.gz
```

---

# Health Check

Run manually:

```bash
systemctl --user start taqwa-healthcheck.service
```

Check status:

```bash
systemctl --user status taqwa-healthcheck.service
```

---

# Timer

View the timer:

```bash
systemctl --user status taqwa-healthcheck.timer
```

List all timers:

```bash
systemctl --user list-timers
```

Reload systemd:

```bash
systemctl --user daemon-reload
```

Restart the timer:

```bash
systemctl --user restart taqwa-healthcheck.timer
```

---

# Logs

View launcher log:

```bash
tail -n 50 ~/.config/taqwa-display/logs/launcher.log
```

Follow launcher log:

```bash
tail -f ~/.config/taqwa-display/logs/launcher.log
```

View health-check logs:

```bash
journalctl --user -u taqwa-healthcheck.service
```

View the latest entries:

```bash
journalctl --user -u taqwa-healthcheck.service -n 50 --no-pager
```

---

# Network

Show IP addresses:

```bash
hostname -I
```

Show network connections:

```bash
nmcli connection show --active
```

---

# SSH

Connect over the local network:

```bash
ssh piuser@raspberrypi.local
```

Connect using Tailscale:

```bash
ssh piuser@<tailscale-hostname>
```

---

# Tailscale

View connection status:

```bash
tailscale status
```

Show the assigned IP:

```bash
tailscale ip -4
```

---

# Raspberry Pi

Reboot:

```bash
sudo reboot
```

Shutdown:

```bash
sudo shutdown -h now
```

Update the operating system:

```bash
sudo apt update
sudo apt full-upgrade -y
```

---

# Troubleshooting Commands

Display information:

```bash
wlr-randr
```

Chromium:

```bash
pgrep -a chromium
```

Configuration:

```bash
cat ~/.config/taqwa-display/config.env
```

Health Check:

```bash
systemctl --user status taqwa-healthcheck.service
```

Timer:

```bash
systemctl --user status taqwa-healthcheck.timer
```

Status Utility:

```bash
taqwa-status
```

---

# Related Documentation

- Installation
- Configuration
- Services
- Troubleshooting
- TV Compatibility