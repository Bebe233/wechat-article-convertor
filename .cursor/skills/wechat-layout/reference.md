# raw.md → snippet 映射表



| raw.md 结构 | Snippet | 备注 |

|-------------|---------|------|

| `# 标题`（文首一次） | 不单独 snippet；标题在公众号标题栏填写 | 正文从导语开始 |

| `【lead】` 行（单独一行，下一行起为导语正文） | `paragraph-lead.html` | 去掉 `【lead】` 标记；仅文首或章节引导段 |

| `【pull】` 行 | `pull-quote.html` | 去掉 `【pull】` 标记；金句单独成段 |

| `## 【plain】...` | `h2.html` | 裸 H2，宜用于次要大节 |

| `## ...`（默认） | `h2-accent.html` | 色条章节标题，全文宜 3～4 处 |

| `### ...` | `h3.html` | 小节路标 |

| 普通段落 | `paragraph.html` | 连续段落各用一段 |

| `> ...` | `quote.html` | |

| `- ` / `* ` 列表（行首 emoji） | `list-item-emoji.html` | 拆分 `{{emoji}}` 与剩余 `{{content}}` |

| `- ` / `* ` 列表（无 emoji） | `list-item.html` | 每项一条 snippet |

| `---` / `***` | `divider.html` | |

| `【highlight】` 或编辑标注的卖点块 | `highlight.html` | 去掉标记行，内容入 `{{content}}` |

| `【cta】` 行 | `cta.html` | 去掉标记；内容可含 `<a href="https://...">` |
| 文末普通引导段 | `paragraph.html` | 放在 CTA 之后 |

| `<!-- IMAGE: ... -->` | 原样插入 HTML | 不包 snippet |



## 拼接示例



```text

paragraph-lead(开篇引导)

paragraph(展开)

pull-quote(金句)

quote(产品摘要)

<!-- IMAGE: ... -->

h2-accent(主章节)

paragraph + h3(小节)

list-item-emoji × 2～3

highlight(收束)

divider

h2-plain(次章节)

paragraph

cta

```



## 占位符



- `{{content}}`：必填（`divider.html` 无占位符）

- `{{emoji}}`：必填（仅 `list-item-emoji.html`）

- 替换前去除 Markdown 语法符号（`##`、`-` 等），保留加粗为 `<strong>`、斜体为 `<em>`

- 列表项 emoji 识别：`- ` 后紧跟 emoji（及可选空格），余下为正文

