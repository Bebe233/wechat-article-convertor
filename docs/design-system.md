# 微信公众号排版设计规范

本仓库的微信正文样式以**内联 `style`** 实现，便于直接粘贴到公众号编辑器。所有数值与 `snippets/` 保持一致；排版 Skill 不得偏离下列 token。

## 设计 Token

| Token | 用途 | 值 |
|-------|------|-----|
| `--color-text` | 正文 | `#333333` |
| `--color-text-lead` | 导语/次要引导 | `#555555` |
| `--color-text-secondary` | 引用内文 | `#666666` |
| `--color-heading` | 标题 | `#1a1a1a` |
| `--color-accent` | 强调/链接 | `#07c160` |
| `--color-quote-border` | 引用左边线 | `#07c160` |
| `--color-quote-bg` | 引用背景 | `#f7f8fa` |
| `--color-highlight-bg` | 高亮框背景 | `#fff9e6` |
| `--color-highlight-border` | 高亮框左边线 | `#ffd666` |
| `--color-divider` | 分割线 | `#e5e5e5` |
| `--color-heading-bg` | 章节标题浅底 | `#f0faf4` |
| `--font-family` | 字体栈 | `-apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif` |
| `--font-size-body` | 正文 | `16px` |
| `--font-size-lead` | 导语 | `17px` |
| `--font-size-pull` | 金句/强调段 | `18px` |
| `--line-height-body` | 正文行高 | `1.85` |
| `--line-height-quote` | 引用行高 | `1.8` |
| `--line-height-cta` | CTA 行高 | `1.5` |
| `--letter-spacing-body` | 字间距（全文） | `2px` |
| `--text-indent-paragraph` | 段首缩进（叙事段落） | `2em` |
| `--font-size-h2` | 二级标题 | `20px` |
| `--font-size-h3` | 三级标题 | `18px` |
| `--spacing-block` | 段落上下间距 | `20px 0` |
| `--spacing-list` | 列表项上下间距 | `18px 0` |
| `--font-size-list` | 列表项正文 | `15px` |
| `--spacing-section-accent` | 色条 H2 章节间距 | `48px 0 24px` |
| `--spacing-section-plain` | 裸 H2 章节间距 | `28px 0 10px` |
| `--spacing-pull` | 金句段间距 | `28px 16px` |
| `--spacing-divider` | 分割线上下 | `28px 0` |

### Dark 主题 Token（可选变体）

用于 `wechat-dark.html` 等深色底稿；结构与浅色版一致，仅替换色值。粘贴公众号时建议**连同外层 `<section>` 背景一并复制**，否则编辑器可能仍显示白底。

| Token | 用途 | 值 |
|-------|------|-----|
| `--color-canvas` | 全文底色 | `#121816` |
| `--color-text` | 正文 | `#d6ddd8` |
| `--color-text-lead` | 导语 | `#9eaaa4` |
| `--color-text-secondary` | 引用内文 | `#8a9690` |
| `--color-heading` | 标题 | `#f2f6f4` |
| `--color-accent` | 强调/链接 | `#3dd68c` |
| `--color-quote-border` | 引用左边线 | `#3dd68c` |
| `--color-quote-bg` | 引用背景 | `#1a2420` |
| `--color-highlight-bg` | 高亮框背景 | `#2a2418` |
| `--color-highlight-border` | 高亮框左边线 | `#d4a84b` |
| `--color-highlight-text` | 高亮框正文 | `#e8e2d4` |
| `--color-heading-bg` | 章节标题浅底 | `#152820` |
| `--color-heading-border` | 色条 H2 左边线 | `#3dd68c` |

### 组件级样式摘要

- **全文容器** `<section>`：`letter-spacing: 2px`（对应公众号「字间距 2」），子元素继承；Dark 变体另加 `padding: 20px 16px` 与 `--color-canvas` 背景
- **导语** `paragraph-lead.html`：`17px` / `1.85` / `#555`，块间距 `20px 0`，**段首缩进 `2em`**
- **段落** `paragraph.html`：`16px` / `1.85` / `#333`，块间距 `20px 0`，**段首缩进 `2em`**
- **金句** `pull-quote.html`：`18px` 加粗居中，`#1a1a1a`，块间距 `28px 16px`（无段首缩进）
- **H2** `h2.html`：`20px` 加粗，`#1a1a1a`，上 `28px` 下 `10px`（`## 【plain】`）
- **H2 色条** `h2-accent.html`：`20px` 加粗，背景 `#f0faf4`，左 border `4px #07c160`，内边距 `10px 14px`，圆角 `0 6px 6px 0`，上 `48px` 下 `24px`
- **H3** `h3.html`：`18px` 加粗，`#1a1a1a`，上 `24px` 下 `10px`
- **引用** `quote.html`：左 border `3px #07c160`，背景 `#f7f8fa`，`15px` / `1.8`，内边距 `12px 16px`，块间距 `20px 0`（无段首缩进）
- **列表项** `list-item.html`：`15px` / `1.85` / `#333`，圆点，块间距 `18px 0`（无段首缩进；靠左内边距 + 符号对齐）
- **列表项（Emoji）** `list-item-emoji.html`：`15px` / `1.85` / `#333`，`{{emoji}}`，块间距 `18px 0`（无段首缩进）
- **分割线** `divider.html`：`1px` 实线 `#e5e5e5`，上下 `28px`
- **高亮框** `highlight.html`：`<blockquote>`，背景 `#fff9e6`，左 border `4px #ffd666`，内边距 `14px 16px`，`16px` 斜体 / `1.85`，块间距 `20px 0`（无段首缩进）
- **CTA** `cta.html`：居中，`#07c160` 加粗 `17px` / `1.5`，上 `24px` 下 `12px`（无段首缩进）

### 段首缩进与字间距（编辑规范）

- **字间距**：写在全文 `<section>` 上，值为 `2px`；勿在单个段落重复声明，除非某块需例外（须在 `raw-wechat.md` 标注）
- **段首缩进**：仅 **导语** 与 **叙事段落**（`paragraph-lead` / `paragraph`）使用 `text-indent: 2em`（首行缩进 2 个汉字宽）
- **不加缩进**：H2/H3、引用、高亮框、列表项、金句、CTA——这些组件靠结构符号、背景或对齐区分，不再叠加段首缩进

### 章节标题使用建议（编辑规范）

- **色条 H2**（`h2-accent`）：所有 `##` 章节标题的默认样式；全文若超过 **5～6** 个大节，可对最不核心的 1～2 节改用裸 H2 以减轻视觉重复。
- **裸 H2**（`## 【plain】`）：须在 `raw-wechat.md` 中显式标注 `【plain】`，用于刻意弱化的次要章节。
- **H3**：长章节内部的小节路标，宜短、宜少（每大节 0～3 个）。
- **金句**（`【pull】`）：每 800～1200 字可设 1 处，单独成段、便于扫读。
- **列表**：同章连续 emoji/圆点列表不宜超过 **3 条**；更多内容改为叙事段落 + `highlight` 收束。

## 组件清单（与 snippets 一一对应）

| Snippet 文件 | 适用 Markdown / 语义 | 说明 |
|--------------|------------------------|------|
| `paragraph-lead.html` | `【lead】` 标注的首段或导语 | 略大、略浅，仅文首或章节导语使用 |
| `paragraph.html` | 普通段落 | 默认正文 |
| `pull-quote.html` | `【pull】` 金句块 | 去掉标记行，内容入 `{{content}}`；可含 `strong` |
| `h2.html` | `## 【plain】标题` | 裸章节标题 |
| `h2-accent.html` | `## 标题`（默认） | 色条章节大标题 |
| `h3.html` | `### 标题` | 小节标题 |
| `quote.html` | `> 引用` | 产品摘要、引用说明 |
| `list-item.html` | `-` / `*` 无序列表项（无 emoji） | 每条单独一段 |
| `list-item-emoji.html` | `-` 后以 emoji 开头的列表项 | `{{emoji}}` + 正文 |
| `divider.html` | `---` / `***` | 章节分隔 |
| `highlight.html` | `【highlight】` 或编辑标注的卖点/注意块 | 去掉标记行 |
| `cta.html` | 文末行动号召 | 链接、关注引导（纯文字） |

### 占位符替换规则

- `{{content}}`：替换为已转义的纯文本或允许的内联 HTML（**仅** `strong`、`em`、`a`，且 `a` 的 `href` 须为 https）
- `{{emoji}}`：仅用于 `list-item-emoji.html`
- 拼接顺序：按 `raw-wechat.md` 自上而下；多个 `list-item` 连续出现时不额外插入空段
- 外层用单个 `<section style="...">` 包裹全文，须含 `letter-spacing: 2px` 与 `--font-family`；Dark 稿另加 canvas 背景与内边距。**不得**引入 `<style>` 标签或外链 CSS

## 配图占位语法（全项目统一）

在 `raw-wechat.md` 与 `wechat.html` 中使用**同一格式**的 HTML 注释：

```html
<!-- IMAGE: {类型描述} | 比例 {ratio} | 备注 {optional} -->
```

- **类型描述**：画面内容、构图、是否需要文字标注
- **比例**：常见 `16:9`、`4:3`、`1:1`；封面图可用 `2.35:1`
- **备注**：版权、打码、品牌色等（可省略整段 `| 备注 ...`）
- 长文建议约 **每 800～1000 字** 一处配图占位，用图切开文字墙

排版阶段不得将占位替换为外链 `<img>`（公众号需后台上传）。

## 微信公众号约束

1. **禁止** `<script>`、`<iframe>`、表单、音视频自动播放等非常规标签
2. **禁止** 依赖外链 CSS/JS；样式全部内联在 snippet 上
3. **图片**：须在公众号编辑器内上传；外链图易失效，默认只用 `<!-- IMAGE: ... -->`
4. **布局**：避免多列、float、复杂 flex；以单列阅读为主
5. **字体**：使用系统字体栈，不嵌入自定义 webfont
6. **高亮/注意块**：使用 `highlight.html`，勿用带四边框的 `<div>`
7. **默认语言**：中文；语气由用户每次在 pipeline 输入中指定

## 与 Skill 的关系

- `wechat-layout` 读取本文档与 `snippets/`，按 `reference.md` 映射表选片段
- 禁止自由发明新样式；新组件须先更新本文档并新增对应 snippet
