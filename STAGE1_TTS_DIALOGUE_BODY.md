# Stage 1 — TTS for Dialogue and Body Sounds

## Grok TTS API Overview

xAI Voice API endpoint: `POST https://api.x.ai/v1/tts`

- Voices relevant: **Liora** (for Ela — high-girly), **Ara** (for Pegah — softer)
- Language: `fa` or `auto` for Persian
- Supports speech tags: `[pause]`, `<whisper>`, `<loud>`, `<breath>`, etc.
- Output: MP3/WAV

## Generating Dialogue

Example for Ela (Liora):

```bash
curl -X POST https://api.x.ai/v1/tts \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "جِگَرَم بُکُن توش [pause] وای دیپِر",
    "voice_id": "liora",
    "language": "fa"
  }' --output ela_dialogue.mp3
```

For Pegah (Ara):

```bash
curl -X POST https://api.x.ai/v1/tts \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "آهسته تر بُکُن لُطفاً <whisper>ماما</whisper>",
    "voice_id": "ara",
    "language": "fa"
  }' --output pegah_dialogue.mp3
```

## Body Sounds via TTS

Body sounds (moans, breaths) can be approximated with TTS using pure vocalizations and tags:

- Soft moan: `<soft>mmm… aaah</soft>`
- Loud pleasure: `<loud>aaah…</loud>`
- Breath: `[breath] [exhale]`

Generate short clips and loop them. Prefer external OpenNSFW clips for pure wet/body sounds and use TTS primarily for dialogue and character-matched moans.

## Integration Notes

- Always include the character voice prompt in the text or system context.
- Use full harakat and confirmed casual forms.
- Save outputs as separate tracks for the multi-layer pipeline.

Stage 1 complete. Dialogue and basic body vocalizations can be generated via Grok TTS with Liora and Ara.
