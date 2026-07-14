# knowledge-kit

**The template for a `.knowledge` capsule — one self-contained package per subject (client, in-house studio, or person), holding their knowledge, their operable brand (`design.md`), the skills built for them, and their decision history.** Stamp a new capsule from this skeleton. Renamed 2026-07-13 from `client-knowledge-template` — same template, no longer client-only in scope (see `tucker.knowledge`, `creative-systems-studio.knowledge` for non-client examples already stamped from it).

> The *ongoing* work of stamping capsules, migrating content into them, and keeping them current lives in a separate, sibling repo: `Collier-Simon/knowledge-engine`. This repo defines *what a capsule looks like*; that one *runs* the process.

> **"Capsule"** is the adopted term — a sealed, portable package, per the [dotKnowledge](https://github.com/inkxel/dotKnowledge) `.knowledge` standard this template conforms to (`capsule.yaml`, SPEC.md §5). Real capsules are named `<client>.knowledge` — e.g. `turbotax.knowledge`, `group1.knowledge`.
>
> **Status:** Phase 0 — **structure and spec only.** No real client data lives here; this is the empty shape we agree on *before* stamping any client. The data line ([`BOUNDARY.md`](BOUNDARY.md)) needs legal/contract sign-off before a real capsule is filled.

## What a capsule is

A client's whole "game" in one sealed package:

- **the world** — their knowledge, history, what we've learned (`knowledge/`)
- **the characters** — their operable brand: voice, `design.md`, tokens, motion (`brand/`)
- **the special moves** — the skills/specialists built for them (`skills/`)

It's self-contained, portable, and client-ownable. The agency's *shared* brain (`cosi-knowledge`) keeps only de-identified, generalized craft — never a client's rich layer. Full model: [`cosi-knowledge/docs/vision/2026-06-18-client-knowledge-cartridges.md`](https://github.com/Collier-Simon/cosi-knowledge/blob/main/docs/vision/2026-06-18-client-knowledge-cartridges.md).

## The structure

```
<client>.knowledge/
  README.md             what this capsule is (can be client-shareable)
  AGENTS.md             how agents work inside it (boundary rule is paramount)
  capsule.yaml          manifest — dotKnowledge SPEC.md §5: subject/type/relationship/parent/
                          status/rises/access/local/legal_signoff, plus a CoSi-specific contents: block
  BOUNDARY.md           the line — what rises to the shared brain vs. what stays
  knowledge/            the rich knowledge layer
    wiki/               curated per-channel / per-topic articles
    decisions/          dated ADRs — brand & creative decisions, with the why
    people/             client-side + account people
    sources/            pointers to raw sources (raw itself stays at source)
    ledger/             append-only, agent-authored — what changed in this capsule and why (no journal/ — that's person-bundles only, SPEC §3)
  brand/                the operable brand layer — schema'd by brand-substrate
    design.md  voice.md  personas.md  tokens.json  motion.md
  skills/               client-specific skills / specialists — only capability that only makes sense because of this one client (SPEC §3); generic mechanism stays in the console
```

## The line — read [`BOUNDARY.md`](BOUNDARY.md)

The one rule that makes the model honest: **rich, raw, and identifying material stays in the capsule; only de-identified, generalized craft rises into `cosi-knowledge`.** This is the same boundary as the CoSi [data-handling standard](https://github.com/Collier-Simon/cosi-standards/blob/main/standards/data-handling.md) — the capsule wall and "what's allowed to leave a client's container" are one line.

## How to stamp a new client (later, once the line is signed off)

1. Copy this template to `<client>.knowledge`.
2. Fill `capsule.yaml`'s `<placeholders>` (`subject`, `name`, `status`) and confirm the pre-filled fields still fit (`type: brand`, `relationship: client`, `parent: cosi`, `rises: de-identified`) — set `legal_signoff: true` only after sign-off, not before.
3. Eject the client's existing `cosi-knowledge/clients/<client>/` partition into `knowledge/`.
4. Author `brand/` to the brand-substrate schema (including `personas.md`); add the client-specific `skills/`.
5. Keep the boundary: nothing identifying leaves the capsule un-sanitized.

## Related

- **Vision / model:** `cosi-knowledge/docs/vision/2026-06-18-client-knowledge-cartridges.md`
- **The boundary standard:** `cosi-standards/standards/data-handling.md`
- **Operable-brand schema:** `brand-substrate` (BrandOS)
- **The shared brain:** `cosi-knowledge`
- **Portability / local-run:** `data-sanitization-gateway`
