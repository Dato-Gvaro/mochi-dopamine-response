# mandelbrot_dive2 — the x1,000,000,000,000 dive, re-cut so the immersive part is on screen from frame 0

- Batch25 rework of mandelbrot_dive (docs/BRIEF_batch25.md). Owner on v1: "good but boring at start; at 17 s it gets very immersive — we need that under 3 seconds. Also the music sucks." New file `scenes/mandelbrot_dive2.py`; v1, lib/ and tools/ untouched.
- Same maths and the SAME plane as v1: it reads v1's cache `output/mandelbrot_dive_cache/` (identical cache key, nothing recomputed). Period-39 copy #1 (x250k) and period-1170 copy (x1e12) near -0.7436439 + 0.1318259i.

## What was immersive in v1 (read off the encoded batch23 clip)
- v1's 17-27 s = real depth D 17.5-27.6 (x40M-x1T): copy #1's OWN Seahorse Valley. Sub-pixel filaments everywhere, so the whole frame glows in broad pink/orange/blue/teal fields.
- Dull: 1-6 s (the whole set, then the main cardioid/bulb neck: 17-87% dark interior) and 15-16 s (copy #1's neck, D 14.5-16.8: 54-87% interior).
- The main-set valley (D 7-12, v1 7-13 s) keeps big empty gaps even with a stronger glow, so it is not in v2.

## Structure (29.65 s, 1779 frames)
- **0-4.5 s, cold open = payoff + fast immersive REWIND.**
  - Frame 0 is the final copy at x1,000,000,000,000.
  - The whole dive then plays BACKWARDS, spinning out through the deep spirals: D 27.6 -> 19.3 in 3.6 s, ~2.3-2.9 ln/s with 110-150 deg/s roll, motion-blurred.
  - It then slows and cross-dissolves (0.9 s) straight into copy #1's valley (x60-90k), landing there on bar 4.
  - The rewind is a time-warp of the forward camera (same roll(V), same hue(t_fwd)), so it never shows a frame the dive doesn't.
- **4.5-9.0 s:** the forward dive starts (bar 4 "dies illa"). Copy #1 grows from a jewel to 45% width, rolling 80 deg into upright.
- **9.0 s, the twist:** "a copy?!" on the choir's re-entry (bar 5 "qua").
- **11.25 s:** "...keep diving" ("ex"). The plunge: copy #1 swells to fill the frame and swirl-dissolves (11.25-12.0 s) into its own valley.
- **12.4-24.9 s:** the deep spirals, rolling ~32 deg/s and accelerating, 0.64 -> 0.82 ln/s. A new region and a hue step land on bar 6 (13.5 s), bar 7 forte "judicandus" (18.0 s) and bar 8 "homo" (22.5 s).
- **24.92 s, the climax tutti ("re-", trumpets + timpani + boom + cymbal peak):** the perfect tiny copy at 34% width, with a golden halo ring and "a PERFECT copy of the whole set!".
- **26.25 s:** the A major final chord ("-us", half cadence). The copy eases to 50% and upright, and holds on the end view; the last 1.5 s is silent.
- Loop: payoff -> payoff. The end view (frame 1778) = frame 0's camera; the rewind starts from it.

## Tricks
- **Virtual depth V + neck skip:**
  - Real depth 13.15 .. 17.85 (copy #1's body, then its cardioid and bulb filling the frame) is skipped.
  - Around V = 13.15 +/- 0.40 the frame cross-dissolves from real depth V into V + 4.70. Both streams share the roll, so the dissolve reads as one swirl.
  - The counter shows the real depth, interpolated, so it climbs smoothly through the skip.
- **Roll is a function of V:** 41 -> 122 deg (copy #1 upright at D39 = 12.44) -> 692 deg (the final copy upright, plus 1 extra turn). The dive is a corkscrew: spin speed follows zoom speed.
- **Motion blur over zoom AND roll:** sub-samples = max(dV / 0.05, roll arc at the frame corner / 9 px), capped at 8. 2x2 AA near the end view.
- **Depth-adaptive glow** (GK 3.4 -> 1.1, base 0.27 -> 0.20, halo 0.28 -> 0.18 from D 13.6 to 17.2) fills copy #1's surroundings. The deep zone keeps v1's look.
- **Hue steps:** the palette phase steps 1/7 of a cycle (over 0.9 s) on each phrase start: bar 4, bar 5, the plunge, bars 6/7/8 and the climax. That is exactly 1 cycle per loop. They are iso-luminant stops (85% to L 0.16, as in v1), so these are HUE changes, not brightness.
- **Glow breaths:** 0.12 on the hits, 0.06 on each rising choir step of bars 5-6 ("qua re-sur-get ex fa-vil-la"), and a swell on the climax. None before 0.4 s, so frame 0 == the end view.

## Music
- **Piece:** W. A. Mozart, Requiem in D minor K.626, "Lacrimosa" (1791; Mozart d. 1791). Bars 1-8 are Mozart's; the orchestration is completed by F. X. Süssmayr (d. 1803). Public domain everywhere. Our arrangement, rendered with lib/orchestra.py (MuseScore_General.sf2, MIT).
- **Excerpt:** bars 3-8, from beat 12 ("La-cri-mo-sa", the choir entry = 0.0 s) to beat 46.5 (the A major half cadence, held 1.9 s).
  - Quarter = 0.75 s (dotted quarter = 53 bpm, a flowing Larghetto; the reference MIDI is at 43).
  - Ritardando +0.05/+0.12/+0.20 s into beats 43.5/45/46.5.
- **Notes:** from `<SOUNDFONTS_DIR>\scores\mozart_lacrimosa\saomai_musicxml\` (MusicXML transcription of the full score, MuseScore 3, musescore.com/user/3420186/scores/5553262), parsed by `read_mxl()` in the scene.
  - All SATB lines were cross-checked note-for-note against an independent MIDI sequence (kunstderfuge, D. Viens 1997). That file carries a "no commercial use" notice, so it is used ONLY as a check and nothing is taken from it.
  - Only score pitches and positions are used, no performance data.
- **Arrangement (thin -> FULL):**
  - Bars 3-4 (p): choir SATB on "oohs" + "aah" pads on the alto/tenor/bass harmony, strings (the violins' sighing figure; violins II + violas), cellos, contrabass + sub octave + sine sub, and timpani D on bar 4.
  - Bars 5-6 (crescendo): trombones as written (alto/tenor/bass), the pads swell (CC11), timpani on bars 5/6.
  - Bars 7-8 (f): horns double the soprano an octave down (Eb4 -> A4), boom on bar 7, a timpani roll from bar 8 into beat 45, cymbal swell + crash + boom on beat 45, and trumpets + timpani on A at 45 / 46.5 where the score has them.
  - Highest note: A5 (the soprano peak at the climax); the melody otherwise stays in D4-G5.
- **Sync (beats -> s):**
  - 18 -> 4.50 rewind lands / dive starts.
  - 24 -> 9.00 twist.
  - 27 -> 11.25 plunge.
  - 30 -> 13.50, 36 -> 18.00, 42 -> 22.50: new regions.
  - 45 -> 24.92 the copy reveal.
  - 46.5 -> 26.25 the final chord.
- **Measured (preview):** per-second RMS -24 dB (bars 3-4) -> -19 (bar 5) -> -16 (bar 6) -> -14 (bars 7-8). Onsets at 0.00 / 4.49 / 8.99 / 11.27 / 12.38 / 13.49 / 17.99 / 24.91 s.

## Args
- `--q` (0.75 s per quarter), `--iso`, `--freq`, `--blurmax` (8), `--procs` (6), `--cap`, `--label`.
- `--still --frame a,b,c`, `--range a,b` (partial render), `--silent-only`, `--audio-only` (re-mux onto the existing silent render), `--preview` (bed only), `--report`.

## Glow breaths in the plunge
- The 0.06 choir-step breaths are muted from t_pl0 - 0.1 to t_pl1 + 0.3 (11.15-12.68 s).
- With them on, the plunge measured exactly 3 flashes/s (events of 145-147 cells against a threshold of 144).

## Render (Full HD, machine shared with ~10 renders, --procs 6)
- v3: 38 min. The cold open is the heavy part (up to 8 motion-blur samples, two streams in the dissolves); the rest is 1-2 samples/frame. File size: 294 MB at crf 18 (dense fractal detail, ~80 Mbps).
- **4K estimate:**
  - No new cache: the map stays at Full HD density and is upsampled, as in v1.
  - About 4x the pixels -> **~2.5-3 h** on a shared machine.
  - Use --procs 3-4: each worker holds several 4K float arrays (two streams in the dissolves), ~1-1.5 GB.
  - Expect ~1 GB.

## Checks (encoded Full HD, label v3 = the delivered clip)
- **Format:** h264 yuv420p 1080x1920, 60 fps, 29.65 s (1779 frames); AAC 48 kHz stereo.
- **Loudness:** -14.01 LUFS, peak -4.66 dBFS. Per-5 s RMS -23.0 / -24.5 / -19.8 / -16.8 / -13.6 / -13.2 (the thin -> FULL build).
- **Tail:** last 1.3 s peak -43.9 dBFS (the hall reverb fading out), last 1.0 s -58.5, last 0.5 s -80.8.
- **Onsets** on the muxed mp4: 0.00 / 4.49 / 8.99 / 11.27 / 12.38 / 13.49 / 17.99 / 24.91 s, all on the visual keys.
- **flash_check: PASS**, 11 flashes, worst 2/s (1.88 s).
  - v1 of this file FAILED: 6/s at 3.7 s (the rewind swept copy #1's dark body across the screen at speed) and 3/s at 11.7 s (the plunge).
  - Fixed with the cold-open cross-dissolve, the earlier and wider neck dissolve, and no glow breaths in the plunge. The cut and look were not detuned.
- **Loop seam:**
  - Pre-encode, frame 1778 -> frame 0: 0.06 mean (only the pod's 1-frame bob differs).
  - Encoded: 2.46 mean, crf-18 noise on dense fractal detail, as in v1 (2.25).
  - Frame 0 is forced to the hold's sharp 2x2-AA sampling (an earlier render blurred it: seam 4.0).
- **Frames read (encoded):** 0, 0.25, 0.5, 1, 2, 3 s, 4.0-4.75 s (the dissolve), 9.0 (twist), 11.25-12.4 (plunge), 14.8 (mid), 24.92 (climax) and 29.63 (last).
  - Every frame is dense and colourful; the only large dark areas are copy #1's body at the twist and the copies themselves.
  - A 1:1 crop of the climax copy is crisp, with no float64 artefacts.

## Doubts
- The opening is a 4.5 s REWIND (zoom-out) before the dive runs forward. The owner asked for the immersive look by 3 s and "at most a 0.3 s flash-back to the whole set"; this keeps the deep spirals on screen for 0-3.6 s instead. If he wants a forward dive from frame 0, the alternative is a forward dive with the twist dropped.
- The twist comes at 9 s (30%), before the deep half: copy #1 lies shallower than the colourful zone, so it cannot come later without the dull stretch.
- Tempo: dotted quarter = 53 bpm, ~25% quicker than the reference MIDI (43), so that bars 3-8 fit into 30 s.
- The ending is the score's half cadence (D minor 6/4 -> A major at "re-us"), not a full close. It sounds like an arrival but is the dominant.
- Score provenance: the MusicXML (Sao Mai Center library; a MuseScore export, musescore.com/user/3420186/scores/5553262) has no stated engraving licence (pages return 403). The orchestra builder flags the same file "re-source before monetised use" (lib/orchestra_pieces.py). The notes themselves are Mozart/Süssmayr (PD) and match an independent MIDI note-for-note. Before upload, re-verify bars 3-8 against a PD print (IMSLP Breitkopf 1877) — expected to be identical.
- Not listened to by ear (no audio playback here); judged by score, levels and onsets.

- **Delivered:** <VIDEOS_DIR>\batch25\mandelbrot_dive2.mp4 (Full HD). Owner review: pending.
- Owner review (2026-10-11): at ~11 s it jumps to another view; it must ZOOM continuously, never jump -> mandelbrot_dive3.
- Owner review (2026-10-11): "at 11 seconds we have a jump to another view — we must ZOOM, not jump from scene to scene." The neck-skip dissolves read as cuts -> mandelbrot_dive3 (one continuous camera).
