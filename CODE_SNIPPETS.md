# 🔧 Code Examples & Architecture

This document showcases the architecture, design patterns, and code examples that power the MCLP Discord Bot.

> **Note:** The actual bot source code is private. The examples below are illustrative and demonstrate the general patterns and approaches used in the bot's development.

---

## 📁 Architecture Overview

### Project Structure

```
Discord-Bot/
├── main.py                      # Entry point
├── bot.py                       # Bot initialization and event handling
├── command_router.py            # Intelligent command routing
├── command_modules/
│   ├── moderation_commands.py   # Kick, ban, timeout
│   ├── minigames.py             # Games: Quiz, Hangman, RPS
│   ├── utility_commands.py      # Weather, time, reminders
│   ├── public_commands.py       # Help, info, serverinfo
│   ├── system_commands.py       # Admin controls
│   ├── calculator.py            # Advanced calculator
│   ├── scientific_commands.py   # NASA APIs
│   └── music/
│       ├── music_commands.py    # Music control commands
│       └── player.py            # Music player logic
├── utils.py                     # Helper functions
├── logging_setup.py             # Advanced logging
├── status_cycle.py              # Status rotation
├── rate_limiter.py              # Rate limiting system
└── config/                      # Configuration files
    ├── config.json              # Global configuration
    └── per_guild/               # Per-server configs
        └── {guild_id}.json
```

---

## 🎯 Design Patterns

### 1. Command Router Pattern

The bot uses a centralized command routing system for efficient command handling:

```python
# Simplified example of the command routing approach
class CommandRouter:
    def __init__(self):
        self.commands = {}
        self.prefix = "!"
    
    def register(self, name, handler, aliases=None):
        """Register a command with its handler"""
        self.commands[name] = handler
        if aliases:
            for alias in aliases:
                self.commands[alias] = handler
    
    async def route(self, message):
        """Route commands to appropriate handlers"""
        if not message.content.startswith(self.prefix):
            return
        
        # Extract command name
        parts = message.content[len(self.prefix):].split()
        command_name = parts[0].lower()
        
        # Find and execute handler
        handler = self.commands.get(command_name)
        if handler:
            await handler(message, parts[1:])
```

**Benefits:**
- ✅ Centralized command management
- ✅ Easy to add new commands
- ✅ Support for command aliases
- ✅ Consistent error handling

---

### 2. Rate Limiting System

Token bucket algorithm for rate limiting:

```python
# Simplified rate limiting example
class RateLimiter:
    def __init__(self):
        self.user_buckets = {}
        self.command_cooldowns = {}
    
    def check_rate_limit(self, user_id, command):
        """Check if user can execute command"""
        # Check per-user global limit (15 commands/60s)
        user_bucket = self.user_buckets.get(user_id, {
            'tokens': 15,
            'last_update': time.time()
        })
        
        # Refill tokens based on time passed
        now = time.time()
        elapsed = now - user_bucket['last_update']
        refill = (elapsed / 60.0) * 15
        user_bucket['tokens'] = min(15, user_bucket['tokens'] + refill)
        user_bucket['last_update'] = now
        
        # Check if user has tokens
        if user_bucket['tokens'] < 1:
            return False, "Rate limit exceeded"
        
        # Check command-specific cooldown
        cooldown_key = f"{user_id}:{command}"
        last_used = self.command_cooldowns.get(cooldown_key, 0)
        cooldown_time = COMMAND_COOLDOWNS.get(command, 0)
        
        if now - last_used < cooldown_time:
            remaining = cooldown_time - (now - last_used)
            return False, f"Cooldown: {remaining:.1f}s remaining"
        
        # Allow command
        user_bucket['tokens'] -= 1
        self.user_buckets[user_id] = user_bucket
        self.command_cooldowns[cooldown_key] = now
        
        return True, None
```

**Features:**
- ⚡ Per-user rate limiting (15 commands/60s)
- ⏱️ Per-command cooldowns (configurable)
- 🪣 Token bucket algorithm for fair usage
- 🔒 Protection against spam and abuse

---

### 3. Permission System

Hierarchical permission checking:

```python
# Simplified permission system example
class PermissionManager:
    def __init__(self):
        self.global_whitelist = set()
        self.global_blacklist = set()
        self.guild_whitelists = {}  # {guild_id: set(user_ids)}
    
    async def check_permission(self, user_id, guild_id, command):
        """
        Check if user has permission to execute command.
        Hierarchy: Blacklist > Global Whitelist > Guild Whitelist
        """
        # 1. Check blacklist (absolute block)
        if user_id in self.global_blacklist:
            return False, "User is blacklisted"
        
        # 2. Check global whitelist (full access)
        if user_id in self.global_whitelist:
            return True, None
        
        # 3. Check guild-specific whitelist
        guild_whitelist = self.guild_whitelists.get(guild_id, set())
        if user_id in guild_whitelist:
            return True, None
        
        # 4. Check if command requires authorization
        if command in ADMIN_COMMANDS:
            return False, "Command requires authorization"
        
        # 5. Public command - allow
        return True, None
```

**Hierarchy:**
1. 🚫 **Blacklist** (highest priority) - Absolute block
2. ✅ **Global Whitelist** - Full bot access
3. ✅ **Guild Whitelist** - Server-specific access
4. 📋 **Public Commands** - Available to all

---

### 4. Configuration Management

Atomic file operations for safe configuration:

```python
import json
import fcntl
from pathlib import Path

class ConfigManager:
    def __init__(self, config_dir="config"):
        self.config_dir = Path(config_dir)
        self.config_dir.mkdir(exist_ok=True)
    
    def read_config(self, guild_id=None):
        """Atomically read configuration"""
        if guild_id:
            config_path = self.config_dir / "per_guild" / f"{guild_id}.json"
        else:
            config_path = self.config_dir / "config.json"
        
        if not config_path.exists():
            return self.get_default_config()
        
        with open(config_path, 'r') as f:
            fcntl.flock(f.fileno(), fcntl.LOCK_SH)
            try:
                config = json.load(f)
            finally:
                fcntl.flock(f.fileno(), fcntl.LOCK_UN)
        
        return config
    
    def write_config(self, config, guild_id=None):
        """Atomically write configuration"""
        if guild_id:
            config_path = self.config_dir / "per_guild" / f"{guild_id}.json"
            config_path.parent.mkdir(exist_ok=True)
        else:
            config_path = self.config_dir / "config.json"
        
        # Write to temporary file first
        temp_path = config_path.with_suffix('.tmp')
        with open(temp_path, 'w') as f:
            fcntl.flock(f.fileno(), fcntl.LOCK_EX)
            try:
                json.dump(config, f, indent=2)
                f.flush()
                os.fsync(f.fileno())
            finally:
                fcntl.flock(f.fileno(), fcntl.LOCK_UN)
        
        # Atomic rename
        temp_path.replace(config_path)
```

**Safety Features:**
- 🔒 File locking prevents race conditions
- ⚛️ Atomic writes via temporary files
- 💾 fsync() ensures data is written to disk
- 🔄 Automatic retry on failure

---

## 🎵 Music System Architecture

### Player Design

```python
# Simplified music player example
class MusicPlayer:
    def __init__(self, voice_client):
        self.voice_client = voice_client
        self.queue = []
        self.current = None
        self.repeat_mode = False
    
    async def add_to_queue(self, url):
        """Add song to queue using yt-dlp"""
        # Extract info from YouTube/SoundCloud
        info = await self.extract_info(url)
        
        self.queue.append({
            'title': info['title'],
            'url': info['url'],
            'duration': info['duration'],
            'requester': info['requester']
        })
        
        # Start playing if nothing is playing
        if not self.voice_client.is_playing():
            await self.play_next()
    
    async def play_next(self):
        """Play next song in queue"""
        if not self.queue:
            self.current = None
            return
        
        self.current = self.queue.pop(0)
        
        # Create audio source
        source = await discord.FFmpegOpusAudio.from_probe(
            self.current['url'],
            **FFMPEG_OPTIONS
        )
        
        # Play with callback
        self.voice_client.play(
            source,
            after=lambda e: self.after_play(e)
        )
    
    def after_play(self, error):
        """Callback after song finishes"""
        if error:
            print(f"Player error: {error}")
        
        # Handle repeat mode
        if self.repeat_mode and self.current:
            self.queue.insert(0, self.current)
        
        # Play next song
        asyncio.run_coroutine_threadsafe(
            self.play_next(),
            self.voice_client.loop
        )
```

**Features:**
- 🎵 YouTube & SoundCloud support via yt-dlp
- 📋 Queue management
- 🔁 Repeat mode
- ⏭️ Skip functionality
- 🔊 Volume control

---

## 🛡️ Security Practices

### 1. Input Validation

```python
def validate_calculator_input(expression):
    """Validate calculator expression for security"""
    # Length check
    if len(expression) > 500:
        return False, "Expression too long (max 500 chars)"
    
    # Complexity check
    operation_count = sum(expression.count(op) for op in '+-*/^')
    if operation_count > 50:
        return False, "Expression too complex (max 50 operations)"
    
    # Nesting depth check
    depth = 0
    max_depth = 0
    for char in expression:
        if char == '(':
            depth += 1
            max_depth = max(max_depth, depth)
        elif char == ')':
            depth -= 1
    
    if max_depth > 10:
        return False, "Expression too deeply nested (max 10 levels)"
    
    # Forbidden patterns
    forbidden = ['__', 'import', 'eval', 'exec', 'open', 'file']
    if any(pattern in expression.lower() for pattern in forbidden):
        return False, "Expression contains forbidden patterns"
    
    return True, None
```

### 2. Path Traversal Prevention

```python
def safe_file_access(base_dir, filename):
    """Prevent path traversal attacks"""
    # Normalize and resolve paths
    base_path = Path(base_dir).resolve()
    file_path = (base_path / filename).resolve()
    
    # Ensure file is within base directory
    if not str(file_path).startswith(str(base_path)):
        raise ValueError("Path traversal attempt detected")
    
    return file_path
```

### 3. Timeout Protection

```python
async def execute_with_timeout(coro, timeout=5.0):
    """Execute coroutine with timeout"""
    try:
        return await asyncio.wait_for(coro, timeout=timeout)
    except asyncio.TimeoutError:
        raise TimeoutError(f"Operation timed out after {timeout}s")
```

---

## 📊 Logging System

### Structured Logging

```python
import logging
from logging.handlers import RotatingFileHandler

def setup_logging():
    """Setup logging with rotation"""
    logger = logging.getLogger('discord_bot')
    logger.setLevel(logging.INFO)
    
    # Console handler
    console_handler = logging.StreamHandler()
    console_handler.setLevel(logging.INFO)
    console_format = logging.Formatter(
        '%(asctime)s - %(levelname)s - %(message)s'
    )
    console_handler.setFormatter(console_format)
    
    # File handler with rotation
    file_handler = RotatingFileHandler(
        'logs/bot.log',
        maxBytes=10*1024*1024,  # 10 MB
        backupCount=14           # 14 days of logs
    )
    file_handler.setLevel(logging.INFO)
    file_format = logging.Formatter(
        '%(asctime)s - %(levelname)s - %(name)s - %(message)s'
    )
    file_handler.setFormatter(file_format)
    
    logger.addHandler(console_handler)
    logger.addHandler(file_handler)
    
    return logger
```

**Features:**
- 🔄 Automatic log rotation (10 MB per file)
- 📅 14-day retention period
- 📝 Structured log format
- 🖥️ Console + file output
- 🔍 Configurable log levels

---

## 🚨 Emergency System

```python
class EmergencySystem:
    def __init__(self):
        self.lockdown_active = False
        self.emergency_cooldown = 0
        self.activated_by = None
        self.activated_at = None
    
    async def activate_lockdown(self, user_id):
        """Restrict bot to global whitelist only"""
        self.lockdown_active = True
        self.activated_by = user_id
        self.activated_at = datetime.now()
        
        # Update bot status
        await bot.change_presence(
            activity=discord.Game(name="🚨 Emergency Lockdown Active")
        )
        
        # Persist to config
        await self.save_emergency_state()
        
        logger.critical(f"EMERGENCY LOCKDOWN activated by {user_id}")
    
    async def activate_cooldown(self, seconds, user_id):
        """Set global cooldown on all commands"""
        self.emergency_cooldown = seconds
        self.activated_by = user_id
        self.activated_at = datetime.now()
        
        # Update bot status
        await bot.change_presence(
            activity=discord.Game(name=f"⏱️ Emergency Cooldown: {seconds}s")
        )
        
        # Persist to config
        await self.save_emergency_state()
        
        logger.warning(f"EMERGENCY COOLDOWN ({seconds}s) activated by {user_id}")
    
    async def reset(self, user_id):
        """Deactivate all emergency measures"""
        self.lockdown_active = False
        self.emergency_cooldown = 0
        
        # Restore normal status
        await bot.change_presence(activity=discord.Game(name="!help"))
        
        # Clear persisted state
        await self.clear_emergency_state()
        
        logger.info(f"Emergency measures reset by {user_id}")
```

---

## 🔄 Status Rotation

```python
class StatusCycle:
    def __init__(self, bot):
        self.bot = bot
        self.statuses = []
        self.current_index = 0
        self.task = None
    
    async def start(self):
        """Start status rotation loop"""
        self.task = asyncio.create_task(self._cycle_loop())
    
    async def _cycle_loop(self):
        """Rotate through status messages"""
        while True:
            if not self.statuses:
                await asyncio.sleep(60)
                continue
            
            # Get current status
            status = self.statuses[self.current_index]
            
            # Parse placeholders
            text = status['text'].format(
                servers=len(self.bot.guilds),
                users=len(self.bot.users),
                commands=len(self.bot.commands)
            )
            
            # Update presence
            await self.bot.change_presence(
                activity=discord.Game(name=text)
            )
            
            # Wait for duration
            await asyncio.sleep(status['duration'])
            
            # Move to next status
            self.current_index = (self.current_index + 1) % len(self.statuses)
```

---

## 📚 API Integration Patterns

### NASA API Example

```python
class NASAClient:
    def __init__(self, api_key):
        self.api_key = api_key
        self.session = aiohttp.ClientSession()
    
    async def get_apod(self, date=None):
        """Get Astronomy Picture of the Day"""
        params = {
            'api_key': self.api_key,
            'date': date or datetime.now().strftime('%Y-%m-%d')
        }
        
        async with self.session.get(
            'https://api.nasa.gov/planetary/apod',
            params=params
        ) as response:
            if response.status == 200:
                return await response.json()
            else:
                raise APIError(f"NASA API error: {response.status}")
```

---

## 💡 Best Practices Used

### Code Quality
- ✅ Type hints for better code clarity
- ✅ Comprehensive error handling
- ✅ Input validation and sanitization
- ✅ Docstrings for all functions
- ✅ Consistent code formatting

### Security
- 🔒 No hardcoded secrets (environment variables)
- 🔒 Input validation on all user inputs
- 🔒 Rate limiting and cooldowns
- 🔒 Permission checks before actions
- 🔒 Timeout protection for long operations

### Performance
- ⚡ Async/await for non-blocking operations
- ⚡ Connection pooling for HTTP requests
- ⚡ Caching for frequently accessed data
- ⚡ Efficient data structures (sets for lookups)
- ⚡ Batch operations where possible

### Maintainability
- 📦 Modular architecture (separate files per feature)
- 📦 Clear separation of concerns
- 📦 Configuration-driven behavior
- 📦 Comprehensive logging
- 📦 Documentation and comments

---

## 🎓 Learning Resources

If you're interested in building similar bots, check out:

- **Discord.py Documentation:** https://discordpy.readthedocs.io/
- **Discord API Documentation:** https://discord.com/developers/docs
- **Python Async Programming:** https://docs.python.org/3/library/asyncio.html
- **OAuth2 Flow:** https://discord.com/developers/docs/topics/oauth2

---

## 📝 Notes

- The examples above are simplified for educational purposes
- Actual bot code includes additional error handling, validation, and features
- Code patterns and architecture are continuously improved based on best practices
- Security is a top priority in all implementations

---

<div align="center">

**Made with ❤️ in Germany 🇩🇪**

[Back to README](./README.md)

</div>
