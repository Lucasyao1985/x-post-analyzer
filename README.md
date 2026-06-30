<p align="center">
  <a href="https://github.com/Lucasyao1985/x-post-analyzer"><img src="https://opengraph.githubassets.com/1/Lucasyao1985/x-post-analyzer" alt="X/Twitter Post Analyzer" width="100%"></a>
</p>

# X/Twitter Post Analyzer
<p align="center">
  <a href="https://github.com/Lucasyao1985/x-post-analyzer">GitHub</a> | <a href="SKILL.md">SKILL.md</a>
</p>
<p align="center">
  <a href="https://github.com/Lucasyao1985/x-post-analyzer"><img alt="Release version" src="https://img.shields.io/github/v/release/Lucasyao1985/x-post-analyzer?color=brightgreen&label=Latest&style=for-the-badge" /></a>
  <a href="LICENSE"><img alt="License: Unlicense" src="https://img.shields.io/badge/-Unlicense-red.svg?style=for-the-badge" /></a>
  <a href="https://github.com/Lucasyao1985/x-post-analyzer/commits"><img alt="Commits" src="https://img.shields.io/github/commit-activity/m/Lucasyao1985/x-post-analyzer?label=commits&style=for-the-badge" /></a>
  <a href="README.zh-CN.md"><img alt="中文" src="https://img.shields.io/badge/中文-red?style=for-the-badge" /></a>
</p>

---

**X/Twitter Post Analyzer is a [Claude Code](https://claude.ai) skill that fetches and analyzes X/Twitter post content, outputting a structured Chinese report.** One URL in, three tool calls max, zero noise.

<table>
<tr><td><b>Smart fetch with fallback</b></td><td>Tries fxtwitter API first, falls back to WebSearch, then direct fetch. Single agent, sequential retry.</td></tr>
<tr><td><b>Structured Chinese report</b></td><td>Original text, translation, media description, quoted tweets, and a clear plain-language explanation.</td></tr>
<tr><td><b>Minimal tool usage</b></td><td>1-3 tool calls total. Fetch agent uses 1 tool; analyze agent uses zero.</td></tr>
<tr><td><b>Privacy aware</b></td><td>Private accounts and rate limits handled gracefully without breaking.</td></tr>
</table>

---

## Quick Install

```bash
git clone https://github.com/Lucasyao1985/x-post-analyzer.git
```

Place the folder in your Claude Code skills directory:
- **Windows:** `C:\Users\<you>\.claude\skills\`
- **macOS/Linux:** `~/.claude/skills/`

## Usage

Share an X/Twitter URL with Claude:

```
Analyze this post: https://x.com/user/status/123
```

Or ask naturally:

```
What does this tweet say?
```

The skill auto-triggers on X/Twitter links, fetches the content, and produces a structured report covering:

- **Original text** (verbatim)
- **Chinese translation**
- **Media attachments** (type, visual description)
- **Quoted tweets** (full text if any)
- **What the post is saying** (clear multi-paragraph explanation)

## How It Works

```
URL → [Fetch Agent] ──┬─ fxtwitter API (priority)
                       ├─ WebSearch (fallback)
                       └─ Direct fetch (last resort)
         ↓
      [Analyze Agent] → Structured Chinese report
```

### Fetch Strategy (priority order)

1. **fxtwitter API** — returns full JSON (text, media, engagement, user info). Highest success rate.
2. **WebSearch** — searches for the tweet if the API fails.
3. **Direct fetch** — fetches the original x.com URL as a last resort (often blocked).

### Report Sections

| Section | Content |
|---|---|
| Original | Verbatim post text |
| Translation | Full Chinese translation |
| Media | Type, visual description, duration/resolution |
| Quoted | Full text + author of quoted tweet |
| Summary | Multi-paragraph plain-language explanation |

## Project Structure

```
x-post-analyzer/
├── SKILL.md                 # Skill definition
├── README.md                # This file (English)
├── README.zh-CN.md          # Chinese documentation
├── scripts/
│   └── x-post-workflow.js   # Core workflow (v2)
├── references/
│   ├── fetch-strategies.md  # Fetch strategy details
│   └── report-template.md   # Report template
└── assets/
```

## License

Unlicense — see [LICENSE](LICENSE).

Built with [opencode](https://github.com/anomalyco/opencode).