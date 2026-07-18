# Scope — self, client, project

Three capsule types, not CoSi's multi-tenant model. A solo studio doesn't need a shared-brain routing policy across seventy clients — it needs a clear line between three things.

## Self
`tucker.knowledge` — first-person, lived experience. Journal, decisions made as a person, not on behalf of any one client. The default target for anything that's really about you, not the work.

## Client / Brand
`<client>.knowledge` — canonical facts about a subject that isn't you: their history, their voice, their positioning, the relationship. Sealed and portable, one capsule per subject, never blended with your own residue or another client's.

## Project / Campaign (if needed)
A narrower slice than a full client relationship — one bounded body of work. Nests under the client capsule it belongs to when there is one (`<client>.knowledge/projects/<project>/`); stands alone when there isn't (a personal project, an open-source release). Doesn't need its own top-level capsule unless it outlives or outgrows the relationship it started under.

## The one rule that matters
Residue about you stays in `tucker.knowledge`, even when it's about a client — an opinion, a doubt, a private read on a relationship is yours, not theirs. Canonical facts about the client stay in the client's capsule — you read them, you don't rewrite them from memory. That's the whole boundary. No sign-off gate, no shared-brain routing tier — those solve a seventy-client agency's problem, not a solo studio's.

*Still uses [dotKnowledge](https://github.com/polychrome-studio/dotKnowledge)'s `rises:` field (`capsule.yaml`, SPEC.md §6) — it's just usually `none` here. If Polychrome ever needs a shared cross-client layer, that's a `polychrome.knowledge` capsule to build when it's actually needed, not a protocol to build in advance.*
