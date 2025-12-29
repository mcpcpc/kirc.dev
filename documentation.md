---
layout: default
title:  Documentation - kirc
---

# Documentation

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

Before you can install kirc, you’ll need a few basic development tools on your system.  Don’t worry if you’re not familiar with these—they’re standard tools that come pre-installed on most Unix-like systems, and they’re easy to install if you don’t have them. 

You’ll need a C compiler, which is the program that transforms kirc’s source code into an executable program your computer can run. The most common C compilers are GCC (GNU Compiler Collection) and Clang. Either one will work fine. 

You’ll also need the `make` utility, which automates the build process. Instead of typing out long compiler commands, you can simply type `make` and it handles everything for you.

Finally, you’ll need Git to download the source code from GitHub. Git is a version control system that developers use to track changes to their code and collaborate with others.

**Installing prerequisites on Debian or Ubuntu:**

If you’re running Debian, Ubuntu, Linux Mint, or any other Debian-based distribution, you can install everything you need with the following commands.  Open your terminal and type:

```bash
sudo apt update
sudo apt install build-essential git
```

The `build-essential` package includes GCC, make, and other tools commonly needed to compile software from source. The `sudo` command runs the installation with administrator privileges, so you’ll be prompted for your password. 

**Installing prerequisites on macOS:**

On macOS, you’ll want to install the Xcode Command Line Tools, which include a C compiler and make. Open Terminal and run: 

```bash
xcode-select —install
```

A dialog box will appear asking if you want to install the tools. Click “Install” and wait for the download to complete.  This can take a few minutes depending on your internet connection.

If you don’t already have Git installed, the easiest way to get it is through Homebrew, a popular package manager for macOS.  If you don’t have Homebrew, you can install it by visiting brew.sh, but Git is usually included with the Xcode tools.

**Installing prerequisites on Fedora:**

Fedora users can install the necessary tools with the DNF package manager: 

```bash
sudo dnf install gcc make git
```

**Installing prerequisites on Arch Linux:**

Arch Linux users can install the base development tools with pacman:

```bash
sudo pacman -S base-devel git
```

The `base-devel` group includes GCC, make, and other essential build tools. 

### Building from Source

Once you have the prerequisites installed, building kirc is straightforward. The process involves downloading the source code, compiling it, and optionally installing it to your system.

**Step 1: Clone the repository**

First, you need to download the kirc source code from GitHub. Open your terminal and navigate to a directory where you’d like to store the source code. Your home directory or a dedicated “projects” folder works well.  Then run:

```bash
git clone https://github.com/mcpcpc/kirc
```

This command creates a new folder called “kirc” containing all the source code and related files.

**Step 2: Navigate to the directory**

Change into the newly created kirc directory: 

```bash
cd kirc/
```

**Step 3: Build kirc**

Now you can compile the source code into an executable program. Simply run:

```bash
make
```

The make utility reads the instructions in the Makefile and compiles the source code.  You’ll see some output as the compiler does its work.  If everything goes well, you’ll have a new executable file called `kirc` in the current directory.

**Step 4: Install system-wide (optional)**

If you want to be able to run kirc from anywhere on your system without specifying the full path, you can install it to a system directory. This step requires administrator privileges: 

```bash
sudo make install
```

By default, this copies the kirc executable to `/usr/local/bin/`, which is typically in your system’s PATH. After installation, you can run kirc from any directory by simply typing `kirc`.

If you prefer not to install system-wide, you can always run kirc directly from the build directory by typing `./kirc` (the `./` tells your shell to look in the current directory).

### Verifying Your Installation

After installation, it’s a good idea to verify that everything is working correctly. If you installed kirc system-wide, open a new terminal window and type:

```bash
kirc —help
```

If you see usage information and a list of available options, congratulations—kirc is installed and ready to use! 

If you get a “command not found” error, make sure `/usr/local/bin` is in your PATH environment variable, or try running kirc from the build directory with `./kirc`.

---

## Basic Usage

### Understanding IRC

Before diving into kirc specifically, it helps to understand a bit about how IRC works.  IRC, which stands for Internet Relay Chat, is a protocol for real-time text communication.  Unlike modern chat applications that are controlled by a single company, IRC is a decentralized network of servers that anyone can connect to.

When you use IRC, you connect to a server (or a network of servers) and can join various channels, which are like chat rooms focused on different topics. Channel names always start with a hash symbol, like `#linux` or `#music`. You can also send private messages directly to other users.

Every user on IRC has a nickname, which is the name that others see when you send messages.  Nicknames must be unique on each network, so if someone else is already using the name you want, you’ll need to choose a different one.

### Connecting to IRC

Using kirc is refreshingly simple. At its most basic, you only need to provide one thing: a nickname. Open your terminal and type: 

```bash
kirc your_nickname
```

Replace “your_nickname” with whatever name you’d like to use on IRC. Keep in mind that nicknames can only contain letters, numbers, and a few special characters like underscores and hyphens.  They can’t contain spaces. 

When you run this command, kirc connects to the default IRC server, which is irc.libera.chat, on port 6667. Libera Chat is one of the largest and most popular IRC networks, home to thousands of open-source project channels and communities.

### The Command Line Syntax

While connecting with just a nickname works great for getting started, kirc offers several options for customizing your connection. The full command syntax looks like this:

```
kirc [-s server] [-p port] [-c channels] [-r realname]
     [-u username] [-k password] [-a auth] <nickname>
```

Everything inside square brackets is optional. The only required argument is your nickname, which appears at the end without brackets.  We’ll explore each of these options in detail in the Command Line Options section. 

### Your First IRC Session

Let’s walk through a complete first session with kirc. This will help you understand the basic workflow and get comfortable with the interface. 

**Starting the connection:**

Open your terminal and connect to Libera Chat with a nickname of your choice:

```bash
kirc mynickname
```

After a moment, you’ll see connection messages scroll by as kirc establishes a connection to the server. You’ll see information about the network, the message of the day (MOTD), and other server announcements. 

**Joining a channel:**

Once connected, you’re not automatically in any channels. To join a channel, use the `/join` command followed by the channel name.  Let’s join the #libera channel, which is a general discussion channel:

```
/join #libera
```

You’ll see a message confirming that you’ve joined the channel, and you might see messages from other users who are currently chatting.

**Sending a message:**

To send a message to the channel, simply type your message and press Enter.  There’s no special command needed—just type what you want to say: 

```
Hello everyone! I’m new to IRC and trying out kirc. 
```

Your message will be sent to the channel and everyone there will see it. 

**Sending a private message:**

Sometimes you want to send a message to a specific person rather than the whole channel. You can do this using the @ symbol followed by the person’s nickname:

```
@someuser Hey, I had a question for you! 
```

This sends a private message to “someuser” that only they can see.

**Leaving a channel:**

When you’re done with a channel, you can leave it with the `/part` command:

```
/part #libera
```

You can optionally include a message explaining why you’re leaving:

```
/part #libera Goodbye for now!
```

**Disconnecting:**

When you’re ready to end your IRC session, you can disconnect gracefully with the `/quit` command:

```
/quit See you next time!
```

This sends a quit message to the server and closes the connection.  Alternatively, if you need to exit immediately, you can press `CTRL+C` to force quit.

---

## Command Line Options

kirc accepts several command-line options that let you customize your connection.  These options are specified before your nickname when you launch kirc. Let’s explore each one in detail. 

### Specifying a Server with -s

By default, kirc connects to irc.libera. chat, but you can connect to any IRC server using the `-s` option. Different IRC networks have different communities and channels, so you might want to connect to a specific network where your friends or a project community hangs out.

To connect to a different server, use the `-s` flag followed by the server’s hostname:

```bash
kirc -s irc.rizon.net mynickname
```

This connects you to the Rizon network instead of Libera Chat.  Some other popular IRC networks include EFnet, DALnet, and OFTC.  Each network has its own set of channels and communities. 

### Specifying a Port with -p

IRC servers typically listen on port 6667 for unencrypted connections, and kirc uses this as the default.  However, some servers use different ports, and if you’re connecting through an SSL tunnel (more on that later), you might need to specify a different port.

To connect on a specific port, use the `-p` flag: 

```bash
kirc -s irc.example.org -p 6697 mynickname
```

Port 6697 is commonly used for SSL-encrypted IRC connections, though you’ll need to set up an SSL tunnel separately since kirc doesn’t handle encryption directly.

### Auto-joining Channels with -c

If you always join the same channels when you connect to IRC, you can save time by telling kirc to join them automatically. The `-c` option lets you specify one or more channels to join immediately after connecting. 

To auto-join a single channel: 

```bash
kirc -c “#linux” mynickname
```

Note that you should put the channel name in quotes because the hash symbol has special meaning in most shells.

To auto-join multiple channels, separate them with commas: 

```bash
kirc -c “#linux,#python,#music” mynickname
```

An important thing to know: the first channel in the list becomes your default target for messages. This means when you type a message without specifying a target, it goes to that first channel.

### Setting Your Real Name with -r

On IRC, users have both a nickname (which everyone sees when you chat) and a “real name” field (which people can see if they look up information about you with the WHOIS command). By default, kirc uses your nickname as your real name, but you can set a different value. 

To set your real name: 

```bash
kirc -r “Jane Smith” mynickname
```

The real name can contain spaces and doesn’t have the same restrictions as nicknames. Some people use their actual name, while others use a description or leave it blank.

### Setting Your Username with -u

The username, also called the “ident,” is another piece of information associated with your connection. It appears in your hostmask, which is the string that identifies you on IRC (it looks something like `nickname!username@hostname`). By default, kirc uses your nickname as the username. 

To set a different username:

```bash
kirc -u jsmith mynickname
```

The username is mostly relevant for server administrators and doesn’t affect normal chatting.

### Providing a Server Password with -k

Some IRC servers require a password to connect. This is different from your NickServ password (which authenticates your nickname)—it’s a password required just to access the server at all. This is relatively uncommon but is sometimes used for private or restricted servers.

If a server requires a password: 

```bash
kirc -k secretpassword mynickname
```

### SASL Authentication with -a

SASL (Simple Authentication and Security Layer) is a method for authenticating with IRC services during the connection process, before you even join any channels. This is useful for networks that require authentication, and it’s more secure than sending your password in a regular message after connecting.

The `-a` option takes an argument in the format `MECHANISM:TOKEN`, where MECHANISM is the authentication method (usually “PLAIN”) and TOKEN is a Base64-encoded string containing your credentials.

For example:

```bash
kirc -a PLAIN:YWxpY2UAYWxpY2UAcGFzc3dvcmQ= alice
```

Generating the authentication token requires encoding your credentials in a specific format. See the Advanced Usage section for detailed instructions on creating SASL tokens.

---

## Environment Variables

If you find yourself typing the same options every time you start kirc, you can set default values using environment variables.  These are like preferences that kirc reads when it starts up.  Any command-line options you specify will override the environment variable values, so you can still customize individual sessions.

### Available Environment Variables

kirc recognizes several environment variables that correspond to command-line options. 

The `KIRC_SERVER` variable sets the default IRC server hostname. If you always connect to the same server, setting this variable means you don’t need to use the `-s` option every time.

The `KIRC_PORT` variable sets the default port number. This is useful if you always connect through an SSL tunnel on a non-standard port. 

The `KIRC_CHANNELS` variable specifies default channels to auto-join, using the same comma-separated format as the `-c` option.

The `KIRC_REALNAME` variable sets your default real name. 

The `KIRC_USERNAME` variable sets your default username (ident).

The `KIRC_PASSWORD` variable sets a default server password.

The `KIRC_AUTH` variable sets a default SASL authentication token.

### Setting Environment Variables Temporarily

If you want to set an environment variable for just one session, you can do so directly in your terminal before running kirc. For example: 

```bash
export KIRC_SERVER=irc.libera.chat
export KIRC_CHANNELS=“#mychannel,#anotherchannel”
kirc mynickname
```

The `export` command sets the variable for the current shell session.  Once you close the terminal, these settings are lost. 

You can also set variables for a single command by putting them on the same line: 

```bash
KIRC_SERVER=irc.libera.chat KIRC_PORT=6667 kirc mynickname
```

### Setting Environment Variables Permanently

To make your settings permanent, you need to add them to your shell’s configuration file. This file is read every time you open a new terminal window. 

If you’re using Bash (the default shell on most Linux distributions), add your settings to the file `~/.bashrc`. Open it in your favorite text editor: 

```bash
nano ~/.bashrc
```

Add lines at the end of the file for each variable you want to set: 

```bash
export KIRC_SERVER=“irc.libera.chat”
export KIRC_PORT=“6667”
export KIRC_CHANNELS=“#favorite,#channels”
export KIRC_REALNAME=“Your Name”
```

Save the file and exit the editor. For the changes to take effect in your current terminal, you need to reload the configuration: 

```bash
source ~/.bashrc
```

Any new terminal windows you open will automatically have these settings.

If you’re using Zsh (the default shell on macOS), the process is the same but you edit `~/.zshrc` instead of `~/.bashrc`.

---

## Commands and Aliases

Once you’re connected to IRC, you interact with the server and other users by typing commands and messages. kirc uses a simple, intuitive command system that will feel familiar if you’ve used other IRC clients.

### Sending Messages to the Current Target

The most common thing you’ll do on IRC is send messages.  kirc maintains a “current target,” which is the channel or user that your messages go to by default. When you auto-join channels with the `-c` option, the first channel becomes your current target.

To send a message to your current target, simply type the message and press Enter: 

```
Hello everyone, how’s it going?
```

There’s no command prefix needed—kirc knows that plain text should be sent as a message. 

### Sending Messages to a Specific Target

Sometimes you want to send a message to someone other than your current target. Maybe you’re chatting in one channel but want to send a quick message to another channel or to a specific user. You can do this using the @ symbol:

```
@#otherchannel Hey folks in the other channel!
```

```
@username Hey, can you help me with something?
```

The message goes to the specified target, but your current target doesn’t change. Your next message (without the @ prefix) will still go to your original target.

### Changing Your Current Target

If you want to switch which channel or user receives your messages by default, use the `/set` command:

```
/set #newchannel
```

Now when you type a message without a target prefix, it goes to #newchannel.  You can also set a user as your target for extended private conversations:

```
/set username
```

### Sending Raw IRC Commands

IRC has a rich set of commands for doing things like joining channels, changing your nickname, and getting information about users. kirc lets you send any IRC command by prefixing it with a forward slash. 

For example, to join a channel:

```
/join #newchannel
```

To leave a channel:

```
/part #channelname
```

To change your nickname:

```
/nick newnickname
```

To get information about a user:

```
/whois username
```

To see a list of available channels (warning—this can be a very long list on large networks):

```
/list
```

To view or change a channel’s topic: 

```
/topic #channelname
```

Or to set a new topic (if you have permission):

```
/topic #channelname This is the new topic! 
```

To disconnect from the server:

```
/quit Goodbye message here
```

Any valid IRC command can be sent this way.  If you’re curious about what commands are available, the IRC protocol documentation describes them all, though the ones listed here cover most everyday needs.

### Sending Actions with /me

Sometimes you want to describe what you’re doing rather than just saying something. This is called an “action” and is displayed differently in most IRC clients. For example, instead of seeing: 

```
<yournick> waves hello
```

Other users see:

```
* yournick waves hello
```

To send an action, use the `/me` command:

```
/me waves hello
```

```
/me is thinking about what to have for lunch
```

Actions are a fun way to add expression to your conversations. 

### Sending CTCP Commands with /ctcp

CTCP, which stands for Client-To-Client Protocol, is a way to send special requests to other IRC users. The most common uses are requesting information about someone’s IRC client or initiating file transfers.

To send a CTCP command, use the `/ctcp` command followed by the target nickname and the CTCP command: 

```
/ctcp username VERSION
```

This asks the user’s IRC client to report its name and version.  Common CTCP commands include VERSION (client version), TIME (user’s local time), PING (response time), and CLIENTINFO (list of supported CTCP commands).

CTCP is also used for DCC (Direct Client-to-Client) file transfers, which we’ll cover in a later section.

---

## Key Bindings

kirc is designed to be used entirely from the keyboard, with no mouse required. The key bindings are designed to be intuitive and similar to other command-line programs you might be familiar with.

### Moving the Cursor

When you’re typing a message, you might need to go back and fix a typo or insert something in the middle.  kirc provides several ways to move the cursor. 

The left and right arrow keys move the cursor one character at a time in the corresponding direction. This is the most straightforward way to navigate within your current line.

If you need to jump to the beginning of the line, press the Home key. On some keyboards this might be labeled differently or require a function key combination.  If Home doesn’t work, you can also use the escape sequence ESC followed by [ and H. 

Similarly, the End key jumps to the end of the line. The escape sequence ESC [ F also works.

### Navigating Command History

kirc remembers the commands and messages you’ve typed, allowing you to recall and reuse them.  This is especially useful when you need to repeat a command or fix a typo in something you just sent.

Press the up arrow key to go back through your history. Each press shows the previous command or message. 

Press the down arrow key to go forward through your history. If you’ve gone back several commands and want to return to what you were typing, keep pressing down until you get there.

### Deleting Text

When you need to delete text, kirc provides a few options depending on what you want to remove.

The Backspace key deletes the character immediately before the cursor. This is the most common way to fix typos as you type.

The Delete key removes the character at the cursor position (the character the cursor is on or immediately after, depending on your terminal).

If you want to clear the entire line and start over, press CTRL+U. This deletes everything you’ve typed on the current line, giving you a fresh start. 

### Exiting kirc

When you’re done with your IRC session, you have a couple of options for exiting. 

The graceful way to exit is to type the `/quit` command, optionally with a message that other users will see: 

```
/quit Goodnight everyone!
```

If you need to exit immediately without sending a quit message, press CTRL+C.  This forces kirc to terminate right away.  Use this if the normal quit isn’t working or if you need to disconnect quickly.

—

## DCC File Transfers

DCC, which stands for Direct Client-to-Client, is a protocol that allows IRC users to send files directly to each other. Unlike regular IRC messages that go through the server, DCC transfers happen directly between your computer and the other user’s computer, which is faster and more efficient for large files.

kirc includes support for receiving files via DCC, including the popular XDCC protocol used by file-sharing bots on many IRC networks.

### Receiving Files

When another IRC user sends you a file via DCC, kirc automatically detects the incoming transfer request and begins downloading the file. You’ll see a message like this: 

```
dcc:  receiving <filename> from <sender> (<size> bytes)
```

The file is saved to your current working directory—that is, the directory you were in when you started kirc.  As the download progresses, you’ll see status updates, and a final message when the transfer is complete.

You don’t need to do anything to accept the transfer; kirc handles it automatically. If you don’t want to receive files, simply don’t run kirc from a directory where you don’t want files saved.

### XDCC Requests

XDCC is an extension to DCC that’s commonly used by file-sharing bots on IRC.  These bots maintain lists of files that users can request.  When you request a file, the bot initiates a DCC transfer to send it to you.

To request a file from an XDCC bot, you send a CTCP message in a specific format.  Use the `/ctcp` command with the bot’s nickname, followed by “XDCC SEND” and the pack number:

```
/ctcp BotName XDCC SEND #42
```

The pack number (42 in this example) refers to a specific file in the bot’s list.  Bots typically have a command to show their file list, often triggered by messaging the bot with “xdcc list” or similar.

After you send the request, the bot will initiate a DCC transfer, and kirc will automatically start receiving the file.

### Understanding DCC Limitations

There are a few things to keep in mind when using DCC transfers with kirc. 

kirc supports up to 16 simultaneous DCC transfers.  If you try to receive more files at once, additional transfers will fail until some of the current ones complete.

Files are saved with their original filenames to your current working directory. If a file with the same name already exists, it may be overwritten, so be careful about where you run kirc if you’re expecting to receive files. 

Because DCC transfers happen directly between computers, they may not work if you’re behind certain types of firewalls or NAT devices. If transfers fail to start, network configuration might be the issue. 

### Preparing to Receive Files

If you know you’re going to be receiving files via DCC, it’s a good practice to start kirc from a directory where you want those files saved. For example: 

```bash
cd ~/Downloads
kirc mynickname
```

Now any files you receive will be saved to your Downloads folder, keeping them organized and easy to find. 

---

## Advanced Usage

Once you’re comfortable with the basics, kirc offers several ways to extend its functionality and integrate it with other tools.  This section covers some advanced techniques that power users will find useful.

### Connecting with TLS/SSL Encryption

IRC traffic is unencrypted by default, which means anyone who can intercept your network traffic can read your messages.  Many IRC networks offer encrypted connections on port 6697 to address this concern.

kirc itself doesn’t handle encryption directly—this keeps the code simple and focused.  However, you can easily add encryption using a tool called `socat`, which can create encrypted tunnels. 

First, you need to have socat installed.  On Debian/Ubuntu: 

```bash
sudo apt install socat
```

On macOS with Homebrew: 

```bash
brew install socat
```

To connect to an IRC server with SSL encryption, you’ll set up a local tunnel. Open one terminal window and run:

```bash
socat tcp-listen:6667,reuseaddr,fork,bind=127.0.0.1 ssl:irc.libera.chat:6697
```

This command creates a local server on port 6667 that forwards traffic to irc.libera. chat’s SSL port (6697), handling all the encryption transparently.

Now, in another terminal window, connect kirc to your local tunnel:

```bash
kirc -s 127.0.0.1 -p 6667 mynickname
```

kirc thinks it’s connecting to a local server, but socat is forwarding everything securely to the real IRC server.  Your messages are encrypted between your computer and the IRC network.

### Connecting Through a Proxy

If you need to connect to IRC through an HTTP or HTTPS proxy (common in corporate environments), socat can help with this too. 

Set up a proxy tunnel in one terminal:

```bash
socat tcp-listen:6667,fork,reuseaddr,bind=127.0.0.1 \
    proxy:proxyserver. example.com:irc.libera.chat:6667,proxyport=8080
```

Replace `proxyserver.example.com` with your proxy server’s address and `8080` with the proxy port.

Then connect kirc to the tunnel:

```bash
kirc -s 127.0.0.1 -p 6667 mynickname
```

### Generating SASL Authentication Tokens

SASL PLAIN authentication requires a Base64-encoded token that contains your username and password.  The format is `username\0username\0password`, where `\0` represents a null byte.

You can generate this token using Python.  Open a Python interpreter or create a small script:

```python
import base64

username = “yournick”
password = “yourpassword”

# Format: username\x00username\x00password
credentials = f”{username}\x00{username}\x00{password}”
token = base64.b64encode(credentials.encode()).decode()

print(f”PLAIN:{token}”)
```

This will output something like: 

```
PLAIN:eW91cm5pY2sAeW91cm5pY2sAeW91cnBhc3N3b3Jk
```

Use this value with the `-a` option: 

```bash
kirc -a PLAIN:eW91cm5pY2sAeW91cm5pY2sAeW91cnBhc3N3b3Jk yournick
```

### Logging Your IRC Sessions

Since kirc outputs to standard output (STDOUT), you can easily create logs of your IRC sessions using standard Unix tools. The `tee` command is perfect for this—it writes output to a file while still displaying it on your screen.

To create a dated log file:

```bash
kirc mynickname | tee -a irc-$(date +%Y%m%d).log
```

The `-a` flag tells tee to append to the file rather than overwriting it, so you can have multiple sessions in the same day’s log.  The `$(date +%Y%m%d)` part generates the current date in YYYYMMDD format.

For more detailed logs with timestamps, you can pipe through a utility like `ts` (from the moreutils package):

```bash
kirc mynickname | ts ‘[%Y-%m-%d %H:%M:%S]’ | tee -a irc. log
```

### Creating Shell Aliases

If you connect to the same servers with the same settings regularly, shell aliases can save you a lot of typing. Add them to your shell configuration file (~/.bashrc or ~/. zshrc):

```bash
alias irc=‘kirc -s irc.libera. chat -c “#mychannel” mynick’
alias irc-work=‘kirc -s irc.company.com -k serverpassword -c “#team” worknick’
alias irc-gaming=‘kirc -s irc.gamesurge.net -c “#myguild” gamenick’
```

After adding these and reloading your shell config, you can connect to your favorite servers with simple commands:

```bash
irc
irc-work
irc-gaming
```

### Creating a Wrapper Script

For even more sophisticated setups, you might want a wrapper script that handles multiple concerns like logging, directory setup, and environment configuration. Here’s an example: 

```bash
#!/bin/bash
# Save as ~/bin/myirc and make executable with:  chmod +x ~/bin/myirc

# Configuration
IRC_LOG_DIR=“$HOME/irc-logs”
IRC_SERVER=“irc.libera.chat”
IRC_CHANNELS=“#channel1,#channel2”
IRC_NICK=“mynickname”

# Create log directory if it doesn’t exist
mkdir -p “$IRC_LOG_DIR”

# Change to a safe directory for any DCC downloads
cd “$HOME/Downloads”

# Start kirc with logging
kirc -s “$IRC_SERVER” -c “$IRC_CHANNELS” “$IRC_NICK” \
    | tee -a “$IRC_LOG_DIR/session-$(date +%Y%m%d-%H%M%S).log”
```

This script ensures your logs are organized in a dedicated directory, DCC downloads go to your Downloads folder, and each session is logged with a timestamp.

—

## Troubleshooting

Even with a simple client like kirc, you might occasionally encounter issues. This section covers common problems and their solutions.

### Connection Refused

If you see a “connection refused” error when trying to connect, it means kirc couldn’t establish a connection to the IRC server. There are several possible causes. 

First, double-check that you have the correct server address.  A typo in the hostname will prevent connection. Try pinging the server to verify it’s reachable:

```bash
ping irc.libera.chat
```

Second, make sure you’re using the correct port. The default port 6667 works for most servers, but some use different ports.  Check the network’s website for connection information. 

Third, your network might be blocking IRC traffic. Some corporate and school networks block the ports used by IRC.  You might need to use a VPN or connect through an SSL tunnel on a different port. 

Finally, the server itself might be down. IRC servers occasionally go offline for maintenance. Try again later or try a different server on the same network. 

### Nickname Already in Use

If you see a message saying your nickname is already in use, someone else is currently connected with that name. IRC requires unique nicknames on each network. 

The simplest solution is to try a different nickname: 

```bash
kirc different_nickname
```

You can also change your nickname after connecting (though you’ll initially connect with a temporary nick):

```
/nick preferred_nickname
```

On many networks, you can register your nickname with NickServ to reserve it. When you’re using your registered nickname and someone else is using it, you can “ghost” them (disconnect them) after authenticating.  The process varies by network—check the network’s documentation. 

### Messages Not Appearing

If you’re typing messages but they don’t seem to be going anywhere, there are a few things to check. 

Make sure you’ve joined a channel.  If you connected without the `-c` option and haven’t joined any channels, there’s nowhere for your messages to go. Join a channel: 

```
/join #channelname
```

Check your current target with `/set`. If your target is set to a user who’s offline or a channel you’re not in, messages won’t go through.

Some channels are moderated, meaning only certain users can speak. If you’ve joined a moderated channel and don’t have voice (+v), your messages won’t be visible to others.

### Colors or Formatting Not Displaying

kirc uses ANSI escape codes for colors, which should work in most modern terminals. If colors aren’t displaying correctly, your terminal might not be configured properly.

Make sure your TERM environment variable is set to a color-capable value: 

```bash
export TERM=xterm-256color
```

Add this to your shell configuration file to make it permanent.

If you’re connecting through SSH or tmux, make sure those are also configured for 256 colors.

### Text Appears Garbled

If text appears scrambled or contains strange characters, it’s usually an encoding issue. 

Make sure your terminal is using UTF-8 encoding.  Most modern systems default to UTF-8, but it might be set differently on older systems or when connecting remotely.

Try resizing your terminal window, which forces a redraw and sometimes fixes display glitches.

If the problem persists, it might be an issue with your terminal emulator’s font.  Try a different font that has good Unicode support, like DejaVu Sans Mono or a Nerd Font.

### DCC Transfers Not Working

DCC transfers require a direct connection between you and the other user, which can be blocked by firewalls or NAT. 

If you’re behind a router, you might need to configure port forwarding. DCC typically uses ports in a high range (often 1024-65535).

Some IRC networks offer alternative file transfer methods that work better through NAT. Check the network’s documentation. 

If you’re on a restrictive network (like at work or school), DCC transfers might simply not be possible.

—

## Getting Help

If you’ve gone through this documentation and still have questions or are experiencing issues, there are several places to get help. 

The kirc GitHub repository is the primary place for bug reports and feature requests. If you’ve found a bug, please open an issue at https://github.com/mcpcpc/kirc/issues with as much detail as possible about what happened and how to reproduce it. 

After installing kirc, you can read the man page for a quick reference of options and commands:

```bash
man kirc
```

For questions about IRC in general (not specific to kirc), the various IRC networks have help channels.  On Libera Chat, try #libera for general questions. 

---

*This documentation is for kirc version 1.0.0. For the latest updates and source code, visit the [GitHub repository](https://github.com/mcpcpc/kirc).*