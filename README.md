# 🤖 MCLP Discord Bot

<div align="center">

### A Feature-Rich Discord Bot for Your Community

A comprehensive Discord bot built with [Discord.py](https://discordpy.readthedocs.io/en/stable/), providing moderation tools, minigames, utility commands, music streaming, and much more!

**Designed for private server use with sophisticated permission handling and logging.**

[![Discord](https://img.shields.io/badge/Discord-Join%20MCLP-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/tssKYweM3h)
[![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Discord.py](https://img.shields.io/badge/Discord.py-2.6.4-5865F2?style=for-the-badge)](https://discordpy.readthedocs.io/)
[![License](https://img.shields.io/badge/License-Private-red?style=for-the-badge)](./license.txt)

</div>

---

## 📖 Table of Contents

- [About This Repository](#-about-this-repository)
- [Features Overview](#-features-overview)
- [Screenshots](#-screenshots)
- [Getting Started](#-getting-started)
- [Tech Stack](#-tech-stack)
- [Core Functionality](#core-functionality)
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

The bot is an exclusive, privately-operated service running on dedicated hardware. While the code is not open source, this repository provides transparency about the bot's functionality, data handling, and legal compliance.

---

## ✨ Features Overview

### 🎵 Music Streaming
Stream music directly from YouTube and SoundCloud in voice channels with queue management, playback controls, and volume adjustment.

### 🎮 Interactive Games
Enjoy text-based minigames including Quiz, Hangman, Rock-Paper-Scissors, Number Guessing, and more!

### 🛠️ Utility Tools
Access weather information, time zones, reminders, polls, and even an advanced calculator with equation solving.

### 🛡️ Moderation Features
Comprehensive moderation tools including kick, ban, timeout, reaction roles, and a sophisticated permission system.

### 🌌 Science & Astronomy
Explore space with NASA's Astronomy Picture of the Day, Mars rover photos, asteroid tracking, and exoplanet data.

### ⚡ System Features
- Advanced logging with rotation
- Rate limiting and cooldown protection
- Emergency lockdown system
- Status rotation
- DSGVO/GDPR compliant data handling

---

## 📸 Screenshots

> **Note:** This is a showcase repository. Screenshots demonstrating the bot's features will be added progressively.
> 
> For detailed screenshot plans and guidelines, see [SCREENSHOTS.md](./SCREENSHOTS.md)

### Planned Visual Content

- 🎵 **Music Player** - Queue management and playback controls
- 🎮 **Interactive Games** - Quiz, Hangman, and other minigames in action  
- 🛠️ **Utility Commands** - Weather, reminders, polls, and status checks
- 🌌 **Science Features** - NASA imagery and astronomical data displays
- 🛡️ **Moderation Tools** - Permission systems and configuration interfaces
- ⚙️ **System Features** - Emergency systems and logging configuration

**Coming Soon:** Visual demonstrations of key features with real Discord UI examples.

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

While the bot's source code is private, we provide detailed examples and architectural insights to demonstrate the design patterns and best practices used in the bot's development.

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

### Key Technical Highlights

**Example: Rate Limiting System**
- Token bucket algorithm for fair usage
- Per-user global limits
- Per-command cooldowns
- Protection against spam and abuse

**Example: Permission System**
- Hierarchical permission checks
- Blacklist > Global Whitelist > Guild Whitelist
- Atomic configuration file operations
- Safe and consistent authorization

---

## Core Functionality

### Source Files

- `main.py` - Entry point
- `bot.py` - Main bot initialization and event handling
- `command_router.py` - Command routing system

### Command Modules

- `moderation_commands.py` - Discord moderation - Kick, Ban, Timeout etc.
- `minigames.py` - Text-based minigames - RPS, Hangman, Quiz, Scrabble etc.
- `utility_commands.py` - Utility tools - Weather, Time, Reminder etc.
- `public_commands.py` - Public commands - Help, Info, Serverinfo etc.
- `system_commands.py` - Admin controls, logging configuration and system commands.
- `calculator.py` - Advanced text-based calculator with equation solving.
- `sciencecific_commands.py` - Science commands - Exoplanets, Sun activity etc.
- `music_commands.py` - Music commands / voice channel controls - !join / leave !play etc.
- `player.py` - Plays the music and houses the code to search for the song

### Support Modules

- `utils.py` - Helper functions for loading / writing data and authorization.
- `logging_setup.py` - Advanced logging with rotation.
- `status_cycle.py` - Cycles through pre-defined status messages in set intervalls
- `rate_limiter.py` - Handles per user and global cooldowns and rate limits

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
- **Polls** - Create interactive polls (`!poll`)
- **Cat Facts** - Random cat facts (`!catfact`)
- **Calculator** - Advanced math calculator with equation solving (`!calc`)
- **Discord Status** - Check Discord service status (`!status`)

---

### 🛡️ Moderation Tools

Comprehensive server management features.

- **User Management** - Kick, ban, unban users
- **Timeout System** - Temporary muting (`!timeout`, `!untimeout`)
- **Reaction Roles** - Auto-assign roles via reactions
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

- **Advanced Logging** - Automatic log rotation with 14-day retention
- **Rate Limiting** - Per-user and per-command cooldowns
- **Emergency System** - Lockdown and cooldown modes for abuse protection
- **Status Rotation** - Automatic rotating status messages
- **Multi-API Integration** - NASA, OpenWeatherMap, Dictionary, and more

---

### 📡 External Features

Advanced Broadcast System for announcing updates, problems, or important news.

- **Shared Files** - Broadcast System uses the same server config files as the bot.
- **Completely Optional** - By setting or not setting the update-channel via the `!update-channel` command you can control if you get the updates.
- **Dry-Run and Confirmation** - The tool prompts for confirmation of sending and previews the text so that mishaps are prevented.
- **Supports reading files** - The owner can type text into the console or specify a file to read from.
- **Isolated from bot** - This tool is executed inside another environment with no connection to the bot (Read-only)

---

## 💼 Tech Stack

### Core Packages

- **Python 3.13.5** - Python runtime version
- **Discord.py 2.6.4** - Discord API Wrapper
- **PyNaCl 1.6.1** - Voice support
- **aiohttp 3.13.2** - HTTP/WebSocket client
- **asyncio 4.0.0** - Async operations
- **python-dotenv 1.2.1** - Environment variables
- **sympy 1.14.0** - Advanced math & calculator
- **DateTime 6.0** - Time-based utilities
- **pytz 2025.2** - Timezone handling
- **yt-dlp** - YouTube music streaming

### Runtime Environment

- **Linux infrastructure** - Runs on a dedicated linux infrastructure.
- **Python venv** - Isolated dependency environment
- **FFMPEG** - Audio encoding/decoding
- **JSON** - Data storage (configs, quiz data)
- **Logging with rotation** - Auto log management

---

## APIs & Data Sources

- **Discord API** - Login, chat, slash commands, events
- **Discord Voice API** - Voice support (via PyNaCl)
- **Cat Fact API** - Random cat facts
- **Free Dictionary API** - English & German dictionaries
- **OpenWeatherMap API** - Real-time weather and city data
- **NASA API** - Mars photos, asteroids, astronomy, space weather, exoplanets
- **Status Discord API** - Displaying gateway and API status

---

## ⚖️ Legal & Compliance

The bot operates under strict [Terms of Service](./TERMS_OF_SERVICE.md) that cover:
- Usage rights and limitations
- Acceptable use policies
- Logging and monitoring practices
- Blacklist system and enforcement
- **Broadcast System (optional announcements)**
- Data retention and deletion rights

**Current Version:** 1.5 (Last Updated: January 13, 2026)

### Privacy Policy

Your data is protected under our [Privacy Policy](./PRIVACY_POLICY.md) compliant with **DSGVO/GDPR**:
- What data is collected and why
- How data is stored and protected
- Your rights regarding your data
- Blacklist data handling
- Complete data categories with retention periods

**Current Version:** 1.5 (Last Updated: January 13, 2026)

### Data Protection

- **Server Location:** Germany
- **Compliance:** DSGVO/GDPR Article 13 & 14, German Data Protection Laws
- **Retention:** Command logs deleted after 14 days automatically
- **Blacklist:** Indefinite until appeal/removal
- **Contact:** dennisplischke755@gmail.com

---

## 🌟 Why Choose MCLP Bot?

### 🔒 Privacy First
- **DSGVO/GDPR Compliant** - Full European data protection standards
- **Transparent Data Handling** - Clear documentation of what data is collected and why
- **User Rights Respected** - Easy data access and deletion requests
- **Germany-Based** - Server located in Germany 🇩🇪

### 🚀 Performance & Reliability
- **Dedicated Hardware** - Running on Raspberry Pi 5 with 8GB RAM
- **99%+ Uptime** - Stable and reliable service
- **Rate Limiting** - Fair usage protection for all users
- **Error Handling** - Graceful recovery from issues

### 🛡️ Security Focused
- **Blacklist System** - Automated enforcement against abuse
- **Permission Hierarchy** - Sophisticated authorization system
- **Emergency Lockdown** - Protection against attacks and spam
- **Regular Updates** - Continuous security improvements

### 🎨 Feature Rich
- **50+ Commands** - Comprehensive command library
- **Multiple APIs** - Integration with NASA, OpenWeather, YouTube, and more
- **Active Development** - Regular feature additions and improvements
- **Community Driven** - Responsive to user feedback

---

## 🔧 Technical Requirements

**For hosting (informational - bot is privately hosted):**

This bot requires the following to operate:

- **Python 3.11.2 - 3.13.5** - Python runtime
- **Discord.py 2.6.4** - Discord API wrapper
- **FFMPEG** - Audio encoding/decoding for music features
- **Various Python packages** - See [`requirements.txt`](./requirements.txt)

### Hardware Specifications (Current Setup)
- **Platform:** Raspberry Pi 5 B
- **CPU:** Quad-Core 64-Bit 2.4 GHz
- **RAM:** 8 GB LPDDR4X
- **Storage:** SSD for fast I/O
- **Network:** Stable internet connection

### Software Stack
- **OS:** Linux (Raspberry Pi OS / Debian-based)
- **Environment:** Python venv for isolated dependencies
- **Database:** JSON files for configuration storage
- **Logging:** Automatic rotation with 14-day retention

**Note:** The bot is privately hosted and not available for self-hosting. This information is provided for transparency about the technical infrastructure.

## 📜 Changelog

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

## Recent Features (v1.6+)

- Added new rate limits for music commands
- Added a new per user rate limiting / cooldown system
- Moved to a command-token based command matching for better performance
- Added new module status_cycle.py for status rotation
- Added new commands `!status`, `!scheduled-reminder`, `!reminders`
- Added emergency-measure system for protection against spam / dos
- Updated legal documents accordingly

## Previous Features (v1.5)

- Added optional Broadcast System for announcements and updates
- New command `!update-channel` to enable announcements in a channel
- Broadcast tool (`tools/broadcast-system/`) with message loading and delivery
- Configuration stored in server configs (`announcements` setting)
- Detailed error messages for missing announcement files
- Updated Terms of Service to document Broadcast System
- Updated documentation regarding notification methods

---

## 📞 Contact & Support

For privacy-related inquiries or legal questions:
- Email: dennisplischke755@gmail.com
- Discord: @MinecraftLetsPlay2912

For bug reports:
- GitHub Issues (if public repository)  

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
- 🐛 Reporting bugs through Discord or Github Issues
- 💡 Suggesting features or improvements
- 📣 Sharing feedback about the bot
- ⭐ Starring this repository if you find it useful

---

## 📈 Project Status

- **Current Version:** 1.6
- **Status:** Active Development ✅
- **Uptime:** 99%+ 
- **Last Updated:** February 15, 2026

---

<div align="center">

### 💙 Thank you for your interest in MCLP Discord Bot!

[![Join Discord](https://img.shields.io/badge/Join-MCLP%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/tssKYweM3h)

**Made with ❤️ in Germany 🇩🇪**

---

*This is a private, exclusive bot operated by Dennis Plischke.*  
*For inquiries, please join the MCLP Discord server or send an email.*

</div>
