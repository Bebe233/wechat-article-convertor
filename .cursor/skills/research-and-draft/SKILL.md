---
name: research-and-draft
description: >-
  Researches local paths or URLs and produces facts.md then platform-specific
  raw-wechat.md and/or raw-xhs.md. Use when gathering product facts, drafting
  公众号/小红书成稿, or before layout stage in wechat-article-convertor workflow.
disable-model-invocation: true
---

# Research and Draft

从用户提供的**本地路径**和/或**网站 URL** 调研，产出 `facts.md` 与平台成稿。由 **wechat-article-pipeline** 调用；本 Skill 不生成 `wechat.html` 或 `xhs.md` 终稿。

## 调研范围（只读）

- README、package/依赖清单、目录结构、`docs/`、`src/` 核心模块
- 网站：MCP 或用户提供的 URL；不可访问时在 `facts.md` 标注「待核实」
- **禁止**编造来源中不存在的功能；不确定写入「待核实」

## 产出 1：`articles/<slug>/facts.md`

```markdown
# 事实表 — {项目名}

## 产品一句话
（一句定位）

## 功能列表
- ...

## 技术亮点
- ...

## 差异化
- ...

## 目标用户
- ...

## 可引用数据/案例
- ...

## 不宜夸大项
- ...

## 待核实
- （缺口、未读到的模块）
```

调研完成后**停止**，等待用户确认事实表/大纲（pipeline 卡点 1）。

## 产出 2a：`articles/<slug>/raw-wechat.md`（平台含微信时）

用户确认 `facts.md` 后撰写。中文营销稿，**Markdown 结构**，**不含**微信 HTML：

```markdown
# 文章标题

（导语 1–2 段）

<!-- IMAGE: ... -->

## 痛点
...

## 方案
...

## 功能亮点
- ...

## 场景/案例
...

## 总结
...

（文末 CTA 一句）
```

- 语气、受众、字数、是否 CTA：按 pipeline 收集的**微信**侧输入执行
- 至少一处 `<!-- IMAGE: {desc} | 比例 {ratio} | 备注 {optional} -->`
- 功能亮点 3–5 条为宜
- 与 `raw-xhs.md` **独立撰写**，不共用 master 稿

## 产出 2b：`articles/<slug>/raw-xhs.md`（平台含小红书时）

用户确认 `facts.md` 后撰写。应用 **[xhs-draft](../xhs-draft/SKILL.md)** 规则与模板。

- 语气、字数、配图张数、标签策略：按 pipeline 收集的**小红书**侧输入执行

## 卡点 2

平台所需的成稿文件**都写完**后再**停止**，请用户**一次**确认 `raw-wechat.md` 和/或 `raw-xhs.md`，再交给 **wechat-layout** / **xhs-format**。

## 大仓库说明

若由 pipeline 并行 `explore` 合并信息，仍以本结构写入单一 `facts.md`，不并行写 `raw-*.md`。
