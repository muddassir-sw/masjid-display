# Configuration

Masjid Display is configured using a simple environment file that is read every time the launcher starts Chromium.

This allows the display URL and screen settings to be changed without modifying the application scripts.

---

# Configuration File

The default configuration file is:

```text
~/.config/taqwa-display/config.env
```

The repository includes an example:

```text
config/config.env.example
```

Copy it to the Raspberry Pi:

```bash
mkdir -p ~/.config/taqwa-display

cp config/config.env.example \
   ~/.config/taqwa-display/config.env
```

---

# Example Configuration

```bash
DISPLAY_URL="https://example.org/display"
DISPLAY_OUTPUT="HDMI-A-1"
DISPLAY_TRANSFORM="90"
DISPLAY_MODE=""
HEALTHCHECK_INTERVAL_MINUTES="5"
```

---

# Configuration Options

## DISPLAY_URL

The web page that Chromium opens in kiosk mode.

Example:

```bash
DISPLAY_URL="https://example.org/prayer-times"
```

Requirements:

- Must begin with `http://` or `https://`
- Must be accessible from the Raspberry Pi
- Should be designed for full-screen display
- Should not require frequent user interaction

---

## DISPLAY_OUTPUT

The display output controlled by `wlr-randr`.

Typical value:

```bash
DISPLAY_OUTPUT="HDMI-A-1"
```

To list available outputs:

```bash
wlr-randr
```

Example output:

```text
HDMI-A-1
```

Some hardware may expose different output names.

---

## DISPLAY_TRANSFORM

Controls screen rotation.

Supported values:

```text
normal
90
180
270
```

Example:

```bash
DISPLAY_TRANSFORM="90"
```

Typical usage:

| Value | Result |
|-------|--------|
| normal | Landscape |
| 90 | Portrait clockwise |
| 180 | Upside down |
| 270 | Portrait anti-clockwise |

---

## DISPLAY_MODE

Optional display resolution and refresh rate.

Example:

```bash
DISPLAY_MODE="2560x1440@59.951Hz"
```

Leave empty if no specific mode is required:

```bash
DISPLAY_MODE=""
```

Available modes can be viewed using:

```bash
wlr-randr
```

Always use a mode reported by your television.

Different televisions support different resolutions and refresh rates.

---

## HEALTHCHECK_INTERVAL_MINUTES

Documents the intended health check frequency.

Example:

```bash
HEALTHCHECK_INTERVAL_MINUTES="5"
```

The actual schedule is controlled by the systemd timer.

Keep both values consistent.

---

# Editing the Configuration

Open the configuration file:

```bash
nano ~/.config/taqwa-display/config.env
```

Save the file.

Restart Chromium:

```bash
pkill -x chromium
```

The launcher will automatically start Chromium again using the updated configuration.

---

# Validating the Configuration

View the current configuration:

```bash
cat ~/.config/taqwa-display/config.env
```

Verify the display:

```bash
wlr-randr
```

Check Chromium:

```bash
pgrep -a chromium
```

Display the current status:

```bash
taqwa-status
```

---

# Updating the Display URL

The URL can also be changed using the helper utility.

```bash
taqwa-update-url
```

Or:

```bash
taqwa-update-url "https://example.org/display"
```

The launcher will restart Chromium using the updated URL.

---

# Portrait Displays

Most portrait televisions use:

```bash
DISPLAY_TRANSFORM="90"
```

The required value depends on how the television is physically mounted.

If the screen appears upside down or rotated incorrectly, try:

```text
normal
90
180
270
```

---

# Display Resolution

Most installations work correctly using the television's preferred mode.

If scaling problems occur:

1. List supported modes.

```bash
wlr-randr
```

2. Select one of the reported modes.

Example:

```bash
DISPLAY_MODE="2560x1440@59.951Hz"
```

Do not configure unsupported resolutions.

---

# Best Practices

- Keep the configuration file simple.
- Use HTTPS whenever possible.
- Keep the display URL publicly accessible if remote monitoring is required.
- Back up the configuration before making major changes.
- Test configuration changes before deploying to a production display.

---

# Common Problems

## Chromium shows the wrong page

Verify:

```bash
cat ~/.config/taqwa-display/config.env
```

Confirm that `DISPLAY_URL` is correct.

---

## Rotation is incorrect

Verify:

```bash
wlr-randr
```

Try another transform value.

---

## Black border around the display

Verify:

- television aspect ratio;
- overscan settings;
- selected display mode;
- browser scaling.

Some televisions require manual adjustment.

---

## Display mode is ignored

Check that:

- `DISPLAY_MODE` exactly matches one of the modes reported by `wlr-randr`;
- the television supports the requested refresh rate.

---

# Related Documentation

- Installation
- Commands
- Services
- TV Compatibility
- Troubleshooting