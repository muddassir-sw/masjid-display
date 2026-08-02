# Contributing to Masjid Display

Thank you for your interest in contributing to Masjid Display.

Whether you're fixing a bug, improving the documentation or suggesting a new feature, your contribution is appreciated.

The goal of this project is to provide a reliable, lightweight and easy-to-maintain Raspberry Pi display platform for mosques and community organisations.

---

# Ways to Contribute

Contributions may include:

- Bug fixes
- Documentation improvements
- Installation guides
- New features
- Performance improvements
- TV compatibility testing
- Raspberry Pi compatibility testing
- Shell script improvements
- Security improvements
- General suggestions

---

# Before You Begin

Please:

- Read the README.
- Review the existing documentation.
- Check existing issues before creating a new one.
- Discuss significant changes before starting large pieces of work.

---

# Development Philosophy

Masjid Display follows a few simple principles.

## Keep It Simple

Avoid unnecessary complexity.

Simple code is easier to maintain and troubleshoot.

---

## Keep It Reliable

This project is intended for unattended operation.

Reliability should always take priority over adding new features.

---

## Keep Dependencies Minimal

Avoid introducing additional software unless it provides a clear operational benefit.

The project intentionally relies on standard Raspberry Pi tools wherever possible.

---

## Preserve Compatibility

Where possible, avoid breaking existing deployments.

If a breaking change is required, explain it clearly and document the migration process.

---

# Coding Guidelines

When contributing:

- Write readable code.
- Use meaningful variable names.
- Comment unusual behaviour.
- Keep shell scripts consistent with the existing style.
- Test changes before submitting them.

---

# Documentation

Documentation is considered as important as the code itself.

If you change behaviour, please update the relevant documentation.

Examples include:

- README
- Installation Guide
- Configuration Guide
- Commands
- Services
- Troubleshooting

---

# Testing

Before submitting changes, verify:

- Raspberry Pi boots successfully.
- Chromium launches automatically.
- Health checks continue to operate.
- Browser restarts correctly.
- Existing functionality has not been broken.

---

# Pull Requests

Please keep pull requests focused.

A pull request should normally address a single feature, bug or improvement.

Clearly explain:

- what changed;
- why it changed;
- how it was tested.

---

# Bug Reports

When reporting a bug, include as much information as possible.

Helpful information includes:

- Raspberry Pi model
- Raspberry Pi OS version
- Display model
- Output from:

```bash
wlr-randr
```

Configuration:

```bash
cat ~/.config/taqwa-display/config.env
```

System status:

```bash
taqwa-status
```

Screenshots are also helpful where appropriate.

---

# Feature Requests

Feature requests are welcome.

Please explain:

- the problem being solved;
- why the feature is useful;
- any alternative approaches considered.

---

# Security

Please do not publicly disclose security vulnerabilities.

Instead, follow the guidance in **SECURITY.md**.

---

# Code of Conduct

All contributors are expected to follow the project's Code of Conduct.

Please read:

**CODE_OF_CONDUCT.md**

---

# Thank You

Every contribution—whether it is code, documentation, testing or feedback—helps improve Masjid Display for everyone.

Thank you for taking the time to contribute.