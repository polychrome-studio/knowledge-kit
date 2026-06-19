# Client Knowledge Template

**The template + spec for a client knowledge cartridge — one self-contained `.knowledge` package per client, holding their knowledge, their operable brand (`design.md`), the skills built for them, and their decision history.** Stamp a new client's cartridge from this skeleton.

> **Working name.** "Cartridge" is the explanatory metaphor (a sealed package you pick up whole); the formal label may change. Real cartridges are named `<client>.knowledge` — e.g. `turbotax.knowledge`, `group1.knowledge`.
>
> **Status:** Phase 0 — **structure and spec only.** No real client data lives here; this is the empty shape we agree on *before* stamping any client. The data line ([`BOUNDARY.md`](BOUNDARY.md)) needs legal/contract sign-off before a real cartridge is filled.

## What a cartridge is

A client's whole "game" in one sealed package:

- **the world** — their knowledge, history, what we've learned (`knowledge/`)
- **the characters** — their operable brand: voice, `design.md`, tokens, motion (`brand/`)
- **the special moves** — the skills/specialists built for them (`skills/`)

It's self-contained, portable, and client-ownable. The agency's *shared* brain (`cosi-knowledge`) keeps only de-identified, generalized craft — never a client's rich layer. Full model: [`cosi-knowledge/docs/vision/2026-06-18-client-knowledge-cartridges.md`](https://github.com/Collier-Simon/cosi-knowledge/blob/main/docs/vision/2026-06-18-client-knowledge-cartridges.md).

## The structure

```
<client>.knowledge/
  README.md             what this cartridge is (can be client-shareable)
  AGENTS.md             how agents work inside it (boundary rule is paramount)
  cartridge.yaml        manifest — client id, format version, contents, boundary policy
  BOUNDARY.md           the line — what rises to the shared brain vs. what stays
  knowledge/            the rich knowledge layer
    wiki/               curated per-channel / per-topic articles
    decisions/          dated ADRs — brand & creative decisions, with the why
    people/             client-side + account people
    sources/            pointers to raw sources (raw itself stays at source)
  brand/                the operable brand layer — schema'd by brand-substrate
    design.md  voice.md  tokens.json  motion.md
  skills/               client-specific skills / specialists built for them
```

## The line — read [`BOUNDARY.md`](BOUNDARY.md)

The one rule that makes the model honest: **rich, raw, and identifying material stays in the cartridge; only de-identified, generalized craft rises into `cosi-knowledge`.** This is the same boundary as the CoSi [data-handling standard](https://github.com/Collier-Simon/cosi-standards/blob/main/standards/data-handling.md) — the cartridge wall and "what's allowed to leave a client's container" are one line.

## How to stamp a new client (later, once the line is signed off)

1. Copy this template to `<client>.knowledge`.
2. Fill `cartridge.yaml` (client id, name, contents, set `boundary.legal_signoff: true` only after sign-off).
3. Eject the client's existing `cosi-knowledge/clients/<client>/` partition into `knowledge/`.
4. Author `brand/` to the brand-substrate schema; add the client-specific `skills/`.
5. Keep the boundary: nothing identifying leaves the cartridge un-sanitized.

## Related

- **Vision / model:** `cosi-knowledge/docs/vision/2026-06-18-client-knowledge-cartridges.md`
- **The boundary standard:** `cosi-standards/standards/data-handling.md`
- **Operable-brand schema:** `brand-substrate` (BrandOS)
- **The shared brain:** `cosi-knowledge`
- **Portability / local-run:** `data-sanitization-gateway`
