<p align="center">
  <a href="README.md"><img alt="English" src="https://img.shields.io/badge/Lang-English-blue?style=for-the-badge" /></a>
  <a href="README.zh-CN.md"><img alt="中文" src="https://img.shields.io/badge/Lang-中文-red?style=for-the-badge" /></a>
</p>

# X/Twitter 帖子分析器

<p align="center">
  <a href="https://github.com/Lucasyao1985/x-post-analyzer"><img alt="Release version" src="https://img.shields.io/github/v/release/Lucasyao1985/x-post-analyzer?color=brightgreen&label=Latest&style=for-the-badge" /></a>
  <a href="LICENSE"><img alt="License: Unlicense" src="https://img.shields.io/badge/-Unlicense-red.svg?style=for-the-badge" /></a>
  <a href="https://github.com/Lucasyao1985/x-post-analyzer/commits"><img alt="Commits" src="https://img.shields.io/github/commit-activity/m/Lucasyao1985/x-post-analyzer?label=commits&style=for-the-badge" /></a>
</p>

**X/Twitter 帖子分析器是一个 [Claude Code](https://claude.ai) 技能，自动获取并分析 X/Twitter 帖子内容，输出结构化中文报告。** 一个链接，最多 3 次工具调用，零噪音。

<table>
<tr><td><b>智能获取，多重后备</b></td><td>优先使用 fxtwitter API，失败后依次尝试 WebSearch 和直接抓取。单一 Agent，顺序重试。</td></tr>
<tr><td><b>结构化中文报告</b></td><td>原文、翻译、媒体描述、引用推文、以及清晰的通俗解释。</td></tr>
<tr><td><b>极低成本</b></td><td>总共 1-3 次工具调用。获取 Agent 用 1 个工具，分析 Agent 用 0 个。</td></tr>
<tr><td><b>隐私友好</b></td><td>私密账号和频率限制优雅处理，不会中断流程。</td></tr>
</table>

---

## 快速安装

```bash
git clone https://github.com/Lucasyao1985/x-post-analyzer.git
```

将文件夹放入 Claude Code skills 目录：
- **Windows:** `C:\Users\<你的用户名>\.claude\skills\`
- **macOS/Linux:** `~/.claude/skills/`

## 使用方法

向 Claude 分享 X/Twitter 链接：

```
请分析这个帖子：https://x.com/user/status/123
```

或者直接提问：

```
这个推文在说什么？
```

技能会自动识别 X/Twitter 链接，获取内容，输出结构化报告：

- **原文**（逐字原文）
- **中文翻译**
- **媒体附件**（类型、画面描述）
- **引用推文**（如有）
- **内容解读**（多段通俗解释）

## 工作原理

```
URL → [获取 Agent] ──┬─ fxtwitter API（优先）
                       ├─ WebSearch（后备）
                       └─ 直接抓取（最后手段）
         ↓
      [分析 Agent] → 结构化中文报告
```

### 获取策略（优先级）

1. **fxtwitter API** — 返回完整 JSON（正文、媒体、互动数据、用户信息）。成功率最高。
2. **WebSearch** — 搜索该推文，API 失败时自动使用。
3. **直接抓取** — 抓取原始 x.com URL 作为最后手段（常被屏蔽）。

### 报告结构

| 部分 | 内容 |
|---|---|
| 原文 | 逐字帖子正文 |
| 翻译 | 完整中文翻译 |
| 媒体 | 类型、画面描述、时长/分辨率 |
| 引用 | 被引用推文的全文 + 作者 |
| 解读 | 多段通俗语言解释 |

## 项目结构

```
x-post-analyzer/
├── SKILL.md                 # 技能定义文件
├── README.md                # 英文文档
├── README.zh-CN.md          # 中文文档
├── scripts/
│   └── x-post-workflow.js   # 核心工作流（v2）
├── references/
│   ├── fetch-strategies.md  # 获取策略文档
│   └── report-template.md   # 报告模板
└── assets/
```

## 许可证

Unlicense — 见 [LICENSE](LICENSE)。

由 [opencode](https://github.com/anomalyco/opencode) 构建。