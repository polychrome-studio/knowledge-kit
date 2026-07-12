# Client Knowledge Template — Knowledge Layer (AGENTS.md)

> **What client-knowledge-template is.** The template + spec for a client knowledge capsule — a self-contained `<client>.knowledge` package holding one client's knowledge, their operable brand (`design.md`), the skills built for them, and their decision history. **Status: Phase 0 — structure and spec only.** No real client data lives here; this is the empty shape agreed on before stamping any client's capsule. See the root [`README.md`](../README.md) for the full model and [`BOUNDARY.md`](../BOUNDARY.md) for the data-boundary rule.

This is the **canonical** agent-instructions file for this knowledge layer, per the cross-tool [AGENTS.md](https://agents.md) standard — any agent (Claude Code, Cursor, Codex, …) reads it. The sibling `knowledge/CLAUDE.md` is a thin pointer back here; keep the orientation in this file, not duplicated there. Read this before touching `knowledge/` — whether you're improving the template's own spec, or about to stamp a new client's capsule from it.

## What this knowledge layer is

Unusual among CoSi repos: this `knowledge/` folder is not a build-log of developing the template — it **is** the schema being templated. `wiki/`, `decisions/`, `people/`, and `sources/` are the exact shape that gets copied whole into `<client>.knowledge/knowledge/` when a client capsule is stamped (per root `AGENTS.md`: "`knowledge/` follows the CoSi knowledge-layer pattern (wiki / decisions / people / sources), append-only with wiki-links"). Right now the four subfolders are empty placeholders (each holding only a `.gitkeep`, except `wiki/_overview.md`, which is itself a fill-in-the-blank template for the client's orientation page). Once a real client's capsule is stamped and an account team starts working it, this same folder — in the copy — fills up with real wiki articles, decision records, people entries, and source pointers, and the three rules below govern that accumulation.

### The doc surfaces (don't confuse them)

- **`knowledge/`** (this layer) — the capsule's rich-knowledge schema: curated wiki, brand/creative decision records, client + account people, pointers to raw sources. Empty here; populated once stamped for a real client.
- **`README.md`** (repo root) — the plan: what a capsule is, the full structure, how to stamp a new client. Read for *why this template exists and how to use it*.
- **`AGENTS.md`** (repo root) — how agents must behave *inside a stamped capsule*, principally the data boundary. A different concern from this file: that one is a data-handling contract binding on any capsule stamped from this template; this one is knowledge-layer orientation for working inside `knowledge/` specifically.
- **`BOUNDARY.md`** — the line itself: what's allowed to leave a client's container (rises to `cosi-knowledge`) vs. what never leaves un-sanitized.
- **`capsule.yaml`** — the manifest. dotKnowledge SPEC.md §5-conformant: `subject`/`type`/`relationship`/`parent`/`status`/`format_version`/`rises`/`access`/`legal_signoff`, plus a CoSi-specific `contents:` block on top (§8: the format is designed to be extended).
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

This schema swaps the usual `journal/` + `research/` pair for `people/` + `sources/` — a stamped capsule's session material is expected to flow from `sources/` (pointers to transcripts/meetings held elsewhere) into `wiki/`/`decisions/` at compile time, rather than through an interim journal folder. If that turns out to be the wrong call once a real client is stamped and actively worked, add `journal/` then — don't add it speculatively here.

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
basis: authored | live-source | partner-attested | vendor-doc | forecast | computed | inferred   # SPEC.md §4 — where the claim came from
status: proposed | accepted | superseded | deprecated   # SPEC.md §4 — has *this record* been affirmed; distinct from basis, see below
superseded_by: [[YYYY-MM-DD-slug]]   # only present when status: superseded — the pointer lives here, not embedded in status
deciders: {{approver role, not a name — see note below}}
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

**`basis:` and `status:` are different axes — do not conflate them.** A claim can be `authored` (a person stated it directly) and still be an unaffirmed `status: proposed` record. Confusing the two is the exact bug this split exists to prevent (dotKnowledge SPEC.md §4).

**Automated writers may only ever write `status: proposed`.** Moving a record to `accepted`, `superseded`, or `deprecated` requires an append-only affirmation event (who, role, evidence, when) — never an in-place edit of this field. This capsule doesn't yet have its own affirmation tooling; until it does, treat any `status:` above `proposed` written by an agent as a bug, not a shortcut.

**`deciders:` — do not hardcode a name.** Who is authorized to affirm a decision *in this specific client's capsule* must resolve to a live role (e.g. "the account lead of record"), never a name baked into the file — a hardcoded name goes stale the moment that person leaves the account. This is a real, currently-open question — see dotKnowledge SPEC.md §9 ("Capsule-approver identity") and FOUNDRY's `knowledge/specs/2026-07-09-decision-record-affirmation.md` for the fuller framing. Resolving it is the mounting platform's job, not this template's — until it's resolved, leave `deciders:` naming a role description in prose, not a person.

## Wiki article frontmatter convention

```yaml
---
name: short-kebab-slug
type: subsystem | topic | meta | roadmap
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
basis: authored | live-source | partner-attested | vendor-doc | forecast | computed | inferred   # optional — where the claim came from; SPEC.md §4
confidence: high | medium | low | speculative
score: 0.0-1.0   # optional — only when actually computed; absent means "not computed"
classification: public | internal | confidential | restricted   # sensitivity — assign for anything client-identifying (see BOUNDARY.md)
related: [[other-article-1]], [[other-article-2]]
---
```

**`confidence:`** — **high** (in code / ratified in a decision / repeatedly confirmed) · **medium** (said once, one source, not contradicted) · **low** (inference / single source, provisional) · **speculative** (extrapolation, revisit before acting). Add it when an article is touched for a real reason, not in a bulk pass.

**`basis:`, `score:`, and `classification:` are optional and additive** (dotKnowledge SPEC.md §4) — add them when they carry real signal, not as a bulk backfill. `basis:` and `status:` (decisions only, see below) are different axes — a claim can be `authored` and still unaffirmed; don't conflate "where it came from" with "has a human signed off on it." `classification:` matters most here: this capsule holds one client's identifying data by design, so tagging anything genuinely sensitive `confidential`/`restricted` is what lets `rises:` (BOUNDARY.md, `capsule.yaml`) actually be enforced rather than just declared.

---

## Context log

### 2026-07-01 — AGENTS.md + CLAUDE.md added
This template's `knowledge/` folder had `wiki/`, `decisions/`, `people/`, and `sources/` but no orientation file — nothing telling a session how the folder is meant to be used, or that it's the capsule schema itself rather than a build-log of this repo. Added per the CoSi standard (`cosi-standards/standards/knowledge-layer.md`), which every CoSi build repo now follows: canonical `knowledge/AGENTS.md` + thin `knowledge/CLAUDE.md` pointer.

### 2026-07-12 — Brought current to dotKnowledge SPEC.md, ahead of real capsule builds
Audited against the real spec (github.com/inkxel/dotKnowledge) ahead of Tucker stamping real client capsules over the following days. Findings and fixes:
- **`cartridge.yaml` → `capsule.yaml` was a rename debt, not just a rename.** The 2026-06-25 cartridge→capsule terminology sweep (`cosi-knowledge` decision `2026-06-25-rename-cartridge-term.md`) never touched this repo's manifest — it was still `cartridge.yaml`, and its schema had independently drifted from SPEC §5 (missing `type:`/`relationship:`/`parent:`/`access:` entirely, `format:`/`version:` using different keys than `format_version:`, `rises:` as free prose instead of the 3-value enum, `legal_signoff` nested under a `boundary:` key the real spec doesn't have). Rebuilt against §5 directly, kept a `contents:` block as an explicit, additive CoSi extension (permitted per §8). Swept the "cartridge" prose sweep across README/AGENTS.md/BOUNDARY.md/design.md/skills-README (word-boundary-safe — the two references to `cosi-knowledge`'s actual, still-cartridge-named vision doc filename were deliberately left alone since the target file itself was never renamed).
- **Added `brand/personas.md`** — was missing entirely; `brand/` had design/voice/motion/tokens but no audience layer. Added following the same fill-in-blank pattern as `voice.md`.
- **Wiki and decision frontmatter brought current to SPEC §4** — `basis:`/`score:`/`classification:` were entirely absent from both the documented convention and `wiki/_overview.md`'s own template (which had no frontmatter block at all). Added, with an explicit note that `basis:` and `status:` are different axes.
- **Stated the affirmation-event behavioral contract explicitly** — the `status:` enum existed but nothing said agents may only ever write `proposed`, or that promotion requires an append-only event. This capsule has no affirmation tooling of its own yet; until it does, treat any agent-written `status:` above `proposed` as a bug.
- **`deciders: {{DECIDERS}}` replaced with a real pointer**, not a blank placeholder — capsule-approver identity is a known-open question (dotKnowledge SPEC.md §9, FOUNDRY's `2026-07-09-decision-record-affirmation.md`), and the answer must never be a hardcoded name. Left as an explicit note rather than inventing a resolution mechanism this template isn't positioned to own.
- Fixed three `capsule.yaml → boundary.legal_signoff: true` references (README/AGENTS.md/BOUNDARY.md) to the flattened `capsule.yaml → legal_signoff: true` path, matching the rebuilt manifest.

**Not fixed, flagged for Tucker:** the "Journal entry format" section above documents a `journal/YYYY-MM-DD-slug.md` format, but this template's own schema explicitly has no `journal/` folder (swapped for `people/`+`sources/`, per this file's own "How it's organized" section). That's a pre-existing internal inconsistency, not something introduced today — left as-is rather than guessing which side is stale.
