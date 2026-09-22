# Changelog

## 0.1.0 — 2026-09-21

- Extracted two long-running daily AI intelligence workflows into a reusable public structure.
- Added machine-readable `manifest.yaml`, `AGENTS.md`, and `SKILL.md`.
- Parameterized user-specific schedule/language assumptions.
- Preserved Follow Builders upstream-sync, freshness, cross-day dedup and podcast zero-window fallback rules.
- Preserved AIHOT REST cursor integrity, webpage fallback, event-level dedup and A/B/C coverage grading.
- Switched AIHOT references to the current canonical `aihot.news` contract.
- Added third-party and redistribution boundaries.
- Clarified that AIHOT grade A means completeness of the queried public pool/window, not the entire AIHOT database or the whole web.
- Added `llms.txt` and a full English README for easier agent/human discovery.
