# 🔧 Code Examples & Architecture

This document showcases the architecture, design patterns, and code examples that power the MCLP Discord Bot.

> **Note:** The actual bot source code is private. The examples below are illustrative and demonstrate the general patterns and approaches used in the bot's development.

---

## 📁 Architecture Overview

### Project Structure

```
Discord-Bot/src/
├── main.py                             # Entry point
├── bot.py                              # Bot initialization and event handling
└── internal/
   ├── command_router.py                # Intelligent command routing
   ├── rate_limiter.py                  # Multi-layered rate limiting
   ├── status_cycle.py                  # Status rotation system
   ├── utils.py                         # Helper functions & config management
   ├── command_modules/
   │   ├── __init__.py                  # Module initialization
   │   ├── calculator.py                # Advanced calculator
   │   ├── logging_setup.py             # Custom logging handler
   │   ├── minigames.py                 # Games: Quiz, Hangman, RPS
   │   ├── moderation_commands.py       # Kick, ban, timeout
   │   ├── public_commands.py           # Help, info, serverinfo
   │   ├── sciencecific_commands.py     # NASA & space APIs
   │   ├── system_commands.py           # Admin controls
   │   ├── utility_commands.py          # Weather, time, reminders
   │   └── music/
   │       ├── music_commands.py        # Music control commands
   │       └── player.py                # Music player logic
   └── data/
       ├── config.json                  # Global bot configuration
       ├── hangman.json                 # Hangman word lists
       ├── quiz.json                    # Quiz questions
       ├── reactionrole.json            # Reaction role mappings
       └── servers/
           └── <guild_id>.json          # Per-server configuration
```

---

## 🎯 Design Patterns

### 1. Command Router Pattern

The bot uses a centralized command routing system with grouped command handlers:

```python
# Simplified example of the command routing approach

# Command groups definition
command_groups = {
    'utility': ['!ping', '!uptime', '!weather', '!city',  ...],
    'minigames': ['!rps', '!hangman', '!quiz', '!guess', '!roll'],
    'public': ['!help', '!info', '!rules', '!userinfo', ...],
    'moderation': ['!kick', '!ban', '!unban', '!timeout', ...],
    'sciencecific': ['!apod', '!marsphoto', '!asteroids', ...],
    'music': ['!join', '!leave', '!play', '!pause', ...],
}

# Command handlers mapping
command_handlers = {
    'utility': handle_utility_commands,
    'minigames': handle_minigames_commands,
    'public': handle_public_commands,
    'moderation': handle_moderation_commands,
    'sciencecific': handle_sciencecific_commands,
    'music': handle_music_commands,
}

# Commands that cannot be executed in DMs
no_dm_commands = ['!kick', '!ban', '!unban', '!timeout', '!play', '!join', ...]


async def handle_command(client, message):
    # Route incoming commands to the appropriate handler.
    user_message = message.content.strip()
    command_token = user_message.split(maxsplit=1)[0].lower()

    # Per-user spam protection
    if command_token.startswith('!'):
        spam_allowed, spam_msg = await check_user_spam(message.author.id)
        if not spam_allowed:
            await message.channel.send(spam_msg)
            return None

    # Block commands that require a server context
    if message.guild is None and command_token in no_dm_commands:
        await message.channel.send("⚠️ This command cannot be executed in a DM environment.")
        return None

    # Route to the matching command group handler
    for group, commands in command_groups.items():
        if command_token in commands:
            return await command_handlers[group](client, message, user_message)

    # Unknown command feedback
    if command_token.startswith('!'):
        await message.channel.send("❓ Unknown command. Type !help for a list of available commands.")
    return None
```

**Benefits:**
- 📖 Centralized command management via dictionaries
- 📦 Grouped handlers for modular code organization
- 🚫 DM-aware command blocking
- 🛡️ Built-in spam protection before routing
- ⚠️ Consistent error handling across all command groups

---

### 2. Rate Limiting System

Multi-layered rate limiting with token bucket algorithm, per-command cooldowns, and emergency controls:

```python
# Simplified rate limiting example

class RateLimiter:
    #Token bucket algorithm for API rate limiting.
    def __init__(self, max_requests: int, time_window: int):
        self.max_requests = max_requests
        self.time_window = time_window
        self.requests = defaultdict(list)

    def is_allowed(self, identifier: str) -> Tuple[bool, float]:
        # Clean old requests, check limit, return (allowed, retry_after)
        # Clean old requests outside time window
        if identifier in self.requests:
            ...

        # Check if limit exceeded
        if len(self.requests[identifier]) >= self.max_requests:
            ...

        ...

class CommandCooldown:
    #Per-user, per-command cooldown tracking.
    def __init__(self):
        ...

    def is_on_cooldown(self, command: str, cooldown_seconds: int, user_id: int) -> Tuple[bool, float]:

        def set_cooldown(self, command: str, user_id: int):
            ...
        
        def get_remaining(self, command: str, cooldown_seconds: int, user_id: int) -> float:
            ...
    
    ...


class GlobalCooldown:
    #Global emergency cooldown for all commands (spam/attack protection).

    def __init__(self):
        ...

    def activate(self, cooldown_seconds: int = 60, reason: str = "..."):
        ...

    def deactivate(self):
        ...

    def check_allowed(self, user_id: int) -> Tuple[bool, float]:
        
        if len(self.last_command_time) > 10000:
            ...

        if user_id in self.last_command_time:
            ...

# API-specific rate limiters
api_limiter_nasa = RateLimiter(max_requests=5, time_window=60)
api_limiter_openweather = RateLimiter(max_requests=10, time_window=60)

# Per-user spam protection (separate from API limits)
user_spam_limiter = RateLimiter(max_requests=15, time_window=60)

# Usage in commands:
allowed, error_msg = await check_command_cooldown('apod', message.author.id)
if not allowed:
    await safe_send(message, content=error_msg)
    return

allowed, error_msg = await check_api_limit(api_limiter_nasa, "NASA API")
if not allowed:
    await safe_send(message, content=error_msg)
    return
```

**Features:**
- 👤 Per-user rate limiting (15 commands/60s)
- ⏱️ Per-command cooldowns (configurable per command)
- 🪣 Token bucket algorithm for fair usage
- 🚨 Global emergency cooldown for attack protection
- 🛡️ Separate API rate limiters per external service

---

### 3. Permission System

Hierarchical permission checking with two authorization levels:

```python
# Simplified permission system example

def is_authorized_global(user):
    # Check if user has global (owner-level) access.
    # Hierarchy: Blacklist > Global Whitelist
    
    # 1. Blacklist check (overrides everything)
    if is_user_blacklisted(user.id):
        return False
    
    # 2. Check global whitelist
    cfg = load_config()
    whitelist = cfg.get("whitelist", []) or []
    return str(user.id) in whitelist


def is_authorized_server(user, guild_id):
    # Check if user has server-level access.
    # Hierarchy: User Blacklist > Server Blacklist > Server Whitelist > Guild Owner
    
    # 1. User blacklist (overrides everything)
    if is_user_blacklisted(user.id):
        return False
    
    # 2. Server blacklist
    if is_server_blacklisted(guild_id):
        return False
    
    # 3. Check server-specific whitelist
    server_config = load_server_config(guild_id)
    whitelist = server_config.get("whitelist", []) or []
    
    if whitelist:
        return str(user.id) in whitelist
    
    # 4. Whitelist empty -> auto-trust only the guild owner
    if hasattr(user, 'guild') and user.guild is not None:
        if user.id == user.guild.owner_id:
            return True
    
    return False


# Usage in commands:

# Owner-only commands (e.g. shutdown)
if is_authorized_global(interaction.user):
    await interaction.response.send_message("Shutting down the bot...")

# Server-level commands (e.g. moderation)
if await check_blacklist(interaction):  # Early blacklist rejection
    return
if not is_authorized_server(interaction.user, guild_id=interaction.guild.id):
    await interaction.response.send_message("❌ **Permission denied.**", ephemeral=True)
    return
```

**Hierarchy:**
1. 🚫 **User Blacklist** (highest priority) - Absolute block, overrides all whitelists
2. 🏴 **Server Blacklist** - Blocks entire servers from using the bot
3. 🔑 **Global Whitelist** - Full bot access including owner-only commands
4. 📋 **Server Whitelist** - Server-specific access for moderation commands
5. 👑 **Guild Owner** - Auto-trusted when server whitelist is empty
6. 🌍 **Public Commands** - Available to all non-blacklisted users

---

### 4. Configuration Management

Thread-safe atomic file operations for safe configuration handling:

```python
# Simplified configuration management example

# In-process file locks for thread safety
_file_locks = {}
_file_locks_lock = threading.Lock()

def _get_lock(path: str) -> threading.Lock:
    with _file_locks_lock:
        return _file_locks.setdefault(path, threading.Lock())


def _atomic_write(file_path: str, data: dict):
    # Atomically write data using temp file + os.replace().
    lock = _get_lock(file_path)
    with lock:
        # Generate a temporary file to write data from temp into target and clean up afterwards


def _atomic_read(file_path: str) -> dict:
    # Thread-safe read with automatic corrupt file backup.
    lock = _get_lock(file_path)
    with lock:
        # Read the data from the file

            # Backup corrupt file instead of losing data
            shutil.copy2(file_path, file_path + ".corrupt")
            return {}


# Global config helpers
def load_config() -> dict:
    return _atomic_read(_abs_path("..."))

def set_config_value(key: str, value):
    # Read-modify-write under a single lock.
    path = _abs_path("...")
    lock = _get_lock(path)
    with lock:
        cfg = _atomic_read(path) if os.path.exists(path) else {}
        cfg[key] = value
        _atomic_write(path, cfg)


# Per-server config with auto-creation
def load_server_config(guild_id: int) -> dict:
    path = _abs_path("...")
    data = _atomic_read(path)
    if not data:
        return create_server_config(guild_id)
    return data

def save_server_config(guild_id: int, data: dict):
    _atomic_write(_abs_path("..."), data)

def _default_server_config() -> dict:
    return {
        ...
    }
```

**Safety Features:**
- 🔐 Per-file thread locks prevent race conditions
- ⚛️ Atomic writes via `tempfile` + `os.replace()`
- 💾 `fsync()` ensures data reaches disk
- 🗂️ Corrupt file backup instead of silent data loss
- 🏗️ Auto-creation of server configs with sensible defaults
- 🧹 Periodic lock cleanup for unused file locks
---

## 🎵 Music System Architecture

### Player Design

The music system uses a per-guild state dictionary with platform-aware configuration:

```python
# Simplified music player example

# Platform detection for cross-platform support
IS_PI = ARCH in ["armv7l", "armv6l", "aarch64"]
IS_WINDOWS = platform.system() == "Windows"

music_state = {}
max_queue_size = 20 if IS_PI else 50

def get_guild_state(guild_id: int) -> dict:
    # Get or create per-guild music state.
    if guild_id not in music_state:
        music_state[guild_id] = {
            "queue": [],
            "current": None,
            "voice_client": None,
            "playing": False,
            "repeat_mode": "off",
            "error_count": 0,
        }
    return music_state[guild_id]
```

### Source Detection & yt-dlp Configuration

```python
# Source-specific yt-dlp options
YTDLP_OPTIONS_YT = {
    **_YTDLP_BASE,
    "format": "251/250/249/140/opus/m4a/aac/best...",
    "default_search": "ytsearch",
    "extractor_args": {"youtube": {"player_client": ["android", "web"]}},
}

YTDLP_OPTIONS_SC = {
    **_YTDLP_BASE,
    "format": "http_mp3/hls_mp3/hls_opus/hls_aac/best",
}

# Source-specific ffmpeg options
FFMPEG_OPTIONS_YT = {
    "before_options": "-reconnect 1 -reconnect_streamed 1 -reconnect_delay_max 10",
    "options": "-vn",
}

FFMPEG_OPTIONS_SC = {
    "before_options": "-rw_timeout 20000000",  # No -reconnect (crashes with HLS/redirects)
    "options": "-vn",
}

def get_ytdlp_options(query: str) -> dict:
    # Return appropriate yt-dlp options based on query source.
    if "soundcloud.com" in query.lower():
        return YTDLP_OPTIONS_SC
    return YTDLP_OPTIONS_YT
```

### FFmpeg Resolution

```python
def resolve_ffmpeg_executable() -> str:
    # Resolve ffmpeg path with platform-specific search.
    # 1. Check FFMPEG_PATH environment variable
    # 2. Check platform-specific paths (Pi / Windows)
    # 3. Fall back to PATH lookup via shutil.which()
    # 4. Raise PlayerError with platform-specific install instructions
    ...
```

### Playback & Queue Logic

```python
async def add_to_queue(guild: discord.Guild, query: str):
    # Add a song to the queue with queue size limits.
    state = get_guild_state(guild.id)

    if len(state["queue"]) >= max_queue_size:
        raise PlayerError(f"Queue limit reached ({max_queue_size} tracks).")

    song = extract_audio(query)
    state["queue"].append(song)

    if not state["playing"]:
        await play_next(guild)
    return song


async def play_next(guild: discord.Guild):
    # Play next song with repeat mode support and error recovery.
    state = get_guild_state(guild.id)
    repeat_mode = state.get("repeat_mode", "off")
    current = state.get("current")

    # Handle repeat modes (one / all / off)
    if repeat_mode == "one" and current:
        song = current
    elif repeat_mode == "all" and current and not state["queue"]:
        song = current
    else:
        if not state["queue"]:
            state["playing"] = False
            state["current"] = None
            return
        song = state["queue"].pop(0)

    source = discord.FFmpegPCMAudio(song["url"], **get_ffmpeg_options(song.get("source")))

    def after_play(error):
        if error:
            ...
        else:
            state["error_count"] = 0
        loop.call_soon_threadsafe(asyncio.create_task, play_next(guild))

    voice_client.play(source, after=after_play)
```

### Graceful Shutdown

```python
async def disconnect(guild_id: int):
    # Graceful disconnect: stop playback, wait for FFmpeg, then disconnect.
    state = get_guild_state(guild_id)
    vc = state.get("voice_client")
    if vc:
        if vc.is_playing() or vc.is_paused():
            vc.stop()
            await asyncio.sleep(0.5)  # Wait for FFmpeg to terminate
        await vc.disconnect(force=True)
        # Cleanup state
        ...


async def cleanup_all_guilds(bot):
    # Clean up all voice connections before bot shutdown.
    for guild in bot.guilds:
        if guild.voice_client:
            await disconnect(guild.id)
    music_state.clear()
```

### Music Channel Enforcement

```python
# URL domain whitelist
ALLOWED_MUSIC_DOMAINS = {"youtube.com", "www.youtube.com", "youtu.be",
                          "soundcloud.com", "www.soundcloud.com"}

async def is_music_channel(message) -> bool:
    # Ensure commands are used in the designated music channel.
    cfg = load_server_config(message.guild.id)
    music_channel_id = cfg.get("music_channel_id")
    if music_channel_id is None:
        await message.channel.send("❌ Music channel not set. Use !music-channel.")
        return False
    if message.channel.id != int(music_channel_id):
        await message.channel.send(f"❌ Please use <#{music_channel_id}>.")
        return False
    return True
```

### Interactive Queue Display

```python
class QueueView(ui.View):
    # Paginated queue display with interactive buttons.
    def __init__(self, guild_id: int, current_page: int = 0, owner_id: int | None = None):
        super().__init__(timeout=180)
        ...

    async def interaction_check(self, interaction) -> bool:
        # Only the command user can change pages.
        ...

    @ui.button(label="⬅️ Previous", style=discord.ButtonStyle.blurple)
    async def previous_page(self, interaction, button): ...

    @ui.button(label="➡️ Next", style=discord.ButtonStyle.blurple)
    async def next_page(self, interaction, button): ...

    async def on_timeout(self):
        # Disable buttons after 3 minutes.
        ...
```

**Features:**
- 🎵 YouTube & SoundCloud support with source-specific configurations
- 📋 Per-guild queue management with size limits (20 on Pi, 50 on desktop)
- 🔁 Three repeat modes: off, one, all
- 🛡️ Consecutive error tracking with auto-stop after 5 failures
- 🖥️ Cross-platform FFmpeg detection (Windows, Linux, Raspberry Pi)
- 📺 Paginated queue display with interactive Discord UI buttons
- 🔒 Music channel enforcement and URL domain whitelist
- 🧹 Graceful shutdown with FFmpeg cleanup across all guilds

---

## 🛡️ Security Practices

### 1. Calculator Input Validation

Multi-layered security for safe expression evaluation with code injection prevention:

```python
# Simplified calculator security example

# Constants
MAX_EXPRESSION_LENGTH
CALCULATION_TIMEOUT
MAX_NESTING_DEPTH
MAX_OPERATIONS

class CalculatorError(Exception):
    pass

class SecurityError(CalculatorError):
    pass


def is_safe_expression(expression: str) -> Tuple[bool, str]:
    # Main validation entry point - 5 security layers.
    if not expression or len(expression) > MAX_EXPRESSION_LENGTH:
        return False, f"Expression too long (max {MAX_EXPRESSION_LENGTH} chars)"

    if '\x00' in expression:
        return False, "Expression contains null bytes"

    # ===== LAYER 1: BLACKLIST DANGEROUS PATTERNS =====
    dangerous_patterns = [
        # Code execution
        r'\b__import__\b', r'\beval\b', ...
        # Module imports
        r'\bimport\s', r'\bfrom\s',
        # File/System operations
        r'\bopen\b', r'\bos\.', ...
        # Object/Class manipulation
        r'__[a-z]+__',  # Dunder methods
        r'\.__bases__', r'\.__class__', ...
        # Lambda abuse
        r'lambda\s+.*:.*import',
    ]

    normalized = ' '.join(expression.split()).lower()
    for pattern in dangerous_patterns:
        if re.search(pattern, normalized):
            return False, "Expression contains forbidden keywords or patterns"

    # Suspicious escape sequences
    for seq in ['\\\\', '\\x', '\\u']:
        if seq in expression:
            return False, "Expression contains suspicious escape sequences"

    # ===== LAYER 2: CHECK COMPLEXITY =====
    is_valid, error_msg = check_expression_complexity(expression)
    if not is_valid:
        return False, error_msg

    # ===== LAYER 3: VALIDATE FUNCTION CALLS (WHITELIST) =====
    is_valid, error_msg = validate_function_calls(expression)
    if not is_valid:
        return False, error_msg

    # ===== LAYER 4: VALIDATE VARIABLE NAMES (WHITELIST) =====
    is_valid, error_msg = validate_variable_names(expression)
    if not is_valid:
        return False, error_msg

    # ===== LAYER 5: CHECK BALANCED BRACKETS =====
    for open_b, close_b, name in [('(', ')', 'parentheses'),
                                    ('[', ']', 'brackets'),
                                    ('{', '}', 'braces')]:
        if expression.count(open_b) != expression.count(close_b):
            return False, f"Unbalanced {name}"

    return True, ""


def check_expression_complexity(expression: str) -> Tuple[bool, str]:
    # Prevent DoS via deeply nested or overly complex expressions.
    # Check nesting depth
    max_depth = 0
    current_depth = 0
    for char in expression:
        if char in '([{':
            current_depth += 1
            max_depth = max(max_depth, current_depth)
        elif char in ')]}':
            current_depth -= 1

    if max_depth > MAX_NESTING_DEPTH:
        return False, f"Expression nesting too deep (max {MAX_NESTING_DEPTH} levels)"

    # Count operations
    operation_count = sum(expression.count(op) for op in ['+', '-', '*', ...])
    if operation_count > MAX_OPERATIONS:
        return False, f"Expression too complex (max {MAX_OPERATIONS} operations)"

    return True, ""


def validate_function_calls(expression: str) -> Tuple[bool, str]:
    # Only allow whitelisted math functions (e.g. sin, cos, sqrt, log).
    found_functions = set(re.findall(r'([a-zA-Z_]\w*)\s*\(', expression))
    disallowed = found_functions - set(SAFE_FUNCTIONS.keys())
    if disallowed:
        return False, f"Function(s) not allowed: {', '.join(list(disallowed)[:3])}"
    return True, ""


def validate_variable_names(expression: str) -> Tuple[bool, str]:
    # Only allow whitelisted variable names (e.g. x, y, z, ans).
    found = set(re.findall(r'\b([a-zA-Z_]\w*)\b', expression))
    safe = set(SAFE_FUNCTIONS.keys()) | {'ans', 'x', 'y', 'z', ...}
    unknown = found - safe
    if unknown:
        return False, f"Unknown identifiers: {', '.join(list(unknown)[:3])}"
    return True, ""
```

**Security Layers:**
- 🚫 **Layer 1:** Blacklist — blocks dangerous keywords (`eval`, `exec`, `import`, `__dunder__`, ...)
- 📐 **Layer 2:** Complexity — limits nesting depth (10) and operation count (50)
- ✅ **Layer 3:** Function whitelist — only safe math functions allowed
- ✅ **Layer 4:** Variable whitelist — only known identifiers permitted
- ⚖️ **Layer 5:** Bracket balancing — rejects malformed expressions

---

### 2. Path Traversal Prevention

```python
# Simplified example of the path traversal guards

def save_json_file(data: dict, rel_path: str):
    # Save JSON file with path traversal protection.
    # Block absolute paths and directory traversal
    if rel_path.startswith("/") or ".." in rel_path:
        raise ValueError(f"Invalid path: {rel_path} (path traversal not allowed)")

    parts = rel_path.split("/")

    # Validate every path component
    for part in parts:
        if part in ("..", "."):
            raise ValueError(f"Invalid path component: {part}")

    path = _abs_path(*parts)
    _atomic_write(path, data)
```

**Protection:**
- 🛤️ Rejects absolute paths (`/etc/passwd`)
- 🔙 Blocks `..` traversal in all path components
- 📁 Resolves paths only within the data directory

---

### 3. Timeout Protection

```python
# Simplified example of the timeout protections

async def calculate_with_timeout(expression: str) -> str:
    # Execute calculation with timeout to prevent DoS.
    try:
        loop = asyncio.get_event_loop()
        result = await asyncio.wait_for(
            loop.run_in_executor(
                None,
                lambda: sympify(expression, locals=SAFE_FUNCTIONS)
            ),
            timeout=CALCULATION_TIMEOUT
        )

        if isinstance(result, (int, float, Number)):
            return format_number(float(result))
        return str(result)

    except asyncio.TimeoutError:
        raise CalculatorError(f"Calculation timed out (exceeded {CALCULATION_TIMEOUT}s)")
    except ZeroDivisionError:
        raise CalculatorError("Cannot divide by zero")
    except OverflowError:
        raise CalculatorError("Result exceeds allowed range")
    except sympy.SympifyError as e:
        raise CalculatorError(f"Invalid mathematical expression: {str(e)}")

# In other places like minigames

except asyncio.TimeoutError:
    await safe_send(message, content="⚠️ Timeout - Game cancelled!")
    logging.warning("Timeout - Game cancelled!")
```

**Protection:**
- ⏱️ Hard timeout prevents resource exhaustion
- 🧵 Runs in executor to avoid blocking the event loop
- 🎯 Specific exception handling for each failure mode
- 🎮 Also used for minigame input timeouts (`asyncio.wait_for`)
---

## 📊 Logging System

### Custom Timed Rotating File Handler

The bot uses a custom logging handler with daily rotation, timezone-aware timestamps, and automatic cleanup:

```python
# Simplified logging system example

# Local timezone
try:
    LOCAL_TZ = zoneinfo.ZoneInfo("Europe/Berlin")
except Exception:
    LOCAL_TZ = None

def now_local():
    # Get current time in local timezone, fallback to UTC.
    if LOCAL_TZ:
        return datetime.now(LOCAL_TZ)
    return datetime.now(timezone.utc)


class CustomTimedRotatingFileHandler(logging.FileHandler):
    # Daily log rotation with timestamped filenames and automatic cleanup.

    def __init__(self, filename, when='midnight', interval=1, backupCount=0, encoding=None):
        ...

        # Create initial log file with timestamp
        timestamp = now_local().strftime("%d.%m.%Y_%H-%M-%S")
        current_file = f"{self.base_filename}-{timestamp}.txt"
        super().__init__(current_file, encoding=encoding)
        self.last_rollover = now_local().date()

        self._cleanup_old_logs()

    def emit(self, record):
        # Check for date change before each log entry.
        current_date = now_local().date()
        ...
        super().emit(record)

    def doRollover(self):
        # Close current file and create new one with fresh timestamp.
        if self.stream:
            self.stream.close()
        timestamp = now_local().strftime("%d.%m.%Y_%H-%M-%S")
        ...

    def _cleanup_old_logs(self):
        # Delete old log files exceeding backupCount.

        log_files = sorted(
            [f for f in os.listdir(log_dir)
             if f.startswith(log_basename) and f.endswith('.txt')],
            key=lambda f: os.path.getmtime(os.path.join(log_dir, f))
        )

        # Never delete the currently active file
        ...

        current_basename = os.path.basename(self.baseFilename)
        files_to_consider = [f for f in log_files if f != current_basename]

        files_to_delete = len(files_to_consider) - (self.backupCount - 1)
        if files_to_delete > 0:
            for old_file in files_to_consider[:files_to_delete]:
                os.remove(os.path.join(log_dir, old_file))
```

### Logging Setup

```python
# Simplified overview of the logging setup

def setup_logging():
    # Setup logging with config-driven debug mode and Discord noise reduction.
    config = utils.load_config()
    debug_mode = config.get("DebugModeActivated", False)
    log_directory = config.get("log_file_location", "Logs")

    root_logger = logging.getLogger()

    # Remove old handlers on reload
    for handler in root_logger.handlers[:]:
        root_logger.removeHandler(handler)

    formatter = logging.Formatter(
        '%(asctime)s - %(module)s : %(levelname)s - %(message)s',
        datefmt="%Y-%m-%d %H:%M:%S"
    )

    # File handler with daily rotation and 14-day retention
    file_handler = CustomTimedRotatingFileHandler(
        os.path.join(log_directory, "bot.log"),
        when="midnight",
        interval=1,
        backupCount=14,
        encoding="utf-8"
    )
    file_handler.setFormatter(formatter)
    file_handler.setLevel(logging.DEBUG if debug_mode else logging.INFO)

    # Console handler
    console_handler = logging.StreamHandler(sys.stdout)
    console_handler.setFormatter(formatter)
    console_handler.setLevel(logging.DEBUG if debug_mode else logging.INFO)

    root_logger.addHandler(file_handler)
    root_logger.addHandler(console_handler)
    root_logger.setLevel(logging.DEBUG if debug_mode else logging.INFO)

    # Reduce Discord.py noise
    logging.getLogger('discord').setLevel(logging.WARNING)

    return root_logger
```

### Usage Throughout the Bot

```python
# Standard Python logging used everywhere — no custom logger needed

logging.info(f"System: Bot started successfully on {len(bot.guilds)} servers")
logging.warning("No letters could be drawn because the pool is empty.")
logging.error(f"Failed to create directory {path}: {e}")
logging.critical(f"EMERGENCY LOCKDOWN activated by {user_id}")
logging.debug(f"User {user.id} not in global whitelist")
```

**Features:**
- 📅 Daily rotation with timestamped filenames (`bot.log-15.02.2026_08-30-00.txt`)
- 🗑️ Automatic cleanup after 14 days (`backupCount=14`)
- 🕐 Timezone-aware timestamps (`Europe/Berlin`, fallback to UTC)
- 🔒 Thread-safe rollover with double-checked locking
- 🐛 Config-driven debug mode (`DebugModeActivated`)
- 🔇 Discord.py logger reduced to `WARNING` to minimize noise
- 🖥️ Dual output: file + console with identical formatting
---

## 🚨 Emergency System

Two emergency measures controlled via slash commands, with state persistence across restarts:

```python
# Simplified emergency system example

# Emergency state stored in rate_limiter module (not a class)
emergency_lockdown_mode = False
emergency_lockdown_owner_id = None
emergency_lockdown_time = None


class GlobalCooldown:
    # Global emergency cooldown for all commands
    def __init__(self):
        self.is_active = False
        self.cooldown_seconds = 0
        self.last_command_time = {}  # user_id -> timestamp

    def activate(self, cooldown_seconds: int = 60, reason: str = "..."): ...
    def deactivate(self): ...
    def check_allowed(self, user_id: int) -> Tuple[bool, float]: ...
    def get_status(self) -> str: ...

global_cooldown = GlobalCooldown()


# Slash commands (owner-only, global scope)
# /emergency-lockdown  — Bot responds only to whitelisted users, all guild messages and / or DM messages ignored
# /emergency-cooldown  — Enforces N-second cooldown on all commands for all users (1-300s)
# /emergency-reset     — Deactivates both measures, restores normal bot status


# State persisted to config.json (survives restarts)
utils.set_config_value("EmergencyState", {
    "lockdown": True,
    "lockdown_owner_id": str(user_id),
    "lockdown_time": datetime.now().isoformat(),
    "cooldown": True,
    "cooldown_seconds": 60
})

# Bot status reflects emergency state
# Lockdown:  🚨 Emergency Lockdown Active  (DND)
# Cooldown:  ⏸️ Global Cooldown: 60s        (Idle)
# Reset:     Restores original status from BotStatus config


# Enforcement in on_message event handler
if emergency_lockdown_mode:
    if message.guild is not None:
        return  # Ignore all guild messages during lockdown
    if not is_authorized_global(message.author):
        return  # Only whitelisted users in DMs

if global_cooldown.is_active:
    allowed, remaining = global_cooldown.check_allowed(message.author.id)
    if not allowed:
        await message.reply(f"⏸️ Global cooldown active. Wait {remaining:.0f}s")
        return
```

**Features:**
- 🚨 **Lockdown** — restricts bot to whitelisted users only, blocks all guild messages
- ⏸️ **Cooldown** — enforces per-user delay on all commands (1-300s configurable)
- 💾 State persisted to config (survives bot restarts)
- 🔄 Automatic state restoration on startup
- 🎭 Bot presence reflects active emergency measures
- 🔓 `/emergency-reset` deactivates both and restores original status

---

## 🔄 Status Rotation

Config-driven status cycling with safety limits, uptime placeholders, and message parsing:

```python
# Simplified status cycle example

# Safety constants
MIN_STATUS_DURATION_MINUTES = 2.5
MIN_CYCLE_INTERVAL_MINUTES = 30
MAX_STATUSES_PER_CYCLE = 10

_last_activity_signature: tuple[str, str] | None = None


class StatusCycleBot(commands.Bot):
    # Extends commands.Bot with status cycle management
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.status_cycle_task: asyncio.Task | None = None
        self.status_cycle_stop_event: asyncio.Event | None = None

    async def start_status_cycle(self) -> bool: ...
    async def stop_status_cycle(self) -> bool: ...


def _build_activity(status_type: str, status_text: str) -> discord.Activity | None:
    # Map config strings to Discord activity types
    mapping = {
        "playing": discord.ActivityType.playing,
        "listening": discord.ActivityType.listening,
        "watching": discord.ActivityType.watching,
        "competing": discord.ActivityType.competing
    }
    activity_type = mapping.get(status_type.lower().strip())
    if not activity_type:
        return None
    return discord.Activity(type=activity_type, name=status_text)


async def _apply_status(bot: commands.Bot, status_data: dict) -> None:
    # Apply a status, replacing placeholders like {uptime}
    status_text = status_data.get("text", "")
    status_text = status_text.replace("{uptime}", _format_uptime())

    activity = _build_activity(status_data.get("type", ""), status_text)
    if activity is None:
        return

    # Skip if status hasn't changed (avoid unnecessary API calls)
    signature = (activity.type.name, activity.name or "")
    if _last_activity_signature == signature:
        return

    await bot.change_presence(activity=activity)


async def _run_status_cycle(bot: commands.Bot, stop_event: asyncio.Event) -> None:
    # Main cycle loop
    while not stop_event.is_set():
        cfg = utils.get_config_value("StatusCycle", default={}) or {}
        statuses = cfg.get("statuses", []) or []
        every_minutes = cfg.get("every_minutes", 120)

        # Enforce safety limits
        if every_minutes < MIN_CYCLE_INTERVAL_MINUTES:
            every_minutes = MIN_CYCLE_INTERVAL_MINUTES
        if len(statuses) > MAX_STATUSES_PER_CYCLE:
            statuses = statuses[:MAX_STATUSES_PER_CYCLE]

        # Cycle through statuses
        for status in statuses:
            ...

        # Restore default status between cycles
        default_status = utils.get_config_value("BotStatus", default=None)
        if isinstance(default_status, dict):
            await _apply_status(bot, default_status)

        # Wait for next cycle
        try:
            await asyncio.wait_for(stop_event.wait(), timeout=every_minutes * 60)
        except asyncio.TimeoutError:
            pass
```

### Slash Command: `/status_cycle`

```python
# /status_cycle action:<start|stop|status|set|from_message>

# Actions:
# start        — Start the cycle (persists "enabled" to config)
# stop         — Stop the cycle, restore default BotStatus
# status       — Show current config (interval, entry count, on/off)
# set          — Update interval and/or statuses via JSON parameter
# from_message — Parse status lines from a Discord message

# from_message format (one status per line):
# [playing] "Exploring the cosmos" 5
# [listening] "to {uptime}" 2.5
# [watching] "over {servers} servers" 10

# Lines starting with # are ignored
# Default type applied if no [tag] prefix
# Duration in minutes (min 2.5, enforced)
```

**Features:**
- 🔄 Configurable cycle with per-status durations and activity types
- 🛡️ Safety limits: min 2.5min per status, min 30min cycle interval, max 10 entries
- 📝 Placeholder support (`{uptime}`, `{uptime_duration}`)
- 📨 `from_message` — parse statuses directly from a Discord message
- ⏹️ Graceful stop via `asyncio.Event` (no task cancellation)
- 🎭 Restores default `BotStatus` between cycles and on stop
- 🔇 Duplicate detection — skips API call if status unchanged
---

## 📚 API Integration Patterns

All external API calls follow the same pattern: rate limit check → request with timeout → error handling.

```python
# Simplified API integration example

# API keys loaded from environment variables (never hardcoded)
NASA_API_KEY = os.getenv('NASA_API_KEY')
OPENWEATHERMAP_API_KEY = os.getenv('OPENWEATHERMAP_API_KEY')

# Rate limiters (defined in rate_limiter.py)
api_limiter_nasa = RateLimiter(max_requests=5, time_window=60)
api_limiter_openweather = RateLimiter(max_requests=10, time_window=60)


async def api_request(url: str, params: dict, timeout: int = 10) -> dict | None:
    # Shared request logic for all external APIs.
    try:
        async with aiohttp.ClientSession() as session:
            async with session.get(
                url,
                params={k: v for k, v in params.items() if v is not None},
                timeout=aiohttp.ClientTimeout(total=timeout)
            ) as response:
                if response.status == 200:
                    return await response.json()
                logging.warning(f"API error: {response.status} for {url}")
                return None
    except asyncio.TimeoutError:
        logging.error(f"API request timed out: {url}")
        return None
    except aiohttp.ClientError as e:
        logging.error(f"API request failed: {e}")
        return None


# Usage in commands:

# 1. Check rate limit
allowed, error_msg = await check_api_limit(api_limiter_nasa, "NASA API")
if not allowed:
    await safe_send(message, content=error_msg)
    return

# 2. Make request
data = await api_request(
    "https://api.nasa.gov/planetary/apod",
    params={"api_key": NASA_API_KEY}
)

# 3. Build embed from response
if data:
    embed = discord.Embed(
        title=data.get('title', 'Astronomy Picture of the Day'),
        description=data.get('explanation', 'No explanation available.'),
        color=discord.Color.blue()
    )
    await safe_send(message, embed=embed)
```

**Integrated APIs:**

- NASA APOD
- NASA Mars Rover
- NASA Asteroids
- Exoplanet Archive TAP (IPAC Caltech)
- OpenWeatherMap

**Pattern:**
- 🔑 API keys from environment variables (`.env`)
- 🪣 Rate limit check before every request
- ⏱️ Per-API timeout configuration
- 🔄 Consistent error handling (`TimeoutError`, `ClientError`, non-200 status)
- 📊 Response data transformed into Discord embeds
---

## 💡 Practices Used

### Code Quality
- ✅ Type hints for better code clarity
- ✅ Comprehensive error handling with specific exception types
- ✅ Input validation and sanitization
- ✅ Consistent code formatting and naming conventions

### Security
- 🔒 No hardcoded secrets (environment variables via `.env`)
- 🔒 Multi-layer input validation (blacklist + whitelist)
- 🔒 Rate limiting and cooldowns at multiple levels
- 🔒 Permission checks before every privileged action
- 🔒 Timeout protection for calculations and API calls
- 🔒 Path traversal prevention for file operations

### Performance
- ⚡ Async/await for non-blocking I/O
- ⚡ Efficient data structures (sets for lookups, dicts for routing)
- ⚡ Platform-aware resource limits (Pi vs. desktop)
- ⚡ Duplicate detection to avoid unnecessary API calls

### Maintainability
- 📦 Modular architecture (separate files per feature)
- 📦 Centralized configuration management (JSON-based)
- 📦 Structured logging with daily rotation
- 📦 Per-server configuration with auto-creation

---

## 🎓 Learning Resources

If you're interested in building similar bots, check out:

- **Discord.py Documentation:** https://discordpy.readthedocs.io/
- **Discord API Documentation:** https://discord.com/developers/docs
- **Python Async Programming:** https://docs.python.org/3/library/asyncio.html

---

<div align="center">

**Made with ❤️ in Germany 🇩🇪**

[Back to README](./README.md)

</div>
