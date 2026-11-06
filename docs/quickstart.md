# Quick Start

## 方式一：ChatGPT Automations

创建两条独立定时任务：

1. **Follow Builders 日报**
   - 时间：每天 08:00
   - 时区：Asia/Shanghai
   - Prompt：`prompts/follow-builders-daily.zh-CN.md`

2. **AIHOT 每日情报**
   - 时间：每天 08:10
   - 时区：Asia/Shanghai
   - Prompt：`prompts/aihot-daily.zh-CN.md`

08:10 的错峰是有意的：AIHOT 官方日报在北京时间 08:00 发布，留出短暂缓冲后再执行查漏和汇总更合理。它不是协议要求，用户可自行修改。

## 方式二：Claude Code / Codex / 其他 Agent

把本仓库 clone 到本地后告诉 Agent：

> Read `AGENTS.md` and `manifest.yaml`, then run `follow-builders-daily`.

或：

> Read `AGENTS.md` and `manifest.yaml`, then run `aihot-daily`.

如果平台支持 Agent Skills，可让它加载根目录 `SKILL.md`。

## 方式三：只复制 Prompt

不想 clone 仓库时，直接复制对应 `prompts/*.md` 即可。仍建议在每次运行前检查上游，因为两个上游都可能调整数据结构与规则。

## 可选：Blog 研究待办候选

两条日报均可在原有正文与趋势总结之后增加 0–5 项「Blog 待办候选（待你确认）」。作者当前参考配置使用 `MarkTian-Long/marktian-long.github.io`；其他使用者须明确换成自己的 Blog 研究库。候选必须对照已有研究卡与已发布文章，避免重复选题。**定时任务只提出建议，不自动修改 Blog 待办、正文或排期**；后续必须等用户明确确认。

## 参数化建议

可以调整：

- `timezone`
- `schedule time`
- 输出语言
- 最终摘要长度
- 是否把两条日报再合并成一个 cross-source synthesis

不建议随意修改：

- 完整性判定条件
- cursor 原样回传规则
- “无数据”和“无新增”的区分
- 关键事实回源核验要求
