---
layout: default
title: Documentation
—-—

# kirc Documentation

This guide will walk you through everything you need to know to use kirc effectively.  Whether you’re new to IRC or just new to kirc, this documentation will help you get started.

---

## Table of Contents

1. [Installation](#installation)
2. [Basic Usage](#basic-usage)
3. [Command Line Options](#command-line-options)
4. [Environment Variables](#environment-variables)
5. [Commands and Aliases](#commands-and-aliases)
6. [Key Bindings](#key-bindings)
7. [DCC File Transfers](#dcc-file-transfers)
8. [Advanced Usage](#advanced-usage)
9. [Troubleshooting](#troubleshooting)

---

## Installation

### Prerequisites

Before installing kirc, make sure you have: 

- A C compiler (like `gcc` or `clang`)
- `make` build tool
- A Unix-like operating system (Linux, macOS, BSD, etc.)

Most Linux distributions and macOS come with these tools pre-installed.  If not, you can install them using your system’s package manager. 

**On Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install build-essential git
```

**On macOS (with Homebrew):**
```bash
xcode-select —install
brew install git
```

**On Fedora:**
```bash
sudo dnf install gcc make git
```

**On Arch Linux:**
```bash
sudo pacman -S base-devel git
```

### Building from Source

1. **Clone the repository:**
   ```bash
   git clone https://github.com/mcpcpc/kirc
   ```

2. **Navigate to the directory:**
   ```bash
   cd kirc/
   ```

3. **Build kirc:**
   ```bash
   make
   ```

4. **Install system-wide (optional):**
   ```bash
   sudo make install
   ```

   This installs kirc to `/usr/local/bin/` by default.

5. **Or run directly from the build directory:**
   ```bash
   ./kirc
   ```

### Verifying Installation

After installation, verify kirc is working: 

```bash
kirc —help
```

If you see the usage information, you’re ready to go!

---

## Basic Usage

### Connecting to IRC

At minimum, you only need to provide a nickname to connect: 

```bash
kirc your_nickname
```

This connects you to the default server (`irc.libera.chat`) on port `6667`.

### The Command Line Syntax

The full command syntax is:

```
kirc [-s server] [-p port] [-c channels] [-r realname]
     [-u username] [-k password] [-a auth] <nickname>
```

Let’s break this down: 
- Everything in `[ ]` is optional
- `<nickname>` is required - this is the name others will see when you chat

### Your First Connection

1. **Open your terminal**

2. **Connect to Libera Chat** (a popular IRC network):
   ```bash
   kirc mynickname
   ```

3. **Join a channel** after connecting:
   ```
   /join #libera
   ```

4. **Say hello! **
   ```
   Hello everyone!
   ```

5. **Quit when you’re done:**
   ```
   /quit Goodbye!
   ```
   Or press `CTRL+C` to force quit.

---

## Command Line Options

Here’s a detailed explanation of all available options: 

### -s server

Specifies the IRC server hostname to connect to.

**Default:** `irc.libera.chat`

**Example:**
```bash
kirc -s irc.rizon.net mynickname
```

### -p port

Specifies the IRC server port. 

**Default:** `6667`

**Example:**
```bash
kirc -s irc.example.org -p 6697 mynickname
```

### -c channel(s)

Specifies the channel(s) to automatically join after connecting.  You can specify multiple channels separated by commas. 

> **Note:** The first channel in the list becomes your default messaging target.

**Example - Single channel:**
```bash
kirc -c “#general” mynickname
```

**Example - Multiple channels:**
```bash
kirc -c “#general,#help,#random” mynickname
```

### -r realname

Sets your “real name” that others can see with the WHOIS command.

**Default:** Uses your nickname

**Example:**
```bash
kirc -r “John Doe” mynickname
```

### -u username

Sets your username (ident) for the connection.

**Default:** Uses your nickname

**Example:**
```bash
kirc -u john mynickname
```

### -k password

Specifies a server password (if the server requires one).

**Example:**
```bash
kirc -k mysecretpassword mynickname
```

### -a auth

Specifies SASL authentication mechanism and token.  This is used for authenticating with services like NickServ automatically.

**Format:** `MECHANISM:BASE64_TOKEN`

**Example:**
```bash
kirc -a PLAIN:YWxpY2UAYWxpY2UAcGFzc3dvcmQ= alice
```

See the [Advanced Usage](#advanced-usage) section for details on generating authentication tokens.

—--

## Environment Variables

Instead of typing options every time, you can set defaults using environment variables.  These are overridden by command-line options when specified.

| Variable | Description |
| `KIRC_SERVER` | Default IRC server hostname |
| `KIRC_PORT` | Default server port |
| `KIRC_CHANNELS` | Default channels to join (comma separated) |
| `KIRC_REALNAME` | Default real name |
| `KIRC_USERNAME` | Default username |
| `KIRC_PASSWORD` | Default password |
| `KIRC_AUTH` | Default SASL authentication token |

### Setting Environment Variables

**Temporarily (current session only):**
```bash
export KIRC_SERVER=irc.libera.chat
export KIRC_CHANNELS=“#mychannel”
kirc mynickname
```

**Permanently (add to your shell config file):**

For Bash, add to `~/.bashrc`:
```bash
export KIRC_SERVER=irc.libera.chat
export KIRC_PORT=6667
export KIRC_CHANNELS=“#favorite,#channel”
```

For Zsh, add to `~/.zshrc` instead. 

After editing, reload your config:
```bash
source ~/.bashrc
```

---

## Commands and Aliases

kirc uses a simple command system.  Here are all the commands you need to know:

### Sending Messages

| Command | Description | Example |
| `<message>` | Send a message to the current target | `Hello everyone!` |
| `@<target> <message>` | Send a message to a specific user or channel | `@alice Hey there!` |

### IRC Commands

| Command | Description | Example |
| `/<command>` | Send a raw IRC command | `/join #newchannel` |
| `/set <target>` | Set the default message target | `/set #general` |
| `/me <action>` | Send an action (like emotes) | `/me waves hello` |
| `/ctcp <nick> <cmd>` | Send a CTCP command | `/ctcp alice VERSION` |

### Common Raw IRC Commands

Since kirc lets you send raw IRC commands with `/`, here are the most useful ones: 

| Command | Description | Example |
| `/join` | Join a channel | `/join #help` |
| `/part` | Leave a channel | `/part #help` |
| `/nick` | Change your nickname | `/nick newnickname` |
| `/msg` | Send a private message | `/msg alice Hello!` |
| `/whois` | Get info about a user | `/whois alice` |
| `/quit` | Disconnect from the server | `/quit Goodbye!` |
| `/list` | List available channels | `/list` |
| `/topic` | View or set channel topic | `/topic #channel New topic` |

### Message Target Examples

**Set your default target to a channel:**
```
/set #general
Hello everyone!    <- This goes to #general
```

**Send a quick message to someone else:**
```
@alice Private message to Alice
@#help This goes to #help channel
```

---

## Key Bindings

kirc uses keyboard shortcuts similar to other command-line programs.  Here’s your complete reference:

### Navigation

| Key | Action |
| `←` (Left Arrow) | Move cursor left |
| `→` (Right Arrow) | Move cursor right |
| `Home` | Move cursor to start of line |
| `End` | Move cursor to end of line |

### History

| Key | Action |
| `↑` (Up Arrow) | Previous command in history |
| `↓` (Down Arrow) | Next command in history |

### Editing

| Key | Action |
| `Backspace` | Delete character before cursor |
| `Delete` | Delete character at cursor |
| `CTRL+U` | Delete entire line |

### Control

| Key | Action |
| `CTRL+C` | Force quit kirc |

---

## DCC File Transfers

kirc supports Direct Client-to-Client (DCC) file transfers. This allows you to send and receive files directly from other IRC users.

### Receiving Files

When someone sends you a file via DCC, kirc automatically detects and downloads it: 

```
dcc:  receiving <filename> from <sender> (<size> bytes)
```

Files are saved to your current working directory (the folder where you ran kirc).

### XDCC Requests

XDCC is a protocol used by file-sharing bots on IRC. To request a file:

```
/ctcp <botname> XDCC SEND #<packet_number>
```

**Example:**
```
/ctcp FileBot XDCC SEND #42
```

### DCC Limits

- kirc supports up to **16 simultaneous** DCC transfers
- Files are saved with their original filenames
- Files are saved to your current working directory

### Tips for File Transfers

1. **Change to your downloads folder** before starting kirc if you expect to receive files: 
   ```bash
   cd ~/Downloads
   kirc mynickname
   ```

2. **Check for filename conflicts** - if a file with the same name exists, it may be overwritten

---

## Advanced Usage

### Connecting with TLS/SSL

kirc doesn’t have built-in TLS support, but you can use `socat` to create a secure tunnel:

```bash
# In one terminal, create the tunnel: 
socat tcp-listen:6667,reuseaddr,fork,bind=127.0.0.1 \
    ssl:irc.libera.chat:6697

# In another terminal, connect kirc:
kirc -s 127.0.0.1 -p 6667 mynickname
```

### Connecting Through a Proxy

Use `socat` to connect through an HTTP/HTTPS proxy:

```bash
socat tcp-listen:6667,fork,reuseaddr,bind=127.0.0.1 \
    proxy: <proxyhost>: irc.example.org:6667,proxyport=<proxyport>

kirc -s 127.0.0.1 -p 6667 mynickname
```

### Generating SASL Authentication Tokens

SASL allows you to authenticate with IRC services (like NickServ) during the connection process. 

**Using Python to generate a PLAIN token:**

```python
import base64
# Format: nickname\x00nickname\x00password
token = base64.b64encode(b’alice\x00alice\x00mypassword’)
print(token. decode())
```

**Then use it:**
```bash
kirc -a PLAIN:YWxpY2UAYWxpY2UAbXlwYXNzd29yZA== alice
```

### Logging Your Sessions

Since kirc outputs to STDOUT, you can easily create logs:

```bash
kirc -s irc.libera.chat mynickname | tee -a irc-$(date +%Y%m%d).log
```

This creates a dated log file while still showing output in your terminal.

### Creating Shell Aliases

For servers you connect to frequently, create shell aliases:

**Add to `~/.bashrc` or `~/.zshrc`:**
```bash
alias irc-libera=‘kirc -s irc.libera.chat -c “#mychannel” mynickname’
alias irc-work=‘kirc -s irc.work.com -k mypassword -c “#team” workname’
```

Then just type: 
```bash
irc-libera
```

### Creating a Wrapper Script

For more complex configurations, create a wrapper script:

```bash
#!/bin/bash
# ~/bin/myirc

export KIRC_SERVER=“irc.libera.chat”
export KIRC_PORT=“6667”
export KIRC_CHANNELS=“#channel1,#channel2”

cd ~/irc-logs
kirc “$@“ | tee -a “session-$(date +%Y%m%d-%H%M%S).log”
```

Make it executable:
```bash
chmod +x ~/bin/myirc
```

---

## Troubleshooting

### “Connection refused” error

**Possible causes:**
- The server address is incorrect
- The port is blocked by a firewall
- The server is down

**Solutions:**
1. Verify the server address and port
2. Try a different port (common IRC ports: 6667, 6697 for SSL)
3. Check if your network blocks IRC ports

### “Nickname already in use”

Someone else is using that nickname. Try:
1. Use a different nickname: 
   ```bash
   kirc different_nickname
   ```
2. Or change your nick after connecting:
   ```
   /nick new_nickname
   ```

### Messages not appearing

**Check your target:**
```
/set #channelname
```

Make sure you’ve joined the channel: 
```
/join #channelname
```

### Colors not displaying correctly

kirc uses ANSI escape codes for colors. Make sure: 

1. Your terminal supports 256 colors
2. Set your TERM variable: 
   ```bash
   export TERM=xterm-256color
   ```

### Terminal rendering issues

If text appears garbled: 
1. Try resizing your terminal window
2. Use a monospace font
3. Check your terminal’s character encoding (should be UTF-8)

---

## Getting Help

- **GitHub Issues:** [Report bugs or request features](https://github.com/mcpcpc/kirc/issues)
- **Source Code:** [View on GitHub](https://github.com/mcpcpc/kirc)
- **Man Page:** Run `man kirc` after installation

---

*This documentation is for kirc 1.0.0. For the latest updates, visit the [GitHub repository](https://github.com/mcpcpc/kirc).*