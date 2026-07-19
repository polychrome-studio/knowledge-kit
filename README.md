# knowledge-kit

**The template for a `.knowledge` bundle — one self-contained package per subject (yourself, a client/brand, or a project), holding their knowledge, their operable brand (`brand-kit`), the skills built for them, and their decision history.** Stamp a new bundle from this skeleton.

> **"Bundle"** is the adopted term — a sealed, portable package, per the [dotKnowledge](https://github.com/polychrome-studio/dotKnowledge) `.knowledge` standard this template conforms to (`bundle.yaml`, SPEC.md §5).
>
> **Status:** structure and spec only. No real data lives here — this is the empty shape, agreed on before stamping anything real. See [`SCOPE.md`](SCOPE.md) for the three subject types and what stays where.

## What a bundle is

A subject's whole "game" in one sealed package:

- **the world** — their knowledge, history, what's been learned (`knowledge/`)
- **the characters** — their operable brand: voice, design, tokens, motion, personas (`brand/`, per [brand-kit](https://github.com/polychrome-studio/brand-kit))
- **the special moves** — the skills/specialists built for them (`skills/`, per [skills-kit](https://github.com/polychrome-studio/skills-kit))

It's self-contained, portable, and ownable by whoever the subject is.

## The structure

```
<subject>.knowledge/
  README.md             what this bundle is (can be shared with the subject, if it's a client)
  AGENTS.md              how agents work inside it — the scope rule is paramount
  bundle.yaml           manifest — dotKnowledge SPEC.md §5: subject/type/relationship/parent/
                          status/rises/access/local/legal_signoff
  SCOPE.md                the line — self vs. client/brand vs. project, and what stays where
  knowledge/             the rich knowledge layer — wiki, decisions, sources, ledger
  brand/                 the operable brand layer, per brand-kit
  skills/                subject-specific skills — generic operating mechanism stays in the harness, never here
```

## Related

- [dotKnowledge](https://github.com/polychrome-studio/dotKnowledge) — the format this template conforms to
- [brand-kit](https://github.com/polychrome-studio/brand-kit) — what goes inside `brand/`
- [skills-kit](https://github.com/polychrome-studio/skills-kit) — how a skill in `skills/` is addressed
- [foundry](https://github.com/polychrome-studio/foundry) — a harness that mounts a stamped bundle
