# Stage 2 — Sidechain Ducking Techniques

## Core Concept

Sidechain compression automatically lowers background music or body sounds when dialogue is present, then raises them during pauses. Implemented in ffmpeg with `sidechaincompress`.

## Basic Ducking Command

```bash
ffmpeg -i dialogue.wav -i bg.wav \
  -filter_complex \
  "[0:a]asplit=2[voice][sc]; \
   [1:a]volume=0.25[bg]; \
   [bg][sc]sidechaincompress=threshold=0.03:ratio=8:attack=20:release=600[ducked]; \
   [voice][ducked]amix=inputs=2:duration=first:normalize=0[a]" \
  -map "[a]" -c:a libmp3lame output_ducked.mp3
```

## Parameter Guide

| Parameter | Recommended | Effect |
|-----------|-------------|--------|
| threshold | 0.02–0.05 | When voice triggers duck |
| ratio | 6–10 | How hard bg is reduced |
| attack | 10–30 ms | How fast duck engages |
| release | 400–800 ms | How slowly bg returns |

## Multi-Layer Ducking (dialogue + body + bg)

```bash
ffmpeg -i dialogue.wav -i body.wav -i bg.wav \
  -filter_complex \
  "[0:a]asplit=2[voice][sc]; \
   [1:a]volume=0.4[body]; \
   [2:a]volume=0.15[bg]; \
   [bg][sc]sidechaincompress=threshold=0.03:ratio=6:attack=20:release=700[bgduck]; \
   [voice][body][bgduck]amix=inputs=3:duration=longest[a]" \
  -map "[a]" output_full.mp3
```

## Tips

- Longer release prevents pumping between words.
- Test threshold so breaths don’t constantly trigger ducking.
- Combine with loudnorm for consistent final levels.

Stage 2 complete. Sidechain ducking is documented and ready for use in the pipeline.
