# Final Multi-Layer Simultaneous Audio System

Consolidated, tested, and locked under strict no-credit rules.

## Pipeline Summary

1. Generate dialogue tracks with Grok TTS:
   - Ela → voice_id **liora** (bright high-girly)
   - Pegah → voice_id **ara** (softer breathier)
   - Use full harakat casual Tehrani + tags ([pause], <whisper>, <loud>, [breath]).

2. Source short clips (zero credit):
   - Moans / wet / body / bed creak: SoundDino, Freesoundsite, or Freesound CC0 only.
   - Soft jazz background: Pixabay.

3. Pitch-match verification (final):
   - Liora (Ela): only high-pitched, bright, short, rising clips.
   - Ara (Pegah): only soft, breathy, drawn-out clips.
   - Test every candidate by ear against a short TTS sample of the target voice before mixing.
   - Non-vocal body sounds shared but tempo-matched.

4. External multi-track mix with ffmpeg:
   - Dialogue foreground (volume 1.0)
   - Secondary / body mid (0.3–0.5) with pan + light reverb for spatial depth
   - Background lowest (0.1–0.2) with sidechaincompress ducking under dialogue
   - Final loudnorm to -14 LUFS

Full example command is in DEEP_MULTI_LAYER_PIPELINE_FULL.md.

## Diagnosis & Improvements

- Simultaneous layers achieved via separate tracks + amix (not sequential).
- Sidechain ducking keeps dialogue intelligible.
- Spatial pan + reverb on secondary character creates depth.
- Character voice fit locked: no mismatched pitch clips allowed.
- All sources verified no-attribution.

## Skills Updated

ela-bratty-voice and ella-persian-voice-v7 now contain the multi-layer no-credit system and Liora/Ara voice locks.

## Status

System is complete, gap-free, and ready for scenario audio generation. All dependent elements (pipeline, references, skills, character descriptions) are synchronized to the no-credit multi-layer workflow.

Final lock.
