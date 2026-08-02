# Troubleshooting

This guide documents common issues encountered when installing and operating Masjid Display, together with recommended diagnostic steps.

Always start with the simplest checks before making configuration changes.

---

# General Health Check

Before investigating a specific issue, check the overall system status.

```bash
taqwa-status
```

Verify Chromium is running:

```bash
pgrep -a chromium
```

Check the health-check timer:

```bash
systemctl --user status taqwa-healthcheck.timer
```

View recent launcher activity:

```bash
tail -n 50 ~/.config/taqwa-display/logs/launcher.log
```

---

# Chromium Does Not Start

## Symptoms

- Black screen
- Desktop visible instead of kiosk mode
- Browser never appears

## Checks

Confirm Chromium is installed:

```bash
chromium --version
```

Check if Chromium is already running:

```bash
pgrep -a chromium
```

Attempt to start Chromium manually:

```bash
chromium \
    --ozone-platform=wayland \
    --kiosk \
    https://example.org/display
```

If Chromium starts manually but not automatically, review the launcher script and Labwc autostart configuration.

---

# Wrong Screen Rotation

## Symptoms

- Display sideways
- Upside down
- Incorrect portrait orientation

Check available outputs:

```bash
wlr-randr
```

Test rotation manually:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 90
```

Other valid values:

```text
normal
90
180
270
```

Once the correct orientation is identified, update:

```text
DISPLAY_TRANSFORM
```

in:

```text
~/.config/taqwa-display/config.env
```

---

# Incorrect Screen Size

## Symptoms

- Black border around the display
- Browser does not fill the screen
- Content appears too small or too large

List available display modes:

```bash
wlr-randr
```

If required, test a specific mode:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --mode 2560x1440@59.951Hz \
    --transform 90
```

Only use modes reported by the connected display.

Different televisions may require different resolutions and refresh rates.

---

# Website Does Not Load

Check the configured URL:

```bash
cat ~/.config/taqwa-display/config.env
```

Verify network connectivity:

```bash
ping google.com
```

If the URL is incorrect, update it:

```bash
taqwa-update-url
```

---

# Browser Closes Unexpectedly

The launcher should restart Chromium automatically.

Verify that the launcher is running:

```bash
pgrep -af taqwa-launcher
```

Review recent launcher activity:

```bash
tail -n 50 ~/.config/taqwa-display/logs/launcher.log
```

---

# Health Check Not Running

Check the timer:

```bash
systemctl --user status taqwa-healthcheck.timer
```

List timers:

```bash
systemctl --user list-timers
```

Start a health check manually:

```bash
systemctl --user start taqwa-healthcheck.service
```

Review the service log:

```bash
journalctl --user -u taqwa-healthcheck.service
```

---

# Display Sleeps

Wake the display:

```bash
wlopm --on '*'
```

Ensure power management has not been re-enabled.

---

# Remote SSH Access Fails

Confirm SSH is running:

```bash
sudo systemctl status ssh
```

Check the Raspberry Pi IP address:

```bash
hostname -I
```

If using Tailscale:

```bash
tailscale status
```

---

# Configuration Changes Have No Effect

Display the current configuration:

```bash
cat ~/.config/taqwa-display/config.env
```

Restart Chromium:

```bash
pkill -x chromium
```

The launcher should reload the configuration and start Chromium again.

---

# Launcher Does Not Start Automatically

Verify the Labwc autostart file:

```text
~/.config/labwc/autostart
```

Ensure it launches:

```text
~/.local/share/taqwa-display/taqwa-launcher
```

---

# Display Looks Different on Another TV

Different televisions may:

- expose different HDMI modes;
- apply overscan;
- support different refresh rates;
- scale content differently.

Always verify:

```bash
wlr-randr
```

on the target television.

Do not assume settings from one TV will work correctly on another.

---

# Creating a Diagnostic Snapshot

When requesting support, collect:

Operating system:

```bash
cat /etc/os-release
```

Display information:

```bash
wlr-randr
```

Configuration:

```bash
cat ~/.config/taqwa-display/config.env
```

Processes:

```bash
pgrep -a chromium
```

Status:

```bash
taqwa-status
```

These details usually provide enough information to diagnose most issues.

---

# Before Requesting Help

Check:

- Raspberry Pi has power.
- HDMI cable is connected securely.
- Network connection is working.
- Chromium launches manually.
- Configuration file is correct.
- Health-check timer is active.
- Display rotation and resolution are correct.

Most issues can be identified by following the steps in this document.

---

# Related Documentation

- Installation
- Configuration
- Commands
- Services
- Deployment
- TV Compatibility