# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in this project, please report it responsibly. **Do not open a public GitHub Issue for security-related concerns.**

### How to Report

1. **GitHub Private Vulnerability Reporting** (preferred)
   - Go to the [Security tab](../../security/advisories/new) of this repository
   - Click "Report a vulnerability"
   - Provide a detailed description

2. **Discord**
   - Contact the maintainer directly via [Discord Server](https://discord.com/invite/tssKYweM3h)
   - Send a private message — do not post in public channels

3. **E-Mail**
   - E-Mail: dennisplischke755@gmail.com
   - Subject: `[SECURITY] Discord Bot Vulnerability Report`

### What to Include

- Description of the vulnerability
- Steps to reproduce the issue
- Potential impact or severity
- Suggested fix (if applicable)

## Scope

The following areas are considered in scope:

- Permission bypass or privilege escalation
- Command injection or code execution
- Path traversal or unauthorized file access
- Rate limiting bypass
- Data leakage (e.g., token exposure, config data)
- Denial of service via bot commands

The following are **out of scope**:

- Issues in third-party dependencies (report these upstream)
- Social engineering attacks
- Attacks requiring physical access to the host machine

## Response

|          Action          |      Timeframe      |
|--------------------------|---------------------|
| Acknowledgment of report |   Within 48 hours   |
| Initial assessment       |    Within 7 days    |
| Fix or mitigation        | Depends on severity |

Reports will be handled confidentially. Credit will be given to reporters upon request, unless anonymity is preferred.

## Supported Versions

Only the latest version on the `main` branch is actively maintained and receives security updates.

|     Version     | Supported |
|-----------------|-----------|
| Latest (`main`) |    Yes    |
| Older versions  |    No     |

---

For non-security-related bug reports or feature suggestions, please see [Contributing](./CONTRIBUTING.md).
