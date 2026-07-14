---
name: overview
type: meta
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
confidence: high
related: []
---

# <Client> — knowledge overview

> Template. The entry point to this client's rich knowledge layer. Mirrors the `cosi-knowledge` partition shape — when a client is promoted, their existing `cosi-knowledge/clients/<client>/` partition ejects into this `knowledge/` folder.

## Who they are
<one-paragraph orientation — sector, what we do for them, the relationship>

## How we work with them
<channels, cadence, what's worked, what hasn't>

## Where things live
- `wiki/` — curated per-channel / per-topic / per-project / per-person articles (`type: person` for people — no separate `people/` folder)
- `decisions/` — dated ADRs (brand & creative decisions, with the why)
- `sources/` — pointers to raw sources (raw stays at source)
