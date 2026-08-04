# Scope — self, client, project

Three bundle types, and one line between them. Most of the mess in a knowledge
system comes from blurring these, not from any of them being hard.

## Self
`<you>.knowledge` — first-person, lived experience. Journal, decisions made as a person rather than on behalf of a client, opinions, doubts, your private read on a relationship. `type: person`. This is the default target for anything that's really about you, not about the work. A person bundle is the only type with a `journal/` — first-person voice is what it's for (dotKnowledge SPEC §3).

## Client / Brand
`<client>.knowledge` — canonical facts about a subject that isn't you: their history, their voice, their positioning, the relationship. Sealed and portable, one bundle per subject, never blended with your own residue or another client's. `type: brand` or `type: org`.

## Project / Campaign (if needed)
A narrower slice than a full client relationship — one bounded body of work. Nests under the client bundle it belongs to when there is one (`<client>.knowledge/projects/<project>/`); stands alone when there isn't (a personal project, an open-source release). Doesn't need its own top-level bundle unless it outlives or outgrows the relationship it started under. `type: project`, and it freezes at ship rather than decaying.

## The one rule that matters
Residue about you stays in your own bundle, even when it's about a client — an opinion, a doubt, a private read on a relationship is yours, not theirs, no matter whose name is in the sentence. Canonical facts about the client stay in the client's bundle — you read them there, you don't restate them from memory somewhere else. A fact with two homes has two truths the moment one of them is edited. That's the whole boundary.

## If you need more than this
Bigger organizations usually need another tier — a shared layer collecting generalized craft across many subjects, with an explicit gate on what may rise into it. dotKnowledge supports that through the `rises:` field (`bundle.yaml`, SPEC.md §6): `never`, `filtered`, or `de-identified`, plus a `legal_signoff` gate for material a contract governs.

*This template defaults to `rises: none`. A shared tier solves a multi-tenant problem and is pure overhead until you actually have one — build it when the second consumer exists, not in advance.*
