# Terms of Service - MCLP Discord Bot

**Last Updated:** February 15, 2026  
**Effective Date:** January 5, 2026  
**Version:** 1.7 - Added Discord Status API, SoundCloud, scheduled reminders, updated rate limits, status cycle

---

## 1. Agreement to Terms

By adding the MCLP Discord Bot ("Bot") to your server or using its features, you agree to be bound by these Terms of Service. If you do not agree, do not use the Bot.

---

## 2. Description of Service

The Bot provides the following comprehensive features:

### 2.1 Music Features
- Play music from YouTube and SoundCloud (`!play`, `!join`, `!leave`)
- Queue management (`!queue`, `!nowplaying`)
- Playback controls (`!pause`, `!resume`, `!skip`)
- Volume and repeat control
- URL whitelist: Only YouTube (youtube.com, youtu.be) and SoundCloud (soundcloud.com) URLs accepted
- Search queries limited to 200 characters
- Requires FFMPEG and active voice connection

### 2.2 Games & Entertainment
- **Quiz:** Multiple categories, multi-language support
- **Hangman:** Word guessing game
- **Rock Paper Scissors:** `!rps` interactive game
- **Number Guess:** `!guess` the number
- **Dice Rolling:** `!roll` with custom dice

### 2.3 Utility Commands
- **Weather:** Real-time weather data (`!weather`)
- **City Info:** Geographic and timezone info (`!city`)
- **Time:** Local time for any location (`!time`)
- **Reminders:** One-time scheduled notifications (`!reminder`) with timezone support
- **Scheduled Reminders:** Recurring reminders with `every` or `daily` modes (`!scheduled-reminder`)
- **Reminder management** Delete your reminders with (`!reminders`) by choosing one in the dropdown menu.
- **Discord Status:** Live Discord API and Gateway status (`!status`)
- **Polls:** Create interactive polls (`!poll`)
- **Cat Facts:** Random cat facts (`!catfact`)
- **File Download:** `/download` specific files (admin-configured)

### 2.4 Moderation Features
- **User Management:** Kick, ban, unban
- **Timeout:** Temporary muting (`!timeout`, `!untimeout`)
- **Reaction Roles:** Auto-assign roles via reactions
- **Whitelists:** Server and global authorization lists
- **Permission System:** Global and server-specific auth

### 2.5 Science & Astronomy
- **NASA APOD:** Astronomy Picture of the Day (`!apod`)
- **Mars Photos:** Curiosity & Spirit rover images (`!marsphoto`)
- **Asteroids:** Asteroid near-Earth tracking (`!asteroids`)
- **Solar Data:** Sun activity information (`!sun`)
- **Exoplanets:** Habitable exoplanet finder (`!exoplanet`)

### 2.6 System & Admin Commands
- **Logging Control:** Configure logging channel filters (operational logging cannot be disabled)
- **Bot Status:** Set custom bot activity/status
- **Status Cycle:** Automatic rotating bot status messages (`/status_cycle`) with configurable texts, durations, and dynamic placeholders
- **Debug Mode:** Advanced debugging (owner only)
- **System Logs:** Access log files (`/log`)
- **Shutdown:** Emergency bot shutdown
- **Restart:** Restart the bot
- **Blacklist Management:** Global user and server blacklists (owner only)

### 2.7 Emergency Commands (Global Whitelist Only)
- **Emergency Lockdown** (`/emergency-lockdown`): Restrict bot to authorized users (global whitelist) only
  - Blocks ALL guild interactions
  - Only accepts commands from global whitelist users via DM
  - Changes bot status to show "🚨 Emergency Lockdown Active"
  - Used during bot attacks or abuse situations
- **Emergency Cooldown** (`/emergency-cooldown`): Activate global command cooldown
  - Sets 1-300 second cooldown across ALL commands
  - Affects all users equally (Special system commnds like `/log` are not rate-limited)
  - Used to prevent spam or abuse attacks
  - Changes bot status to show cooldown duration
- **Emergency Reset** (`/emergency-reset`): Deactivate emergency measures
  - Deactivates emergency lockdown and/or global cooldown
  - Restores bot status to normal
  - Clears persisted emergency state from config
- **Emergency Status** (`/emergency-status`): Check emergency system status
  - Shows current lockdown and cooldown state
  - Displays activation timestamps

**Emergency State Persistence:** Emergency lockdown and cooldown states are persisted in `config.json`
and automatically restored on bot restart. The emergency remains active until explicitly reset
via `/emergency-reset`.

### 2.8 Advanced Features
- **Calculator:** `!calc` with equation solving, sympy integration
- **Command Router:** Intelligent command routing
- **Rate Limiting:** Protection against abuse
- **Error Handling:** Graceful error recovery

### 2.9 Broadcast System (Optional)

The Bot includes an **optional Broadcast System** for announcing updates and changes:

**How It Works:**
- Server administrators can enable announcements via `!update-channel` command
- Stores announcement channel in server configuration (`announcements` data)
- Runs as an external tool (`tools/broadcast-system/broadcast.py`)
- Requires the bot token to operate (outside of Discord Bot)
- Sends messages to all configured announcement channels

**Configuration:**
- **Enabling:** Server admin uses `!update-channel` in desired channel
- **Storage:** Announcement channel ID stored in server config
- **Optional:** Servers can disable by not running the `!update-channel` command.
- **Data:** Uses existing server configuration architecture

**Important Notes:**
- Broadcast system is completely optional and voluntary
- Servers must explicitly enable announcements to receive broadcasts
- Bot-Owner must actively run the broadcast tool (not automatic)
- Only reaches servers that have announcements enabled
- Respects server configurations and authorization settings

**Use Cases:**
- Announcing bot updates and new features
- Communicating breaking changes or deprecations
- Notifying about scheduled maintenance
- Sharing important information with multiple servers

### 2.10 Feature Availability Disclaimer

The features listed above are provided as currently available. **Features may be added, modified, removed, or suspended at any time** without prior notice.
While we strive to maintain stability, no feature is guaranteed to remain available indefinitely. Changes may occur due to:
- Technical limitations or compatibility issues
- Third-party API changes or discontinuation
- Security or stability concerns
- Resource constraints
- Regulatory requirements

---

## 3. Use License

We grant you a limited, non-exclusive, non-transferable license to use the Bot. You agree NOT to:

- Modify, reverse-engineer, or decompile the Bot, except where explicitly permitted by applicable law (including EU Directive 2009/24/EC for interoperability)
- Use the Bot for illegal purposes
- Attempt to gain unauthorized access to systems
- Spam, flood, or abuse the Bot
- Bypass rate limits or security measures
- Use the Bot in violation of Discord's Terms of Service
- Impersonate others using the Bot
- Harass or threaten users via the Bot
- Exploit bugs or vulnerabilities
- Distribute or republish Bot code without permission

---

## 4. User Responsibilities

### 4.1 Server Administrators & Global Commands

If you add the Bot to your server, you are responsible for:

- Monitoring Bot usage on your server
- Ensuring all users follow these Terms
- Configuring moderation appropriately via whitelist/permissions
- Setting up logging channel restrictions (`/logging_channel`)
- Not using the Bot to violate Discord ToS
- Respecting rate limits and cooldowns

**Global Administrative Commands (Owner Only):**

The following commands are restricted to the bot owner (Dennis Plischke) and co-developer (Robin Stiller):
- `/shutdown` - Emergency bot shutdown
- `/restart` - Bot restart
- `/debugmode` - Activate debug logging mode
- `/log` - Access system logs
- `/logging` - Global logging configuration
- `/blacklist` - Manage global blacklists (users and servers)
- `/status_cycle` - Configure automatic status rotation
- `/emergency-lockdown` - Restrict bot to authorized users only
- `/emergency-cooldown` - Activate global command cooldown
- `/emergency-reset` - Deactivate emergency measures

These commands require server-level access and are used only for maintenance, debugging, and enforcement of these Terms.

### 4.2 All Users

All users agree to:

- Use the Bot in good faith
- Respect other users' privacy and safety
- Not engage in harassment or threats
- Comply with server rules and Discord ToS
- Report bugs responsibly (not exploit them)
- Respect rate limits and command cooldowns

---

## 5. Acceptable Use Policy

### 5.1 Prohibited Activities

You may NOT use the Bot to:

- Create or distribute malware
- Facilitate illegal activities
- Harass, bully, or threaten others
- Share illegal content (pirated music, etc.)
- Bypass security measures or rate limits
- Circumvent cooldown protections
- Engage in automated abuse (spam, flooding)
- Collect data on other users without consent
- Impersonate others
- Violate intellectual property rights
- DDoS or resource exhaustion attacks
- Share private API keys or credentials

### 5.2 Music Feature Compliance

When using music features (`!play`, `!join`, etc.):

- Only play music you have the right to
- Respect copyright restrictions
- Comply with DMCA and similar laws
- Use only in private or authorized settings
- Do NOT redistribute copyrighted music
- Do NOT use for commercial purposes
- Do NOT record and share copyrighted content
- Only YouTube and SoundCloud URLs are accepted; other platforms are blocked

**Important:** YouTube and SoundCloud music playback is subject to their respective Terms of Service.
The Bot uses `yt-dlp` to stream content. Any violations of YouTube's or SoundCloud's ToS are
your responsibility.

### 5.3 Moderation Features

Moderation commands (!kick, !ban, !timeout):

- May only be used by whitelisted administrators
- Must comply with Discord's Community Guidelines
- Abuse may result in blacklisting (see Section 6.5) or a request to remove the bot from your server
- Appeals (for global blacklist) can be submitted to bot owner

---

## 6. Logging and Monitoring

### 6.1 Automatic Logging

The Bot automatically logs two categories of data:

**Category 1: Command Execution Logging (Can be controlled)**
- Command names only (not parameters or message content)
- User IDs and Guild IDs
- Channel IDs for context
- Timestamps of all command executions
- *This can be disabled per server via `/logging off` or `/logging_channel`*

**Category 2: Operational Logging (Cannot be disabled)**
- Error messages and exceptions
- System events and warnings
- Security-related activities
- Application crashes and recovery
- *This mandatory logging ensures bot stability and security*

### 6.2 Your Consent

By using the Bot, you consent to:

**Mandatory Operational Logging** (Cannot be disabled):
- Error messages, warnings, and system events
- These are essential for bot stability and security
- Will continue to be logged regardless of `/logging` settings

**Command Execution Logging** (Can be controlled):
- Command names, User IDs, Guild IDs, Channel IDs, Timestamps
- You can control this with:
  - `/logging off` - Disables command logging for entire server
  - `/logging_channel` - Restricts command logging to specific channels only

**Important Clarification:**
- The `/logging on|off` command only affects **command execution logging**, NOT operational logging
- Errors and warnings will always be logged for security and stability
- If you disable command logging, operational logs still provide bot health monitoring

### 6.3 Debug Mode

Debug Mode (Global Whitelist Only):
- Only bot owner (Dennis Plischke) and Co-developer (Robin Stiller) can activate
- Temporarily logs message content and usernames
- Used for technical debugging and troubleshooting
- Always gets deactivated after debugging session
- Logs still deleted after 14 days
- Requires server-level access to activate

---

## 6.5 Blacklist System

### 6.5.1 Purpose

The Bot maintains global blacklists to enforce compliance with these Terms and protect service integrity:

- **User Blacklist:** Globally blocks specific user IDs from using any Bot features
- **Server Blacklist:** Globally blocks specific server IDs from using any Bot features

### 6.5.2 Blacklist Enforcement

**How Blacklists Work:**
- Blacklisted users cannot execute any Bot commands (prefix or slash)
- Blacklisted servers cannot use the Bot in any way
- Blacklist checks happen before command execution
- No commands are processed for blacklisted users/servers

**Data Storage:**
- User IDs and Server IDs in blacklists are stored in global configuration
- Stored as plaintext IDs (not usernames or server names)
- DSGVO-compliant storage (IDs only, no personal data)

### 6.5.3 Blacklist Management

**Who Can Manage Blacklists:**
- Bot owner (Dennis Plischke)
- Co-developer (Robin Stiller)

**Management Commands:**
- `/blacklist add user|server <id>` - Add to blacklist
- `/blacklist remove user|server <id>` - Remove from blacklist
- `/blacklist list user|server` - View blacklist

**Reasons for Blacklisting:**
- Violation of these Terms of Service
- Harassment or threats via Bot
- Illegal activity
- Unauthorized access attempts or hacking
- Abuse of Bot features or rate limit evasion
- Spam or DDoS attacks
- Hosting illegal content
- Other severe violations

### 6.5.4 Blacklist Appeals

Users or server administrators who believe they have been blacklisted incorrectly may appeal:

1. **Contact:** Email dennisplischke755@gmail.com with subject "Blacklist Appeal"
2. **Information:** Include User ID or Server ID, and reason for appeal
3. **Review:** Owner will review within 14 days
4. **Decision:** Appeal will be accepted or denied with explanation
5. **Removal:** If appeal approved, ID will be removed from blacklist

---

## 6.6 Rate Limiting & Cooldowns

The Bot enforces rate limits to ensure fair service:

**API Rate Limits (global, token-bucket):**
- NASA API: 5 requests/minute
- OpenWeatherMap: 10 requests/minute
- Dictionary API: 20 requests/minute
- CatFact API: 30 requests/minute
- Discord status API 30 requests/minute

**Per-User Spam Protection:**
- Maximum 15 commands per 60 seconds per user

**Command Cooldowns (per-user, per-command):**
- Calculator: 2 seconds
- Cat Fact: 3 seconds
- Weather/City: 5 seconds
- Time: 8 seconds
- RPS/Guess/Roll: 3 seconds
- Quiz: 10 seconds
- Hangman: 15 seconds
- Status: 10 seconds
- Science commands (APOD, Mars, Asteroids, Sun, Exoplanet): 5 seconds
- Music commands: 3–5 seconds (varies by command)

**Reminder Limits:**
- Maximum 25 active one-time reminders per user
- Maximum 5 active scheduled reminders per user
- Minimum scheduled reminder interval: 60 minutes

Attempting to bypass these limits may result in restrictions.

---

## 7. Intellectual Property

### 7.1 Bot Code & Features

The Bot code and features are copyrighted:
- © 2026 Dennis Plischke
- Licensed under provided license (see LICENSE.txt)
- All rights reserved

### 7.2 Your Content

You retain all rights to content you create or input through the Bot:
- Reminder text remains yours
- Server configurations remain yours
- Poll questions remain yours
- Music you request remains copyrighted by original creator

### 7.3 Third-Party Content

Content from third-party APIs remains subject to their terms:
- NASA images and data (see NASA API ToS)
- OpenWeatherMap data (see their ToS)
- YouTube content (see YouTube ToS)
- SoundCloud content (see SoundCloud ToS)
- Dictionary definitions (see respective ToS)
- Discord Status data (see Discord ToS)

---

## 8. API and Third-Party Services

The Bot uses these third-party APIs and services:

### 8.1 External APIs

| Service                     | Purpose        | ToS                   | Privacy        |
|-----------------------------|----------------|-----------------------|----------------|
| **NASA API**                | Astronomy data | nasa.gov              | See NASA       |
| **OpenWeatherMap**          | Weather/city   | openweathermap.org    | See OWM        |
| **Free Dictionary**         | Definitions    | api.dictionaryapi.dev | Open API       |
| **CatFact API**             | Cat facts      | catfact.ninja         | See site       |
| **YouTube** (via yt-dlp)    | Music playback | youtube.com           | See YouTube    |
| **SoundCloud** (via yt-dlp) | Music playback | soundcloud.com        | See SoundCloud |
| **Discord Status API**      | Service status | discord.com           | Public API     |

### 8.2 Our Responsibility

We are NOT responsible for:

- Third-party API availability or downtime
- Changes to third-party API terms or pricing
- Data breaches at third-party services
- Third-party privacy policy changes
- Quality or accuracy of third-party data

You must review each service's privacy policy and ToS independently.

---

## 9. Music Playback & Streaming

### 9.1 Copyright and Legal Compliance

The music feature allows playing music from YouTube and SoundCloud. You agree to:

- Only use music you have rights to
- Respect copyright restrictions
- Comply with DMCA and similar laws
- Use the Bot only in private or authorized settings
- Not redistribute or record content
- Not use for commercial purposes

### 9.2 Technical Requirements

Music playback requires:
- FFMPEG installed on host system
- Active voice channel connection
- Bot permissions (voice channel access, message sending)
- Stable internet connection
- YouTube/SoundCloud availability in your region

### 9.3 Service Availability

Music playback may be unavailable due to:
- YouTube/SoundCloud API changes or limitations
- Regional restrictions on YouTube/SoundCloud
- FFMPEG installation issues
- Network connectivity problems
- Service provider changes
- Bot maintenance or updates

We are not liable for music unavailability. Use at your own risk.

---

## 10. Warranty Disclaimer

### 10.1 "AS-IS" Service

The Bot is provided "AS-IS" without warranties:

- No guarantee of availability
- No guarantee of accuracy of data
- No guarantee of performance
- No guarantee of specific results
- No guarantee of uninterrupted service

### 10.2 No Liability for Damages

We are NOT liable for:

- Lost data or configurations
- Missed reminders or scheduled tasks
- Incorrect command results
- Third-party service failures
- Indirect or consequential damages
- Data loss due to server issues
- Unauthorized access or data breaches
- Loss of revenue or business interruption

---

## 11. Limitation of Liability

**Maximum Liability:**  
To the maximum extent permitted by applicable law, our total liability shall not exceed zero (0 USD).
This limitation does not apply to liabilities that cannot be limited under applicable law, including but not limited to:
- Gross negligence or wilful misconduct
- Liability for death or personal injury
- Mandatory statutory consumer rights
- Liabilities under German law (DSGVO violations, etc.)

**In summary:** You use this Bot at your own risk. We accept no liability except where required by law.

---

## 12. Termination of Service

### 12.1 We May Terminate

We reserve the right to ask you to remove the Bot or to manually block further use if:

- Servers abuse the Bot
- Users repeatedly violate these Terms
- Accounts engage in illegal activity
- Users violate Discord ToS
- Servers attempt unauthorized access

**Enforcement Mechanism:**
Automated blacklisting system is now implemented. Users and servers in violation may be added to global blacklists, resulting in immediate and complete blocking from all Bot features.

### 12.2 Immediate Termination

We may immediately request removal or apply a manual block for:
- Hacking or unauthorized access attempts
- Harassment or threats
- Illegal activity
- Severe repeated violations
- Security threats

### 12.3 Your Termination Rights

You can:
- Remove the Bot from your server at any time
- Delete your configurations
- Request data deletion (see Privacy Policy)
- Stop using the Bot without notice

**Effect of Termination:**
- Bot access ends once the bot is removed or a manual block is applied
- Server configurations are deleted
- Other server-realated data like reactionroles are deleted
- Logs follow the standard 14-day retention policy

---

## 13. Modifications to Terms

We may modify these Terms at any time. Changes become effective upon posting.

**Your Rights:**
- Continued use constitutes acceptance
- Right to stop using the Bot
- Right to request account deletion before changes apply

**Notification Methods (in order of preference):**
1. **Broadcast System:** Significant changes announced via Bot's optional Broadcast System to servers that have enabled announcements
2. **Discord:** Announcements in official MCLP Discord server
3. **GitHub:** Updates may be posted in the repository
4. **Documentation:** Check back regularly for updates in Terms/Privacy Policy

**Important Notes:**
- Significant changes will be announced using **at least one method above**
- If you have enabled announcements (`!update-channel`), you'll receive broadcasts directly
- If you haven't enabled announcements, check Discord or GitHub regularly
- Minor clarifications may be made without formal notice
- Servers without announcements enabled may not receive notifications—opt-in via `!update-channel` to stay informed

---

## 14. Disclaimer of Endorsements

The Bot is NOT:
- Affiliated with Discord Inc.
- Endorsed by Discord Inc.
- Associated with NASA, OpenWeather, YouTube, or other APIs
- Responsible for third-party content or policies

---

## 15. Governing Law and Jurisdiction

These Terms are governed by:
- **Primary Law:** German Law (Deutsches Recht)
- **Data Protection:** DSGVO (German/EU Data Protection Regulation)
- **Jurisdiction:** German courts
- **Language:** English version is official; German translation available

**For EU Users:**  
EU/DSGVO consumer protection laws apply.

**For Non-EU Users:**  
By using this Bot, you agree to be bound by German law.

---

## 16. Dispute Resolution

### 16.1 Informal Resolution (Recommended)

For disputes:
1. Contact bot owner via Discord or E-mail
2. Provide detailed description of issue
3. Allow 14 days for response
4. Attempt good-faith resolution

### 16.2 Formal Dispute Resolution

If informal resolution fails:
- German courts have jurisdiction
- Applicable law is German law
- Both parties agree to submit to jurisdiction
- Location of dispute: Germany

---

## 17. Severability

If any provision is unenforceable:
- The remaining provisions stay in full effect
- The unenforceable provision is modified minimally to be valid
- The intent and spirit of these Terms are preserved
- Courts interpret ambiguities against the drafter

---

## 18. Entire Agreement

These Terms constitute the entire agreement between you and the Bot operator regarding the Bot's use, services, and features. Any prior communications, negotiations, or understandings are completely superseded.

---

## 19. Contact Information

**For Questions About These Terms:**

- **Discord:** Message the bot owner (Dennis Plischke)
- **Server:** MCLP (MinecraftLetsPlay Discord) [Invite](https://discord.com/invite/tssKYweM3h)
- **E-Mail:** Dennisplischke755@gmail.com
- **Response Time:** 14 days

**For Data Subject Rights (DSGVO):**  
See Privacy Policy ([`PRIVACY_POLICY.md`](./PRIVACY_POLICY.md)) for detailed information.

**For Bug Reports:**  
GitHub Issues (if public repository available)

---

## Appendix A: Quick Summary - What You Can/Cannot Do

| What You CAN Do                      | What You CANNOT Do             |
|--------------------------------------|--------------------------------|
| Use Bot for fun                      | Hack or exploit                |
| Request features                     | Spam or flood                  |
| Report bugs responsibly              | Abuse rate limits              |
| Play music you own                   | Pirate copyrighted music       |
| Configure per server                 | Modify Bot code                |
| Delete your data                     | Steal other's data             |
| Request data deletion                | Circumvent operational logging |
| Use moderation tools (if authorized) | Abuse moderation commands      |
| Create polls/reminders               | Use for harassment             |
| Play games with friends              | Cheat or exploit               |
| Filter logging channels              | Disable error/warning logs     |

---

## Appendix B: Feature Comparison Table

| Feature      | Availability  | Auth      | Logging | Rate Limit       |
|--------------|---------------|-----------|---------|------------------|
| Music        | Voice channel | Anyone    | Basic   | Per-user 3-5s    |
| Games        | Any           | Anyone    | Basic   | Per-user 3-15s   |
| Weather      | Any           | Anyone    | Basic   | 10/min + 5s      |
| Status       | Any           | Anyone    | Basic   | 30/min + 10s     |
| Reminders    | Any           | Anyone    | Basic   | 25 max/user      |
| Sched. Rem.  | Any           | Anyone    | Basic   | 5 max/user       |
| Science      | Any           | Anyone    | Basic   | 5/min + 5s       |
| Moderation   | Guild         | Whitelist | Full    | None             |
| Music Server | Guild         | Owner     | Full    | None             |

---

## Appendix C: Emergency Procedures

**Bot Not Responding?**
1. Check Discord status
2. Check bot permissions
3. Wait for automatic restart
4. Contact owner if persistent

**Data Loss?**
1. Check if logs still exist (14-day window)
2. Contact owner within 14 days
3. Provide evidence and affected Guild ID

**Security Incident?**
1. Change any exposed API keys immediately
2. Contact owner via DM
3. Do not post security issues publicly

---

**Version:** 1.7
**Status:** Active  
**Language:** English (German translation available upon request)  
**Last Updated:** February 15, 2026  
**Compliance:** German Law, DSGVO, Discord ToS
