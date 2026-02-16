# 📸 Screenshots & Visual Showcase

This document provides placeholders and guidelines for adding screenshots to showcase the MCLP Discord Bot's features.

---

## 🎨 Screenshot Guidelines

When adding screenshots to this repository:

### Quality Standards
- ✅ High resolution (minimum 1920x1080 recommended)
- ✅ Clear, readable text
- ✅ Show relevant UI elements
- ✅ Use Discord's dark or light theme consistently
- ✅ Blur or remove sensitive information (user IDs, server names if needed)

### Naming Convention
- Use descriptive names: `music-play-command.png`
- Use kebab-case: `weather-command-example.png`
- Include feature name: `quiz-game-in-action.png`

---

## 📷 Needed Screenshots

### 1. Command Examples

#### Music Commands
- [ ] `!play` command showing song being added to queue
- [ ] `!queue` command showing multiple songs
- [ ] `!nowplaying` command showing current song info
- [ ] Music player in action in voice channel

**Example placeholder:**
```
[Screenshot: Music player showing queue with 3 songs]
```

#### Game Commands
- [ ] `!quiz` command with multiple choice questions
- [ ] `!hangman` game in progress
- [ ] `!rps` rock-paper-scissors game
- [ ] `!guess` number guessing game

**Example placeholder:**
```
[Screenshot: Quiz game showing question and reaction buttons]
```

#### Utility Commands
- [ ] `!weather` command showing detailed weather info
- [ ] `!city` command showing city information
- [ ] `!time` command showing time in different timezone
- [ ] `!reminder` command confirmation
- [ ] `!poll` command creating an interactive poll
- [ ] `!status` command showing Discord service status

**Example placeholder:**
```
[Screenshot: Weather command showing temperature, conditions, and forecast]
```

#### Science Commands
- [ ] `!apod` command showing NASA's Astronomy Picture of the Day
- [ ] `!marsphoto` showing Mars rover images
- [ ] `!asteroids` showing near-Earth objects
- [ ] `!exoplanet` showing habitable planet data

**Example placeholder:**
```
[Screenshot: APOD command showing beautiful space image with description]
```

#### Moderation Commands
- [ ] `!timeout` command in action
- [ ] Reaction role setup
- [ ] Permission denied message
- [ ] Logging configuration interface

**Example placeholder:**
```
[Screenshot: Moderation command showing successful timeout]
```

---

### 2. Feature Showcases

#### Permission System
- [ ] Global whitelist configuration
- [ ] Server-specific whitelist setup
- [ ] Permission hierarchy diagram
- [ ] Access denied message for unauthorized user

**Example placeholder:**
```
[Screenshot: Permission system showing different access levels]
```

#### Logging System
- [ ] Log output examples (command logging)
- [ ] Log file structure
- [ ] `/logging_channel` configuration
- [ ] Log rotation in action

**Example placeholder:**
```
[Screenshot: Logging configuration showing enabled/disabled channels]
```

#### Emergency System
- [ ] Emergency lockdown activation
- [ ] Emergency cooldown message
- [ ] Bot status during emergency
- [ ] Emergency reset confirmation

**Example placeholder:**
```
[Screenshot: Emergency lockdown message with bot status indicator]
```

#### Rate Limiting
- [ ] Rate limit exceeded message
- [ ] Cooldown remaining notification
- [ ] Normal command execution

**Example placeholder:**
```
[Screenshot: Rate limit message showing remaining cooldown time]
```

---

### 3. UI Elements

#### Help Menu
- [ ] `!help` command showing all categories
- [ ] Detailed help for specific command
- [ ] Command syntax examples

**Example placeholder:**
```
[Screenshot: Help menu with categories (Music, Games, Utility, etc.)]
```

#### Bot Information
- [ ] Bot profile/about section
- [ ] Server list showing bot presence
- [ ] Bot statistics (uptime, servers, users)

**Example placeholder:**
```
[Screenshot: Bot info showing version, uptime, and statistics]
```

#### Configuration
- [ ] Server configuration panel
- [ ] Setting up logging channels
- [ ] Music channel configuration

**Example placeholder:**
```
[Screenshot: Configuration menu with various settings]
```

---

## 🎥 Video Demonstrations

Consider creating short video clips (GIFs or MP4) for:

### Music Player Demo
- Playing a song from start to finish
- Queue management (add, skip, remove)
- Volume control demonstration

### Game Interaction
- Full quiz game round
- Hangman game completion
- Rock-paper-scissors match

### Emergency System
- Activating emergency lockdown
- Bot behavior during lockdown
- Resetting emergency state

---

## 📝 Screenshot Descriptions Template

When adding screenshots, use this template:

```markdown
### [Feature Name]

![Feature Screenshot](./screenshots/path/to/image.png)

**Command:** `!command`

**Description:**
Brief description of what this screenshot shows and why it's useful.

**Highlights:**
- ✨ Feature 1 shown in image
- ✨ Feature 2 shown in image
- ✨ Feature 3 shown in image
```

---

## 🔒 Privacy Considerations

When taking screenshots:

### DO Blur/Remove:
- ❌ Real Discord user IDs (unless public figures)
- ❌ Real server names (unless you have permission)
- ❌ Personal information in messages
- ❌ API keys or tokens
- ❌ Email addresses

### OK to Show:
- ✅ Bot's username and avatar
- ✅ Command syntax and responses
- ✅ Public information (weather, NASA images, etc.)
- ✅ Game content and quiz questions
- ✅ Bot configuration screens
- ✅ Generic feature demonstrations

---

## 📊 Screenshot Examples (Placeholders)

### Example 1: Music Command
```
┌─────────────────────────────────────────────────┐
│ MCLP Bot                                   Bot  │
├─────────────────────────────────────────────────┤
│ User: !play never gonna give you up             │
│                                                 │
│ MCLP Bot:                                       │
│ 🎵 Added to queue                               │
│ Title: Rick Astley - Never Gonna Give You Up    │
│ Duration: 3:33                                  │
│ Position in queue: #1                           │
│                                                 │
│ Now playing in Voice Channel                    │
└─────────────────────────────────────────────────┘
```

### Example 2: Weather Command
```
┌─────────────────────────────────────────────────┐
│ MCLP Bot                                   Bot  │
├─────────────────────────────────────────────────┤
│ User: !weather Berlin                           │
│                                                 │
│ MCLP Bot:                                       │
│ 🌤️ Weather in Berlin, Germany                   │
│ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│ Temperature: 18°C (feels like 17°C)             │
│ Conditions: Partly Cloudy                       │
│ Humidity: 65%                                   │
│ Wind: 12 km/h NW                                │
│ Pressure: 1013 hPa                              │
└─────────────────────────────────────────────────┘
```

### Example 3: Quiz Game
```
┌─────────────────────────────────────────────────┐
│ MCLP Bot                                   Bot  │
├─────────────────────────────────────────────────┤
│ User: !quiz                                     │
│                                                 │
│ MCLP Bot:                                       │
│ 📚 Quiz Time! Category: Science                 │
│ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│ Question: What is the speed of light?           │
│                                                 │
│ React with:                                     │
│ 🅰️ 299,792 km/s                                 │
│ 🅱️ 300,000 km/s                                 │
│ 🅲️ 150,000 km/s                                 │
│ 🅳️ 250,000 km/s                                 │
│                                                 │
│ Time remaining: 30 seconds                      │
└─────────────────────────────────────────────────┘
```

---

## 📌 Next Steps

1. Take screenshots following the guidelines above
2. Organize them in the `screenshots/` directory
3. Add them to README.md in appropriate sections
4. Update this document with actual screenshot references
5. Consider creating a video showcase/demo

---

## 🎯 Priority Screenshots

**High Priority (most impactful for users):**
1. Music player in action
2. Help menu overview
3. Quiz or Hangman game
4. Weather command result
5. NASA APOD feature

**Medium Priority:**
1. Permission configuration
2. Logging setup
3. Emergency system demo
4. Reminder creation
5. Poll creation

**Low Priority (nice to have):**
1. Configuration details
2. All individual commands
3. Error messages
4. Edge cases

---

<div align="center">

**Ready to showcase the MCLP Discord Bot! 📸**

[Back to README](./README.md) | [See Code Examples](./CODE_SNIPPETS.md)

</div>
