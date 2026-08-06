# Schema

Every bank file is YAML with the same shape: domain metadata, a working
vocabulary, and a list of entries. Entries are the product — each one
translates **intent language** (what people say they want) into **acoustic
language** (what a generation model can act on).

```yaml
domain: magic            # kebab-case, matches filename
mode: sfx                # sfx | music
formula: "texture + motion + pitch direction + tail + duration"
core_rule: >
  One-line principle for this domain.

vocabulary:              # the palette entries draw from
  texture: [shimmer, glassy chimes, granular sparkle]
  motion: [rising sweep, swell, burst]
  # keys vary by domain — sfx uses texture/motion/pitch/tail,
  # music uses genre/energy/instrumentation, foley uses source/material/action

entries:
  - id: spell-cast       # kebab-case, unique within the file
    want: "spell cast"   # intent language — what a user would say/search
    prompt: "bright glassy shimmer with ascending chimes, airy whoosh, soft bell tail"
    endpoint: text_to_sfx     # text_to_sfx | video_to_sfx | text_to_music | video_to_music
    duration_hint: "1.5–3 s"  # optional
    notes: "optional — layering, pitfalls, variations"
    tags: [magic, cast, bright]

tips:                    # domain-level guidance, list of strings
  - "One sound event per call — 'spell cast then explosion' = muddy; two calls, layer in edit."
```

Rules that keep entries useful:

- **Physics, not concepts.** The `prompt` names acoustic ingredients
  (texture, motion, materials), never the abstraction ("magical", "epic",
  "exciting sounds"). Concept words are allowed only as modifiers.
- **One dominant sound bundle per entry** — one physical event and its
  immediate by-products. Compound wants get a `notes:` line telling the
  reader to split and layer.
- **No mix directions.** "Loud", "punchy", levels — not promptable. State
  the role instead ("background bed", "drums carry the track").
- **Exclusions are best-effort.** Entries may include "no X" phrasing but
  never promise it.
- Keep `want` in the words people actually use — that's the lookup key and
  the search surface.
