# Privacy Policy - MCLP Discord Bot

**Last Updated:** February 15, 2026  
**Effective Date:** January 5, 2026  
**Version:** 1.6 - Added Discord Status API, scheduled reminders, SoundCloud, updated rate limits, emergency persistence

## 1. Data Controller

Dennis Plischke  
Discord Server: MCLP (MinecraftLetsPlay)  
Location: Germany 🇩🇪

---

## 2. Introduction

The MCLP Discord Bot ("Bot") is a comprehensive Discord application providing:
- Music streaming and playback (YouTube, SoundCloud)
- Games and entertainment
- Utility tools (weather, reminders, scheduled reminders, polls, downloads)
- Discord service status monitoring
- Moderation and server management
- Science and astronomy data
- System administration (including status cycling)

This privacy policy explains how we collect, use, store, and protect your data under DSGVO/GDPR compliance.

---

## 3. What Data We Collect

### 3.1 Command Execution Logging (Controllable)

When you use the Bot, we optionally collect command execution data:

- **User IDs** (Discord unique identifier, NOT your username)
- **Guild IDs** (Server identifiers)
- **Channel IDs** (Channel identifiers)
- **Command Names** (Which commands executed, NOT parameters)
- **Timestamps** (When commands were executed)

**Example:** When you type `!weather London`:
- Logged: User ID, Guild ID, Channel ID, Command "!weather"
- NOT Logged: "London" or any message content

**Control:** You can disable this via `/logging off` (entire server) or `/logging_channel` (specific channels only)

### 3.2 Operational Logging (Mandatory - Cannot be disabled)

The Bot always logs for security and stability purposes:

- **Error Messages** (For debugging and monitoring purposes)
- **System Events** (Bot startup, shutdown, crashes)
- **Security Events** (Permission denials, abuse attempts)
- **Warnings and Exceptions** (Application issues)

These cannot be disabled while using the bot. They are essential for:
- Detecting bugs and fixing issues
- Preventing abuse and attacks
- Monitoring bot health and uptime

**Storage Duration:** 14 days (same as command execution logs)

### 3.3 Data We Do NOT Collect (Standard Mode)

The Bot **explicitly does NOT** collect or log:

- Your username or display name
- Your avatar or profile picture
- Message content from Direct Messages (DMs)
- Message content from server channels
- Email addresses or personal information
- IP addresses or device information
- Location data
- Browsing history or metadata

### 3.4 Special Mode: Debug Logging

When Debug Mode is activated (Global Whitelist Only):

**Who can activate:** Bot owner (Dennis Plischke) and Co-developer (Robin Stiller)

**What gets logged additionally:**
- Full message content (including text)
- Usernames (NOT user IDs, actual names)
- Detailed parameter values
- Command arguments

**Important Disclaimers:**
- Debug Mode is temporary and intended for technical troubleshooting
- Debug logs are deleted after 14 days (same as normal logs)
- Only used in controlled environment
- Gets disabled after debugging

### 3.4 Configuration Data Stored

The Bot stores local configuration files:

**Global Configuration (config.json):**
- Debug Mode status
- Bot status and activity
- Status cycle configuration (status texts, durations)
- Global whitelist (User IDs)
- Global blacklist (User IDs) - for enforcement purposes
- Global server blacklist (Server IDs) - for enforcement purposes
- Download folder paths
- Log file location
- Logging activation status
- Command cooldown values (per-user, per-command)
- Emergency state (lockdown/cooldown persistence across restarts)

**Blacklist Data Details:**
- User blacklist: Discord User IDs (numeric identifiers)
- Server blacklist: Discord Server IDs (numeric identifiers)
- No personal information (usernames, emails, etc.) is stored in blacklists
- Blacklist entries are stored purely for enforcement of Terms of Service
- Management: Owner and Co-developer only
- Purpose: Prevent abuse and enforce compliance with Terms of Service

**Server-Specific Configuration (per_guild/{guild_id}.json):**
- Server whitelist (User IDs)
- Logging settings (enabled/disabled)
- Enabled/disabled logging channels
- Rules channel name
- Music channel ID
- Announcement/update channel ID
- Repeat mode settings
- Server-specific bot settings

**Special Data Files:**
- `reactionrole.json` - Message IDs, Channel IDs, Role IDs for reaction roles
- `hangman.json` - Word lists for hangman game
- `quiz.json` - Quiz questions and answers

**None of these files contain personal message content or usernames.**

---

## 3.6 Blacklist Data Processing

### 3.6.1 What Blacklist Data Is Collected

The Bot stores User IDs and Server IDs in global blacklists for enforcement purposes:

**User Blacklist:**
- Discord User IDs (numeric identifiers only)
- No username, email, or personal information

**Server Blacklist:**
- Discord Server IDs (numeric identifiers only)
- No server name or other identifying information

### 3.6.2 Why Blacklist Data Is Collected

Blacklists are maintained to:
- Enforce compliance with Terms of Service
- Prevent abuse and protect service integrity
- Block users/servers that violate Terms
- Protect other users from harassment or threats
- Prevent hacking attempts or unauthorized access

### 3.6.3 Who Manages Blacklists

- **Bot Owner:** Dennis Plischke
- **Co-developer:** Robin Stiller

Only these two individuals can add/remove IDs from blacklists.

### 3.6.4 Blacklist Retention

- Blacklist data is retained indefinitely until manually removed
- Users and servers can appeal blacklist status
- See Terms of Service Section 6.5.4 for appeal process
- Upon successful appeal, ID is removed from blacklist

### 3.6.5 Blacklist Legal Basis (DSGVO Article 6(1)(f))

**Legitimate Interest:**
The Bot operator has a legitimate interest in maintaining blacklists because:
- Protects service integrity and availability
- Prevents abuse, spam, and harassment
- Protects other users from harm
- Necessary for security and enforcement

**No Override of User Rights:**
- Blacklist data is minimal (IDs only)
- No profiling or decision-making based on behavior (only enforcement)
- Users can request erasure (right to be forgotten) - see Section 7, Article 17

### 3.7 Emergency System Data

When emergency lockdown mode or emergency cooldown mode is activated via `/emergency-lockdown` or `/emergency-cooldown`, the Bot stores:

**Data Stored:**
- User ID of the person who activated the measure
- Timestamp of when the measure was activated
- Status of the measure (active/inactive)
- Bot activity status changes

**What Gets Logged:**
- Critical log entry like: "EMERGENCY LOCKDOWN activated by {user_id}"
- All blocked interactions during lockdown (UserID)
- All blocked interactions during cooldown (UserID)
- Authorization checks (failed/successful)

**Duration:**
- Lockdown or Cooldown data is **persisted in config.json** and survives bot restarts
- Emergency state remains active until `/emergency-reset` is executed
- Log entries retained for 14 days (same as other operational logs)

**Purpose:**
- Security measure against spam attacks or abuse
- Temporary restriction of bot functionality
- Audit trail for emergency measures
- Automatic reset capability

**Legal Basis (DSGVO Article 6(1)(f)):**
- Legitimate interest in service protection
- Prevents abuse and protects other users
- Minimal data collection (IDs only)
- Temporary and reversible measure

### 3.8 Music Feature Data

When using music commands (!play, !pause, etc.):

**What we store (in-memory only, lost on restart):**
- YouTube/SoundCloud video IDs (from search)
- Video titles and durations
- Queue order

**What we don't store:**
- Your search history
- Your listening preferences
- Personal recommendations

**URL Restrictions:**
- Only YouTube (youtube.com, youtu.be) and SoundCloud (soundcloud.com) URLs are accepted
- Non-URL text is treated as a YouTube search query
- Search queries are limited to 200 characters

**External Services (yt-dlp/YouTube/SoundCloud):**
- The Bot uses `yt-dlp` to query YouTube and SoundCloud
- YouTube/SoundCloud receives your search query
- Your IP may be visible to YouTube/SoundCloud
- See YouTube's and SoundCloud's Privacy Policies for their practices

### 3.9 Reminder Data

When using `!reminder` or `!scheduled-reminder`:

**What we store (in-memory only, lost on restart):**
- Reminder text (your message)
- Target channel or DM preference
- Timezone information
- Scheduled interval and next execution time (for scheduled reminders)
- User ID of the creator

**Limits:**
- Maximum 25 active one-time reminders per user
- Maximum 5 active scheduled reminders per user
- Minimum interval for scheduled reminders: 60 minutes

**Important:** All reminder data is stored **in-memory only** and is **lost when the bot restarts**. No reminder content is written to disk or logged.

**Important:** If you value privacy, reminder commands should be used in DM (Direct Message) context.
When used in a server text channel, both your command (including the reminder text) and the bot's response are visible to all members of that channel.

### 3.10 Discord Status Data

When using the `!status` command:

**What we do:**
- Query the public Discord Status API (`status.discord.com/api/v2/summary.json`)
- Display Discord API and Gateway component status
- Show bot uptime, ping, and server/user counts

**What we send to Discord Status API:**
- No personal data is sent
- Only a generic HTTP GET request

**What we don't store:**
- No status query history
- No user-specific status data

---

## 4. How We Use Your Data

Your data is used only for:

- Executing commands you request
- System logging and error tracking
- Improving bot stability and performance
- Security and moderation (preventing abuse/spam)
- Debugging technical issues (Debug Mode only)
- Reaction role assignments

Your data is **NOT** used for:

- Marketing or advertising
- Third-party sharing
- Profiling or behavioral analysis
- Commercial purposes
- Selling or trading with other services

---

## 5. Legal Basis for Data Processing (DSGVO Article 6)

Under German and EU data protection law (DSGVO), we can only process your personal data if we have a legal basis. Here are ours:

### Article 6(1)(b) DSGVO - Performance of a Contract

**What:** When you use the Bot, you enter an implicit contract.

**Why we process:** To fulfill this contract by:
- Processing your commands
- Storing your configurations
- Executing requested actions (reminders, music, games, etc.)

**Duration:** As long as you use the Bot and for 14 days after

### Article 6(1)(f) DSGVO - Legitimate Interests

**What:** We have a legitimate interest in:
- Security and abuse prevention (blocking hackers, spam bots)
- System stability (monitoring errors, performance)
- Legal compliance (documenting usage for disputes)
- Service improvement (understanding which features work)

**Why this is legitimate:** Your interests don't override ours because:
- We don't profile or make decisions about you
- We only store anonymous command names and IDs
- We delete data after 14 days
- We don't use data for marketing or targeting

**Your right:** You can object to this processing (see Article 21 in Section 7), but operational logging cannot be disabled while using the bot.

### What This Means for You

- We have legal permission to log your commands
- We have legal permission to detect abuse
- We cannot use this data for purposes beyond what's stated
- You have rights to object, access, or delete your data

---

## 5. Data Storage and Security

### 5.1 Storage Location

- Stored on a self-hosted server located in Germany 🇩🇪
- Data is kept in local JSON files (no cloud sync)
- Access is limited to the bot owner and co-developer

### 5.2 Protective Measures (Summary)

We protect the server with layered controls (network hardening, restricted accounts, and process isolation). We avoid publishing exact configurations to reduce attack surface.
Data is never shared with third parties, and remote access is encrypted.

### 5.3 Data Retention Schedule

**Automatic Deletion (14 Days):**
- All command logs deleted after 14 days
- Debug logs deleted after 14 days
- Old rotation logs purged automatically

**Configuration Data Retention:**
- Server configs kept while the bot is in the server (removed when the server removes the bot or upon owner request)
- Reaction role data kept until manually removed
- Quiz/Hangman data kept for game functionality

---

## 6. Third-Party Services

The Bot integrates with these external APIs:

### 6.1 NASA API
- **Purpose:** Astronomy features (!apod, !marsphoto, !asteroids, !sun, !exoplanet)
- **Data Sent:** Only API key (no personal data)
- **Rate Limit:** 5 requests/minute
- **Privacy:** See NASA's privacy policy

### 6.2 OpenWeatherMap API
- **Purpose:** Weather and city information (!weather, !city, !time)
- **Data Sent:** Location name only (no personal data)
- **Rate Limit:** 10 requests/minute
- **Privacy:** See OpenWeatherMap's privacy policy

### 6.3 Dictionary API (Free Dictionary)
- **Purpose:** Word definitions
- **Data Sent:** Word to define only
- **Rate Limit:** 20 requests/minute
- **Privacy:** API is open and free

### 6.4 CatFact API
- **Purpose:** Random cat facts (!catfact)
- **Data Sent:** None (generic request)
- **Rate Limit:** 30 requests/minute
- **Privacy:** See catfact.ninja privacy policy

### 6.5 YouTube/yt-dlp (Music Feature)
- **Purpose:** Music streaming and playback (!play, !join, etc.)
- **Data Sent:** Search queries, video IDs
- **Privacy:** YouTube can see your searches
- **Note:** Uses yt-dlp library (open source alternative)
- **Compliance:** Your responsibility to respect YouTube ToS

### 6.6 SoundCloud (Music Feature)
- **Purpose:** Music streaming and playback via `!play` with SoundCloud URLs
- **Data Sent:** Track URLs
- **Privacy:** SoundCloud can see your requests
- **Note:** Uses yt-dlp library for extraction
- **Compliance:** Your responsibility to respect SoundCloud ToS

### 6.7 Discord Status API
- **Purpose:** Display Discord service status (`!status` command)
- **Data Sent:** None (generic GET request to public API)
- **URL:** `https://status.discord.com/api/v2/summary.json`
- **Rate Limit:** 10-second command cooldown per user
- **Privacy:** No personal data transmitted; public API

---

## 7. Your Rights (DSGVO Articles 15-22)

### Article 15: Right of Access
You have the right to know what personal data we hold about you.

**To request:**
- Contact bot owner via Discord
- Alternative: E-Mail to: dennisplischke755@gmail.com
- Provide your User ID
- Will receive data within 30 days

### Article 16: Right to Rectification
You have the right to correct inaccurate data.

**Process:**
- Limited applicability (we only store IDs and commands)
- Contact bot owner for corrections

### Article 17: Right to Erasure ("Right to be Forgotten")
You have the right to request deletion of your data.

**What gets deleted:**
- All log entries mentioning your User ID
- Your server whitelists/configurations

**What doesn't get deleted:**
- Quiz answers already submitted (game functionality)
- Reaction role assignments (unless you leave server)
- Votes (You can simply revoke your vote when the poll is active)

**Timeframe:** 7 days of request

### Important Note: Mandatory Operational Logging vs. Controllable Command Logging

**Mandatory Operational Logging (Cannot be disabled):**
- Error messages, warnings, system events
- Essential for bot security and stability
- Continues regardless of `/logging` settings
- Retention: 14 days

**Controllable Command Execution Logging (Can be disabled):**
- User IDs, Guild IDs, Channel IDs, command names, timestamps
- Disabled via `/logging off` (entire server) or `/logging_channel` (specific channels)
- Retention: 14 days (if enabled)

**If you do not consent to mandatory operational logging,** please stop using the bot or remove it from your server.

### Article 18: Right to Restrict Processing
Because operational logging is required for the bot to function and for security purposes, we cannot disable it while keeping the bot usable.
You can restrict processing by discontinuing use or removing the bot from your server.

### Article 19: Right to Data Portability
You have the right to receive your data in machine-readable format.

**Available as:**
- JSON export of your configs
- Text file of your command history

### Article 21: Right to Object
Operational logging cannot be switched off for individual users or servers. If you object to this processing, the practical remedy is to stop using the bot or remove it from your server.

### To Exercise Your Rights

**Contact Method:**
- Discord DM to: Bot Owner (Dennis Plischke)
- E-Mail to: dennisplischke755@gmail.com
- Include: Your User ID, Request Type, Details

**Response Time:** Within 30 days of request (DSGVO requirement)

**Verification:** We may ask for verification that you're the User ID owner

---

## 8. Rate Limiting & Performance Protection

To prevent abuse and ensure fair service:

**API Rate Limits (global, token-bucket):**
- NASA API: 5 requests/minute
- OpenWeatherMap: 10 requests/minute
- Dictionary API: 20 requests/minute
- CatFact API: 30 requests/minute

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

**DoS Protection:**
- Calculator expression length limited to 500 chars
- Expression complexity checked (max 50 operations, max 10 nesting depth)
- Timeout protection (5 seconds max)
- No recursive expression evaluation
- Music search query limited to 200 characters

---

## 9. Data Breach & Incident Response

### Notification Process

In the unlikely event of a security incident:

1. **Immediate Actions:**
   - Isolate affected systems
   - Determine scope of breach
   - Begin investigation

2. **User Notification:**
   - Users affected will be notified via Discord
   - Notification within 72 hours of discovery
   - Details of what data was exposed

3. **Authorities:**
   - German data protection authorities informed if required
   - Documentation maintained for regulatory review

### Historical Security

As of February 2026: No security breaches reported

---

## 10. Data Protection Officer & Contact

**Data Controller:**
Dennis Plischke  
Germany 🇩🇪

**Contact Methods for Privacy Inquiries:**

You can reach out for:
- Data access requests (DSGVO Article 15)
- Deletion requests (DSGVO Article 17)
- Complaints about data processing
- General privacy questions

**Primary Contact (Discord):**
- Discord Username: @MinecraftLetsPlay2912
- Type `/dsgvo` in-bot for privacy information
- Direct Message to bot owner

**Alternative Contacts:**
- E-Mail: dennisplischke755@gmail.com
- GitHub Issues: https://github.com/MinecraftLetsPlay/Discord-Bot/issues
- GitHub Discussion: https://github.com/MinecraftLetsPlay/Discord-Bot/discussions
- Response time: Within 30 days (DSGVO legal requirement)

**Data Subject Access:**
- Include your User ID in requests
- Briefly describe what you're requesting
- We may ask for verification

**Important:** This is a hobby bot run by one person. While we respond as quickly as possible, allow up to 14 days for processing during busy times.

---

## 11. Changes to This Policy

We review and update this policy:
- Every 6 months minimum
- When major features are added
- When data handling changes
- When legal requirements change

### How You'll Be Notified

**Major Changes** (Significant changes to your rights or data handling):
- Will be announced on the Bot's GitHub page.
- Posted in MCLP server announcements
- Effective after 30 days notice

**Minor Changes** (Clarifications, formatting, minor additions):
- Updated on GitHub without advance notice
- Effective immediately

### Your Rights When We Change Terms

- Right to withdraw consent and stop using Bot
- Right to request deletion of data before accepting changes
- Continued use of Bot = acceptance of new policy
- Right to review version history (GitHub)

### Version History

- **v1.0** → Initial policy
- **v1.1** → Added complete feature overview, Art. 6 DSGVO basis, contact procedures (January 4, 2026)
- **v1.2** → Added more contact methods and corrected some information. Described security measures.
- **v1.3** → Clarified mandatory operational logging and summarized security measures (January 5, 2026)
- **v1.4** → Added blacklist system documentation and data processing details (January 7, 2026)
- **v1.5** → Added emergency lockdown system documentation (January 16, 2026)
- **v1.6** → Added Discord Status API, SoundCloud, scheduled reminders, reminder data/limits,
  status cycle, per-user cooldowns, emergency persistence, updated data categories (February 14, 2026)

---

## Appendix A: Complete Data Categories

| Data Type          | Collected | Command Logging | Operational Logging | Retention      | Purpose                   |
|--------------------|-----------|-----------------|---------------------|----------------|---------------------------|
| User ID            |    YES    |  YES (control)  |     YES (always)    |    14 days     | Command tracking          |
| Guild ID           |    YES    |  YES (control)  |     YES (always)    |    14 days     | Server identification     |
| Channel ID         |    YES    |  YES (control)  |     Limited         |    14 days     | Context for logs          |
| Command Name       |    YES    |  YES (control)  |        NO           |    14 days     | Usage tracking            |
| Timestamps         |    YES    |  YES (control)  |     YES (always)    |    14 days     | When events occurred      |
| Error Messages     |    NO     |       NO        |     YES (always)    |    14 days     | Bot stability             |
| Warnings/Events    |    NO     |       NO        |     YES (always)    |    14 days     | Security monitoring       |
| Username           |    NO     | NO (debug: YES) |    NO (debug: YES)  |    14 days     | Usage tracking / Security |
| Command Args       |    NO     | NO (debug: YES) |    NO (debug: YES)  |    14 days     | Usage tracking / Security |
| Message Content    |    NO     | NO (debug: YES) |    NO (debug: YES)  |    14 days     | Usage tracking / Security |
| DM Content         |    NO     |       NO        |        NO           |      N/A       | Never logged              |
| Config Data        |    YES    |       NO        |        NO           | Until deletion | Server/User settings      |
| Emergency State    |    YES    |       NO        |   YES (activated)   |  Until reset   | Security enforcement      |
| Reminder Data      | In-memory |       NO        |        NO           | Until restart  | Command execution         |
| Music Queue        | In-memory |       NO        |        NO           | Until restart  | Playback functionality    |
| Status Cycle Config|    YES    |       NO        |        NO           | Until deletion | Bot status rotation       |
| Blacklist User ID  |    YES    |       NO        |        NO           |  Until appeal  | Enforcement of ToS        |
| Blacklist Server ID|    YES    |       NO        |        NO           |  Until appeal  | Enforcement of ToS        |

**Legend:**
- **Command Logging (Control)**: Can be disabled with `/logging off` or `/logging_channel`
- **Operational Logging (Always)**: Cannot be disabled - essential for security and stability
- **Debug: YES**: Only logged when Debug Mode is active (owner/co-dev only)

---

## Appendix B: FAQ

**Q: Do you sell my data?**
A: Absolutely not. We have no commercial use for your data.

**Q: Can I opt-out of command logging?**
A: Yes. Use `/logging off` to disable command execution logging for the entire server, or `/logging_channel` to disable it for specific channels only.

**Q: Can I opt-out of operational logging (errors, warnings)?**
A: No. Operational logging (errors, warnings, security events) is mandatory and cannot be disabled. If you disagree, remove the bot or stop using it.

**Q: How do I delete my data?**
A: Submit a data deletion request to the bot owner. Command logs are automatically deleted after 14 days.

**Q: Is my music history logged?**
A: No. Music playback doesn't create command logs. Only operational logs (errors/warnings) apply. Music queue data is stored in-memory only and lost on restart.

**Q: Are my reminders stored permanently?**
A: No. All reminder data (one-time and scheduled) is stored in-memory only. It is lost when the bot restarts. No reminder content is written to disk or logged.

**Q: What if I disagree with this policy?**
A: You can stop using the Bot anytime. Your data will be deleted after 14 days (automatically).

**Q: Can I be blacklisted?**
A: Yes, if you violate the Terms of Service. Blacklisting blocks you from all Bot features. You can appeal via email to dennisplischke755@gmail.com.

**Q: What data is stored if I'm blacklisted?**
A: Only your User ID (numeric identifier). No personal information like username or email is stored in the blacklist.

**Q: Who manages the blacklist?**
A: Only the bot owner (Dennis Plischke) and co-developer (Robin Stiller) can add/remove users or servers from blacklists.

---

**Version:** 1.6
**Status:** Active  
**Language:** English (German equivalent available upon request)  
**Last Updated:** February 15, 2026  
**Compliance:** DSGVO/GDPR Article 13 & 14
