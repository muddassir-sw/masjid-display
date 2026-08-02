# Installation

This guide explains how to install and configure Masjid Display on a Raspberry Pi running Raspberry Pi OS.

The current documentation is based on the production deployment captured in this repository.

---

# Hardware Requirements

Recommended hardware:

- Raspberry Pi 4 (2 GB RAM or higher)
- Official Raspberry Pi power supply
- MicroSD card (16 GB minimum, 32 GB recommended)
- HDMI television or monitor
- HDMI cable
- Network connection (Wi-Fi or Ethernet)
- USB keyboard (recommended during installation)

The software may also work on other Raspberry Pi models, but only the Raspberry Pi 4 has been tested.

---

# Software Requirements

Install:

- Raspberry Pi OS (64-bit)
- Chromium Browser
- Labwc (Wayland desktop)
- systemd
- Git (optional)
- SSH (recommended)

Update the operating system:

```bash
sudo apt update
sudo apt full-upgrade -y
sudo reboot
```

---

# Clone the Repository

Clone the project:

```bash
git clone https://github.com/<your-username>/masjid-display.git
```

Enter the project directory:

```bash
cd masjid-display
```

Alternatively, copy the project files manually to the Raspberry Pi.

---

# Install the Scripts

Create the application directory:

```bash
mkdir -p ~/.local/share/taqwa-display
```

Copy the scripts:

```bash
cp scripts/* ~/.local/share/taqwa-display/
```

Make the scripts executable:

```bash
chmod +x ~/.local/share/taqwa-display/*
```

---

# Install the Configuration

Create the configuration directory:

```bash
mkdir -p ~/.config/taqwa-display
```

Copy the example configuration:

```bash
cp config/config.env.example ~/.config/taqwa-display/config.env
```

Edit the configuration:

```bash
nano ~/.config/taqwa-display/config.env
```

Typical configuration:

```text
DISPLAY_URL="https://example.org/display"
DISPLAY_OUTPUT="HDMI-A-1"
DISPLAY_TRANSFORM="90"
DISPLAY_MODE=""
HEALTHCHECK_INTERVAL_MINUTES="5"
```

---

# Configure Labwc

Copy the supplied autostart file:

```bash
mkdir -p ~/.config/labwc
cp config/labwc-autostart ~/.config/labwc/autostart
```

The autostart file launches the display automatically when the desktop session starts.

---

# Install the systemd User Services

Create the systemd user directory:

```bash
mkdir -p ~/.config/systemd/user
```

Copy the supplied files:

```bash
cp systemd/taqwa-healthcheck.service ~/.config/systemd/user/
cp systemd/taqwa-healthcheck.timer ~/.config/systemd/user/
```

Reload systemd:

```bash
systemctl --user daemon-reload
```

Enable the timer:

```bash
systemctl --user enable --now taqwa-healthcheck.timer
```

Verify:

```bash
systemctl --user status taqwa-healthcheck.timer
```

---

# Test Chromium

Launch Chromium manually:

```bash
chromium \
    --ozone-platform=wayland \
    --kiosk \
    https://example.org/display
```

Replace the URL with your own display page.

Close Chromium once the test is complete.

---

# Verify the Display

Check the connected displays:

```bash
wlr-randr
```

If using a portrait screen:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --transform 90
```

If required, apply a specific display mode:

```bash
wlr-randr \
    --output HDMI-A-1 \
    --mode 2560x1440@59.951Hz \
    --transform 90
```

Only use display modes supported by your television.

---

# First Boot Test

Restart the Raspberry Pi:

```bash
sudo reboot
```

After rebooting, verify that:

- the desktop starts normally;
- Chromium opens automatically;
- the configured webpage loads;
- the display orientation is correct;
- the display remains awake.

---

# Verify the Health Check

Confirm the timer is active:

```bash
systemctl --user list-timers
```

Run the health check manually:

```bash
systemctl --user start taqwa-healthcheck.service
```

View its status:

```bash
systemctl --user status taqwa-healthcheck.service
```

---

# Useful Commands

Show display status:

```bash
taqwa-status
```

Update the display URL:

```bash
taqwa-update-url
```

Create a backup:

```bash
taqwa-backup
```

---

# Troubleshooting

## Chromium does not start

Check that Chromium is installed:

```bash
chromium --version
```

Check for running processes:

```bash
pgrep -a chromium
```

---

## Display rotation is incorrect

List outputs:

```bash
wlr-randr
```

Try different transforms:

```text
normal
90
180
270
```

---

## Incorrect display size

Check the available modes:

```bash
wlr-randr
```

Only use display modes reported by your television.

Different TV models may require different resolutions and refresh rates.

---

## Black screen after boot

Check:

- HDMI cable
- Power supply
- Display input selection
- Raspberry Pi boot process
- Labwc autostart configuration

---

## Browser crashes

The launcher should restart Chromium automatically.

Check the launcher log:

```bash
tail -n 50 ~/.config/taqwa-display/logs/launcher.log
```

---

# Next Steps

Once the installation is complete, continue with:

- Configuration
- Commands
- Services
- Architecture
- Deployment
- TV Compatibility
- Troubleshooting