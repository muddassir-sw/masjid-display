# TV Compatibility

Masjid Display is designed to work with a wide range of HDMI televisions and monitors.

However, different manufacturers implement HDMI, scaling, overscan and supported display modes differently. As a result, settings that work perfectly on one display may require adjustment on another.

This document provides guidance for configuring different displays and resolving common compatibility issues.

---

# Supported Displays

Masjid Display has been designed for use with:

- Consumer televisions
- Commercial digital signage displays
- Computer monitors
- Portrait information screens
- Landscape information screens

Any HDMI-compatible display supported by Raspberry Pi OS should work.

---

# Before Installation

Before mounting the display:

- Connect the Raspberry Pi.
- Boot into Raspberry Pi OS.
- Verify the display is detected.
- Check the available display modes.

Run:

```bash
wlr-randr
```

This displays:

- connected outputs;
- current resolution;
- supported resolutions;
- supported refresh rates;
- current rotation.

---

# Display Orientation

Masjid Display supports both landscape and portrait installations.

Landscape:

```text
DISPLAY_TRANSFORM="normal"
```

Portrait:

```text
DISPLAY_TRANSFORM="90"
```

Other available values:

```text
180
270
```

Always verify the orientation after physically mounting the display.

---

# Display Resolution

Most televisions work correctly using their preferred resolution.

If necessary, specify a display mode:

```text
DISPLAY_MODE="2560x1440@59.951Hz"
```

To view supported modes:

```bash
wlr-randr
```

Only configure modes reported by the connected display.

---

# Overscan

Some televisions apply overscan, causing parts of the display to be cropped.

Symptoms include:

- edges cut off;
- browser not filling the screen correctly;
- missing text near the edges.

Check the television's picture settings and disable overscan if available.

Manufacturers use different names, including:

- Just Scan
- Screen Fit
- Full Pixel
- 1:1 Pixel Mapping
- PC Mode

Consult the television manual for the appropriate option.

---

# Black Borders

Black borders may be caused by:

- unsupported resolution;
- browser scaling;
- television aspect ratio;
- overscan;
- HDMI scaling.

Verify:

```bash
wlr-randr
```

and ensure the display mode matches one supported by the television.

---

# Browser Scaling

Some websites include their own responsive layouts.

If the browser content does not fill the display:

- check the website itself;
- verify browser zoom is 100%;
- confirm the display resolution;
- test on another television if possible.

---

# Refresh Rates

Different televisions support different refresh rates.

Examples:

```
60 Hz
59.94 Hz
59.951 Hz
50 Hz
30 Hz
```

Always use a refresh rate reported by `wlr-randr`.

---

# Portrait Displays

Portrait installations should be tested after mounting.

Verify:

- rotation;
- readable text size;
- browser scaling;
- touch support (if applicable);
- automatic startup.

---

# Multiple Displays

Each Raspberry Pi should normally drive a single display.

If deploying multiple displays:

- configure each Raspberry Pi separately;
- test each display individually;
- do not assume identical settings.

Even identical television models may expose different supported modes depending on firmware versions.

---

# Troubleshooting Checklist

If the display does not appear correctly:

1. Check the HDMI cable.
2. Confirm the television input.
3. Run:

```bash
wlr-randr
```

4. Verify:

- output name;
- display mode;
- rotation.

5. Test another HDMI cable if necessary.

6. Restart Chromium:

```bash
pkill -x chromium
```

The launcher should restart it automatically.

---

# Deployment Notes

During development, different televisions required different combinations of:

- resolution;
- refresh rate;
- rotation;
- browser scaling.

For this reason, Masjid Display intentionally allows these settings to be configured rather than hardcoding values.

Treat each television as a separate device and validate the configuration before placing it into production.

---

# Best Practices

- Use the television's preferred resolution whenever possible.
- Avoid unsupported display modes.
- Disable overscan where possible.
- Test portrait mode after installation.
- Verify the display after every operating system upgrade.
- Record any TV-specific settings for future maintenance.

---

# Related Documentation

- Installation
- Configuration
- Deployment
- Troubleshooting
- Commands