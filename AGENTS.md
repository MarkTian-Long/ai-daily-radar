# AGENTS.md

This repository is designed to be readable and executable by AI agents.

## Entry procedure

1. Read `manifest.yaml` first.
2. Select exactly one task unless the user explicitly asks for both.
3. Read the corresponding file under `prompts/` in full before execution.
4. Before using an upstream source, check the current upstream contract described in `docs/source-contracts.md`.
5. Treat upstream source lists, endpoint schemas, cursor rules and feed structure as dynamic unless explicitly documented as stable.

## Non-negotiable rules

- Never claim a complete 24-hour set unless the prompt's completion condition is actually satisfied. For AIHOT, “complete” means the queried public pool/window only, never the entire AIHOT database or the whole web.
- Distinguish “no new content” from “feed/API not refreshed or inaccessible”.
- Never guess pagination URLs, story IDs, cursors, API fields or source metadata.
- Event-level deduplication is preferred over article-level deduplication.
- Important numbers, policies and quotations should be verified against the original source when possible.
- Do not republish full third-party articles or feeds into this repository or output unless redistribution is explicitly allowed.
- Upstream changes override stale implementation details here; local editorial preferences still apply unless they conflict with the upstream contract.

## Task dispatch

- `follow-builders-daily` → `prompts/follow-builders-daily.zh-CN.md`
- `aihot-daily` → `prompts/aihot-daily.zh-CN.md`

## Defaults

- Output language: Simplified Chinese
- Time display: Beijing time unless user requests another timezone
- Follow Builders schedule: 08:00 Asia/Shanghai
- AIHOT schedule: 08:10 Asia/Shanghai
- Delivery: in-chat unless the hosting agent provides another configured channel

These are defaults, not protocol requirements.
