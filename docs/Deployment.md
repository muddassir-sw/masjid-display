# Deployment Guide

This document provides recommended practices for deploying Masjid Display in a production environment.

Unlike the Installation Guide, which explains how to install the software, this guide focuses on planning, testing and maintaining a reliable deployment.

---

# Deployment Workflow

A typical deployment should follow these stages:

```
Prepare Raspberry Pi
        │
        ▼
Install Raspberry Pi OS
        │
        ▼
Install Masjid Display
        │
        ▼
Configure Display
        │
        ▼
Test Everything
        │
        ▼
Install at Mosque
        │
        ▼
Remote Monitoring
        │
        ▼
Maintenance
```

---

# Before You Begin

Before deploying to a production environment, ensure you have:

- Raspberry Pi
- Official power supply
- MicroSD card
- HDMI cable
- Television or monitor
- Stable network connection
- Keyboard and mouse (recommended for initial setup)

---

# Prepare the Raspberry Pi

Install the latest Raspberry Pi OS.

Update the operating system:

```bash
sudo apt update
sudo apt full-upgrade -y
sudo reboot
```

Enable SSH if remote administration is required.

---

# Install Masjid Display

Follow the installation guide:

- Installation.md
- Configuration.md

Do not deploy to production until the installation has been tested locally.

---

# Configure the Display

Configure:

- Display URL
- Screen rotation
- Display mode
- Browser startup

Verify that Chromium starts correctly.

---

# Test Before Deployment

Perform a complete functional test.

Verify:

- Chromium launches automatically
- Correct webpage loads
- Portrait or landscape orientation is correct
- Screen fills the display correctly
- Browser restarts after being closed
- Health check is running
- Timer is active

---

# Test Display Resolution

Different televisions support different display modes.

Check available modes:

```bash
wlr-randr
```

Only configure resolutions reported by the connected television.

Avoid copying display modes from another deployment without testing.

---

# Test Portrait Mode

If using a portrait display, verify:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 90
```

Ensure:

- text is readable;
- content fills the screen;
- touch controls (if applicable) remain usable.

---

# Verify Automatic Startup

Reboot the Raspberry Pi:

```bash
sudo reboot
```

Confirm:

- Labwc starts correctly
- Launcher starts automatically
- Chromium opens
- Display loads without user interaction

---

# Verify Health Monitoring

Confirm the timer is running:

```bash
systemctl --user status taqwa-healthcheck.timer
```

Run a manual health check:

```bash
systemctl --user start taqwa-healthcheck.service
```

Review status:

```bash
taqwa-status
```

---

# Remote Administration

SSH is strongly recommended.

Example:

```bash
ssh piuser@raspberrypi.local
```

If using Tailscale:

```bash
tailscale status
```

Remote access allows software updates and troubleshooting without physical access to the display.

---

# Backup Strategy

Before making major changes:

```bash
taqwa-backup
```

Also consider creating a complete SD card image after a successful deployment.

This provides the fastest recovery option if the SD card fails.

---

# Updating the Display URL

The display URL can be updated without reinstalling the software:

```bash
taqwa-update-url
```

or

```bash
taqwa-update-url "https://example.org/display"
```

---

# Production Checklist

Before leaving the installation site, confirm:

- Raspberry Pi boots successfully
- Display powers on correctly
- Chromium launches automatically
- Correct webpage loads
- Screen orientation is correct
- Display fills the screen
- Health-check timer is active
- SSH access works
- Backup has been created

---

# Maintenance

Recommended routine maintenance:

Monthly:

- Install operating system updates
- Verify available disk space
- Confirm Chromium launches correctly
- Check health-check status

Quarterly:

- Create a fresh backup
- Review display configuration
- Test automatic recovery
- Inspect HDMI and power connections

---

# Common Deployment Issues

## Wrong Display Size

Check:

```bash
wlr-randr
```

Verify the configured display mode matches the television.

---

## Wrong Rotation

Adjust:

```bash
DISPLAY_TRANSFORM
```

or test:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 90
```

---

## Chromium Does Not Start

Check:

```bash
pgrep -a chromium
```

Review:

```bash
taqwa-status
```

---

## Display Sleeps

Wake the display:

```bash
wlopm --on '*'
```

Confirm power-saving settings are configured correctly.

---

## Website Does Not Load

Verify:

- Internet connectivity
- Correct DISPLAY_URL
- DNS resolution
- Firewall rules (if applicable)

---

# Recommended Deployment Practices

- Test every Raspberry Pi before installation.
- Use reliable power supplies.
- Keep spare SD cards available.
- Document the display configuration.
- Keep regular backups.
- Use remote access where possible.
- Test updates before deploying them to production systems.

---

# Future Improvements

Future releases may include:

- Automated installer
- Automated deployment script
- Configuration validation
- Centralised management
- Fleet deployment support
- Remote monitoring dashboard

---

# Related Documentation

- Installation
- Configuration
- Commands
- Services
- Architecture
- Troubleshooting
- TV Compatibility