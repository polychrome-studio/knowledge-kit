# Knowledge Capsule — agent contract

A self-contained `.knowledge` capsule for ONE subject: their knowledge + operable brand + subject-specific skills + decisions. (This repo is the empty **template** — no real data.)

## The rule that matters most here
**Respect the scope in [`SCOPE.md`](SCOPE.md).** Residue about you stays in your own capsule; canonical facts about a subject stay in that subject's own capsule. Don't blend them.

## Project-specific
- **No real data while this is the template.** Don't fill `knowledge/` or `brand/` with a real subject until `capsule.yaml → legal_signoff: true` (if a formal agreement matters for that subject at all — see `SCOPE.md`).
- **Knowledge layer:** `knowledge/` follows the pattern in `knowledge/AGENTS.md` (wiki / decisions / sources / ledger), append-only with wiki-links. No `journal/` — that's a `person`-bundle-only folder (dotKnowledge SPEC §3); a non-person capsule's agent-authored activity record is `ledger/`.
- **Brand layer:** `brand/` (design.md, voice, personas, tokens, motion) is authored per [brand-kit](https://github.com/polychrome-studio/brand-kit).
- **Portability:** a capsule should be hand-over-able and locally-runnable — keep it self-contained.
