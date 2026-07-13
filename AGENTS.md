# Client Knowledge Capsule — agent contract

A self-contained `.knowledge` capsule for ONE client: their knowledge + operable brand + client-specific skills + decisions. (This repo is the empty **template** — Phase 0, no real client data.)

## Follow the CoSi standards
`Collier-Simon/cosi-standards` is the canonical handbook. The ones that bind here: knowledge-layer, README, **data-handling**, agent-instructions.

## The rule that matters most here
**Respect the boundary in [`BOUNDARY.md`](BOUNDARY.md).** Rich/raw/identifying material stays in this capsule; only de-identified, generalized craft may ever rise into `cosi-knowledge`. Never copy a client's specifics into the shared brain or send them to a non-local model un-sanitized (see the data-handling standard).

## Project-specific
- **No real client data while this is the template.** Don't fill `knowledge/` or `brand/` with a real client until `capsule.yaml → legal_signoff: true`.
- **Knowledge layer:** `knowledge/` follows the CoSi knowledge-layer pattern (wiki / decisions / people / sources / ledger), append-only with wiki-links. No `journal/` — that's a `person`-bundle-only folder (dotKnowledge SPEC §3); a client capsule's agent-authored activity record is `ledger/`.
- **Brand layer:** `brand/` (design.md, voice, personas, tokens, motion) is authored to the `brand-substrate` (BrandOS) schema.
- **Portability:** a capsule should be hand-over-able and local-runnable — keep it self-contained; reference the shared brain, don't depend on it.
