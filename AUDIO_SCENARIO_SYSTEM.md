# Audio Scenario System for Ela / Pegah / Navid (Stage 1)

Structured system for generating longer audio scenarios with spatial voice, body sounds, backgrounds, and character-specific delivery.

## Character Voice Profiles

### Ela (main often)
- High-girly Tehrani, bright, closer/louder when she is the POV character.
- Echoes slightly when she is the listener.
- Confirmed casual forms from USER_CONFIRMED_PATTERNS.md.

### Pegah
- Softer, more mature, variable tempo (slower when sub).
- Further away or whispered when not POV.
- Signature phrases from PEGAH_EXPANDED_CHARACTER.md.

### Navid
- Lower firm male with khash texture.
- Deeper, more distant or commanding when not POV.

## Spatial & Proximity Rules

- **POV character**: closer, slightly louder, more intimate reverb/echo.
- **Secondary character licking / behind**: muffled, further, wet sounds more prominent than speech.
- **Whisper in ear**: very close, breath-heavy, low volume speech + kiss/spit sounds.
- **When someone comes closer**: volume and clarity increase gradually.

## Sound Categories to Reference

1. **Breathing** — slow heavy (post), short strained (close), nasal (mouth full).
2. **Moaning** — soft rising (building), sharp (peak), broken (pain-pleasure), character-specific pitch.
3. **Screaming** — short ecstatic or mixed pain-joy (Ela higher, Pegah softer, Navid rare/low).
4. **Fucking / body** — wet schlick (pussy), denser (ass), soft bed creak + rhythm matching thrust speed.
5. **Kissing / spit / cum** — wet tongue, spit string, thick transfer.
6. **Background layers**:
   - Light distant city (very soft, not crowded).
   - Soft jazz (instrumental or woman vocal, low volume).
   - Soft Persian / Iranian jazz style (elegant, not pop).

## Referencing in Scenarios

Use tags that can be mapped to TTS or external audio:

- `[Ela close breathy]: dialogue`
- `[Pegah further wet]: soft moan + “بیبی اِلا”`
- `[body wet slow]: schlick rhythm`
- `[bg soft jazz]: low volume`
- `[kiss close]: tongue + spit`

When generating long audio, prepend character prompt + current physical state + spatial note.

## Research Notes (to expand)

- HF NSFW TTS datasets for emotion/moan annotations.
- OpenNSFW packs and moan libraries for reference clips.
- orgasmsoundlibrary style authentic recordings for timing.
- Soft jazz and light ambient city loops (royalty-free sources preferred).

This is Stage 1. Next stages will add specific file links, cropped clips, and full scenario templates.
