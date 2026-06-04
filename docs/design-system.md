# 微信公众号排版设计规范

本仓库的微信正文样式以**内联 `style`** 实现，便于直接粘贴到公众号编辑器。所有数值与 `snippets/` 保持一致；排版 Skill 不得偏离下列 token。

## 设计 Token

| Token | 用途 | 值 |
|-------|------|-----|
| `--color-text` | 正文 | `#333333` |
| `--color-text-secondary` | 次要说明 | `#666666` |
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
| `--line-height-body` | 正文行高 | `1.75` |
| `--font-size-h2` | 二级标题 | `20px` |
| `--font-size-h3` | 三级标题 | `18px` |
| `--spacing-block` | 块级上下间距 | `16px 0` |
| `--spacing-section` | 章节间距 | `24px 0 8px` |

### 组件级样式摘要

- **段落** `paragraph.html`：`16px` / `1.75` / `#333`，块间距 `16px 0`
- **H2** `h2.html`：`20px` 加粗，`#1a1a1a`，上 `24px` 下 `8px`（备用；默认章节用 `h2-accent`）
- **H2 色条** `h2-accent.html`：`20px` 加粗，`#1a1a1a`，背景 `#f0faf4`，左 border `4px #07c160`，内边距 `10px 14px`，圆角 `0 6px 6px 0`，上 `24px` 下 `12px`
- **H3** `h3.html`：`18px` 加粗，`#1a1a1a`，上 `20px` 下 `6px`
- **引用** `quote.html`：左 border `3px #07c160`，背景 `#f7f8fa`，内边距 `12px 16px`
- **列表项** `list-item.html`：正文样式 + 左侧圆点 `•`
- **列表项（Emoji）** `list-item-emoji.html`：正文样式 + 行首 `{{emoji}}`（间距 `6px`）
- **分割线** `divider.html`：`1px` 实线 `#e5e5e5`，上下 `24px`
- **高亮框** `highlight.html`：`<blockquote>`，背景 `#fff9e6`，左 border `4px #ffd666`，内边距 `14px 16px`（勿用 `<div>` 四边框，公众号粘贴会丢样式）
- **CTA** `cta.html`：居中，`#07c160` 加粗 `17px`，上 `20px` 下 `8px`

## 组件清单（与 snippets 一一对应）

| Snippet 文件 | 适用 Markdown / 语义 | 说明 |
|--------------|------------------------|------|
| `h2.html` | `## 【plain】标题` | 裸章节标题（例外） |
| `h2-accent.html` | `## 标题`（默认） | 色条章节大标题 |
| `h3.html` | `### 标题` | 小节标题 |
| `paragraph.html` | 普通段落 | 默认正文 |
| `quote.html` | `> 引用` | 金句、摘要、引用说明 |
| `list-item.html` | `-` / `*` 无序列表项（无 emoji） | 每条单独一段，可连续拼接 |
| `list-item-emoji.html` | `-` 后以 emoji 开头的列表项 | `{{emoji}}` + 正文；同章 emoji 不重复 |
| `divider.html` | `---` / `***` | 章节分隔 |
| `highlight.html` | 卖点、数据亮点、「注意」块 | 非标准 MD 时用编辑标注为 highlight |
| `cta.html` | 文末行动号召 | 引导关注、试用、访问链接（纯文字，无按钮组件） |

### 占位符替换规则

- `{{content}}`：替换为已转义的纯文本或允许的内联 HTML（**仅** `strong`、`em`、`a`，且 `a` 的 `href` 须为 https）
- `{{emoji}}`：仅用于 `list-item-emoji.html`，取列表项行首单个 emoji 字符（含组合 emoji）
- 拼接顺序：按 `raw.md` 自上而下；多个 `list-item` 连续出现时不额外插入空段
- 外层可用单个 `<section style="...">` 包裹全文，**不得**引入 `<style>` 标签或外链 CSS

## 配图占位语法（全项目统一）

在 `raw.md` 与 `wechat.html` 中使用**同一格式**的 HTML 注释：

```html
<!-- IMAGE: {类型描述} | 比例 {如16:9} | 备注 {可选} -->
```

示例：

```html
<!-- IMAGE: 产品界面截图，展示 Markdown 预览与导出按钮 | 比例 16:9 | 备注 需打码路径信息 -->
```

- **类型描述**：画面内容、构图、是否需要文字标注
- **比例**：常见 `16:9`、`4:3`、`1:1`；封面图可用 `2.35:1`
- **备注**：版权、打码、品牌色等（可省略整段 `| 备注 ...`）

排版阶段不得将占位替换为外链 `<img>`（公众号需后台上传）；若生成图片放入 `articles/<slug>/assets/`，HTML 中仍保留上述注释并注明文件名。

## 微信公众号约束

1. **禁止** `<script>`、`<iframe>`、表单、音视频自动播放等非常规标签
2. **禁止** 依赖外链 CSS/JS；样式全部内联在 snippet 上
3. **图片**：须在公众号编辑器内上传；外链图易失效，默认只用 `<!-- IMAGE: ... -->`
4. **布局**：避免多列、float、复杂 flex；以单列阅读为主
5. **字体**：使用系统字体栈，不嵌入自定义 webfont
6. **高亮/注意块**：使用 `highlight.html`（`<blockquote>` + 左色条 + 浅底），勿用带四边框的 `<div>`
7. **默认语言**：中文；语气由用户每次在 pipeline 输入中指定

## 与 Skill 的关系

- `wechat-layout` 读取本文档与 `snippets/`，按 `reference.md` 映射表选片段
- 禁止自由发明新样式；新组件须先更新本文档并新增对应 snippet
