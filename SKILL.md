---
name: ai-daily-radar
description: Two-source AI intelligence workflow using Follow Builders and AIHOT. Use for daily AI digests, builder updates, broad AI news coverage, freshness auditing, event-level deduplication, and source-aware trend summaries.
---

# AI Daily Radar

Use this repository as a routing skill, not as a replacement for either upstream service.

## When invoked

1. Read `manifest.yaml`.
2. If the user asks for builder/researcher/founder activity, run `follow-builders-daily`.
3. If the user asks for broad AI news coverage or a 24-hour AI digest, run `aihot-daily`.
4. If the user asks for the full radar, run both independently, preserve each task's coverage boundary, then optionally produce a short cross-source synthesis after both reports.

Do not merge raw source pools before each task has independently completed its own freshness and coverage checks.

For execution rules, read the full prompt file referenced by the selected task in `manifest.yaml`.
