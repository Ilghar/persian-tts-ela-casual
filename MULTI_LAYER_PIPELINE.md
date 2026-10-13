# Multi-Layer Audio Pipeline (No-Credit)

Practical method to generate true simultaneous layers (dialogue + body sounds + background).

## Tools Available

- **ffmpeg** is present in the environment and is the primary recommended tool.
- **pydub** (Python) can be installed if needed for more complex scripting.
- External DAW (Audacity, Reaper) for final polishing.

## Recommended Workflow

1. Generate or source separate tracks:
   - Dialogue / POV character (TTS with Liora or Ara)
   - Secondary character moans (pitch-matched clips from no-credit sources)
   - Body sounds (wet schlick, bed creak) looped to match tempo
   - Background (soft jazz, Persian jazz, light city) at low volume

2. Mix with ffmpeg using amix and volume control:

```bash
ffmpeg -i dialogue.wav -i body.wav -i bg.wav \
  -filter_complex \
  "[0:a]volume=1.0[dlg]; \
   [1:a]volume=0.4[body]; \
   [2:a]volume=0.15[bg]; \
   [dlg][body][bg]amix=inputs=3:duration=longest:dropout_transition=2[a]" \
  -map "[a]" -c:a libmp3lame -q:a 2 output_mixed.mp3
```

3. For automatic ducking of background under speech:

```bash
ffmpeg -i dialogue.wav -i bg.wav \
  -filter_complex \
  "[0:a]asplit=2[voice][sc]; \
   [1:a]volume=0.3[bg]; \
   [bg][sc]sidechaincompress=threshold=0.03:ratio=6:attack=200:release=800[ducked]; \
   [voice][ducked]amix=inputs=2:duration=first[a]" \
  -map "[a]" output_ducked.mp3
```

## Volume Hierarchy (recommended)

- Dialogue / POV character: 1.0 (foreground)
- Secondary moans / body sounds: 0.3–0.5
- Background music / city: 0.1–0.2
- Peak loud pleasure: temporarily boost dialogue or add a short higher layer

## Character Voice Fit in Pipeline

- Ela/Liora dialogue: generate with high-girly prompt; select bright higher-pitch moan clips.
- Pegah/Ara dialogue: generate with softer breathier prompt; select drawn-out softer clips.
- Never mix a mismatched pitch moan into the wrong character layer.

## Source Recommendation (Strict No-Credit)

- Moans and body sounds: SoundDino, Freesoundsite, or Freesound CC0 only.
- Background: Pixabay soft jazz (no attribution required).
- See AUDIO_REFERENCES.md and STRICT_NO_CREDIT_WORKFLOW.md.

## Notes

- Loop short body and background clips to match scene length.
- Use `duration=longest` or `shortest` depending on whether dialogue or the full scene should control length.
- For Grok long scenario audio: generate dialogue first, then layer external clips with this pipeline.

This pipeline operates entirely under the strict no-credit workflow.
