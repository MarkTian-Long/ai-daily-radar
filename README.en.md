# AI Daily Radar

[中文](README.md) · **English**

AI Daily Radar is a reusable two-lane AI intelligence workflow for ChatGPT, Claude Code, Codex, and other web-enabled agents. It combines two complementary upstreams without mirroring their content:

- **Follow Builders Daily** — high-signal updates from people building AI products, research, and infrastructure, plus tracked podcasts and official blogs.
- **AIHOT Daily** — broader public AI-news coverage with explicit freshness checks, cursor-chain auditing, event-level deduplication, and coverage grades.

The reference schedule is 08:00 and 08:10 in `Asia/Shanghai`. Both tasks can run independently. A downstream agent may synthesize them only after each lane has completed its own coverage checks.

## Quick start

For an AI agent:

1. Read `AGENTS.md`.
2. Read `manifest.yaml`.
3. Select one task and read its prompt in `prompts/` in full.
4. Check the current upstream contract before execution.
5. Run the task without weakening its freshness/completeness rules.

Task mapping:

- `follow-builders-daily` → `prompts/follow-builders-daily.zh-CN.md`
- `aihot-daily` → `prompts/aihot-daily.zh-CN.md`

If your platform supports Agent Skills, load `SKILL.md`. For scheduler examples, see `automations/chatgpt.yaml` and `docs/quickstart.md`.

## Design principles

- Check upstream changes before every run.
- Distinguish “no new content” from stale or failed upstream data.
- Never guess cursors, pagination URLs, story IDs, schemas, or source metadata.
- Deduplicate at the event level, not merely by article URL.
- Verify critical numbers, policies, and quotations against original sources when possible.
- State coverage boundaries explicitly before making trend claims.

For AIHOT, grade **A** means the queried public pool/window was paginated to completion. It does **not** mean the entire AIHOT database or the whole web was captured.

## Repository map

- `AGENTS.md` — execution rules for general agents
- `SKILL.md` — Agent Skills-style router
- `manifest.yaml` — machine-readable tasks and defaults
- `prompts/` — reusable task prompts
- `automations/chatgpt.yaml` — reference scheduler configuration
- `docs/` — architecture, quick start, source contracts, and origin notes
- `THIRD_PARTY.md` — upstream and redistribution boundaries
- `llms.txt` — compact LLM-oriented index

## Upstreams

Follow Builders: `https://github.com/zarazhangrui/follow-builders`

AIHOT Agent contract: `https://aihot.news/agent`

AIHOT OpenAPI v1: `https://aihot.news/openapi-v1.json`

This repository is an orchestration/documentation layer. It does not vendor or republish upstream feeds, full articles, tweets, podcast transcripts, or API datasets.

## License

Original wrapper prompts, documentation, and configuration in this repository are MIT licensed. Upstream projects, feeds, APIs, and content remain subject to their own licenses and terms. See `THIRD_PARTY.md`.
