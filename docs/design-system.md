# 微信公众号排版设计规范

本仓库的微信正文样式以**内联 `style`** 实现，便于直接粘贴到公众号编辑器。所有数值与 `snippets/` 保持一致；排版 Skill 不得偏离下列 token。

设计方向参考 [量子位 · 微软年度 AI 职场报告](https://mp.weixin.qq.com/s/p59gkROx3CgufDZFaKhrTQ)（2026）：**内容优先、留白充足、单一强调色、结构符号代替段首缩进**，适合科技/商业长文在手机端扫读。

---

## UI/UX 设计原则

| 原则 | 说明 | 参考文章中的体现 |
|------|------|------------------|
| 内容优先 | 白底 + 宽左右边距（约 16px），不叠装饰 | 正文 `margin: 20px 16px`，无背景纹理 |
| 扫读友好 | 短段、大节距、配图切分文字墙 | H2 上间距 40px；关键数据/结论单独成段 |
| 单一强调色 | 青绿 `#00997f` 负责结构线与关键词，正文保持 `#222` | H2 左色条、H4 底边线、`<strong>` 同色 |
| 结构代替缩进 | **不使用**段首 `2em` 缩进；靠 H2/H4/引用块/列表区分层级 | 全文 `text-indent: 0` |
| 轻引用块 | 开场 hook、专家引言、吐槽金句用灰底引用，而非重色边框 | `rgba(128,128,128,0.05)` 背景 + 灰左条 |
| 层级清晰 | H2 = 大章（左色条）；H4 = 章内路标（居中 + 底边线） | 三层「转型悖论」结构 |
| 内联强调 | 数据、专名、结论句用 `<strong>` 染强调色，而非整段加粗 | 「72%」「《Work Trend Index》」等 |
| 辅文降权 | 括号补充、图注、出处用 `#888` / `#8f8f8f` | `（WTI）`、「△图为 AI 生成」 |

### 阅读节奏建议（编辑规范）

- **开篇**：1 句灰底引用（`quote.html`）点题 → 1～2 段叙事展开 → 可选要点列表（≤3 条）
- **章节**：H2 大节 → 若干短段 → 必要时 H4 小节 → 配图或列表 → 1 句 `<strong>` 收束
- **段落长度**：单段宜 **1～3 句**（约 40～120 字）；超过 4 句应拆段
- **配图**：大节之间、长论证中段、案例/对话还原处插入；图下用 `【caption】` 标注来源
- **数字清单**：步骤类内容用「1、… 2、…」写入普通段落，**不必**强行转 ul 列表

---

## 设计 Token

| Token | 用途 | 值 |
|-------|------|-----|
| `--color-text` | 正文 | `#222222` |
| `--color-text-lead` | 导语/次要引导 | `#3e3e3e` |
| `--color-text-secondary` | 括号补充、次要说明 | `#888888` |
| `--color-text-muted` | 图注、出处 | `#8f8f8f` |
| `--color-heading` | 标题 | `#222222` |
| `--color-heading-sub` | H4 小节标题 | `#3e3e3e` |
| `--color-accent` | 强调/链接/结构线 | `#00997f` |
| `--color-callout-bg` | 引用/开场块背景 | `rgba(128,128,128,0.05)` |
| `--color-callout-border` | 引用/开场块左边线 | `rgba(128,128,128,0.075)` |
| `--color-highlight-bg` | 高亮框背景 | `#fff9e6` |
| `--color-highlight-border` | 高亮框左边线 | `#ffd666` |
| `--color-divider` | 分割线 | `#e5e5e5` |
| `--font-family` | 字体栈 | `-apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif` |
| `--font-size-body` | 正文 | `16px` |
| `--font-size-lead` | 导语 | `16px`（同色阶区分，非字号） |
| `--font-size-callout` | 引用块 | `13px` |
| `--font-size-pull` | 强调句 | `16px`（加粗 + 强调色） |
| `--font-size-caption` | 图注 | `13px` |
| `--line-height-body` | 正文行高 | `2` |
| `--line-height-callout` | 引用行高 | `2` |
| `--line-height-cta` | CTA 行高 | `1.5` |
| `--line-height-caption` | 图注行高 | `1.3` |
| `--letter-spacing-body` | 字间距（全文） | `1px` |
| `--spacing-paragraph` | 段落块间距 | `20px 16px` |
| `--font-size-h2` | 二级标题 | `20px` |
| `--font-size-h4` | 四级/小节标题 | `16px` |
| `--spacing-list` | 列表项块间距 | `20px 16px` |
| `--font-size-list` | 列表项正文 | `16px` |
| `--spacing-section-accent` | 色条 H2 章节间距 | `40px 0` |
| `--spacing-section-plain` | 裸 H2 章节间距 | `28px 0 10px` |
| `--spacing-pull` | 强调句间距 | `20px 16px` |
| `--spacing-divider` | 分割线上下 | `28px 0` |
| `--border-h2-accent` | H2 左色条 | `6px solid #00997f` |
| `--border-h4-accent` | H4 底边线 | `3px solid #00997f` |
| `--padding-h2-accent` | H2 左内边距 | `0 0 0 15px` |

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
| `--color-callout-bg` | 引用背景 | `#1e2220` |
| `--color-callout-border` | 引用左边线 | `rgba(255,255,255,0.08)` |
| `--color-highlight-bg` | 高亮框背景 | `#2a2418` |
| `--color-highlight-border` | 高亮框左边线 | `#d4a84b` |
| `--color-highlight-text` | 高亮框正文 | `#e8e2d4` |
| `--color-heading-border` | H2/H4 结构线 | `#3dd68c` |

### 组件级样式摘要

- **全文容器** `<section>`：`letter-spacing: 1px`，子元素继承；Dark 变体另加 `padding: 20px 16px` 与 `--color-canvas` 背景
- **导语** `paragraph-lead.html`：`16px` / `2` / `#3e3e3e`，块间距 `20px 16px`，**无段首缩进**
- **段落** `paragraph.html`：`16px` / `2` / `#222`，块间距 `20px 16px`，**无段首缩进**
- **强调句** `pull-quote.html`：`16px` 加粗，`#00997f`，块间距 `20px 16px`（左对齐；用于段内结论句，非居中海报体）
- **H2** `h2.html`：`20px` 加粗，`#222`，上 `28px` 下 `10px`（`## 【plain】`）
- **H2 色条** `h2-accent.html`：`20px` 加粗，`#222`，左 border `6px #00997f`，`padding-left: 15px`，`margin: 40px 0`，无背景、无圆角
- **H4 小节** `h3.html`：`16px` 加粗，`#3e3e3e`，居中，`border-bottom: 3px solid #00997f`，`margin: 10px 60px`，`padding-bottom: 6px`（对应 Markdown `###`）
- **引用/开场** `quote.html`：灰底引用块，左 border `10px rgba(128,128,128,0.075)`，背景 `rgba(128,128,128,0.05)`，`13px` / `2`，块间距 `10px 16px 10px 0`
- **列表项** `list-item.html`：`16px` / `2` / `#222`，圆点 `#00997f`，块间距 `20px 16px`
- **列表项（Emoji）** `list-item-emoji.html`：同上，`{{emoji}}` 前缀
- **分割线** `divider.html`：`1px` 实线 `#e5e5e5`，上下 `28px`
- **高亮框** `highlight.html`：`<blockquote>`，背景 `#fff9e6`，左 border `4px #ffd666`，内边距 `14px 16px`，`16px` 斜体 / `2`，块间距 `20px 16px`（卖点/注意，**非**日常引用）
- **图注** `image-caption.html`：`13px` / `1.3` / `#8f8f8f`，右对齐，`margin: 0 16px 0 0`
- **CTA** `cta.html`：居中，`#00997f` 加粗 `17px` / `1.5`，上 `24px` 下 `12px`

### 内联强调（编辑 + 排版规范）

- **关键词/数据/专名**：成稿阶段用 Markdown `**…**`，排版时转为 `<strong style="color:#00997f;font-weight:bold;">…</strong>`
- **括号补充**：`(…)` / `（…）` 中纯说明文字可包 `<span style="color:#888888;">…</span>`（可选，长文括号多时采用）
- **链接**：`<a href="https://…" style="color:#00997f;font-weight:bold;text-decoration:none;">…</a>`（无下划线）
- **禁止**：整段染强调色；同一段内 `<strong>` 不宜超过 2 处

### 段间距与字间距（编辑规范）

- **字间距**：写在全文 `<section>` 上，值为 `1px`；勿在单个段落重复声明，除非某块需例外（须在 `raw-wechat.md` 标注）
- **段首缩进**：**默认不使用**；叙事段落靠左右 `16px` 边距与段落间距区分
- **不加缩进**：H2/H4、引用、高亮框、列表项、强调句、CTA、图注

### 章节标题使用建议（编辑规范）

- **色条 H2**（`h2-accent`）：所有 `##` 章节标题的**默认**样式；全文 3～5 个大节为宜
- **裸 H2**（`## 【plain】`）：须在 `raw-wechat.md` 中显式标注，用于次要章节或附录
- **H4 小节**（`###` → `h3.html`）：长章节内部的路标，宜短、宜少（每大节 0～3 个）；标题可含「——」连接副题
- **强调句**（`【pull】`）：每 600～1000 字可设 1 处，单独成段、便于扫读；内容为完整结论句
- **引用块**（`>`）：开篇 hook、专家引言、对话还原；与 `highlight` 区分——后者仅用于卖点/警示
- **列表**：同章连续 emoji/圆点列表不宜超过 **3 条**；更多内容改为短段落 + `highlight` 或数字清单段落

## 组件清单（与 snippets 一一对应）

| Snippet 文件 | 适用 Markdown / 语义 | 说明 |
|--------------|------------------------|------|
| `paragraph-lead.html` | `【lead】` 标注的首段或导语 | 同色阶 `#3e3e3e`，仅文首或章节引导段 |
| `paragraph.html` | 普通段落 | 默认正文；数字清单「1、…」亦用此片段 |
| `pull-quote.html` | `【pull】` 强调句 | 去掉标记行；青绿加粗左对齐句 |
| `h2.html` | `## 【plain】标题` | 裸章节标题 |
| `h2-accent.html` | `## 标题`（默认） | 左色条章节大标题 |
| `h3.html` | `### 标题` | H4 小节（居中 + 底边线） |
| `quote.html` | `> 引用` | 开场 hook、专家引言、对话金句 |
| `list-item.html` | `-` / `*` 无序列表项（无 emoji） | 每条单独一段 |
| `list-item-emoji.html` | `-` 后以 emoji 开头的列表项 | `{{emoji}}` + 正文 |
| `divider.html` | `---` / `***` | 章节分隔 |
| `highlight.html` | `【highlight】` 或编辑标注的卖点/注意块 | 黄色警示块；去掉标记行 |
| `image-caption.html` | `【caption】` 或图下说明 | 右对齐灰字，如「△图为 AI 生成」 |
| `cta.html` | 文末行动号召 | 链接、关注引导（纯文字） |

### 占位符替换规则

- `{{content}}`：替换为已转义的纯文本或允许的内联 HTML（**仅** `strong`、`em`、`a`、`span`，且 `a` 的 `href` 须为 https）
- `{{emoji}}`：仅用于 `list-item-emoji.html`
- 拼接顺序：按 `raw-wechat.md` 自上而下；多个 `list-item` 连续出现时不额外插入空段
- 外层用单个 `<section style="...">` 包裹全文，须含 `letter-spacing: 1px` 与 `--font-family`；Dark 稿另加 canvas 背景与内边距。**不得**引入 `<style>` 标签或外链 CSS
- 排版时 `<strong>` 默认补 `color:#00997f`（若 raw 未自带 style）

## 配图占位语法（全项目统一）

在 `raw-wechat.md` 与 `wechat.html` 中使用**同一格式**的 HTML 注释：

```html
<!-- IMAGE: {类型描述} | 比例 {ratio} | 备注 {optional} -->
```

- **类型描述**：画面内容、构图、是否需要文字标注
- **比例**：常见 `16:9`、`4:3`、`1:1`；封面图可用 `2.35:1`；对话/信息图参考文章多用宽幅 `~645px` 内容区宽度
- **备注**：版权、打码、品牌色、是否 AI 生成（若 AI 生成，图下须跟 `【caption】△图为 AI 生成`）
- 长文建议约 **每 600～800 字** 一处配图占位，用大节之间与案例处切分文字墙

排版阶段不得将占位替换为外链 `<img>`（公众号需后台上传）。

## 微信公众号约束

1. **禁止** `<script>`、`<iframe>`、表单、音视频自动播放等非常规标签
2. **禁止** 依赖外链 CSS/JS；样式全部内联在 snippet 上
3. **图片**：须在公众号编辑器内上传；外链图易失效，默认只用 `<!-- IMAGE: ... -->`
4. **布局**：避免多列、float、复杂 flex；以单列阅读为主（引用卡片等多列布局须转图片）
5. **字体**：使用系统字体栈，不嵌入自定义 webfont
6. **高亮/注意块**：使用 `highlight.html`；日常引用用 `quote.html`，勿混用
7. **默认语言**：中文；语气由用户每次在 pipeline 输入中指定
8. **避免** `!important`（微信 Dark Mode 与编辑器清洗可能异常；参考文虽用 `!important`，本仓库 snippet 一律不用）

## 与 Skill 的关系

- `wechat-layout` 读取本文档与 `snippets/`，按 `reference.md` 映射表选片段
- 禁止自由发明新样式；新组件须先更新本文档并新增对应 snippet
