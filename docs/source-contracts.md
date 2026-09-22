# Source Contracts

## Follow Builders

Authority: `https://github.com/zarazhangrui/follow-builders` main branch.

执行时优先读取最新的：

- `SKILL.md`
- README / README.zh-CN
- `prompts/`
- `config/`
- `scripts/`
- 当前 feed 文件

不要在本仓库硬编码 builder 数量、Podcast 数量或永久文件名。上游 README 当前声明其 source list 与 feed 由中心化服务维护，并可能持续更新。

## AIHOT

Canonical agent integration page: `https://aihot.news/agent`

OpenAPI v1: `https://aihot.news/openapi-v1.json`

REST base: `https://aihot.news/api/v1`

关键执行合同：

- 匿名只读，不需要 API Key；
- `mode=all` 指 AIHOT 最近公开池，不等于 AIHOT 全库；公开池还会排除部分来源、未审内容、低相关条目和已合并重复项；
- items 支持 `mode=selected|all`、`window=24h|7d`、`by=timeline|published`；
- cursor 必须原样回传，不跨查询/跨天复用；
- 普通 items 单次 limit 上限为 100；
- Story ID 只能从 Hot Topics 返回结果获取，不能猜；
- 429 遵循 `Retry-After`；
- AIHOT 官方明确说明匿名 RSS/API 可读不等于第三方内容获得公开再分发许可。

如果这些字段或约束与未来官方合同冲突，以官方最新合同为准。
