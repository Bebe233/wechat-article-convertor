# raw-wechat.md → snippet 映射表

输入文件：`raw-wechat.md`；若不存在则回退 legacy `raw.md`。

| raw-wechat.md 结构 | Snippet | 备注 |
|-------------|---------|------|
| `# 标题`（文首一次） | 不单独 snippet；标题在公众号标题栏填写 | 正文从导语开始 |
| `【lead】` 行 | `paragraph-lead.html` | 去掉标记 |
| `【pull】` 行 | `pull-quote.html` | 去掉标记；青绿加粗强调句 |
| `## 【plain】...` | `h2.html` | 裸 H2 |
| `## ...`（默认） | `h2-accent.html` | 色条章节标题 |
| `### ...` | `h3.html` | H4 小节路标（居中 + 底边线；短标题） |
| `### 【left】...` | `h3-left.html` | 左对齐长小节；去掉 `【left】` 标记 |
| 普通段落 | `paragraph.html` | |
| `> ...` | `quote.html` | 灰左边线引用 |
| `- ` / `* ` 列表（行首 emoji） | `list-item-emoji.html` | |
| `- ` / `* ` 列表（无 emoji） | `list-item.html` | |
| `---` / `***` | `divider.html` | |
| `【highlight】` | `highlight.html` | 黄色警示块 |
| `【cta】` 行 | `cta.html` | |
| `【caption】` 行 | `image-caption.html` | |
| `<!-- IMAGE: ... -->` | 原样插入 HTML | |
| `【code】` … `【/code】` | `code-block.html` | `=` 左侧染 `#7fd1ff` |
| `【card】标题 \| 说明` | `kpi-card.html` | 单列堆叠；`{{title}}` / `{{subtitle}}` |
| Markdown 管道表 | `table.html` | 圆角裁切 + 斑马纹；无外框线 |
| `【step】n \| 正文` | `step-box.html` | 圆点序号步骤框 |
| `【tag】标签 \| 说明` | `list-item-tag.html` | 浅绿底标签 |
| `【soft-quote】` | `soft-quote.html` | 灰底圆角收束；可含 `<br>` |
| `【pull-center】` | `pull-center.html` | 居中深绿强调；可含 `<br>` |
| `【footer】标题 \| 行2 \| 行3` | `footer-banner.html` | 深蓝页脚条 |

## 占位符

- `{{content}}`：多数片段必填
- `{{emoji}}`：仅 `list-item-emoji.html`
- `{{title}}` / `{{subtitle}}`：`kpi-card.html`；`footer-banner` 另用 `{{line2}}` / `{{line3}}`
- `{{tag}}`：`list-item-tag.html`
- `{{n}}`：`step-box.html` 序号
- **code-block**：按行处理；若含 `=`，左侧包 `<span style="color:#7fd1ff;">…</span>`
- **table**：表头 `th` 青绿底白字；偶数数据行 `#f5faf7`；末行无 `border-bottom`
- **soft-quote / pull-center**：允许保留显式 `<br>`（成稿中写 `<br>`）
