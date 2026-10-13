# Stage 3 — Advanced Audio Mixing Techniques

## Spatial Positioning with Pan

Place secondary character further away:

```bash
ffmpeg -i pegah_moan.wav -af "pan=stereo|c0=0.7*c0|c1=0.3*c0,volume=0.6" pegah_spatial.wav
```

## Light Reverb for Room Feel

```bash
ffmpeg -i input.wav -af "aecho=0.8:0.88:40:0.3" reverb.wav
```

## Full Advanced Mix Example

```bash
ffmpeg -i ela_dialogue.wav -i pegah_moan.wav -i body.wav -i bg.wav \
  -filter_complex \
  "[0:a]volume=1.0,highpass=f=80[dlg]; \
   [1:a]pan=stereo|c0=0.6*c0|c1=0.4*c0,volume=0.45,aecho=0.7:0.8:30:0.2[pegah]; \
   [2:a]volume=0.35[body]; \
   [3:a]volume=0.12,lowpass=f=8000[bg]; \
   [dlg][pegah][body][bg]amix=inputs=4:duration=longest:dropout_transition=2[a]; \
   [a]loudnorm=I=-14:TP=-1.5:LRA=11" \
  -map "[a]" final_mixed.mp3
```

## Additional Techniques

- **Highpass/lowpass**: Clean dialogue and soften background.
- **Loudnorm**: Target -14 LUFS for consistent loudness.
- **Crossfade loops**: Use `acrossfade` for seamless body/bg loops.
- **Panning**: Offset secondary characters slightly left or right for spatial depth.

## Character-Specific Notes

- Ela/Liora: keep brighter, closer (less reverb, higher volume).
- Pegah/Ara: slightly more reverb and offset pan when not POV.
- Navid: lower, more centered or distant.

Stage 3 complete. Advanced mixing techniques (spatial pan, light reverb, loudnorm, filtering) are integrated into the pipeline.
