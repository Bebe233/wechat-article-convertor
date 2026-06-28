---
name: wechat-layout
description: >-
  Converts Chinese marketing draft raw-wechat.md into paste-ready WeChat HTML
  using project snippets and design tokens. Falls back to legacy raw.md. Use when
  raw-wechat.md is confirmed and user needs wechat.html or WeChat公众号排版.
disable-model-invocation: true
---

# WeChat Layout

将已确认的 `articles/<slug>/raw-wechat.md` 转为可粘贴到公众号后台的 `wechat.html`。若不存在 `raw-wechat.md`，回退读取 legacy `raw.md`。

## 前置条件

- 用户已确认 `raw-wechat.md` 或 legacy `raw.md`（pipeline 卡点 2 通过）
- 读取 [docs/design-system.md](../../../docs/design-system.md) 与 [snippets/](../../../snippets/)
- 语义→片段映射见 [reference.md](reference.md)

## 硬性规则

1. **禁止**自由生成全新样式；只允许：选 snippet → 替换 `{{content}}` → 按序拼接
2. **禁止** `<script>`、外链 CSS、非常规标签（见 design-system 微信约束）
3. 图片：输出 `<!-- IMAGE: {desc} | 比例 {ratio} | 备注 {optional} -->` 占位；不在 HTML 中写外链 `<img>`
4. 允许外层单个 `<section>` 包裹；文首用 HTML 注释说明主题与复制步骤
5. **禁止** GenerateImage 或写入 `assets/`；配图仅占位

## 工作步骤

1. 读取 `raw-wechat.md`（不存在则读 `raw.md`），识别标题（首个 `#` 或文首标题行）、`【lead】`/`【pull】`/`【caption】`、`##`/`###`、段落、引用、列表、分割线、highlight 标注块、CTA
2. 按 [reference.md](reference.md) 选择对应 snippet 文件，读取模板，将 `{{content}}` 替换为内容（保留允许的 `strong`/`em`/`a`/`span`；`strong` 默认补 `color:#00997f`）
3. 将成稿中的配图占位（若有）原样或规范化为 design-system 规定的 `<!-- IMAGE: ... -->` 插入对应位置
4. 写入 `articles/<slug>/wechat.html`
5. 交付时说明：全选复制正文、在公众号编辑器粘贴、按注释上传配图

## 输出检查清单

- [ ] 每个块均来自 `snippets/` 之一
- [ ] 样式数值与 design-system token 一致
- [ ] 至少一处 `<!-- IMAGE: ... -->`（若 raw 无图，在导语后补一张封面/场景占位）
- [ ] 无 `<script>`、无全局 `<style>`

## 参考

详细映射表：[reference.md](reference.md)
