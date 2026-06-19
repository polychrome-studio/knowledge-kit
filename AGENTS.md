# Client Knowledge Cartridge — agent contract

A self-contained `.knowledge` cartridge for ONE client: their knowledge + operable brand + client-specific skills + decisions. (This repo is the empty **template** — Phase 0, no real client data.)

## Follow the CoSi standards
`Collier-Simon/cosi-standards` is the canonical handbook. The ones that bind here: knowledge-layer, README, **data-handling**, agent-instructions.

## The rule that matters most here
**Respect the boundary in [`BOUNDARY.md`](BOUNDARY.md).** Rich/raw/identifying material stays in this cartridge; only de-identified, generalized craft may ever rise into `cosi-knowledge`. Never copy a client's specifics into the shared brain or send them to a non-local model un-sanitized (see the data-handling standard).

## Project-specific
- **No real client data while this is the template.** Don't fill `knowledge/` or `brand/` with a real client until `cartridge.yaml → boundary.legal_signoff: true`.
- **Knowledge layer:** `knowledge/` follows the CoSi knowledge-layer pattern (wiki / decisions / people / sources), append-only with wiki-links.
- **Brand layer:** `brand/` (design.md, voice, tokens, motion) is authored to the `brand-substrate` (BrandOS) schema.
- **Portability:** a cartridge should be hand-over-able and local-runnable — keep it self-contained; reference the shared brain, don't depend on it.
