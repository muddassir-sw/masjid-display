# Security Policy

## Supported Versions

At present, only the latest released version of Masjid Display is actively supported with security updates.

| Version | Supported |
|----------|-----------|
| Latest Release | ✅ Yes |
| Older Releases | ❌ No |

---

## Reporting a Security Vulnerability

If you discover a security vulnerability, please **do not** open a public GitHub Issue.

Instead, contact the project maintainer privately with as much information as possible.

Please include:

- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested mitigation (if known)
- Raspberry Pi OS version
- Masjid Display version

A response will normally be provided as soon as reasonably possible.

---

## Scope

Security issues may include:

- Remote code execution
- Privilege escalation
- Authentication weaknesses
- Sensitive information disclosure
- Configuration vulnerabilities
- Dependency vulnerabilities
- Shell script injection
- Network security issues

General bugs, feature requests and installation problems should be reported through the project's GitHub Issues page.

---

## Security Best Practices

When deploying Masjid Display, it is recommended to:

- Keep Raspberry Pi OS up to date.
- Regularly update installed packages.
- Change default passwords.
- Use SSH key authentication where possible.
- Restrict SSH access to trusted users.
- Enable a firewall if appropriate for your environment.
- Keep regular backups of the configuration.
- Use HTTPS for display URLs whenever possible.
- Avoid storing sensitive credentials in configuration files.
- Protect the Raspberry Pi from unauthorised physical access.

---

## Third-Party Software

Masjid Display relies on several third-party components, including:

- Raspberry Pi OS
- Chromium
- Labwc
- systemd

Please ensure these components are also kept up to date to receive the latest security fixes.

---

## Responsible Disclosure

Security researchers are encouraged to report vulnerabilities responsibly.

Please allow reasonable time for investigation and remediation before publicly disclosing any security issue.

Responsible disclosure helps protect users and organisations that rely on Masjid Display.

---

## Security Updates

Security-related fixes will be documented in the project's `CHANGELOG.md` and included in the next appropriate release.

Where possible, security fixes will be designed to minimise disruption to existing deployments.