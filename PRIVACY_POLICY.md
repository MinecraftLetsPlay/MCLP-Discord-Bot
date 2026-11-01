# Privacy Policy - MCLP Discord Bot

**Last Updated:** November 1, 2026  
**Effective Date:** November 1, 2026  
**Version:** 2.1 - Clarified production hosting, access, backups, providers, and retention

## 1. Data Controller

Dennis Plischke  
Discord Server: MCLP (MinecraftLetsPlay)  
Location: Germany; production database hosted on a self-managed Raspberry Pi at the controller's home

---

## 2. Introduction

The MCLP Discord Bot ("Bot") is a comprehensive Discord application providing:
- Music streaming and playback (YouTube, SoundCloud)
- Games and entertainment
- Game-focused utility commands
- Utility tools (weather, reminders, scheduled reminders, polls, calculator)
- Pet fact commands (cat and dog facts)
- Discord service status monitoring
- Moderation and server management
- Warning moderation with configurable follow-up actions
- Per-guild flood protection and anti-spam mitigation
- Science and astronomy data
- System administration (including status cycling)

This notice describes the data processed by the Bot, why it is processed, where it
is stored, and the known retention behavior. It is an operational description,
not a legal opinion. The controller should verify the legal bases, hosting
location, contact details, and applicable disclosure requirements before
publication.

---

## 3. What Data We Collect

### 3.1 Discord identifiers and command use

The Bot processes Discord data needed to receive and respond to commands and
events. Depending on the feature, this includes Discord user, guild, channel,
message and role IDs; command names and interaction data; and message text
supplied to a command. Discord itself also processes messages and interactions
under its own terms and privacy notice.

The Bot's ordinary guild command log records user, guild and channel IDs, the
command token, and the log timestamp, not command arguments. Guild command
logging is controlled by the guild's logging setting and channel rules. DMs are
not logged with their content; the Bot may log that a DM was received together
with the sender's ID.

### 3.2 Application and security logs

The Bot writes operational logs for startup/shutdown, errors, warnings,
permission denials, command failures, and security or flood-protection events.
Log records can include Discord IDs and exception text. Depending on the error,
text supplied to a command could appear in an exception message. The Bot does
not promise that every operational log is free of user-provided text.

Debug mode can additionally log full guild message content and bot replies when
guild logging is enabled for that message. Debug mode is controlled through the
global configuration by an authorized operator. It does not change the rule
that DM message content is not logged by the message handler.

Debug mode is used only in development with the development database
and is not used on the production Pi.

Log files are written to the global `log_file_location` directory in the
database (or the project `Logs` directory if unset). The application attempts
to delete files older than 14 days based on file modification time and does not
delete the active file. This is a log-file cleanup rule, not a deletion schedule
for database records, backups, console output, or copies outside the configured
log directory.

### 3.3 Data not intentionally collected

The Bot does not request or maintain a profile database of usernames, avatars,
email addresses, IP addresses, device identifiers, or browsing history. Discord
may expose usernames and profile data to the Bot API as part of normal Discord
objects, but the Bot's durable records principally use numeric Discord IDs.
This is not a guarantee that such information can never occur in a third-party
service or an exception/log message.

### 3.4 Global and guild configuration in MariaDB

Operational configuration is stored in MariaDB. It can include:

- Global and guild user IDs in allowlists and blocklists; guild IDs in server blocklists and dedicated-server access rules
- Guild and channel IDs for logging rules, music, announcements, and the chat bridge
- Logging preferences and channel rules
- Warning policy settings, including maximum warning count, role ID, and follow-up action
- Flood-protection thresholds, time window, and mitigation mode
- Global bot status, status-cycle text/configuration, debug/logging settings, emergency lockdown/cooldown state, and log directory
- Command cooldown and external API rate-limit settings

The Bot creates a `guild_settings` row when it sees a guild that has no row.
Configuration is intended to remain until changed or deleted. The current Bot
does not automatically delete the row when it leaves a guild; deletion must be
performed separately by an authorized operator. Static `hangman.json`, `quiz.json`, and
`game_commands_data.json` contain read-only game content. Operational bot state
is stored in MariaDB. The separate broadcast utility also writes the reports
described in Section 3.14.

### 3.5 Blacklists and emergency state

Global user and server blocklists, guild-level user lists, and dedicated-server
allowlists store Discord IDs for access control. Entries remain in MariaDB until
an authorized operator removes them; there is no automatic expiration in the
application. Production database access is limited to Dennis Plischke and Robin
Stiller as authorized administrators. Emergency state stores whether lockdown/cooldown is active, the
activating operator's ID, and the activation time so that an active measure can
be restored after restart. Resetting the emergency measure clears the active
state, not necessarily historical application log entries.

---

## 3.6 Moderation warning records

When staff use the warning features, MariaDB stores the warned user's ID,
moderator's ID, guild ID, case number, warning reason, issue time,
active/deactivated state, and deactivation time. Changes also create audit
records containing the action, actor and target IDs, related warning/case
information, and event time. The reason is free text and may contain personal
information if staff enter it.

Warnings are deactivated rather than erased when removed. The code has no
automatic retention or deletion schedule for warning history or audit records,
and leaving a guild does not delete them. Authorized moderators can manage
warning state through the Bot; database deletion is a separate operator action.

## 3.7 Blacklists and emergency state

Blacklist entries contain Discord user or guild IDs and remain until an
authorized operator removes them. Emergency configuration in MariaDB can
contain the active lockdown/cooldown flag, activating user's ID, activation
timestamp, and cooldown duration. An emergency reset changes the active
configuration; it does not erase associated application logs. Historical
blacklist or emergency records do not have an application-managed expiration.

## 3.8 Music feature data

Music queues, current playback state, track metadata used by playback, and
`!last` state are held in memory and normally disappear when the bot process
stops. The configured music channel ID is stored in the guild configuration
database. Search queries or supplied URLs are sent to YouTube/SoundCloud through
yt-dlp; those services may receive the request and the network address of the
bot host. The Bot does not maintain a durable user search-history table.

## 3.9 Per-guild flood protection

Flood-protection settings (thresholds, time window, and mitigation mode) are
stored with guild configuration in MariaDB until changed. User, channel, and
guild activity counters and temporary cooldowns are runtime state in memory.
Security telemetry stores aggregate counters; application logs may record IDs
and trigger/error details. No dedicated per-message flood-event history table
is written by the current code.

## 3.10 Reminder data

`!reminder` and `!scheduled-reminder` create rows in MariaDB. Stored fields
include the reminder ID, creator user ID, optional guild ID, destination channel
ID, creation and due timestamps, reminder text, delivery type, timezone,
recurrence type/interval, and next scheduled run. The text is user-provided and
may contain personal information.

Active reminders are restored after a bot restart. A reminder row is removed
when the reminder is cancelled with `!reminders` or the one-shot task finishes;
scheduled reminders remain and their next-run time is updated after each cycle. The code
does not define an archive or automatic cleanup period for reminders that
remain active. Limits are 25 active reminders per user, five scheduled
reminders per user, and a minimum scheduled interval of 30 minutes.

Commands issued in a guild are visible in that channel to its members. Reminder
text can also be sent by the Bot to a Discord DM or channel according to the
selected delivery type.

## 3.11 Polls and votes

An active `!poll` is stored in MariaDB with its Discord message ID, optional
guild ID, channel ID, creator ID, question, option labels/order, finite-vote
setting, duration/end time, and votes. Each vote record contains the poll
message ID, voter user ID, and selected option index. Poll questions and option
labels may contain personal information if users include it.

Polls and votes are restored after a bot restart. A user's vote can be changed
or removed unless the poll is finite. Poll data and votes are deleted when a
poll expires or is deleted with `!deletepoll`; no poll history is retained by
the application after deletion. Poll messages themselves are Discord messages
and are subject to Discord's retention and deletion controls.

## 3.12 Reaction roles

Reaction-role mappings stored in MariaDB contain guild ID, channel ID, message
ID, emoji, and role ID. The mapping remains until cleared with
`!reactionrole clear` or removed directly from the database. When a reaction is
added or removed, the Bot looks up the mapping and changes the reacting
member's role in Discord. The mapping table does not store a history of who
reacted.

## 3.13 Runtime telemetry

Telemetry is held in memory while the process runs and written about every 15
seconds to MariaDB. It includes bot instance ID, host name and optional
application version; timestamps and aggregate command/message/API/error/voice/
reconnect counts; recent command names and recent error text; latency and
response-time metrics; process memory/CPU and task counts; guild count; and
aggregate security/rate-limit counters. Current snapshots can include the last
five command names and up to five error messages (each error text is truncated
in the telemetry error collector). Telemetry does not intentionally attach a
user ID to each counter, but error strings can include IDs or other context
copied from an exception/log message. The Bot also stores Discord gateway
disconnect and reconnect timestamps to calculate availability, without linking
each outage to an individual user.

The latest snapshot and bot-instance history have no automatic deletion in the
application. Individual metric samples and completed gateway outage intervals
are automatically pruned after seven days. Aggregate counters and recent-event windows in RAM reset when the bot
restarts; the database snapshot remains until overwritten for that instance.
Dashboard responses expose only a reduced public subset; the console overlay
reads the fuller snapshot locally.

## 3.14 Broadcast reports

The separate broadcast utility writes a timestamped JSON report to
`tools/broadcast_system/logs/` after a broadcast attempt. The report contains a
timestamp, an announcement title, up to 200 characters of the announcement
text, success/failure/skipped counts, target guild and channel IDs, and error
messages for failed deliveries. The preview and error details can contain
personal information if the announcement or an error includes it. The tool has
no automatic report deletion; the controller or operator must manage retention
and protect these local files. The announcement itself is sent to the selected
Discord channels.

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
- Profiling or behavioral analysis
- Sale of personal data

Data is sent to external service providers only when a requested feature needs them, as described in Section 6.

The Bot is operated on a non-commercial basis. Data is not sold or used for
advertising.

---

## 5. Legal Basis for Data Processing (DSGVO Article 6)

The controller must identify and document the legal basis applicable to each
processing purpose. The legal bases below are provisional considerations and
have not yet been legally reviewed. The controller must confirm them before
treating this notice as final.

### Article 6(1)(b) DSGVO - Performance of a Contract

**What:** Processing necessary to provide a feature requested by a user or server, such as executing a command, delivering a reminder, or operating configured moderation features.

**Why we process:** To fulfill this contract by:
- Processing your commands
- Storing your configurations
- Executing requested actions (reminders, music, games, etc.)

**Duration:** For the time needed to provide the feature and for the retention period described in Section 5.3. Different records have different lifetimes; not all data is deleted 14 days after use.

### Article 6(1)(f) DSGVO - Legitimate Interests

**What:** The controller may rely on legitimate interests for proportionate
security and abuse prevention, service reliability, and investigating incidents,
subject to a documented balancing assessment and applicable rights to object or
restrict processing.

### What This Means for You

- Data is processed for the purposes described in this notice
- The applicable legal basis depends on the specific processing and must be confirmed by the controller
- You may exercise the rights described in Section 7, subject to applicable law

---

## 5. Data Storage and Security

### 5.1 Storage location and system

Production operational records are stored in MariaDB on a self-managed
Raspberry Pi located at the controller's home in Germany. The production
database is authoritative; production data is not copied to the development
database. The separate development database contains outdated and test data.
Production and development data must not be treated as synchronized.

Remote access to the server is through a Cloudflare Tunnel using encrypted
connections. Cloudflare may process connection or service metadata as part of
providing the tunnel; see Cloudflare's privacy information. The database is not
intended to be directly exposed to the public internet. Static game content
remains in read-only JSON files in the application repository.

### 5.2 Access and protective measures

Human administrative access to the production server and database is limited to
Dennis Plischke and Robin Stiller. The Bot connects with credentials supplied
through environment configuration. Its application account is intended to
have data read/write privileges but not schema-administration privileges.
Remote server access uses the encrypted Cloudflare Tunnel described above.
No database or log backups are currently made. Encryption at rest is not
claimed by this notice.

Data is not used for advertising or sold. Data is sent to external services when required for a requested feature; see Section 6. Those services process requests under their own terms and privacy notices.

### 5.3 Retention and deletion

The application does not apply one universal 14-day deletion period. Current behavior is:

| Data | Current storage and deletion behavior |
|---|---|
| Rotated application log files | Attempts deletion after 14 days by modification time. Active file is excluded. Console/journal copies and backups are outside this cleanup. |
| Broadcast JSON reports | Stored under `tools/broadcast_system/logs/`; no automatic deletion in the tool, unlike the main rotating log files. |
| Telemetry metric samples | Rows older than 7 days are pruned by the Bot, at most once per hour. |
| Completed gateway outage intervals | Discord disconnect/reconnect timestamps; completed intervals older than 7 days are pruned. |
| Latest snapshots and bot-instance rows | No automatic deletion schedule. A snapshot is overwritten when that instance publishes another. |
| Global/guild configuration and allow/block lists | Remain until changed or removed by an authorized operator. A guild leaving the Bot does not currently trigger deletion of its settings. |
| Warning and moderation audit records | Warning details and audit events have no automatic expiration in the application. Deactivated warnings remain in the database. |
| Reaction-role mappings | Remain until `!reactionrole clear` for the guild or a database operator removes them. |
| Reminders | Active rows remain until cancellation or task completion; recurring reminders remain active and their next-run time is updated. Both can be deleted using `!reminders`. |
| Polls, options and votes | Active records are restored after restart and deleted when the poll ends or is deleted. There is no poll history after deletion. |
| Music queues, rate-limit windows, flood counters, active minigames | Runtime memory only; normally lost when the process stops. |
| Static game JSON files | Application content, not user records; read-only and not written by the Bot. |

No production database or log backups are currently made. If backups are
introduced, they may retain records beyond deletion from the live database and
their retention should be documented.

---

## 6. Third-Party Services

The Bot uses Discord to receive messages/interactions and deliver replies,
moderation actions, roles, reminders, and poll messages. Discord processes the
relevant account, message, interaction, and server data under its own terms and
privacy notice. The Bot also sends feature-specific requests to the services
below. NASA, OpenWeatherMap, Dictionary, CatFact,
DogFact, YouTube, and SoundCloud integrations are actively used. Request
content can be personal data depending on what a user enters.

### 6.1 NASA services
- **Purpose:** Astronomy features such as `!apod`, `!marsphoto`, and `!asteroids`
- **Data Sent:** The feature's API request and configured credential. Any
    user-supplied query parameters are sent with the request. The Bot does not
    intentionally attach the user's Discord ID.
- **Privacy:** See NASA's privacy notice.

### 6.2 OpenWeatherMap
- **Purpose:** Weather and city information (`!weather`, `!city`, `!time`)
- **Data Sent:** The location text supplied to the command and API credentials. A location can reveal information about a person depending on the value entered.
- **Privacy:** See OpenWeatherMap's privacy notice.

### 6.3 Dictionary API
- **Purpose:** Word definitions used by game/utility features
- **Data Sent:** The requested word or lookup term; no Discord user ID is intentionally attached.
- **Privacy:** See the API provider's privacy information.

### 6.4 CatFact API
- **Purpose:** Generic cat facts (`!catfact`)
- **Data Sent:** A generic request; no user ID or message content is intentionally sent.
- **Privacy:** See the provider's privacy notice.

### 6.5 DogFact API
- **Purpose:** Generic dog facts (`!dogfact`)
- **Data Sent:** A generic request; no user ID or message content is intentionally sent.
- **Privacy:** See the provider's privacy notice.

### 6.6 YouTube and yt-dlp
- **Purpose:** Music search and playback (`!play` and related commands)
- **Data Sent:** Search queries, URLs, or video identifiers used to retrieve media. Requests originate from the Bot host and may expose its network address to the service.
- **Privacy:** See YouTube's privacy notice and terms.

### 6.7 SoundCloud
- **Purpose:** Music playback from SoundCloud URLs
- **Data Sent:** The supplied track URL or identifier; requests originate from the Bot host.
- **Privacy:** See SoundCloud's privacy notice and terms.

### 6.8 Discord Status API
- **Purpose:** Display public Discord service status (`!status` command)
- **Data Sent:** A generic request for public status information; no user ID or command text is intentionally attached.

### 6.9 Pterodactyl server panel
- **Purpose:** Server status/control commands and the optional Discord-to-game chat bridge
- **Access:** This integration is limited to the operator's and co-developer's Discord servers and their authorized members.
- **Data Sent:** Server-control requests and, when enabled, Discord channel messages selected for relay. Server console events can be returned to the configured Discord channel.
- **Privacy:** The panel operator/provider may process requests and network metadata under their own terms. Do not send sensitive information through a channel configured for chat relay.

### 6.10 Cloudflare Tunnel
- **Purpose:** Encrypted remote access to the self-hosted production server.
- **Data:** Cloudflare may process connection metadata to provide the tunnel.
    Bot records remain on the Pi. Confirm tunnel settings and Cloudflare's terms.

The monitoring dashboard exposes a limited status/metrics endpoint. Its public
JSON excludes user IDs, message content, detailed errors, and security details.
The local console overlay can display fuller telemetry from the database.

---

## 7. Your Rights and Requests

### Article 15: Right of Access
You have the right to know what personal data we hold about you.

**To request access:**
- Contact the controller using the contact methods below
- Identify the relevant Discord user ID and, where possible, the guild and feature involved
- The controller will respond within the period required by applicable data-protection law

### Article 16: Right to Rectification
You have the right to correct inaccurate data.

**Process:** Contact the controller with the incorrect record and requested
correction. Some records, such as a historical warning reason, may need to be
handled by the relevant guild's authorized staff.

### Article 17: Right to Erasure ("Right to be Forgotten")
You have the right to request deletion of your data.

Deletion is not automatic when a user leaves a guild or removes the Bot. The
controller can review a request and, where applicable, remove records from the
live database and configured log files. Some data can remain in backups,
Discord messages, third-party systems, or records that must be retained for a
legitimate or legal reason. Guild staff may also control their own Discord
messages and moderation decisions.

Command logging can be controlled by guild logging settings and channel rules.
Those settings do not control all operational logs or feature-required database
records. Log files have an attempted 14-day cleanup; database retention differs
by record type as described in Section 5.3.

### Restriction and objection
You may contact the controller to exercise applicable rights to restrict
processing or object. Whether a request can be granted depends on the
processing purpose and applicable law. Turning off guild command logging does
not erase existing database records or disable all operational logs.

### Article 19: Right to Data Portability
You have the right to receive your data in machine-readable format.

The Bot has no self-service data-export command. Contact the controller to
request a copy of data associated with your user ID. The response format and
scope depend on available records and applicable law.

### Article 21: Right to Object
You can object to processing based on legitimate interests. The controller
will assess the request under applicable law. Guild command-logging controls do
not disable all operational logging or feature persistence.

### To Exercise Your Rights

**Contact Method:**
- Discord DM to: Bot Owner (Dennis Plischke)
- E-Mail to: dennisplischke755@gmail.com
- Include: Your User ID, Request Type, Details

**Response Time:** Within the period required by applicable data-protection law

**Verification:** We may ask for verification that you're the User ID owner

---

## 8. Rate Limiting & Performance Protection

To prevent abuse and ensure fair service:

**API Rate Limits (global, token-bucket):**
- NASA API: 5 requests/minute
- OpenWeatherMap: 10 requests/minute
- Dictionary API: 20 requests/minute
- CatFact API: 30 requests/minute
- DogFact API: 30 requests/minute
- Discord Status API: 30 requests/minute

**Per-User Spam Protection:**
- Maximum 15 commands per 60 seconds per user

**Per-Guild Flood Protection (Configurable):**
- User/channel/guild threshold controls via `/flood-protection`
- Configurable time window for threshold evaluation
- Mitigation modes: alert, cooldown, silent drop/block

**Command Cooldowns (per-user, per-command):**
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

**DoS Protection:**
- Calculator expression length limited to 500 chars
- Expression complexity checked (max 50 operations, max 10 nesting depth)
- Timeout protection (5 seconds max)
- No recursive expression evaluation
- Music search query limited to 200 characters

---

## 9. Data Breach & Incident Response

The controller will assess and handle a suspected personal-data breach under
applicable law, including any required supervisory-authority or affected-person
notifications. This policy does not promise a particular notice channel or
timeline; notification requirements depend on the circumstances.

---

## 10. Controller & Contact

**Data Controller:**
Dennis Plischke  
Germany (controller-provided location; hosting location is described in Section 5.1 and should be confirmed for the current deployment)

**Contact Methods for Privacy Inquiries:**

You can reach out for:
- Data access requests (DSGVO Article 15)
- Deletion requests (DSGVO Article 17)
- Complaints about data processing
- General privacy questions

**Privacy contact:**
- Dennis Plischke, the controller and operator, handles access and deletion requests.

**Discord contact:**
- Direct Message to the Bot Owner through Discord
- The `/privacy` command displays a short privacy summary

**Alternative Contacts:**
- E-Mail: dennisplischke755@gmail.com
- GitHub Issues: https://github.com/MinecraftLetsPlay/MCLP-Discord-Bot/issues
- GitHub Discussions: https://github.com/MinecraftLetsPlay/MCLP-Discord-Bot/discussions
- Requests will be handled within the period required by applicable data-protection law

**Data Subject Access:**
- Include your User ID in requests
- Briefly describe what you're requesting
- We may ask for verification

Please do not send passwords, API keys, or other credentials in a privacy request. Include only the information needed to identify the relevant records.

---

## 11. Changes to This Policy

We review and update this policy:
- Every 6 months minimum
- When major features are added
- When data handling changes
- When legal requirements change

The current version and update date are shown at the top of this document.
Material changes should be communicated through an appropriate Bot or project
channel. Continued use is not a substitute for any consent or notice required
by law.

### Version History

- **v1.0** → Initial policy
- **v1.1** → Added complete feature overview, Art. 6 DSGVO basis, contact procedures (January 4, 2026)
- **v1.2** → Added more contact methods and corrected some information. Described security measures.
- **v1.3** → Clarified mandatory operational logging and summarized security measures (January 5, 2026)
- **v1.4** → Added blacklist system documentation and data processing details (January 7, 2026)
- **v1.5** → Added emergency lockdown system documentation (January 16, 2026)
- **v1.6** → Added Discord Status API, SoundCloud, scheduled reminders, reminder data/limits,
  status cycle, per-user cooldowns, emergency persistence, updated data categories (February 14, 2026)
- **v1.7** → Added DogFact API documentation, telemetry transparency, moderation/service runtime updates (June 24, 2026)
- **v1.8** → Added warning moderation (`!warn`) data handling, per-guild flood-protection data handling, and clarified in-memory `!last` track state retention (August 8, 2026)
- **v2.0** → Updated storage to MariaDB, documented durable reminders, polls/votes, reaction-role mappings, current telemetry and database retention behavior (November 1, 2026)
- **v2.1** → Added production/development separation, hosting/access details, no-backup status, active providers, and privacy contact details (November 1, 2026)

---

## Appendix A: Data categories at a glance

| Data category | Examples | Storage | Current deletion behavior |
|---|---|---|---|
| Discord identifiers | User, guild, channel, message and role IDs | MariaDB, logs, or runtime memory depending on feature | Varies by feature; see Section 5.3 |
| Command and message data | Command token, requested content, debug guild content | Logs or transient processing | 14-day log cleanup; feature data varies |
| Configuration and access lists | Settings, channel rules, user/guild IDs, emergency settings | MariaDB | Until changed/removed; no leave-guild auto-deletion |
| Moderation records | User/moderator IDs, guild, reason, case and timestamps | MariaDB | No automatic expiry in application |
| Reminders | Creator/destination IDs, text, schedule and time data | MariaDB while active | Removed on cancellation or completion; recurring items remain active |
| Polls and votes | Poll text/options, creator/voter IDs, message/channel IDs and vote index | MariaDB while active | Deleted when poll ends or is deleted |
| Reaction roles | Guild/channel/message/role IDs and emoji | MariaDB | Until cleared or deleted by database operator |
| Telemetry | Instance/host metadata, metrics, recent command names and error text | MariaDB | Samples: 7 days; current snapshot and instance history: no app-managed expiry |
| Runtime-only data | Music queue, flood counters, active games, limiter windows | Process memory | Normally lost on process stop |

---

## Appendix B: FAQ

**Q: Is operational data stored in JSON files?**
A: Bot operational state is stored in MariaDB. The Bot reads static game data
from JSON files. The separate broadcast utility writes local JSON reports,
which include an announcement preview and target IDs.

**Q: Can I opt-out of command logging?**
A: Yes. Use `/logging off` to disable command execution logging for the entire server, or `/logging_channel` to disable it for specific channels only.

**Q: Does `/logging off` disable all storage?**
A: No. It controls guild command logging. It does not disable database records required by features, moderation, telemetry, or operational error logging.

**Q: How do I request access or deletion?**
A: Contact the controller using Section 10. The Bot has no self-service export. Deletion is reviewed by the controller; there is no universal 14-day deletion of all records.

**Q: Is my music history logged?**
A: No. Music playback doesn't create command logs. Only operational logs (errors/warnings) apply. Music queue data is stored in-memory only and lost on restart.

**Q: What data is processed by `!warn`?**
A: Moderation metadata such as warned user ID, moderator ID, warning counter/state, and configured follow-up action/role state. It is used for moderation enforcement.

**Q: What data is processed by `/flood-protection`?**
A: Runtime activity counters (user/channel/guild) and configured thresholds/time window/mitigation mode. Counters are transient in-memory data.

**Q: Are reminders stored after a restart?**
A: Yes. Active reminders are stored in MariaDB and restored after restart.
One-time reminders are removed after the task completes or is cancelled;
scheduled reminders remain active until cancelled.

**Q: Does leaving a server delete its configuration or moderation records?**
A: Not automatically in the current implementation. Contact the controller.
The request will be assessed for the relevant record.

**Q: Can I be blacklisted?**
A: Yes. A blacklist entry stores a Discord user ID, which can be personal data.
Contact the controller to request review of an entry.

**Q: What data is stored if I'm blacklisted?**
A: The blacklist stores your Discord user ID, not a username or email address.

**Q: Who manages the blacklist?**
A: Authorized Bot operators manage global lists. Guild-level lists and settings are managed through the Bot's permission checks by authorized server users.

**Q: Does telemetry contain only anonymous aggregates?**
A: No. Most metrics are aggregate, but snapshots contain recent command names
and error text that may include identifiers or context. The dashboard exposes
a reduced subset; the local console view is more detailed.

---

**Version:** 2.1
**Status:** Active  
**Language:** English (German equivalent available upon request)  
**Last Updated:** November 1, 2026
