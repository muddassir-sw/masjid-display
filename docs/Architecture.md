# Architecture

Masjid Display is a lightweight Raspberry Pi kiosk platform designed for reliable, unattended operation in mosques.

Rather than being a single application, it consists of a small number of shell scripts, configuration files and systemd user services working together to display a web page in Chromium kiosk mode.

The design prioritises simplicity, reliability and ease of maintenance over unnecessary complexity.

---

# Design Goals

The project was designed with the following objectives:

- Reliable unattended operation
- Simple deployment
- Easy maintenance
- Minimal software dependencies
- Automatic recovery from browser failures
- Easy remote administration
- Support for portrait and landscape displays
- Configuration without modifying application code

---

# High-Level Architecture

```
                    Raspberry Pi OS
                           │
                           ▼
                   Wayland (Labwc)
                           │
                           ▼
                  Labwc Autostart
                           │
                           ▼
                  taqwa-launcher
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
      Display Configuration       Chromium Kiosk
              │                         │
              └────────────┬────────────┘
                           ▼
                  Prayer Display Website

                           ▲
                           │
                taqwa-healthcheck
                           ▲
                           │
                 systemd User Timer
```

---

# Main Components

The platform consists of five major components.

## 1. Raspberry Pi OS

Provides:

- Linux operating system
- Networking
- Wayland desktop
- Package management
- SSH access
- systemd

---

## 2. Labwc

Labwc is the Wayland compositor used by the deployment.

Responsibilities include:

- Desktop session
- Display management
- Launching startup applications
- Window management

Labwc automatically starts the launcher through its autostart configuration.

---

## 3. Launcher

The launcher is responsible for controlling the display.

Responsibilities:

- Load configuration
- Wake the display
- Apply rotation
- Apply display mode
- Start Chromium
- Restart Chromium after unexpected exits

The launcher runs continuously.

If Chromium exits, the launcher waits briefly before starting it again.

---

## 4. Chromium

Chromium provides the full-screen kiosk interface.

It displays:

- Prayer timetable
- Announcements
- Donation campaigns
- Community notices
- Any other supported web page

The launcher starts Chromium using Wayland.

---

## 5. Health Check

The health-check script runs periodically using a systemd user timer.

Responsibilities include:

- Check Chromium
- Check website availability
- Wake the display
- Record status information
- Restart Chromium if required

---

# Configuration Flow

```
config.env
      │
      ▼
Launcher
      │
      ├── DISPLAY_URL
      ├── DISPLAY_OUTPUT
      ├── DISPLAY_TRANSFORM
      ├── DISPLAY_MODE
      └── HEALTHCHECK_INTERVAL_MINUTES
```

The launcher reads the configuration every time Chromium starts.

This allows configuration changes without modifying the scripts.

---

# Startup Sequence

```
Power On
    │
    ▼
Raspberry Pi OS boots
    │
    ▼
User session starts
    │
    ▼
Labwc starts
    │
    ▼
Autostart executes
    │
    ▼
taqwa-launcher
    │
    ▼
Configuration loaded
    │
    ▼
Display configured
    │
    ▼
Chromium starts
    │
    ▼
Prayer display shown
```

---

# Recovery Sequence

```
Chromium exits
       │
       ▼
Launcher detects exit
       │
       ▼
Wait three seconds
       │
       ▼
Restart Chromium
```

No user interaction is required.

---

# Health Monitoring

```
systemd Timer
       │
       ▼
Health Check Service
       │
       ▼
Health Check Script
       │
       ├── Website
       ├── Chromium
       ├── Display
       └── Status File
```

The monitoring process runs independently of Chromium.

---

# File Structure

```
config/
    Configuration templates

scripts/
    Launcher
    Health check
    Backup
    Status
    URL update

systemd/
    User services

docs/
    Project documentation

images/
    Screenshots
```

---

# Why Shell Scripts?

The project intentionally uses shell scripts instead of a compiled application.

Advantages include:

- Easy to understand
- Easy to customise
- Easy to troubleshoot
- Minimal dependencies
- Native Raspberry Pi support
- Easy remote maintenance

The scripts can be edited directly using any text editor.

---

# Why Chromium?

Chromium provides:

- Excellent HTML support
- JavaScript support
- Responsive layouts
- Modern browser engine
- Stable kiosk mode
- Wide compatibility

This allows mosque websites to be updated without changing the Raspberry Pi software.

---

# Why Wayland?

The project uses Wayland because it is the default graphical platform for current Raspberry Pi OS releases.

Benefits include:

- Better security
- Modern graphics stack
- Improved display handling
- Future-proof architecture

---

# Scalability

The same architecture can be used for:

- Main prayer halls
- Women's prayer halls
- Entrance displays
- Information kiosks
- Reception displays
- Educational displays
- Multi-screen deployments

Each Raspberry Pi simply requires its own configuration file.

---

# Future Improvements

Potential future enhancements include:

- Automated installer
- Generic internal naming
- Web management interface
- Remote monitoring dashboard
- Automatic software updates
- Multiple display profiles
- Centralised management
- Containerised development environment

---

# Summary

Masjid Display deliberately keeps the architecture simple.

A small collection of well-defined components provides a reliable, maintainable and easily understandable digital signage platform that can be deployed and maintained with minimal effort.

The architecture has been proven through real-world deployment and is intended to serve as a foundation for future enhancements while remaining lightweight and dependable.