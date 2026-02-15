# MCLP Discord Bot

A **feature-rich** Discord bot built with [Discord.py](https://discordpy.readthedocs.io/en/stable/), providing  
Moderation tools, Minigames, Utility commands, and more!  
Designed for **private server use** with sophisticated permission handling and logging.  

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

- Music streaming from YouTube
- Text-based minigames (Quiz, Hangman, RPS, Number Guess)
- Utility commands (Weather, Time, Reminders, Polls)
- Moderation tools (Kick, Ban, Timeout, Reaction Roles)
- Science & Astronomy features (NASA APOD, Mars Photos, Asteroids, Exoplanets)
- Advanced calculator with equation solving
- Permission system with global and server-specific whitelists
- Global user and server blacklist system with enforcement
- Comprehensive logging system with rotation
- Status rotation enables different status messages and durations
- Emergency-measures system (Global cooldown / bot lockdown)
- DSGVO/GDPR compliant data handling
- Rate limiting and cooldowns  
- **Optional Broadcast System** for announcements and updates

---

## Tech Stack

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

- **Raspberry Pi 5 B** - Quad-Core 64-Bit 2.4 GHz CPU, 8 GB LPDDR4X RAM
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

## Legal & Compliance

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

## Setup

**Important!**
See [`requirements.txt`](./requirements.txt) for full dependencies.

---

## License

**Private License** - All rights reserved.
Permission is granted to view the source code for **personal reference and educational purposes only**.
Any other use (copy, modify, distribute, commercial) requires prior written consent.

See [`license.txt`](./license.txt)

---

## Changelog

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

## Previous Features (v1.4)

- Added optional Broadcast System for announcements and updates
- New command `!update-channel` to enable announcements in a channel
- Broadcast tool (`tools/broadcast-system/`) with message loading and delivery
- Configuration stored in server configs (`announcements` setting)
- Detailed error messages for missing announcement files
- Updated Terms of Service to document Broadcast System
- Updated documentation regarding notification methods

---

## Contact & Support

For privacy-related inquiries or legal questions:
- Email: dennisplischke755@gmail.com
- Discord: @MinecraftLetsPlay2912

For bug reports:
- GitHub Issues (if public repository)  

---

## Authors

- Owner and main developer: Dennis Plischke
- Co-Developer and team member: Robin Stiller
