# AI Daily Radar｜AI 每日情报双源工作流

**中文** · [English](README.en.md)

一个可直接交给 ChatGPT、Claude Code、Codex 或其他支持联网检索/Agent Skills 的 AI 使用的每日 AI 情报工作流。

它不是新的资讯聚合站，也不重新托管第三方内容。项目把两个互补的公开上游组合成两条独立日报：

- **Follow Builders Daily**：关注真正做产品、研究和工程的人，优先原始观点、播客与官方博客。
- **AIHOT Daily**：覆盖更广的 AI 公共资讯池，并对 24 小时抓取完整性、分页连续性、去重和编辑层做显式审计。

默认参考配置来自一套长期运行的 ChatGPT Automations：每天 **08:00** 运行 Follow Builders，**08:10** 运行 AIHOT，时区为 `Asia/Shanghai`。两条任务可以独立使用，也可以在下游再做一次合并摘要。

> 核心设计：**一条追踪高信号 builder，一条追踪更广资讯面；先保真，再筛选；先说明覆盖边界，再做趋势判断。**

## 为什么不是一个“大而全”的 Prompt

两个来源承担不同职责：Follow Builders 更适合观察一手观点、产品/研究者动向和长内容；AIHOT 更适合查漏、形成更广的事件集合并审计覆盖率。把它们硬塞成一个任务，会混淆“来源完整性”和“编辑优先级”，也更难定位漏抓原因。

因此本仓库保留两条独立流水线，只在结构层统一：

1. **Upstream check**：每次先检查上游规则或数据结构是否更新。
2. **Freshness check**：区分“没有新内容”和“上游尚未刷新/抓取异常”。
3. **Coverage disclosure**：只有满足严格条件才宣称“完整”。
4. **Event-level dedup**：按事件而不是按文章去重。
5. **Source-first verification**：关键数字、政策、原话尽量回到一手来源核验。
6. **Decision-oriented output**：重点不是流水账，而是“今天什么真正变了”。

## 目录

```text
.
├── README.md
├── README.en.md              # English overview / quick start
├── llms.txt                  # 给 LLM/Agent 的极简入口索引
├── AGENTS.md                 # 给通用 AI/Agent 的入口
├── SKILL.md                  # Agent Skills 风格入口
├── manifest.yaml             # 机器可读任务清单
├── automations/
│   └── chatgpt.yaml          # 两条定时任务参考配置
├── prompts/
│   ├── follow-builders-daily.zh-CN.md
│   └── aihot-daily.zh-CN.md
├── docs/
│   ├── quickstart.md
│   ├── architecture.md
│   ├── source-contracts.md
│   └── origin.md
├── THIRD_PARTY.md
├── CHANGELOG.md
└── LICENSE
```

## 30 秒开始使用

### ChatGPT / 其他可联网 Agent

1. 先让 AI 读取 `AGENTS.md` 和 `manifest.yaml`。
2. 选择一条任务，把对应 `prompts/*.md` 作为定时任务或定期执行指令。
3. Follow Builders 默认每天 08:00；AIHOT 默认每天 08:10。
4. 如果平台支持 Agent Skills，可直接让 Agent 读取根目录 `SKILL.md`。

更详细的复制使用方式见 [`docs/quickstart.md`](docs/quickstart.md)。

## 两条日报的边界

| 任务 | 更擅长 | 主要上游 | 完整性策略 |
|---|---|---|---|
| Follow Builders | builder 原始观点、播客、官方博客 | `zarazhangrui/follow-builders` | 检查 feed 新鲜度；播客连续两天为 0 时才触发原始源兜底 |
| AIHOT Daily | 更广的 24h AI 公开资讯池、热点、日报 | `aihot.news` REST/RSS/MCP/Skill | REST cursor 完整翻页才可判定 A；A 仅表示当前查询窗口的公开池完整，不代表 AIHOT 全库或全网资讯 |

## 与上游的关系

本仓库是**编排与审计层**，不是上游项目的 fork。

- Follow Builders 的代码、feed、source list 和原始 prompts 仍以上游 `zarazhangrui/follow-builders` 为准；本仓库只提供日报 wrapper 和额外的数据质量规则。
- AIHOT 的 API/Skill/MCP/RSS 合同以 `https://aihot.news/agent` 和其 OpenAPI 为准；本仓库不重新托管 AIHOT 内容。
- 上游发生实质变更时，执行任务应优先遵循最新上游合同，再保留本仓库明确声明的本地策略。

详见 [`THIRD_PARTY.md`](THIRD_PARTY.md) 和 [`docs/source-contracts.md`](docs/source-contracts.md)。

## 适合谁

- 想用 ChatGPT Automations 做稳定 AI 日报，但不想每天手工搜索的人；
- 想同时保留“builder 原始信号”和“行业广覆盖”的产品经理、研究者、工程师；
- 想让 AI 明确说明“我到底抓全了没有”，而不是把可见结果冒充全量的人；
- 想把日报工作流交给 Codex / Claude Code / 其他 Agent 自动维护的人。

## 不做什么

- 不承诺任何第三方上游的 SLA；
- 不把搜索缓存或不完整分页冒充全量；
- 不重新发布第三方受版权保护的正文；
- 不自动把 AI 推断写成事实；
- 不把本仓库的默认时间、语言、来源数量视为永久不变的硬编码。

## License

本仓库原创的 wrapper prompts、文档和配置使用 MIT License。第三方项目、API、feed 与内容仍受各自条款约束，详见 `THIRD_PARTY.md`。

---

## English summary

**AI Daily Radar** is a reusable two-source AI intelligence workflow for ChatGPT and other agents. It combines a builder-first digest (Follow Builders) with a broader AI news coverage workflow (AIHOT), while keeping freshness checks, explicit coverage grades, event-level deduplication, source verification, and upstream-version awareness. It does not mirror or redistribute upstream content.
