# Source Registry

## Purpose

Optional registry of raw and legacy documents and their processing status.

Use this to track which raw sources have been ingested, which are pending, and which were skipped.

---

## Status Values

- `pending` — not yet processed
- `ingested` — key knowledge compiled into docs / memory
- `skipped` — reviewed and determined to have no durable value
- `partial` — partially processed, needs follow-up

---

## Entry Format

| source | location | status | notes |
|--------|----------|--------|-------|

---

<!-- append entries below -->
