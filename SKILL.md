---
name: opencli
description: "把网站变成命令行接口 — 覆盖 B站、知乎、小红书、X、Reddit、GitHub 等 18+ 平台。复用 Chrome 登录态，零风险。AI 可自动发现新网站并生成适配器。"
---

# OpenCLI — 把任何网站变成 CLI

复用浏览器登录态，通过命令行操作社交平台。无需模拟浏览器，直接指令化。

> **何时使用**: 需要批量查看/操作社交平台数据（热榜、搜索、关注、评论等），特别是需要登录态的操作。
> **何时不用**: 简单网页内容提取用 defuddle/web_fetch；需要复杂页面交互用 browser 工具。
> **前提**: 需要 Chrome 安装 Playwright MCP Bridge 扩展并登录目标网站。

## 安装位置

```
~/.npm-global/bin/opencli
```

## 已覆盖平台

| 平台 | 命令 | 模式 |
|------|------|------|
| B站 | hot/search/me/favorite/history/feed/subtitle/ranking/following/user-videos | 🔐 登录 |
| 知乎 | hot/search/question | 🔐 登录 |
| 小红书 | search/notifications/feed/user | 🔐 登录 |
| X/Twitter | trending/bookmarks/profile/search/timeline/thread/following/followers/post/reply/like/follow/unfollow | 🔐 登录 |
| Reddit | hot/frontpage/popular/search/subreddit/read/upvote/save/comment | 🔐 登录 |
| 微博 | hot | 🔐 登录 |
| YouTube | search | 🔐 登录 |
| GitHub | search | 🌐 公开 |
| HackerNews | top | 🌐 公开 |
| V2EX | hot/latest/topic/daily | 🌐/🔐 |
| 雪球 | feed/hot-stock/hot/search/stock/watchlist | 🔐 登录 |
| Reuters | search | 🔐 |
| BBC | news | 🌐 |
| 什么值得买 | search | 🔐 |
| 携程 | search | 🔐 |
| Boss直聘 | search/detail | 🔐 |
| Coupang | search/add-to-cart | 🔐 |
| Yahoo Finance | quote | 🔐 |

## 核心命令

```bash
# 查看所有可用命令
opencli list

# B站热门
opencli bilibili hot --limit 10

# X/Twitter 搜索
opencli twitter search "AI agent" --limit 5

# 小红书搜索
opencli xiaohongshu search "护肤推荐"

# 知乎热榜
opencli zhihu hot -f json

# Reddit 热门
opencli reddit hot --limit 10 -f md
```

## 输出格式

```bash
opencli <平台> <命令> -f table  # 终端表格（默认）
opencli <平台> <命令> -f json   # JSON
opencli <平台> <命令> -f yaml   # YAML
opencli <平台> <命令> -f md     # Markdown
opencli <平台> <命令> -f csv    # CSV
```

## AI 自迭代 — 生成新平台适配器

```bash
# 快速模式：一个 URL + 一句目标
# 参考 CLI-ONESHOT.md

# 完整模式：浏览器探索 + 5层认证策略
# 参考 CLI-EXPLORER.md
```

## ⚠️ 注意事项

- 需要 Chrome 处于运行状态且已登录目标网站
- 需要安装 Playwright MCP Bridge 扩展
- 首次使用运行 `opencli setup` 配置 token
- 登录态依赖 Chrome session，不要清除 cookie
