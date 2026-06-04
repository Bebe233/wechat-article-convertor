# 微信公众号文章工作流

请加载项目 Skill **wechat-article-pipeline**，并按流水线执行（含两个用户确认卡点）。

## 请用户提供或确认

1. **来源**：本地项目路径（如 `D:\projects\foo`）和/或 网站 URL
2. **受众**：例如开发者、产品经理、运营
3. **语气**：例如专业克制、轻松口语、硬核技术（每次指定，不沿用默认值）
4. **字数**：大致篇幅（如 1500 字、短文 800 字）
5. **是否 CTA**：文末是否引导关注/试用/访问链接
6. **slug**（可选）：`articles/<slug>/` 目录名，kebab-case
7. **配图策略**：`占位 only`（默认）或 `尝试生成或引用`

## 执行要求

- 阶段 1 产出 `articles/<slug>/facts.md` 后停止，等待我确认
- 确认后产出 `raw.md` 并再次停止等待确认
- 确认后再调用 wechat-layout 产出 `wechat.html`
- 参考 `articles/_example/` 与 `docs/design-system.md`

开始请先复述你将使用的 slug 与输入摘要，再进入调研。
