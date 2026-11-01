# Terms of Service - MCLP Discord Bot

**Last Updated:** November 1, 2026  
**Effective Date:** November 1, 2026  
**Version:** 2.0 - Updated MariaDB persistence, active polls, reminders, reaction roles, hosting and access limits

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
- **Game Utilities:** Additional game-focused helper tools (for example Minecraft calculations)

### 2.3 Utility Commands
- **Weather:** Real-time weather data (`!weather`)
- **City Info:** Geographic and timezone info (`!city`)
- **Time:** Local time for any location (`!time`)
- **Reminders:** One-time notifications (`!reminder`) with timezone support, stored in the production database while active
- **Scheduled Reminders:** Recurring reminders with `every` or `daily` modes (`!scheduled-reminder`)
- **Reminder management:** View and delete your reminders with `!reminders`; active reminders are restored after restart
- **Discord Status:** Live Discord API and Gateway status (`!status`)
- **Polls:** Create interactive polls (`!poll`) whose active poll data and votes are stored in the database and restored after restart; delete polls with `!deletepoll`
- **Cat Facts:** Random cat facts (`!catfact`)
- **Dog Facts:** Random dog facts (`!dogfact`)

### 2.4 Moderation Features
- **User Management:** Kick, ban, unban
- **Timeout:** Temporary muting (`!timeout`, `!untimeout`)
- **Purge:** Bulk message deletion (`!purge`)
- **Slowmode:** Enable/disable and configure channel slowmode (`!slowmode`)
- **Warnings:** `!warn` with action at three active warnings (timeout, kick, or ban), DM notice, and optional warn role; history and audit events are stored in the database
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
- **Flood Protection:** Per-guild `/flood-protection` command with configurable user/channel/guild thresholds, configurable time window, and mitigation mode (alert, cooldown, silent drop/block)
- **Bot Status:** Set custom bot activity/status
- **Status Cycle:** Automatic rotating bot status messages (`/status_cycle`) with configurable texts, durations, and dynamic placeholders
- **Debug Mode:** Debug setting managed by a globally authorized operator; It is used only in the Windows development environment
- **System Logs:** Access the latest log file (`/log`), for globally authorized operators
- **Shutdown/Restart:** Systemd service controls when a service is configured and the host permits the required command
- **Access management:** Global and guild allowlists, global blocklists, logging configuration, and emergency controls
- **Privacy information:** `/privacy`

### 2.7 Emergency Commands (Global Whitelist Only)
- **Emergency Lockdown** (`/emergency-lockdown`): Restrict bot to authorized users (global whitelist) only
  - Blocks guild messages and application-command interactions
  - Allows authorized global-whitelist users to use commands through DMs
  - Changes bot status to show "🚨 Emergency Lockdown Active"
  - Used during bot attacks or abuse situations
- **Emergency Cooldown** (`/emergency-cooldown`): Activate global command cooldown
  - Sets 1-300 second cooldown across ALL commands
  - Applies to commands according to the central cooldown check; some maintenance commands are exempt
  - Used to prevent spam or abuse attacks
  - Changes bot status to show cooldown duration
- **Emergency Reset** (`/emergency-reset`): Deactivate emergency measures
  - Deactivates emergency lockdown and/or global cooldown
  - Restores bot status to normal
  - Clears active persisted emergency state from MariaDB configuration
**Emergency State Persistence:** Active emergency settings are stored in MariaDB
and restored after restart. They remain active until reset or changed by an
authorized operator.

### 2.8 Advanced Features
- **Calculator:** `!calc` with equation solving, sympy integration
- **Command Router:** Intelligent command routing
- **Rate Limiting:** Protection against abuse
- **Error Handling:** Graceful error recovery
- **Runtime Monitoring:** Internal telemetry for uptime, latency, error trends, ...

### 2.9 Broadcast System (Optional)

The operator can run a separate, optional broadcast utility for announcements:

**How It Works:**
- Server administrators can enable announcements via `!update-channel` command
- Stores enabled state and announcement channel ID in MariaDB guild settings
- Runs as an external tool in `tools/broadcast_system/`
- Requires the bot token and database connection settings
- Sends messages to all configured announcement channels

**Configuration:**
- **Enabling:** Server admin uses `!update-channel` in desired channel
- **Storage:** Announcement channel ID and enabled state stored in MariaDB
- **Opt-out:** Only enabled guilds with a configured channel are targeted. The command enables/configures announcements; disabling requires an authorized database change.
- **Data:** Uses existing server configuration architecture

**Important Notes:**
- Broadcast system is completely optional and voluntary
- Servers must explicitly enable announcements to receive broadcasts
- Bot-Owner must actively run the broadcast tool (not automatic)
- Only reaches servers that have announcements enabled
- The tool creates local JSON reports containing an announcement preview, target IDs and send results; it does not automatically delete those reports

**Use Cases:**
- Announcing bot updates and new features
- Communicating breaking changes or deprecations
- Notifying about scheduled maintenance
- Sharing important information with multiple servers

### 2.10 Feature Availability Disclaimer

The features listed above describe the current service and may change. Subject
to applicable law and any required notice, features may be added, modified,
suspended, or discontinued.
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

**Administrative Access:**

Global administrative commands check the configured global whitelist.
Dennis Plischke and Robin Stiller are the authorized operators for production.
Guild-level commands use the configured guildauthorization list or,
for some commands, Discord administrator/server-owner
permissions. Actual access depends on the relevant command and deployment
configuration.

Global whitelist commands include:
- `/shutdown` - Emergency bot shutdown
- `/restart` - Bot restart
- `/debugmode` - Activate debug logging mode
- `/log` - Access system logs
- `/status` - Set bot activity/status
- `/logging` - Global logging configuration
- `/blacklist` - Manage global blacklists (users and servers)
- `/status_cycle` - Configure automatic status rotation
- `/emergency-lockdown` - Restrict bot to authorized users only
- `/emergency-cooldown` - Activate global command cooldown
- `/emergency-reset` - Deactivate emergency measures

These commands do not all require server-level access. Global whitelist
commands are authorized by the Bot's global configuration; guild commands use
their guild-level checks. `/logging` uses the global whitelist for global
settings and guild authorization for guild settings.

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

Moderation commands (!kick, !ban, !timeout, !warn):

- May only be used by users who pass the Bot's guild authorization checks; the required Discord permissions also depend on the action
- Must comply with Discord's Community Guidelines
- Abuse may result in blacklisting (see Section 6.5) or a request to remove the bot from your server
- A global blacklist decision can be reviewed by contacting the operator

---

## 6. Logging and Monitoring

### 6.1 Command logging and operational logs

Guild command logging can be controlled with `/logging` and
`/logging_channel`. When enabled, the Bot's ordinary guild command log records
the command token and user, guild, and channel IDs, not command arguments.
Operational logs for errors, warnings, startup/shutdown, and security issues
are separate and are not disabled by these guild settings. Operational log
records may include IDs or exception text.

The logger attempts to remove rotated log files older than 14 days. This is not
a retention promise for database records, broadcast reports, backups, console
output, or other copies. See the Privacy Policy for the current data categories
and retention behavior.

### 6.2 Debug mode

Debug mode is controlled by a globally authorized operator.
It is used only in the Windows development environment with the
development database and is not used on the production Raspberry Pi. The
software can log full guild message content and bot replies in debug mode when
guild logging is enabled. Operators must keep debug mode disabled in production.

### 6.3 Monitoring and persistence

Operational configuration, active reminders, polls and votes, reaction-role
mappings, warning records, and telemetry are persisted in the production
MariaDB database. Some runtime state, such as music queues and limiter windows,
is held in memory. Active reminders and polls are restored after restart.
Telemetry samples are pruned after seven days; other database records do not
all have automatic expiration. See the Privacy Policy for details.

Production uses a MariaDB database on a self-managed Raspberry Pi in Germany.
Database/server access is limited to Dennis Plischke and Robin Stiller
and remote access uses an encrypted Cloudflare
Tunnel. There are no database or log backups.
Details are in the Privacy Policy.

---

## 6.5 Blacklist System

### 6.5.1 Purpose

The Bot maintains global blacklists to enforce compliance with these Terms and protect service integrity:

- **User Blacklist:** Blocks listed user IDs from passing the Bot's command access checks
- **Server Blacklist:** Blocks listed guild IDs from passing the Bot's command access checks

### 6.5.2 Blacklist Enforcement

**How Blacklists Work:**
- Blacklisted users cannot execute prefix commands or application commands covered by the Bot's blacklist checks
- Blacklisted servers cannot execute commands covered by the Bot's guild blacklist checks
- Blacklist checks happen before command execution
- No commands are processed for blacklisted users/servers

**Data Storage:**
- User IDs and Server IDs in blacklists are stored in global configuration
- Stored as Discord IDs; these identifiers may be personal data
- Kept until an authorized operator removes the entry

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

Users or server administrators who believe they have been blacklisted
incorrectly may contact the operator for review:

1. **Contact:** Email dennisplischke755@gmail.com with subject "Blacklist Appeal"
2. **Information:** Include User ID or Server ID, and reason for appeal
3. **Review:** The operator will review the request
4. **Decision:** The operator will communicate the outcome where appropriate
5. **Removal:** If the appeal is accepted, the relevant entry will be removed

---

## 6.6 Rate Limiting & Cooldowns

The Bot enforces rate limits to ensure fair service:

**Default API Rate Limits (global; configuration may override defaults):**
- NASA API: 5 requests/minute
- OpenWeatherMap: 10 requests/minute
- Dictionary API: 20 requests/minute
- CatFact API: 30 requests/minute
- DogFact API: 30 requests/minute
- Discord Status API: 30 requests/minute

**Per-User Spam Protection:**
- Maximum 15 commands per 60 seconds per user

**Command Cooldowns (per-user, per-command):**
The values below are code defaults. Global cooldown settings stored in MariaDB
may override them.

- `calc`: 3 seconds
- `quiz`: 10 seconds
- `hangman`: 10 seconds
- `portal`: 3 seconds
- `ore`: 2 seconds
- `potion`: 2 seconds
- `stronghold`: 3 seconds
- `enchants`: 2 seconds
- `xp-cost`: 5 seconds
- `enchantment-order`: 10 seconds
- `weather`: 8 seconds
- `city`: 8 seconds
- `time`: 8 seconds
- `rps`: 3 seconds
- `guess`: 3 seconds
- `roll`: 3 seconds
- `apod`: 15 seconds
- `marsphoto`: 15 seconds
- `asteroids`: 15 seconds
- `sun`: 15 seconds
- `exoplanet`: 15 seconds
- `catfact`: 3 seconds
- `dogfact`: 3 seconds
- `status`: 10 seconds
- `music-channel`: 5 seconds
- `join`: 5 seconds
- `leave`: 5 seconds
- `play`: 5 seconds
- `pause`: 3 seconds
- `resume`: 3 seconds
- `skip`: 3 seconds
- `last`: 3 seconds
- `stop`: 5 seconds
- `queue`: 3 seconds
- `nowplaying`: 3 seconds
- `repeat`: 3 seconds

**Reminder Limits:**
- Maximum 25 active one-time reminders per user
- Maximum 5 active scheduled reminders per user
- Minimum scheduled reminder interval: 30 minutes

**Per-Guild Flood Protection (configurable):**
- User, channel, and guild activity thresholds
- Configurable time window for threshold evaluation
- Mitigation modes: alert, cooldown, or silent drop/block

Attempting to bypass these limits may result in restrictions.

---

## 7. Intellectual Property

### 7.1 Bot Code & Features

The Bot code and features are copyrighted:
- © 2026 Dennis Plischke
- No additional code license is granted by these Terms. This does not override permissions or exceptions required by applicable law.

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
| **DogFact API**             | Dog facts      | dogapi.dog            | See site       |
| **YouTube** (via yt-dlp)    | Music playback | youtube.com           | See YouTube    |
| **SoundCloud** (via yt-dlp) | Music playback | soundcloud.com        | See SoundCloud |
| **Discord Status API**      | Service status | discord.com           | Public API     |

### 8.2 Pterodactyl Server Panel

Pterodactyl controls apply only to guilds configured in the Bot's dedicated
server allowlist. This is limited to the operator's and
co-developer's Discord servers. Some server power commands additionally
require a globally authorized operator. When the optional chat bridge is
enabled, messages from its configured channel may be relayed to or from the
game server.

### 8.3 Cloudflare Tunnel

The production Raspberry Pi is accessed remotely through a Cloudflare Tunnel
with encrypted connections. Cloudflare may process connection/service
metadata under its own terms and privacy notice.

### 8.4 Third-Party Service Availability

The Bot operator does not control third-party services, their availability,
terms, privacy practices, or returned content. Use of a service is also
subject to that provider's terms. This section does not exclude any liability
that cannot lawfully be excluded.

### 8.5 Our Responsibility

The Bot operator cannot guarantee or control:

- Third-party API availability or downtime
- Changes to third-party API terms or pricing
- Quality or accuracy of third-party data

Review each service's terms and privacy notice independently. The Privacy
Policy lists services and describes the data sent for Bot features.

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

The operator does not guarantee uninterrupted music playback. This statement
does not exclude liability that cannot lawfully be excluded.

---

## 10. Warranty Disclaimer

### 10.1 "AS-IS" Service

The Bot is provided as available. To the extent permitted by applicable law,
the operator does not warrant:

- No guarantee of availability
- No guarantee of accuracy of data
- No guarantee of performance
- No guarantee of specific results
- No guarantee of uninterrupted service

### 10.2 No Liability for Damages

To the extent permitted by applicable law, the operator does not guarantee
against:

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

Nothing in these Terms excludes or limits liability or user rights where such
exclusion or limitation is not permitted by applicable law. Any limitation of
liability must be interpreted subject to mandatory German and EU law,
including applicable consumer-protection rules. This draft requires legal
review before publication.

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
Authorized operators can add a user or guild ID to the global blacklist. A
blacklisted user or guild is blocked by the Bot's access checks. Blacklisting is
not automatic; an operator decides whether to add an entry.

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
- Request review or deletion of data as described in the Privacy Policy
- Stop using the Bot without notice

**Effect of Termination:**
- Bot access ends once the bot is removed or a manual block is applied
- Removal does not currently cause automatic deletion of guild settings, warning/audit history, or reaction-role mappings
- Data remains subject to the retention behavior in the Privacy Policy; a separate deletion request may be needed
- Rotated application log files have an attempted 14-day cleanup; this does not cover database records or broadcast reports

---

## 13. Modifications to Terms

We may update these Terms. The updated text will show its effective date.
Changes take effect subject to applicable law and any required notice or
consent.

**Your Options:**
- You may stop using the Bot or remove it from your server
- Data requests are handled as described in the Privacy Policy

**Notification Methods (in order of preference):**
1. **Broadcast System:** Significant changes announced via Bot's optional Broadcast System to servers that have enabled announcements
2. **Discord:** Announcements in official MCLP Discord server
3. **GitHub:** Updates may be posted in the repository
4. **Documentation:** Check back regularly for updates in Terms/Privacy Policy

**Important Notes:**
- The optional broadcast tool only reaches guilds with announcements enabled and configured in MariaDB
- Broadcasts are operator-triggered, not automatic
- Other announcement methods may be used where appropriate

---

## 14. Disclaimer of Endorsements

The Bot is NOT:
- Affiliated with Discord Inc.
- Endorsed by Discord Inc.
- Associated with NASA, OpenWeather, YouTube, or other APIs
- Responsible for third-party content or policies

---

## 15. Governing Law and Jurisdiction

These Terms are intended to be governed by German law, subject to mandatory
consumer-protection rules and other mandatory law applicable to the user.
Nothing in this clause removes rights that cannot legally be waived or
restricts access to a court where applicable law provides otherwise. The
English text is the version currently provided; a translation, if made
available, does not replace mandatory rights under applicable law.

---

## 16. Dispute Resolution

### 16.1 Informal Resolution (Recommended)

For disputes:
1. Contact bot owner via Discord or E-mail
2. Provide detailed description of issue
3. Allow a reasonable time for a response
4. Attempt good-faith resolution

### 16.2 Formal Dispute Resolution

If informal resolution fails, applicable law and jurisdiction are determined
under Section 15 and any mandatory legal rules that apply.

---

## 17. Severability

If any provision is unenforceable:
- The remaining provisions stay in full effect
- The provision is applied only to the extent permitted by applicable law

---

## 18. Entire Agreement

These Terms describe the conditions for using the Bot and should be read with
the Privacy Policy and applicable Discord terms. They do not override
mandatory legal rights or separate agreements.

---

## 19. Contact Information

**For Questions About These Terms:**

- **Discord:** Message the bot owner (Dennis Plischke)
- **Server:** MCLP (MinecraftLetsPlay Discord) [Invite](https://discord.com/invite/tssKYweM3h)
- **E-Mail:** Dennisplischke755@gmail.com
Privacy requests are handled within applicable statutory time limits. Other
enquiries are answered as reasonably practicable.

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
| Request review/deletion of your data | Steal other's data             |
| Request data deletion                | Circumvent operational logging |
| Use moderation tools (if authorized) | Abuse moderation commands      |
| Create polls/reminders               | Use for harassment             |
| Play games with friends              | Cheat or exploit               |
| Filter logging channels              | Disable error/warning logs     |

---

## Appendix B: Feature Access Summary

| Feature | Access and limits | Persistence |
|---|---|---|
| Music | Guild voice channel and configured music-channel rules | Playback state is in memory; music channel setting is in MariaDB |
| Games and calculator | Commands subject to rate limits | Active game state is temporary; static game data is read-only |
| Reminders | 25 active reminders and five scheduled per user; 30-minute minimum recurrence | Active reminder records in MariaDB; restored after restart |
| Polls | 2-10 options; duration from 10 seconds to 7 days; `!deletepoll` requires Manage Messages | Active polls and votes in MariaDB; removed when closed/deleted |
| Moderation and reaction roles | Guild authorization; some actions also require Discord permissions | Warnings/audit history and mappings in MariaDB |
| Flood protection | Guild owner/admin for settings; runtime counters are transient | Settings in MariaDB; counters in memory |
| Dedicated server controls | Guild allowlist; power commands require global authorization | Allowlist in MariaDB; requests go to configured Pterodactyl server |
| Broadcast tool | Operator-triggered; only opted-in announcement guilds | Guild targets in MariaDB; local JSON result reports |

Rate limits and command cooldowns may be changed through database-backed
configuration. Default values can change between releases.

---

## Appendix C: Emergency Procedures

**Bot Not Responding?**
1. Check the [Bot status dashboard](https://rd-code-forge.net/mclp/dashboard/)
2. Check Discord status
3. Check bot permissions
4. Wait for automatic restart
5. Contact owner if persistent

**Data Loss?**
1. Production database and log files are not currently backed up
2. Contact the operator with the affected guild and feature details
3. Recovery may not be possible if the live record is lost

**Security Incident?**
1. Change any exposed API keys immediately
2. Contact owner via DM
3. Do not post security issues publicly

---

**Version:** 2.0
**Status:** Active  
**Language:** English (German translation available upon request)  
**Last Updated:** November 1, 2026
