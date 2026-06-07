---
name: xhs-format
description: >-
  Converts confirmed raw-xhs.md into paste-ready xhs.md for Xiaohongshu creator
  center. Use when raw-xhs.md is confirmed and user needs xhs.md or 小红书发布稿.
disable-model-invocation: true
---

# XHS Format

将已确认的 `articles/<slug>/raw-xhs.md` 转为可发布的 `xhs.md`。

## 前置条件

- 用户已确认 `raw-xhs.md`（pipeline 卡点 2 通过，可与 raw-wechat 同批确认）
- 读取 [docs/xhs-format.md](../../../docs/xhs-format.md)

## 硬性规则

1. **只做格式整理**，不改事实、不增删功能点
2. 输出纯 Markdown 四段结构，**禁止** HTML、snippets、`<img>`
3. 配图占位转为「配图清单」 numbered list；不写图片文件
4. 发布标题 ≤20 字；正文 ≤1000 字

## 工作步骤

1. 读取 `raw-xhs.md`：首个 `#` 为笔记标题；`## 话题标签` 下为标签行
2. 收集所有 `<!-- COVER: ... -->` 与 `<!-- IMAGE: ... -->`，按出现顺序写入配图清单
3. 正文区：去掉 `#` 标题与 `## 话题标签` 节；保留 emoji 与分段；去掉 Markdown 列表符号时可改为「·」或换行；将 `**强调**` 转为「强调」
4. 写入 `articles/<slug>/xhs.md`
5. 交付：说明复制标题/正文/标签、按清单上传竖图

## 输出模板

```markdown
## 发布标题
（≤20字）

## 正文
（纯文本分段）

## 话题标签
#xxx #yyy

## 配图清单
1. [封面 3:4] {来自 COVER 注释的描述}
2. [内页 3:4] {来自 IMAGE 注释的描述}
```

## 输出检查清单

- [ ] 发布标题 ≤20 字
- [ ] 正文无 HTML、无 `#` 标题层级、无 `**` Markdown 加粗（轻强调用「」）
- [ ] 话题标签 5–10 个
- [ ] 配图清单含至少 1 条封面 + 内页项
- [ ] 无 GenerateImage、无 assets 目录写入
