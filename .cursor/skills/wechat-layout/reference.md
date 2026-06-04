# raw.md → snippet 映射表

| raw.md 结构 | Snippet | 备注 |
|-------------|---------|------|
| `# 标题`（文首一次） | 不单独 snippet；可用 `paragraph` 加粗或首段前注释说明标题已在公众号标题栏填写 | 正文从导语开始 |
| `## 【plain】...` | `h2.html` | 显式标记时用裸 H2 |
| `## ...`（默认） | `h2-accent.html` | 色条章节标题 |
| `### ...` | `h3.html` | |
| 普通段落 | `paragraph.html` | 连续段落各用一段 |
| `> ...` | `quote.html` | |
| `- ` / `* ` 列表（行首 emoji） | `list-item-emoji.html` | 拆分 `{{emoji}}` 与剩余 `{{content}}` |
| `- ` / `* ` 列表（无 emoji） | `list-item.html` | 每项一条 snippet |
| `---` / `***` | `divider.html` | `{{content}}` 无，原样输出文件内容 |
| `【highlight】` 或编辑标注的卖点块 | `highlight.html` | 去掉标记行，内容入 `{{content}}` |
| 文末 CTA 行（如「立即…」「关注…」） | `cta.html` | 通常一段 |
| `<!-- IMAGE: ... -->` | 原样插入 HTML | 不包 snippet |

## 拼接示例

```text
paragraph(导语)
quote(产品摘要)
<!-- IMAGE: ... -->
h2-accent(章节)
list-item-emoji × N
divider
highlight(数据亮点)
cta
```

## 占位符

- `{{content}}`：必填（`divider.html` 无占位符）
- `{{emoji}}`：必填（仅 `list-item-emoji.html`）
- 替换前去除 Markdown 语法符号（`##`、`-` 等），保留加粗为 `<strong>`
- 列表项 emoji 识别：`- ` 后紧跟 emoji（及可选空格），余下为正文
