# Sound Prompt Bank

People describe the music or sound they want by its **effect** — "magical
spell", "epic", "cozy". Generation models need the **acoustic physics** —
"bright glassy shimmer with ascending chimes, airy whoosh, soft bell tail".

This bank is the translation layer: lookup entries that turn intent language
into prompts that work, for both **sound effects** and **music**.

```yaml
want: "dark magic"
prompt: "low sub rumble, reversed whoosh into deep metallic impact, long dark reverb tail"
```

## Structure

| Path | What's in it |
| --- | --- |
| [`bank/sfx/`](./bank/sfx) | SFX domains — [magic](./bank/sfx/magic.yaml), [action-outdoor](./bank/sfx/action-outdoor.yaml), [quiet-interior](./bank/sfx/quiet-interior.yaml) |
| [`bank/music/`](./bank/music) | Music domains — [scene-moods](./bank/music/scene-moods.yaml) |
| [`SCHEMA.md`](./SCHEMA.md) | Entry format + the rules that keep entries useful |

Every file: a domain, its working vocabulary (the palette), entries
(want → prompt), and domain tips. Machine-readable YAML by design — agents
and apps can load entries directly; the docs are just a rendering.

## Hear it

**▶ [Play every sample in the browser](https://sonilo-ai.github.io/sound-prompt-bank/)** — inline players, no download.

Every entry ships with the audio its prompt actually generated (file links below download/raw):

| Want | Prompt → | Sample |
| --- | --- | --- |
| spell cast | bright glassy shimmer, ascending chimes, airy whoosh, soft bell tail | [▶ spell-cast.mp3](./bank/sfx/samples/magic/spell-cast.mp3) |
| dark magic | low sub rumble, reversed whoosh into deep metallic impact, long dark reverb tail | [▶ dark-magic.mp3](./bank/sfx/samples/magic/dark-magic.mp3) |
| healing glow | warm swelling pad, wind chimes, soft harp glissando upward | [▶ healing-glow.mp3](./bank/sfx/samples/magic/healing-glow.mp3) |
| portal open | deep whoosh, electric hum, crackling energy, rising sweep | [▶ portal-open.mp3](./bank/sfx/samples/magic/portal-open.mp3) |
| transformation | granular sparkle, fast pitch rise, resolving crystalline hit | [▶ transformation.mp3](./bank/sfx/samples/magic/transformation.mp3) |
| fairy dust | delicate high bell tinkles, soft glittering shimmer, quick fading sparkle trail | [▶ fairy-dust.mp3](./bank/sfx/samples/magic/fairy-dust.mp3) |

Generated with `text_to_sfx`, unedited output, first take unless noted.

## How to use

**Humans:** find the entry closest to what you want, use its prompt as the
base, swap vocabulary words from the domain palette to steer it.

**Agents:** load the domain file matching the request, match `want` against
the user's ask, use `prompt` as the starting point. The technique layer —
*why* these prompts work — lives in the
[Sonilo skills repo](https://github.com/sonilo-ai/skills):
[music prompting](https://github.com/sonilo-ai/skills/blob/main/music/prompting.md) ·
[SFX prompting](https://github.com/sonilo-ai/skills/blob/main/sound-effects/prompting.md) ·
[pre-flight](https://github.com/sonilo-ai/skills/blob/main/references/preflight.md).

## The rules behind every entry

1. **Physics, not concepts.** Name texture, motion, materials — never the
   abstraction alone.
2. **One sound event per call.** Compound wants split into layered calls.
3. **No mix directions.** Levels aren't promptable; state the role instead.
4. **Exclusions are best-effort.** Say "no vocals", then verify by ear.

## Contributing

Add entries via PR — one `want → prompt` pair per entry, following
[SCHEMA.md](./SCHEMA.md). Entries should be tested against a real generation
before submitting.

## Related

- [Sonilo skills](https://github.com/sonilo-ai/skills) — agent skills that consume this bank
- [Video-to-music cookbook](https://github.com/cindyxu1030/sonilo-video-to-music-cookbook) — integration recipes (Remotion, Inline-Studio, more)
- [Sonilo](https://sonilo.com/?utm_source=github&utm_medium=oss&utm_campaign=sound-prompt-bank) — the API these prompts were tested against; licensed, safe for commercial use (terms apply)

MIT License.
