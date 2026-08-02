# Development History

This document records the evolution of Masjid Display from its original production deployment to the open-source project published on GitHub.

It is intended to preserve the project's history, explain design decisions and document lessons learned during development.

---

# Background

The project began as a practical solution for displaying prayer times and announcements on televisions within a mosque.

The primary goals were:

- Automatic startup after power loss
- Reliable unattended operation
- Remote administration
- Minimal maintenance
- Low hardware cost
- Easy recovery after failures

Rather than developing a complex application, the project adopted a lightweight approach using Raspberry Pi OS, Chromium and a collection of shell scripts.

---

# Initial Deployment

The first production deployment focused on:

- Raspberry Pi 4
- Chromium Kiosk Mode
- Raspberry Pi OS
- Wayland (Labwc)
- Automatic browser startup

The objective was simply to display a webpage reliably after every reboot.

---

# Improving Reliability

As the deployment matured, additional features were introduced to improve reliability.

These included:

- Automatic browser restart
- Display wake-up
- Health monitoring
- Configuration file support
- Backup utilities
- Status reporting
- URL update utility

These improvements significantly reduced the need for manual intervention.

---

# Display Configuration

Different televisions behaved differently with regard to:

- Resolution
- Refresh rate
- Rotation
- Browser scaling
- Overscan

To avoid hardcoding display settings, configuration options were introduced for:

- DISPLAY_OUTPUT
- DISPLAY_TRANSFORM
- DISPLAY_MODE

This allowed the same software to support multiple display types.

---

# Remote Administration

To minimise maintenance, the deployment was designed to support remote administration.

Routine tasks such as:

- Updating the display URL
- Reviewing system status
- Restarting Chromium
- Creating backups

could all be completed over SSH without requiring physical access to the Raspberry Pi.

---

# Health Monitoring

A lightweight health-check script was added together with a systemd timer.

This provides periodic monitoring while keeping the implementation simple and easy to understand.

The monitoring approach intentionally avoids unnecessary complexity and focuses on practical operational checks.

---

# Production Experience

Real-world deployment highlighted several important lessons.

These included:

- Different televisions require different display settings.
- Display configuration should never be hardcoded.
- Automatic recovery is essential for unattended systems.
- Browser failures should be expected and handled automatically.
- Configuration should be separated from application logic.
- Simple solutions are often more reliable than complex ones.

These lessons influenced the current architecture.

---

# Open Source Release

After operating successfully in a production environment, the project was reorganised into a reusable open-source repository.

This work included:

- Cleaning the repository
- Organising scripts
- Writing documentation
- Adding configuration templates
- Creating installation guides
- Preparing contributor documentation
- Publishing under the MIT License

The goal was to make the project useful for other mosques and community organisations.

---

# Internal Naming

Some scripts and directories still use the original `taqwa-display` name.

These names originate from the first production deployment.

Within this repository, **taqwa-display** and **Masjid Display** refer to the same project.

The original naming has been preserved in the first public release to ensure the published repository matches the tested deployment.

Future releases may adopt more generic internal naming while maintaining compatibility.

---

# Future Direction

Planned improvements include:

- Automated installation
- Generic installer
- Improved diagnostics
- Better logging
- Centralised management
- Remote monitoring
- Additional hardware testing
- Multi-display deployments
- Community contributions

The core philosophy will remain unchanged:

- Keep the system simple.
- Keep it reliable.
- Keep it easy to maintain.

---

# Acknowledgements

Masjid Display was developed through practical deployment and continuous improvement in a live mosque environment.

The project exists because of real operational requirements and the experience gained while solving practical deployment challenges.

It is shared as an open-source project in the hope that it will benefit other mosques, charities and community organisations seeking an affordable and reliable digital display platform.

---

# Version 1.0

Version 1.0 represents the first public release of the project.

It captures the production deployment as documented and tested at the time of publication.

Future releases will continue to improve usability while preserving the lightweight and dependable design that forms the foundation of Masjid Display.