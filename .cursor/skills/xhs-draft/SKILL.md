---
name: xhs-draft
description: >-
  Drafts Chinese Xiaohongshu note raw-xhs.md from confirmed facts.md. Use when
  pipeline needs 小红书成稿, xhs raw draft, or before xhs-format stage.
disable-model-invocation: true
---

# XHS Draft

从已确认的 `facts.md` 撰写 `articles/<slug>/raw-xhs.md`。由 **wechat-article-pipeline** 调用；本 Skill 不生成 `xhs.md` 终稿。

## 前置条件

- 用户已确认 `facts.md`（pipeline 卡点 1 通过）
- 读取 [docs/xhs-format.md](../../../docs/xhs-format.md)

## 硬性规则

1. 标题 `#` 行 ≤20 字（含 emoji 按字符计）
2. 正文 ≤1000 字；短段 + 列表，不用 `##` 长文章节（话题标签节除外）
3. 至少 1 处 `<!-- COVER: ... -->` + 若干 `<!-- IMAGE: ... -->`，默认比例 3:4
4. `## 话题标签` 下 5–10 个 `#标签`，须与 facts 相关，禁止编造
5. **禁止** `【highlight】`/`【cta】` 等微信 snippet 标记；**禁止** HTML 与外链图；**禁止** `**` Markdown 加粗，轻强调用「」
6. 配图仅占位，禁止 GenerateImage 或写入 `assets/`

## 模板

```markdown
# 笔记标题（≤20字）

<!-- COVER: {desc} | 比例 3:4 | 备注 {optional} -->

（hook 1–2 短段，可含 emoji）

<!-- IMAGE: {desc} | 比例 3:4 | 备注 {optional} -->

- 要点 1 …
- 要点 2 …

<!-- IMAGE: {desc} | 比例 3:4 | 备注 {optional} -->

（总结 + 轻量引导，非硬广）

## 话题标签
#标签1 #标签2 #标签3
```

## 执行要点

- 语气、字数、配图张数、标签策略：按 pipeline 收集的用户输入执行
- 功能与数据仅来自 `facts.md`；不确定的不写或标注待核实
- 与 `raw-wechat.md` **独立撰写**，不共用 master 稿

## 完成后

与 `raw-wechat.md`（若同批）一并交给 pipeline 卡点 2，等待用户**一次**确认后再进入 **xhs-format**。
