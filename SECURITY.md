# Security Policy

## Reporting Security Vulnerabilities

We take security seriously, especially regarding data protection and user privacy. If you discover a security vulnerability in this Discord bot, please report it responsibly.

### How to Report

**DO NOT** create a public GitHub issue for security vulnerabilities.

Instead, please report security vulnerabilities by email to:
- **Primary Contact:** dennisplischke755@gmail.com
- **Subject:** `[SECURITY] Discord Bot Vulnerability Report`

### What to Include

Please provide:
1. Description of the vulnerability
2. Affected component(s) or code section
3. Steps to reproduce (if applicable)
4. Potential impact
5. Suggested fix (if you have one)

### Response Timeline

- **Initial Response:** Within 48 hours
- **Assessment & Fix:** Within 7 days
- **Public Disclosure:** After patch is available and deployed

## Security Considerations

This bot processes user data under **DSGVO/GDPR compliance**. Vulnerabilities affecting the following are especially critical:

- User identification or authentication bypass
- Command logging or data interception
- Blacklist/Whitelist system manipulation
- Unauthorized access to admin commands
- Data storage or transmission vulnerabilities
- Privacy policy violations

See [Privacy Policy](./docs/PRIVACY_POLICY.md) and [Terms of Service](./docs/TERMS_OF_SERVICE.md) for details.

## Supported Versions

| Version | Status  | Support                    |
|---------|---------|----------------------------|
| 1.6.x   | Current | Receiving security updates |
| 1.5.x   | EOL     | No longer supported        |
| 1.4.x   | EOL     | No longer supported        |
| 1.3.x   | EOL     | No longer supported        |
| < 1.3   | EOL     | No longer supported        |

## Security Features

- Global user and server blacklist system with automated enforcement
- Command execution logging (controllable) + Operational logging (mandatory)
- Role-based authorization with hierarchy enforcement
- Atomic file operations for data consistency
- Error handling and validation on all inputs

## Responsible Disclosure

We commit to:
- Acknowledging receipt of your report within 48 hours
- Providing regular updates on our progress
- Crediting you in the security advisory (if desired)
- Not pursuing legal action against good-faith researchers

## Compliance

This project operates under strict GDPR/DSGVO compliance. Security vulnerabilities may be reported as data protection incidents if they compromise personal data.

---

**Last Updated:** February 15, 2026  
**Version:** 1.2
