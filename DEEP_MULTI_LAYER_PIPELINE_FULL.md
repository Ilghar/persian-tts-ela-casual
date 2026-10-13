# Deep Multi-Layer Audio Pipeline — Full Implementation

Comprehensive system integrating TTS dialogue, sidechain ducking, advanced mixing, spatial techniques, and character voice fit for Ela (Liora) and Pegah (Ara).

## 1. Track Architecture

Recommended 5-layer structure:

1. **Dialogue (POV)** — TTS with Liora or Ara, full harakat, confirmed casual forms. Highest volume.
2. **Secondary character** — TTS moans or short clips, pitch-matched, spatial pan + light reverb.
3. **Body sounds** — Wet schlick, bed creak (looped, tempo-matched). Mid volume.
4. **Kiss / spit / cum** — Short discrete events.
5. **Background** — Soft jazz / Persian jazz / light city. Lowest volume, ducked.

## 2. TTS Generation Strategy

Use Grok TTS API (`POST https://api.x.ai/v1/tts`):

- Ela: `voice_id: "liora"`, language `fa` or `auto`
- Pegah: `voice_id: "ara"`
- Tags: `[pause]`, `<whisper>`, `<loud>`, `[breath]`, `<soft>`
- Generate dialogue separately from pure vocalizations.
- Save as individual tracks for mixing.

## 3. Advanced Mixing Command (full example)

```bash
ffmpeg -i ela_dialogue.wav -i pegah_moan.wav -i body.wav -i bg.wav \
  -filter_complex \
  "[0:a]volume=1.0,highpass=f=80,asplit=2[dlg][sc]; \
   [1:a]pan=stereo|c0=0.65*c0|c1=0.35*c0,volume=0.4,aecho=0.7:0.85:35:0.25[pegah]; \
   [2:a]volume=0.35,adelay=200|200[body]; \
   [3:a]volume=0.12,lowpass=f=9000[bg]; \
   [bg][sc]sidechaincompress=threshold=0.025:ratio=7:attack=25:release=650[bgduck]; \
   [dlg][pegah][body][bgduck]amix=inputs=4:duration=longest:dropout_transition=2:normalize=0[a]; \
   [a]loudnorm=I=-14:TP=-1.5:LRA=11" \
  -map "[a]" final_mixed.mp3
```

## 4. Dynamic Techniques

- **Volume automation**: Use `volume='if(lt(t,5),0.8,1.0)':eval=frame` for builds.
- **Seamless loops**: `acrossfade` or `apad` + loop for body and bg.
- **Spatial depth**: Pan + light `aecho` on secondary characters.
- **Filtering**: Highpass on dialogue, lowpass on background to reduce competition.
- **Loudnorm**: Always target -14 LUFS at the end.

## 5. Character Voice Fit Rules (locked)

- Ela/Liora: brighter, closer, less reverb, higher peaks allowed.
- Pegah/Ara: softer, more pause-heavy, slight pan + reverb when not POV.
- Never use mismatched pitch clips.
- Tempo of body sounds must match described rhythm.

## 6. Production Notes from Research

- Dialogue should carry most of the dramatic weight; effects support it.
- Variable intensity at peaks sounds more authentic than constant loudness.
- Prefer short loopable clips for body and background.
- Credit sources (OpenNSFW CC-BY, etc.).

## 7. Testing Checklist

- [ ] Dialogue intelligible over all layers
- [ ] Background ducks smoothly under speech
- [ ] Secondary character feels spatially distant when appropriate
- [ ] Body sounds match tempo
- [ ] Final loudness consistent (-14 LUFS)
- [ ] Character voice fit maintained (no mismatched pitch)

This document consolidates all previous stages into one deep, production-ready pipeline.
