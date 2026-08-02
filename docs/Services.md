# Services

Masjid Display uses a combination of shell scripts, Labwc startup configuration and systemd user services to provide a reliable, self-recovering display platform.

This document explains the purpose of each component and how they work together.

---

# Overview

The following components make up the system:

```
Labwc Autostart
        │
        ▼
 taqwa-launcher
        │
        ▼
 Chromium (Kiosk Mode)
        │
        ▼
 Prayer Display Website

        ▲
        │
systemd Timer
        │
        ▼
taqwa-healthcheck
```

---

# Launcher

Repository file:

```
scripts/taqwa-launcher
```

Installed location:

```
~/.local/share/taqwa-display/taqwa-launcher
```

The launcher is the heart of the system.

Its responsibilities include:

- Reading the configuration file
- Applying the configured display mode
- Applying the screen rotation
- Powering on the display
- Starting Chromium
- Waiting for Chromium to exit
- Automatically restarting Chromium if it closes unexpectedly

This allows the display to recover without manual intervention.

---

# Health Check

Repository file:

```
scripts/taqwa-healthcheck
```

Installed location:

```
~/.local/share/taqwa-display/taqwa-healthcheck
```

The health check runs periodically and performs basic operational checks.

Typical checks include:

- Is Chromium running?
- Is the configured website reachable?
- Is the display awake?
- Should Chromium be restarted?

The results are recorded so they can be viewed using the status utility.

---

# Status Utility

Repository file:

```
scripts/taqwa-status
```

Displays:

- Current health status
- Chromium processes
- Recent launcher log
- Timer status

Run:

```bash
taqwa-status
```

---

# URL Update Utility

Repository file:

```
scripts/taqwa-update-url
```

This utility updates the configured display URL without manually editing the configuration file.

Example:

```bash
taqwa-update-url
```

or

```bash
taqwa-update-url "https://example.org/display"
```

After updating the configuration, Chromium is restarted automatically.

---

# Backup Utility

Repository file:

```
scripts/taqwa-backup
```

Creates a compressed backup of the configuration and installed scripts.

Example:

```bash
taqwa-backup
```

The backup does not include:

- Raspberry Pi OS
- Installed packages
- SD card image
- User documents

It is intended to back up the display configuration only.

---

# Labwc Autostart

Repository file:

```
config/labwc-autostart
```

Installed location:

```
~/.config/labwc/autostart
```

This file starts the launcher automatically when the desktop session begins.

Typical tasks performed include:

- Wake the display
- Hide the mouse cursor
- Start the launcher

Without this file the display will not start automatically.

---

# systemd Health Check Service

Repository file:

```
systemd/taqwa-healthcheck.service
```

Installed location:

```
~/.config/systemd/user/
```

This service executes the health-check script.

Run manually:

```bash
systemctl --user start taqwa-healthcheck.service
```

Check status:

```bash
systemctl --user status taqwa-healthcheck.service
```

---

# systemd Timer

Repository file:

```
systemd/taqwa-healthcheck.timer
```

The timer starts the health-check service automatically.

Typical configuration:

```text
OnBootSec=2min
OnUnitActiveSec=5min
Persistent=true
```

View status:

```bash
systemctl --user status taqwa-healthcheck.timer
```

List timers:

```bash
systemctl --user list-timers
```

---

# Service Startup Sequence

```
Power On
    │
    ▼
Raspberry Pi OS
    │
    ▼
User Login
    │
    ▼
Labwc Starts
    │
    ▼
Autostart File
    │
    ▼
taqwa-launcher
    │
    ▼
Chromium
    │
    ▼
Prayer Display
```

---

# Recovery Process

If Chromium exits unexpectedly:

```
Chromium exits
        │
        ▼
Launcher detects exit
        │
        ▼
Wait 3 seconds
        │
        ▼
Restart Chromium
```

This automatic recovery is one of the key features of Masjid Display.

---

# Monitoring

The system can be monitored using:

```bash
taqwa-status
```

or

```bash
systemctl --user status taqwa-healthcheck.timer
```

or

```bash
journalctl --user -u taqwa-healthcheck.service
```

---

# Customisation

Advanced users may customise:

- Health-check interval
- Browser startup options
- Screen rotation
- Display mode
- Startup behaviour
- Additional monitoring checks

When making changes, test them thoroughly before deploying to a production display.

---

# Related Documentation

- Installation
- Configuration
- Commands
- Architecture
- Deployment
- Troubleshooting