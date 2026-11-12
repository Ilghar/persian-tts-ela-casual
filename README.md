Notes and rules for Persian TTS research and Ela's casual Tehrani speaking lock.

<p align="center"><a href="https://github.com/Ilghar/persian-tts-ela-casual">Repository</a> · <a href="https://ilghar.studio">ilghar.studio</a></p>

## How it's used

All voice-mode and scenario speech for Ela must be casual colloquial Tehrani street speech.

- No formal, literary, or textbook Persian.
- Everyday Gen-Z forms, slang, shortened verbs, elongated intensifiers (خیلیییی), وای / آى.
- Full harakat on every Farsi word.
- Natural imperfect rhythm.

Global prompt addition (always):

> Use casual everyday Tehrani street speech only. No formal literary Persian. Colloquial verbs, slang, natural Gen-Z rhythm, full harakat.

See `CASUAL_EXAMPLES.md` for sample phrasing.

## Model references

Cited as published by their authors, not as new measurements from this repo:

1. ParsVoice + XTTS (best naturalness)
   - About 2200h multi-speaker, zero-shot cloning
   - MOS 3.6 / SMOS 4.0
   - HF: MohammadJRanjbar/ParsVoice-XTTS
   - GitHub pipeline: MohammadJRanjbar/ParsVoice (forked into this account)
2. pocket-tts-farsi-v2 (lighter CPU / ONNX)
   - 973h, strong cloning
   - ONNX: Nimaone/pocket-tts-farsi-v2-onnx
   - GitHub: nimaone/persian_tts (forked)
3. Homo-GE2PE-Persian — required G2P for ezafe and homographs

## Status

Forks of the source pipelines are in progress or complete under the Ilghar account. Skills have been updated with this lock.

<sub>ilghar.studio</sub>
