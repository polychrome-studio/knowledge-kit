---
name: Research log — client-intelligence freshness manifest
type: manifest
created: TEMPLATE
last_updated: TEMPLATE
---

# {SUBJECT} — research freshness log

Tracks when each component of the standing **client-intelligence layer** was last refreshed, so the bundle's knowledge never goes silently stale. This log ships in **every** bundle (stamped from knowledge-kit). Doctrine + rationale: FOUNDRY `knowledge/plans/2026-07-17-standing-client-intelligence-refresh.md`. Update "last run" + "next due" on every refresh, and log what *changed* since last time (the delta is the point, not just fresh data).

| Component | Source / tool | Last run | Cadence | Next due | Artifact / notes |
|---|---|---|---|---|---|
| Creative — Meta/IG ad library | Apify `apify/facebook-ads-scraper` | — | monthly | — | `ad-library-meta.md` |
| Creative — TikTok ad library | Apify (TikTok actor) | — | monthly | — | |
| Creative — Google Ads Transparency | browser/web | — | monthly | — | `ad-creative-firstlook.md` |
| Website intelligence | Firecrawl (own site) | — | quarterly | — | `website-intel.md` |
| Positioning | web research | — | quarterly | — | `positioning.md` |
| Reputation / social listening | web (reviews · Reddit · X) | — | monthly | — | `reputation.md` |
| Competitive set | web research | — | quarterly | — | `competitive-set.md` |
| Competitor ad-libraries + sites (white-space) | Apify + Firecrawl | — | monthly | — | the white-space layer |
| Slack — client + shared channels | Slack MCP / platform nightly ingest | — | monthly | — | **Match the client name ANYWHERE in the channel name, not as a prefix.** The client-shared Slack Connect channel is conventionally `ext-<client>-<agency>` — a prefix-anchored search misses the one channel the client actually talks in. Separators also vary (`_` and `-`). |

**Cadence rationale:** creative + reputation move fast → monthly; positioning + website + competitive shift slower → quarterly. Bump any row to a faster cadence around a live pitch or campaign launch.
