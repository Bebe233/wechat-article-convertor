---
name: wechat-article-pipeline
description: >-
  Orchestrates content workflow for WeChat and/or Xiaohongshu: facts.md,
  raw-wechat.md, raw-xhs.md, wechat.html, xhs.md with human confirmation gates.
  Use when the user runs /wechat-article, says 写公众号/小红书, or requests
  wechat-article-convertor pipeline.
disable-model-invocation: true
---

# WeChat Article Pipeline

编排「调研 → 事实表 → 平台成稿 → 平台排版」；默认**单会话顺序**执行，两个人工卡点。支持 **微信** / **小红书** / **双平台**。

## 启动：向用户确认或推断

| 字段 | 说明 |
|------|------|
| **平台** | `微信` \| `小红书` \| `双平台`；未指定时从用户意图推断（说「同时」则默认双平台） |
| 来源 | 本地路径 和/或 网站 URL |
| 微信营销需求 | 受众、语气、字数、是否 CTA（平台含微信时） |
| 小红书需求 | 语气（种草/干货/测评等）、字数（默认约 800、正文 ≤1000）、配图张数（默认 4–6 竖图）、标签策略（默认从 facts 提取） |
| `slug` | 可选；否则从标题生成 kebab-case |
| 配图 | 固定 **占位 only** |

工作目录：`articles/<slug>/`

## 阶段与卡点

### 阶段 1 — 调研与事实表

1. 应用 **research-and-draft** 调研规则
2. 写入 `articles/<slug>/facts.md`
3. **停止**，请用户确认事实表/大纲

### 阶段 2 — 平台成稿

1. 用户确认后，按平台参数写入：
   - 含微信 → `raw-wechat.md`（research-and-draft 产出 2a）
   - 含小红书 → `raw-xhs.md`（应用 **xhs-draft**）
2. 所需成稿**全部写完**后**停止**，请用户**一次**确认 `raw-wechat.md` 和/或 `raw-xhs.md`

### 阶段 3 — 平台排版

1. 用户确认后，按平台并行或单独执行：
   - 含微信 → **wechat-layout** → `wechat.html`
   - 含小红书 → **xhs-format** → `xhs.md`

### 阶段 4 — 交付说明

**微信**（若产出）：

- 打开 `wechat.html` 全选复制到公众号后台
- 按 `<!-- IMAGE: ... -->` 在编辑器内上传配图
- 样式来自 `snippets/`，勿在公众号内再套复杂模板

**小红书**（若产出）：

- 打开 `xhs.md`，复制「发布标题」「正文」「话题标签」
- 按「配图清单」顺序上传竖图（3:4）
- 纯文本发布，不使用 HTML

## 大仓库可选优化（v1 无自定义 subagent）

- 可对 `README`、`docs/`、`src/` **并行**调用内置 `explore` Task，**上限 3 路**
- 主 Agent 合并结果为一份 `facts.md`
- **不**并行撰写 `raw-*.md` 或平台终稿
- 未创建 `.cursor/agents/`；不默认 Multitask/后台排版

## 禁止事项

- 用户未确认 `facts.md` 前不写任何 `raw-*.md`
- 用户未确认成稿前不写 `wechat.html` / `xhs.md`
- 配图仅 `<!-- IMAGE: ... -->` / `<!-- COVER: ... -->` 占位；**禁止** GenerateImage 或写 `assets/`
- 不提交 `.env` 或 API 密钥
- v1 不实现 Next.js/CLI/npm 应用代码

## 向后兼容

- 旧目录若仅有 `raw.md`，**wechat-layout** 在缺少 `raw-wechat.md` 时回退读取 `raw.md`

## 相关 Skill

- [research-and-draft](../research-and-draft/SKILL.md)
- [xhs-draft](../xhs-draft/SKILL.md)
- [wechat-layout](../wechat-layout/SKILL.md)
- [xhs-format](../xhs-format/SKILL.md)

## 示例路径

对照 [articles/_example](../../../articles/_example/) 的双平台产物格式。
