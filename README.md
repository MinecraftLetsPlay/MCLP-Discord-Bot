# 🤖 MCLP Discord Bot

<div align="center">

## A Feature-Rich Discord Bot for Your Community

A comprehensive Discord bot built with [Discord.py](https://discordpy.readthedocs.io/en/stable/), providing moderation tools, minigames, utility commands, music streaming, and much more!

**A privately operated bot with permission controls, persistent features, and transparent documentation.**

[![Discord](https://img.shields.io/badge/Discord-Join%20MCLP-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/tssKYweM3h)
[![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Discord.py](https://img.shields.io/badge/Discord.py-2.7.1-5865F2?style=for-the-badge)](https://discordpy.readthedocs.io/)
[![License](https://img.shields.io/badge/License-Private-red?style=for-the-badge)](./LICENSE.txt)

</div>

---

## 📖 Table of Contents

- [About This Repository](#-about-this-repository)
- [Features Overview](#-features-overview)
- [Screenshots](#-screenshots)
- [Getting Started](#-getting-started)
- [Tech Stack](#-tech-stack)
- [How the Bot Works](#how-the-bot-works)
- [Code Examples](#-code-examples--architecture)
- [Legal & Compliance](#-legal--compliance)
- [Changelog](#-changelog)
- [Contact & Support](#-contact--support)

---

## 📚 About This Repository

This is the **public-facing repository** for the MCLP Discord Bot. The actual bot source code is kept private, but this repository serves as:

- **Documentation Hub** - Comprehensive information about the bot's features and capabilities
- **Legal Information** - Privacy Policy, Terms of Service, and Security Policy
- **Feature Showcase** - Demonstrations of what the bot can do
- **Contact Point** - How to get in touch for support or inquiries

The bot is a privately operated service; its source code is not public, and the bot is not available for self-hosting or public invitation.
Production runs on a self-managed Raspberry Pi in Germany, with operational data stored in MariaDB.
This repository documents the service and its features; it does not contain the bot implementation.

---

## ✨ Features Overview

### 🎵 Music Streaming
Stream music directly from YouTube and SoundCloud in voice channels with queue management, playback controls, and volume adjustment.

### 🎮 Interactive Games
Enjoy text-based minigames including Quiz, Hangman, Rock-Paper-Scissors, Number Guessing, and more!

Also includes practical game utilities (for example Minecraft-focused helper tools).

### 🛠️ Utility Tools
Access weather information, time zones, persistent one-time and scheduled reminders, persistent polls, pet facts, Discord service status, and an advanced calculator with equation solving.

### 🛡️ Moderation Features
Moderation tools include kick, ban, timeout, purge, slowmode, configurable warnings, reaction roles, flood protection, and permission controls.

### 🌌 Science & Astronomy
Explore space with NASA's Astronomy Picture of the Day, Mars rover photos, asteroid tracking, and exoplanet data.

### ⚡ System Features
- MariaDB-backed configuration and persistent reminders, polls, warnings, and reaction-role mappings
- Operational logging, rate limits, and command cooldowns
- Emergency lockdown and global cooldown controls
- Per-server flood protection and rotating bot status
- Runtime telemetry and monitoring

---

## 📸 Screenshots

**Note:** This repository includes a collection of screenshots showcasing the MCLP Discord Bot's features and user interface.

For the complete screenshot gallery, see [SCREENSHOTS.md](./SCREENSHOTS.md).

### Featured Categories

- **🎵 Music Player** — Queue management, playback controls, and music-related interactions
- **🎮 Interactive Games** — Quiz, Hangman, and other minigames
- **🛠️ Utility Commands** — Weather, reminders, polls, status checks, and other utilities
- **🌌 Science Features** — NASA imagery, astronomical data, and scientific information
- **🛡️ Moderation Tools** — Moderation commands, warnings, permissions, and server management
- **⚙️ System Features** — System controls, security features, emergency systems, and operational tools

Each category currently contains selected examples of the bot in action, with additional screenshots added as new features are developed.

---

## 🚀 Getting Started

### Join the MCLP Server

Experience the bot in action by joining the official MCLP Discord server:

[![Join Discord](https://img.shields.io/badge/Join-MCLP%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/tssKYweM3h)

### Bot Invitation

> **Note:** This bot is currently operated as an exclusive, privately-hosted service. It is not available for public invitation at this time.
>
> To inquire about availability or partnerships, please contact the bot owner through the MCLP Discord server.

### Quick Start Commands

Once you have access to the bot:

```
!help           - Display all available commands
!weather <city> - Get weather information
!play <song>    - Play music in voice channel
!quiz           - Start a quiz game
!reminder       - Set a reminder
!status         - Check Discord service status
```

---

## 💻 Code Examples & Architecture

The bot's source code is private. The linked examples are illustrative material, not a source release or a complete description of the current runtime implementation.

### 📚 Available Documentation

**[View Code Examples & Architecture →](./CODE_SNIPPETS.md)**

Learn about:
- 🏗️ **Project Architecture** - Module structure and organization
- 🎯 **Design Patterns** - Command routing, rate limiting, permissions
- 🔒 **Security Practices** - Input validation, timeout protection, safe file access
- 🎵 **Music System** - Player design and queue management
- 📊 **Logging System** - Structured logging with rotation
- 🚨 **Emergency System** - Lockdown and cooldown mechanisms
- 📡 **API Integration** - Working with external APIs (NASA, Weather, etc.)

The examples cover topics such as command routing, rate limits, permission checks, music playback, logging, and external APIs.
Refer to the feature and persistence sections below for the current service overview.

---

## How the Bot Works

The bot's implementation is private, so this repository does not provide an installable copy or a complete source-code listing.
At a high level, Discord events and prefix commands are handled by the bot and a central command router;
command modules use shared permission, rate-limit, and database services.

### Data and persistence

- **MariaDB:** Operational configuration, access lists, warnings and audit events, reaction-role mappings, active reminders, polls and votes, and monitoring data.
- **Read-only JSON files:** Static game content only; they are not used for operational state.
- **In-memory state:** Music playback, active games, temporary cooldown/flood counters, and other runtime-only state. This state normally ends when the bot process stops.
- **Environment configuration:** Credentials and API keys are supplied to the private runtime and are not published in this repository.

Active reminders, polls, and emergency settings are restored after a restart. Detailed internal architecture documentation is not included in this public repository.

---

## Features

### 🎵 Music Streaming & Playback

Stream your favorite music directly in Discord voice channels with full playback control.

**Available Commands:**
- `!join`- Let the bot join the current voice channel
- `!leave` - Let the bot leave the current voice channel
- `!play <song>` - Play a song from YouTube or SoundCloud
- `!pause` / `!resume` - Control playback
- `!stop` - Clears the queue and stops the music
- `!skip` - Skip to next song in queue
- `!queue` - View the current queue
- `!nowplaying` - See what's currently playing
- `!repeat` - Lets you repeat a song or the whole queue
- `!last` - Lets you play the last played song again

**Supported Platforms:** YouTube, SoundCloud

---

### 🎮 Interactive Minigames

Engage your community with fun text-based games.

**Available Games:**
- **Quiz** - Multiple categories with multi-language support
- **Hangman** - Classic word guessing game
- **Rock Paper Scissors** - `!rps` challenge the bot
- **Number Guess** - `!guess` the right number
- **Dice Rolling** - `!roll` with custom dice notation

---

### 🛠️ Utility Commands

Helpful tools for everyday use.

- **Weather** - Real-time weather data (`!weather <city>`)
- **City Info** - Geographic and timezone information (`!city <name>`)
- **Time** - Local time for any location (`!time <city>`)
- **Reminders** - Set one-time or scheduled reminders (`!reminder`, `!scheduled-reminder`)
- **Reminder management** - View and delete reminders (`!reminders`); active reminders are stored in MariaDB and restored after a restart
- **Polls** - Create interactive polls (`!poll`) and delete them (`!deletepoll`); active polls and votes are stored in MariaDB and restored after a restart
- **Cat Facts** - Random cat facts (`!catfact`)
- **Dog Facts** - Random dog facts (`!dogfact`)
- **Calculator** - Advanced math calculator with equation solving (`!calc`)
- **Discord Status** - Check Discord service status (`!status`)

---

### 🛡️ Moderation Tools

Comprehensive server management features.

- **User Management** - Kick, ban, unban users
- **Timeout System** - Temporary muting (`!timeout`, `!untimeout`)
- **Message Management** - Bulk message cleanup (`!purge`)
- **Slowmode Control** - Enable/disable and configure slowmode (`!slowmode`)
- **Warnings** - `!warn` with configurable follow-up action and optional role; warning history and audit events are stored in MariaDB
- **Reaction Roles** - Auto-assign roles via reactions
- **Flood Protection** - Per-server thresholds, time windows, and mitigation modes
- **Permission System** - Global and server-specific whitelists
- **Blacklist System** - Global enforcement of Terms of Service
- **Logging Controls** - Configurable command and operational logging

---

### 🌌 Science & Astronomy Features

Explore the cosmos with data from NASA APIs.

- **Astronomy Picture of the Day** - `!apod`
- **Mars Photos** - Curiosity & Spirit rover images (`!marsphoto`)
- **Asteroid Tracking** - Near-Earth objects (`!asteroids`)
- **Solar Activity** - Sun data and space weather (`!sun`)
- **Exoplanets** - Search for potentially habitable worlds (`!exoplanet`)

---

### ⚙️ System Features

Advanced bot capabilities for stability and security.

- **Operational Logging** - Security and stability logs cannot be disabled; old log files are subject to a 14-day cleanup attempt
- **Rate Limiting** - Per-user and per-command cooldowns
- **Emergency System** - Lockdown and cooldown modes for abuse protection
- **Status Rotation** - Automatic rotating status messages
- **Runtime Monitoring** - Telemetry for uptime, latency, errors, and other runtime metrics
- **Multi-API Integration** - NASA, OpenWeatherMap, Dictionary, and more

---

### 📡 External Features

An optional, separately operated tool for announcing updates, problems, or important news.

- **Opt-in** - Server administrators configure an announcement channel with `!update-channel`; only enabled servers with a configured channel are targeted.
- **Operator-triggered** - The bot owner runs the broadcast utility separately; announcements are not sent automatically.
- **MariaDB configuration** - The enabled state and announcement channel are stored in the guild settings.
- **Local reports** - The tool writes JSON reports containing the announcement preview, target IDs, and send results.

---

## 💼 Tech Stack

### Core Packages

The current dependency manifest supports Python **3.11.2 through 3.13.5**. Key direct dependencies include:

- **discord.py[voice] 2.7.1** - Discord API and voice support
- **aiomysql 0.3.2** and **PyMySQL 1.2.3** - MariaDB access
- **Flask 3.1.3** - Monitoring dashboard
- **rich 15.0.0** - Console monitoring
- **yt-dlp 2026.10.26** - Music search and playback
- **sympy 1.14.0** - Calculator and equation solving
- **python-dotenv 1.2.4** - Environment configuration
- **psutil 7.2.2** - Process and system monitoring

For the authoritative list, see [`requirements.txt`](./requirements.txt).

### Runtime Environment

- **Linux infrastructure** - Production runs on a self-managed Raspberry Pi in Germany.
- **Python venv** - Isolated dependency environment
- **FFMPEG** - Audio encoding/decoding
- **MariaDB** - Persistent operational data and configuration
- **Read-only JSON** - Static game content
- **Logging and monitoring** - Operational logs and database-backed telemetry

---

## APIs & Data Sources

- **Discord API** - Login, chat, slash commands, events
- **Discord Voice API** - Voice support (via PyNaCl)
- **Cat Fact API** - Random cat facts
- **Dog Fact API** - Random dog facts
- **Free Dictionary API** - English & German dictionaries
- **OpenWeatherMap API** - Real-time weather and city data
- **NASA API** - Mars photos, asteroids, astronomy, space weather, exoplanets
- **YouTube Music** - Music playback/search via yt-dlp
- **SoundCloud** - Music playback/search via yt-dlp
- **Status Discord API** - Displaying gateway and API status

---

## 📖 Legal & Compliance

The bot's [Terms of Service](./Legal/TERMS_OF_SERVICE.md) cover:
- Usage rights and limitations
- Acceptable use policies
- Logging and monitoring practices
- Blacklist system and enforcement
- **Broadcast System (optional announcements)**
- Data retention and deletion rights

**Current document version:** 2.1 (Last updated: November 6, 2026)

### Privacy Policy

The [Privacy Policy](./Legal/PRIVACY_POLICY.md) (document version 2.2, last updated November 6, 2026) describes:
- What data is collected and why
- How data is stored and protected
- Your rights regarding your data
- Blacklist data handling
- Complete data categories with retention periods

### Data Protection

- **Production hosting:** Self-managed Raspberry Pi at the controller's home in Germany
- **Database:** MariaDB; records have different retention behavior depending on the feature
- **Logs:** The application attempts to delete log files older than 14 days; this does not apply to database records, backups, or other copies
- **Backups:** The production database is backed up locally (compressed, SHA256 checksums, 14 most recent kept); log files are not. Deleted records can remain in backups until rotated out
- **Access requests:** Contact the controller; there is no self-service data export or universal deletion schedule
- **Contact:** dennisplischke755@gmail.com

The Privacy Policy describes current processing and retention behavior; it is not a legal opinion or a blanket guarantee of compliance.

---

## 🌟 Why Choose MCLP Bot?

### 🔒 Transparent Data Handling
- **Documented Practices** - The Privacy Policy describes data categories, storage, and retention behavior
- **Feature-Specific Retention** - Persistent database records are distinguished from temporary in-memory state
- **Contact for Requests** - Data access and deletion requests can be sent to the controller
- **Germany-Based Hosting** - Production runs on a self-managed Raspberry Pi in Germany

### 🚀 Operations
- **Self-Managed Hosting** - The production bot runs on a Raspberry Pi
- **MariaDB Persistence** - Selected operational features are restored after restarts
- **Rate Limiting** - Per-user and command-level controls help limit abuse
- **Runtime Monitoring** - Telemetry tracks service health and errors

### 🛡️ Security Focused
- **Blacklist System** - Automated enforcement against abuse
- **Permission Hierarchy** - Sophisticated authorization system
- **Emergency Lockdown** - Protection against attacks and spam
- **Operational Controls** - Emergency lockdown, cooldown, and per-server flood-protection settings

### 🎨 Feature Rich
- **Broad Feature Set** - Music, games, utilities, moderation, astronomy, and administration
- **Multiple APIs** - Integration with NASA, OpenWeather, YouTube, and more
- **Active Development** - Regular feature additions and improvements
- **Community Driven** - Responsive to user feedback

---

## 🔧 Technical Requirements

**For hosting (informational only; the bot is not available for self-hosting):**

This bot requires the following to operate:

- **Python 3.11.2 - 3.13.5** - Supported runtime range in the dependency manifest
- **discord.py[voice] 2.7.1** - Discord API wrapper and voice support
- **FFMPEG** - Audio encoding/decoding for music features
- **MariaDB** - Required for operational configuration and persistent features
- **Various Python packages** - See [`requirements.txt`](./requirements.txt)

### Hardware Specifications (Current Setup)
- **Platform:** Self-managed Raspberry Pi
- **Location:** Germany
- **Database:** MariaDB

### Software Stack
- **OS:** Linux (Raspberry Pi OS / Debian-based)
- **Environment:** Python venv for isolated dependencies
- **Database:** MariaDB for operational state; read-only JSON files for static game content
- **Logging:** Log-file cleanup attempts to remove files older than 14 days; this is not a general data-retention period

**Note:** The bot is privately hosted and not available for self-hosting. This information is provided for transparency about the technical infrastructure.

---

## 📜 Changelog

### Historical development notes

The entries below describe earlier development milestones and are not the current feature or version list.

### Version 2.0 - Migration from JSON-based atomic reads/writes to an SQL database

- Migrated all production data to an SQL database
- Completely reworked data access across all command modules
- Deleted all old JSON write code and only kept JSON read code
- Changed the reading logic of the Bot-Dashboard to now read directly from DB
- Added several error-handling and edge-case checks
- Added new `!purge` command to quickly delete many messages from a channel
- Updated legal documents and `/privacy` command
- Updated README and code snippets.
- Repaired `!apod` command. Due to changes of NASA deactivating the old endpoint and moving to a new one.
- Updated the Broadcast-Tool to use the DB to read if servers have set up the announcement channel and enabled it
- Rephrased warning and error messages, added comments and docstrings

### Version 1.9 - Code hardening and stability & Feature updates

- Fixed some errors in the telemetry and dashboard modules and updated shown data for better insights
- Recalibrated penalties for the health score on the dashboard
- Added many docstrings and comments for readability and explanation
- The `!poll` command got a huge update, now enabling finite votes and timed polls
- Fixed the `!untimeout` command not finding the wanted person in some cases
- Removed some deprecated code and package imports
- Fixed uptime-tracking of the bot and now counting / tracking downtime from reconnects & internet / connection outages
- Updated color embeds of the !weather command and made colors consistent across all command modules
- Repaired `!sun` command. Due to changes to data provided from the endpoint.

### Version 1.8 - Code efficiency refactoring & Feature expansion

- Complete refactoring of all command modules (moved from an `if command_token ==` system to a sub-router/dispatcher system)
- New module: game_commands with commands like `!portal`, `!stronghold` and `!potion`
- Enhanced !last command from music command to remember last song even if !stop or !skip was used
- Enhanced stability and capability of the Broadcast system
- Added new !warn command to moderation with configurable automatic action if a user hits 3 active warnings
- Added new Flood Protection command that can take configurable actions per guild to defend against DoS attacks
- Patched multiple errors and improved code stability
- Updated Legal Documents and Readme + Opened discussion for MCLP Bot

### Version 1.7 - Service Runtime, Monitoring & Feature Expansion

- Added `!dogfact` command and integrated Dog Fact API handling
- Expanded moderation tools with `!purge` and `!slowmode`
- Extended game feature set with dedicated game utility modules
- Improved reminder parsing with better natural-language support (including German keywords)
- Enhanced music workflow, including easier SoundCloud search and `!last` playback support
- Strengthened calculator stability and abuse protection with safer evaluation flow and timeout isolation
- Added runtime telemetry and a public-facing dashboard with privacy-reduced metrics
- Migrated bot runtime to a managed Linux service setup for improved operational reliability
- Improved shutdown/restart behavior and status transitions
- Updated dependencies and moved runtime to Python 3.13.14

### Version 1.6 - Code hardening and stability update

- Added new rate limits for music commands
- Added a new per user rate limiting / cooldown system
- Added various validation and sanitizing checks
- Closed various edge-cases and stability-issues
- Prevented some loops and race conditions
- Patched path traversal issues
- Added memory cleanups for lists / arrays
- Moved to a command-token based command matching for better performance
- Added new module status_cycle.py for status rotation
- Added new commands `!status`, `!scheduled-reminder`, `!reminders`
- Added emergency-measure system for protection against spam / dos
- Updated legal documents accordingly

### Version 1.5 - Broadcast System Release

- Added optional Broadcast System for announcements and updates
- New command `!update-channel` to enable announcements in a channel
- Broadcast tool (`tools/broadcast-system/`) with message loading and delivery
- Configuration stored in server configs (`announcements` setting)
- Detailed error messages for missing announcement files
- Updated Terms of Service to document Broadcast System
- Updated documentation regarding notification methods

### Version 1.4 - Blacklist System & Logging Refinement

- Global user and server blacklist system
- Blacklist enforced on all command types (prefix and slash)
- Blacklist hierarchy: Blacklist > Whitelist (blacklist is absolute)
- Automatic blacklist status display on bot startup
- Comprehensive blacklist documentation in TOS & Privacy Policy
- Appeal process for incorrectly blacklisted users/servers

### Version 1.3 - Logging & Documentation Update

- Clarified mandatory operational logging vs. controllable command logging
- Updated documentation to be DSGVO/GDPR compliant
- Renamed `/dsgvo` command to `/privacy` with improved content
- Refactored logging documentation in TOS and Privacy Policy
- All logging descriptions now distinguish between command and operational logs

### Version 1.2 - Security & Compliance Update

- Huge security and code structure update
- New security system implemented for calculator
- Prevented path traversal attacks in utility_commands
- Added comprehensive exception handling
- Removed emojis from logging messages for machine readability
- Removed mcserver_commands and associated code
- Implemented rate_limiter.py with rate limits
- Made bot DSGVO/GDPR compliant
- Added Terms of Service & Privacy Policy
- Added `/dsgvo` command for legal information

### Version 1.1 - Music Feature Release

- Music-bot feature fully implemented
- Renamed commands to command_modules with music subfolder
- New music_commands.py for music commands (!join, !play, !pause, !resume)
- New player.py with search and playback logic
- Updated `/logging_channel` to use both enabled/disabled channels
- Updated public_commands and command_router
- Updated requirements.txt

### Version 1.0 - Initial Release

- Authorization system with atomic read/write functions
- Both global and server-based authorization
- Configurable logging with channel inclusion/exclusion
- Per-server config.json files
- Optimized file access and authorization logic

---

## 📞 Contact & Support

For privacy-related inquiries or legal questions:
- Email: dennisplischke755@gmail.com
- Discord: @MinecraftLetsPlay2912

For bug reports:
- GitHub Issues  

---

## 👥 Authors & Contributors

### Core Team

**Dennis Plischke** - *Owner & Lead Developer*
- Discord: @MinecraftLetsPlay2912
- Email: dennisplischke755@gmail.com
- Role: Bot development, infrastructure, legal compliance

**Robin Stiller** - *Co-Developer & Team Member*
- Role: Feature development, testing, code review

### Acknowledgments

Special thanks to:
- The Discord.py community for the excellent API wrapper
- All API providers (NASA, OpenWeatherMap, etc.)
- The MCLP Discord community for feedback and support

---

## 🤝 Contributing

This is a closed-source project. The bot code is private, and contributions are not accepted at this time.

However, you can help by:
- 🐛 Reporting bugs through Discord or GitHub Issues
- 💡 Suggesting features or improvements
- 📣 Sharing feedback about the bot
- ⭐ Starring this repository if you find it useful

For details, see [Contributing Guidelines](./CONTRIBUTING.md) and [Security Policy](./SECURITY.md).

---

## 📈 Project Status

- **Service:** Privately operated; bot source code is not included in this repository
- **Availability:** The bot is not available for public invitation or self-hosting
- **Legal documents:** Terms of Service 2.1 and Privacy Policy 2.2, both updated November 6, 2026
- **README last updated:** November 6, 2026

---

<div align="center">

### 💙 Thank you for your interest in MCLP Discord Bot

[![Join Discord](https://img.shields.io/badge/Join-MCLP%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/tssKYweM3h)

**Made with ❤️ in Germany 🇩🇪**

---

*This is a privately operated bot; its source code is not published here.*  
*For inquiries, please join the MCLP Discord server or send an email.*

</div>
