# Client Knowledge Template — Knowledge Layer (AGENTS.md)

> **What client-knowledge-template is.** The template + spec for a client knowledge cartridge — a self-contained `<client>.knowledge` package holding one client's knowledge, their operable brand (`design.md`), the skills built for them, and their decision history. **Status: Phase 0 — structure and spec only.** No real client data lives here; this is the empty shape agreed on before stamping any client's cartridge. See the root [`README.md`](../README.md) for the full model and [`BOUNDARY.md`](../BOUNDARY.md) for the data-boundary rule.

This is the **canonical** agent-instructions file for this knowledge layer, per the cross-tool [AGENTS.md](https://agents.md) standard — any agent (Claude Code, Cursor, Codex, …) reads it. The sibling `knowledge/CLAUDE.md` is a thin pointer back here; keep the orientation in this file, not duplicated there. Read this before touching `knowledge/` — whether you're improving the template's own spec, or about to stamp a new client's cartridge from it.

## What this knowledge layer is

Unusual among CoSi repos: this `knowledge/` folder is not a build-log of developing the template — it **is** the schema being templated. `wiki/`, `decisions/`, `people/`, and `sources/` are the exact shape that gets copied whole into `<client>.knowledge/knowledge/` when a client cartridge is stamped (per root `AGENTS.md`: "`knowledge/` follows the CoSi knowledge-layer pattern (wiki / decisions / people / sources), append-only with wiki-links"). Right now the four subfolders are empty placeholders (each holding only a `.gitkeep`, except `wiki/_overview.md`, which is itself a fill-in-the-blank template for the client's orientation page). Once a real client's cartridge is stamped and an account team starts working it, this same folder — in the copy — fills up with real wiki articles, decision records, people entries, and source pointers, and the three rules below govern that accumulation.

### The doc surfaces (don't confuse them)

- **`knowledge/`** (this layer) — the cartridge's rich-knowledge schema: curated wiki, brand/creative decision records, client + account people, pointers to raw sources. Empty here; populated once stamped for a real client.
- **`README.md`** (repo root) — the plan: what a cartridge is, the full structure, how to stamp a new client. Read for *why this template exists and how to use it*.
- **`AGENTS.md`** (repo root) — how agents must behave *inside a stamped cartridge*, principally the data boundary. A different concern from this file: that one is a data-handling contract binding on any cartridge stamped from this template; this one is knowledge-layer orientation for working inside `knowledge/` specifically.
- **`BOUNDARY.md`** — the line itself: what's allowed to leave a client's container (rises to `cosi-knowledge`) vs. what never leaves un-sanitized.
- **`cartridge.yaml`** — the manifest (client id, format version, contents, boundary sign-off gate).
- No external runtime source of truth — this is a template/spec repo, not a running system.

## How it's organized

```
knowledge/
  AGENTS.md          this file (canonical) — orientation, the three rules, the formats
  CLAUDE.md          thin pointer to AGENTS.md (so Claude Code discovers the layer)
  wiki/              curated per-channel / per-topic articles — _overview.md is the fill-in template for the client's orientation page
  decisions/         dated ADRs — brand & creative decisions, with the why (currently .gitkeep only)
  people/            client-side + account people (currently .gitkeep only)
  sources/           pointers to raw sources; raw itself stays at source (currently .gitkeep only)
```

This schema swaps the usual `journal/` + `research/` pair for `people/` + `sources/` — a stamped cartridge's session material is expected to flow from `sources/` (pointers to transcripts/meetings held elsewhere) into `wiki/`/`decisions/` at compile time, rather than through an interim journal folder. If that turns out to be the wrong call once a real client is stamped and actively worked, add `journal/` then — don't add it speculatively here.

## Claim provenance tags (optional, use sparingly)

Beyond article-level `confidence:`, an individual claim inside a wiki article or ADR can carry a provenance tag for *how it was known*, not just how confident you are:
- **`EXTRACTED`** — sourced directly from a source in `sources/` (ground truth for what was said/decided)
- **`INFERRED`** — assembled from reading or extrapolation (verify before acting)

Use these inline, only when the distinction matters for the reader.

---

## The three rules — no more

### Rule 1 — Journal *continuously*, wiki at the end

The journal is the firehose — write to it **as you go, not at session end.** Batching journal writes to the end loses information: you forget, you compress it away, or the session crashes and it's gone. The journal must survive a crash at any point.

**Checkpoint cadence — append to today's `journal/YYYY-MM-DD-slug.md` after any of these, while fresh:**
- a larger move lands (a feature works, a subsystem changes, a milestone closes)
- a longer code run completes (a big edit pass, a refactor, a tricky debug)
- **right after each `git commit`** — the commit is the natural "larger move" marker; journal the *why* the commit message doesn't capture (a breadcrumb hook automates the prompt)
- before any risky/irreversible operation (so intent is recorded even if it goes wrong)

A rough running entry beats a perfect one that never gets written. The entry is append-only — keep adding sections as the session progresses.

**Wiki, by contrast, is end-of-session only.** At session end an **explicit compile pass** promotes mature journal entries into wiki updates (per Rule 2). Without an explicit trigger the wiki stays untouched — that keeps it intentional and the prompt cache stable. *Journal hot and often, compile to wiki cold and deliberately.*

For this template's schema (no `journal/` folder — see above), read this as: session material lands in `sources/` as it happens, and the same discipline applies at compile time — wiki/decisions only get written on a real trigger, not "just in case."

### Rule 2 — Wiki updates require a real trigger — only three
1. A new subsystem/capability got added → write a new article or new section.
2. A previously-documented decision is now contradicted → update the article + log the contradiction.
3. The user explicitly said "document this in the wiki."

No "just in case" updates. No proactive rewrites of articles that aren't broken.

### Rule 3 — Append-only, wiki-links everywhere
Wiki articles are append-only context logs with dated entries. Journal and decision entries are append-only. All cross-references use `[[wiki-links]]`. Never edit prior entries; if something is wrong, append a correction with a link to the contradicting source.

---

## Journal entry format — ADR-flavored

Each `journal/YYYY-MM-DD-slug.md`:

```markdown
---
type: Journal                      # OKF-required concept type (keep it)
date: YYYY-MM-DD
session: short-slug
status: in-progress | shipped | abandoned | superseded-by [[YYYY-MM-DD-slug]]
related: [[article-1]], [[article-2]]
---

# Session Title — What we worked on

## Context
Where we were when we started. What problem this session was responding to.

## What changed
- Paths touched: `src/...`
- Subsystems affected: [[article]]
- Behavior shipped: brief description

## Decisions made
- **Decision** — short statement. Rationale + link: [[decisions/YYYY-MM-DD-slug]]

## What was tried and abandoned
- Tried X — dropped because Y. Saves the next teammate from re-litigating.

## Open threads
- [ ] Next-session item with [[wiki-link]]

## Related
- Touched articles: [[article]]
```

## Decision record format — standard ADR

Each `decisions/YYYY-MM-DD-slug.md`:

```markdown
---
type: Decision                     # OKF-required concept type (keep it)
date: YYYY-MM-DD
status: accepted | proposed | deprecated | superseded-by [[YYYY-MM-DD-slug]]
deciders: {{DECIDERS}}
related: [[article-1]]
---

# Decision: One-sentence statement (verb-led, decisive)

## Context
The forces at play. What we were deciding against. Why now.

## Decision
What we're doing.

## Consequences
- **Positive:** what gets easier
- **Negative:** what gets harder, what we're trading away
- **Neutral:** what changes that's neither good nor bad

## Dissent / Alternatives Considered
Options weighed *before* the decision and why each lost. If there were none, say
"None — only viable path given X" so absence is explicit.

## Sources
- [[journal/YYYY-MM-DD-slug]] — session where this surfaced
```

## Wiki article frontmatter convention

```yaml
---
name: short-kebab-slug
type: subsystem | topic | meta | roadmap
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
confidence: high | medium | low | speculative
related: [[other-article-1]], [[other-article-2]]
---
```

**`confidence:`** — **high** (in code / ratified in a decision / repeatedly confirmed) · **medium** (said once, one source, not contradicted) · **low** (inference / single source, provisional) · **speculative** (extrapolation, revisit before acting). Add it when an article is touched for a real reason, not in a bulk pass.

---

## Context log

### 2026-07-01 — AGENTS.md + CLAUDE.md added
This template's `knowledge/` folder had `wiki/`, `decisions/`, `people/`, and `sources/` but no orientation file — nothing telling a session how the folder is meant to be used, or that it's the cartridge schema itself rather than a build-log of this repo. Added per the CoSi standard (`cosi-standards/standards/knowledge-layer.md`), which every CoSi build repo now follows: canonical `knowledge/AGENTS.md` + thin `knowledge/CLAUDE.md` pointer.
