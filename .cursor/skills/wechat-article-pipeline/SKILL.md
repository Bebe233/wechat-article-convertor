---
name: wechat-article-pipeline
description: >-
  Orchestrates the full WeChat article workflow from research through facts.md,
  raw.md, to wechat.html with human confirmation gates. Use when the user runs
  /wechat-article, says 写公众号文章, or requests wechat-article-convertor pipeline.
disable-model-invocation: true
---

# WeChat Article Pipeline

编排「调研 → 事实表 → 成稿 → 排版」四阶段；默认**单会话顺序**执行，两个人工卡点。

## 启动：向用户确认或推断

| 字段 | 说明 |
|------|------|
| 来源 | 本地路径 和/或 网站 URL |
| 营销需求 | 受众、语气、字数、是否 CTA（语气每次由用户指定） |
| `slug` | 可选；否则从标题生成 kebab-case |
| 配图策略 | 默认 `占位 only`；可选「尝试生成或引用」 |

工作目录：`articles/<slug>/`

## 阶段与卡点

### 阶段 1 — 调研与事实表

1. 应用 **research-and-draft** 调研规则
2. 写入 `articles/<slug>/facts.md`
3. **停止**，请用户确认事实表/大纲

### 阶段 2 — 中文成稿

1. 用户确认后，写入 `articles/<slug>/raw.md`（中文，含 IMAGE 占位）
2. **停止**，请用户确认 `raw.md`

### 阶段 3 — 微信排版

1. 用户确认后，应用 **wechat-layout**
2. 写入 `articles/<slug>/wechat.html`；可选 `assets/`

### 阶段 4 — 交付说明

- 如何打开 `wechat.html` 全选复制到公众号后台
- 如何按 `<!-- IMAGE: ... -->` 在编辑器内上传配图
- 样式来自 `snippets/`，勿在公众号内再套复杂模板

## 大仓库可选优化（v1 无自定义 subagent）

- 可对 `README`、`docs/`、`src/` **并行**调用内置 `explore` Task，**上限 3 路**
- 主 Agent 合并结果为一份 `facts.md`
- **不**并行撰写 `raw.md` 或 `wechat.html`
- 未创建 `.cursor/agents/`；不默认 Multitask/后台排版

## 禁止事项

- 用户未确认 `facts.md` 前不写 `raw.md`
- 用户未确认 `raw.md` 前不写 `wechat.html`
- 不提交 `.env` 或 API 密钥
- v1 不实现 Next.js/CLI/npm 应用代码

## 相关 Skill

- [research-and-draft](../research-and-draft/SKILL.md)
- [wechat-layout](../wechat-layout/SKILL.md)

## 示例路径

对照 [articles/_example](../../../articles/_example/) 的三段产物格式。
