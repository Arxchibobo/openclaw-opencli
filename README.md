# openclaw-opencli

> A Claude Code skill that turns any website into a command-line interface — powered by [OpenClaw](https://github.com/Arxchibobo).

## Overview

**opencli** is an OpenClaw skill that lets you operate social platforms and websites from the terminal by reusing your existing Chrome login sessions. No credential management, no bot detection — just your real browser session, exposed as CLI commands.

It covers 18+ platforms including Bilibili, Zhihu, Xiaohongshu, X/Twitter, Reddit, GitHub, YouTube, and more. AI can also auto-generate adapters for new platforms on demand.

## Features

- **18+ platform adapters** — social media, news, finance, job boards, and shopping
- **Reuses Chrome sessions** — zero risk of account lockouts; operates as a real logged-in user
- **Multiple output formats** — table, JSON, YAML, Markdown, CSV
- **AI self-iteration** — auto-discover new websites and generate adapters via CLI-ONESHOT or CLI-EXPLORER mode
- **OpenClaw skill integration** — invokable directly from Claude Code as `/opencli`

## Supported Platforms

| Platform | Commands | Auth |
|----------|----------|------|
| Bilibili (B站) | `hot` `search` `me` `favorite` `history` `feed` `subtitle` `ranking` `following` `user-videos` | Login |
| Zhihu (知乎) | `hot` `search` `question` | Login |
| Xiaohongshu (小红书) | `search` `notifications` `feed` `user` | Login |
| X / Twitter | `trending` `bookmarks` `profile` `search` `timeline` `thread` `following` `followers` `post` `reply` `like` `follow` `unfollow` | Login |
| Reddit | `hot` `frontpage` `popular` `search` `subreddit` `read` `upvote` `save` `comment` | Login |
| Weibo (微博) | `hot` | Login |
| YouTube | `search` | Login |
| GitHub | `search` | Public |
| Hacker News | `top` | Public |
| V2EX | `hot` `latest` `topic` `daily` | Public / Login |
| Xueqiu (雪球) | `feed` `hot-stock` `hot` `search` `stock` `watchlist` | Login |
| Reuters | `search` | Login |
| BBC | `news` | Public |
| Smzdm (什么值得买) | `search` | Login |
| Ctrip (携程) | `search` | Login |
| Boss Zhipin (Boss直聘) | `search` `detail` | Login |
| Coupang | `search` `add-to-cart` | Login |
| Yahoo Finance | `quote` | Login |

## Requirements

- [Node.js](https://nodejs.org) with npm
- Google Chrome running and logged into target websites
- [Playwright MCP Bridge](https://github.com/Arxchibobo) browser extension installed in Chrome

## Installation

The CLI binary is installed at:

```
~/.npm-global/bin/opencli
```

On first use, run setup to configure your token:

```bash
opencli setup
```

> Keep your Chrome session active and do not clear cookies — the tool depends on your existing login sessions.

## Usage

```bash
# List all available commands
opencli list

# Bilibili trending
opencli bilibili hot --limit 10

# X/Twitter search
opencli twitter search "AI agent" --limit 5

# Xiaohongshu search
opencli xiaohongshu search "skincare recommendations"

# Zhihu hot topics (JSON output)
opencli zhihu hot -f json

# Reddit hot posts (Markdown output)
opencli reddit hot --limit 10 -f md

# Yahoo Finance quote
opencli yahoo-finance quote AAPL
```

## Output Formats

```bash
opencli <platform> <command> -f table   # terminal table (default)
opencli <platform> <command> -f json    # JSON
opencli <platform> <command> -f yaml    # YAML
opencli <platform> <command> -f md      # Markdown
opencli <platform> <command> -f csv     # CSV
```

## AI Self-Iteration

opencli can auto-generate adapters for new platforms using two modes:

- **Quick mode** (CLI-ONESHOT): provide a URL and a one-line goal
- **Full mode** (CLI-EXPLORER): browser-based exploration with a 5-layer authentication strategy

Refer to `CLI-ONESHOT.md` and `CLI-EXPLORER.md` for details.

## Using as an OpenClaw Skill

This repository is an OpenClaw skill. Once registered, Claude Code can invoke it via:

```
/opencli
```

The skill activates when you need to batch-read or operate on social platform data (trending, search, feeds, comments, etc.) — especially for operations that require login state.

**Use this skill when:** you need bulk access to authenticated platform data via CLI.
**Use other tools when:** simple page extraction (use `web_fetch`) or complex UI interaction (use browser tools).
