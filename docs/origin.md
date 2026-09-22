# Origin and cleanup notes

This repository was extracted on 2026-09-21 from two active daily ChatGPT automation workflows:

- `Follow Builders 日报` — daily at 08:00, Asia/Shanghai.
- `AIHOT 每日情报` — daily at 08:10, Asia/Shanghai.

The public version is intentionally not a raw dump of private task state. It preserves the operational logic while making the workflow reusable.

## Public cleanup performed

- Removed user-specific wording and made schedule/language settings explicit defaults.
- Replaced hard-coded Follow Builders source counts with “read the current upstream source list”.
- Kept the two-day Podcast zero-window fallback and cross-day dedup rules.
- Kept AIHOT REST cursor integrity, webpage fallback, Pass 2 continuity checks, event-level dedup and A/B/C coverage grading.
- Replaced the historical AIHOT hostname with the current canonical `aihot.news` integration contract.
- Added third-party redistribution boundaries and source-contract documentation.
- Added `AGENTS.md`, `SKILL.md`, and `manifest.yaml` so agents do not need to infer repository structure from the README.

## What was deliberately not published

- Automation runtime IDs, internal execution IDs and platform-specific private state.
- Previous run logs and historical state that are useful only to one account.
- Third-party feed contents or copyrighted full-text material.
