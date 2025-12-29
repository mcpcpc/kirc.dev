---
layout: default
title: Homepage
---

# Welcome to kirc

**kirc** is a tiny, dependency-light IRC client that follows the “Keep It Simple, Stupid” (KISS) philosophy. It’s designed for users who prefer a minimal, keyboard-driven IRC experience in a terminal environment.

## What is IRC?

IRC (Internet Relay Chat) is one of the oldest forms of real-time text communication on the internet. Think of it as the grandfather of modern chat applications like Slack or Discord. IRC allows people to communicate in group channels or privately, and it’s still widely used by open-source communities, tech enthusiasts, and hobbyists worldwide. 

## Why kirc?

In a world of complex, feature-heavy applications, kirc takes a refreshingly different approach: 

### 🚀 Lightweight & Fast

kirc is written in pure C with minimal dependencies. The entire codebase is small and portable, meaning it runs quickly even on older or resource-constrained systems. 

### ⌨️ Keyboard-Driven

Everything in kirc is designed to be controlled from your keyboard. No mouse required.  This makes it incredibly efficient once you learn the simple key bindings.

### 🔧 Unix Philosophy

kirc reads from STDIN and prints to STDOUT, allowing you to pipe, filter, and manipulate IRC traffic using standard Unix tools.  This makes it incredibly flexible and composable with other programs.

### 📦 Easy to Build

With a simple `make` command, you can build kirc from source. No complex build systems or package managers required.

## Key Features

- **Small, portable C codebase** with minimal runtime requirements
- **Keyboard-centric editing** and navigation
- **Simple command and message aliases** for fast interaction
- **Lightweight build** using a standard Makefile
- **DCC file transfer support** including XDCC
- **SASL authentication** for secure connections
- **Environment variable configuration** for persistent settings

## Quick Start

Getting started with kirc is easy!  Here’s how to connect to an IRC server in just a few steps:

### 1. Install kirc

```bash
git clone https://github.com/mcpcpc/kirc
cd kirc/
make
sudo make install
```

### 2. Connect to IRC

```bash
kirc your_nickname
```

That’s it! You’re now connected to the default server (irc.libera.chat) with your chosen nickname.

### 3. Start Chatting

Once connected, you can: 
- Type a message and press Enter to send it to the current channel
- Use `/join #channelname` to join a channel
- Use `@username Hello! ` to send a private message

## Example Sessions

**Connect to Libera Chat (default):**
```bash
kirc alice
```

**Connect to a specific server and channels:**
```bash
kirc -s irc.example.org -p 6667 -c “#general,#help” alice
```

## Getting Help

- 📖 [Read the full documentation](/documentation)
- 🐛 [Report issues on GitHub](https://github.com/mcpcpc/kirc/issues)
- 💻 [View the source code](https://github.com/mcpcpc/kirc)

## License

kirc is open source software.  See the [LICENSE](https://github.com/mcpcpc/kirc/blob/main/LICENSE) file for details.

---

*kirc is maintained by [Michael Czigler](https://github.com/mcpcpc)*