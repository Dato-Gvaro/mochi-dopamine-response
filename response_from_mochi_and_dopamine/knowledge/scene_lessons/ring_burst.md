# ring_burst
- New scene (batch38). It rebuilds the genre classic ("ball escapes the rotating rings") to research/simple_viral_formula.md + the BRIEF_batch25 RESEARCH RULES. **CHARACTER side** of the characters-vs-pure A/B test: Mochi is the ball (r 24 logical, face readable at 1:1), with no other characters. core_drop is the pure side.
- Caption (baked, `--cap`; `--cap ''` = base): `Every ring she breaks spins ^FASTER^|~Until the LAST one~`. The only other text is the readout `RINGS LEFT n` at y 1392 (0.725 h). Its number is in the colour of the current ring, pops on each break and turns gold at 0.
- Opposite of ring_escape2 (26% stayed, 1.2K views): one big full-width rainbow on pure black, no stand or panels, 2 caption lines + 1 readout.

## World (logical px, ring centre 532, 800)
- 14 rings at R 157 → 495 (pitch 26, tube 11). They span x 26-1038 (0.94 w); the outer ring brushes the right strip as decoration. Bottom 1306 (0.68 h).
- Rainbow from the outer ring (red, hue 0) to the centre (violet, 0.78). Each ring is drawn as glow strokes + a dark edge + a core + an inner sheen line. The ring she is in brightens on every knock.
- Gap: 80° of arc on the inner ring → 24° on the outer (geometric). Even the outer gap clears her ~4x.
- Spin: ω_k = 1.4 · 1.06^k rad/s, alternating direction (1.4 → 3.0 rad/s).

## Physics (one model; px, s; G 1300)
- Perfectly elastic, frictionless. The ring is a thick arc with round end caps. The inner face moves tangentially, so it adds no energy. A gap EDGE (cap) is a moving obstacle, resolved in its own frame (honest kick). 16 substeps/frame.
- She breaks ring k when her centre passes its inner face inside the gap. All rings stay intact until she breaks them.
- **Boost:** on each break her energy (0.5v² − G·y) is raised (never lowered) to C_k · G · free radius, with C 1.5 → 9 inner → outer. Speed goes ~700 → ~3800 px/s, so the bounce rate keeps climbing even though the space grows 3.7x.
- A trail (longer and brighter per ring) and a gold halo grow with k.
- Knocks closer than 45 ms (cap + face double contact) count as one knock and get one note.
- **Seed search** (`--search N --jobs J`, `B_TARGETS`): frame 0 may put the first break at 0.30-0.70 s. The search picks the frame 0 whose knock count up to the last break equals a CADENCE index of the melody (89 = the D at beat 38). Filters: last ring ≥ 1.8 s, no ring > 5.5 s, vmax < 4000, knock rate in the last 5 s ≥ 1.15x the first 5 s. 12,000 seeds → 5 pass.
- **s10181** (default). Breaks (clip s): 0.46 · 3.61/3.64 (double) · 5.83 · 7.39/7.40 (double) · 10.62 · 12.65 · 13.24 · 15.91-16.41 (4-ring cascade in 0.5 s) · last ring persists 4.3 s → 20.73.
  - Knocks per 5 s: 16 / 19 / 18 / 32 (3.2/s first 5 s → 6.8/s last 5 s). 89 knocks, 6 gap-edge near-misses. vmax 3870 px/s.
  - The last ring's 4.3 s at 6.8 knocks/s is the "persistence" stretch.

## Finale (last break + 0 → 4.2 s)
- The last ring shatters, and she flies on and curves to the centre (Hermite, 1.0 s).
- 168 motes of light (12 per ring, each in its ring's colour, starting on its old circle) swirl into her.
- At 1.0 s comes the BLOOM: a soft gold glow (alpha ≤ 0.34). The rainbow re-forms as 14 rings of light that expand to the old ring radii. She grows 1.3x, grins and bobs.
- Zoom 1.0 → 1.2 → back to 1.0 by 3.4 s, so the rings of light hand over to the real rings in the 0.6 s dissolve into the pre-roll (the loop).

## Sound
- **Melody:** Vittorio Monti, *Csárdás* (1904; Monti d. 1922 → PD). Allegro vivo theme (source m23-38) + the D-major return (m107-110), 90 onsets, A3-D5.
  - Source: the cellofun.eu "Czardas Monti CL" MusicXML, which IMSLP PMLP13438 lists as "Public Domain (dedicated)". It is cached in `<SOUNDFONTS_DIR>\scores\monti_csardas\` (same file as snake_duel3).
  - `--verify` re-parses it: **LEAD matches the source: True**.
- One note per knock (onsets 0-88). Onset 89 (the cadence D4, beat 38) lands on the LAST ring's break. The tune turns from D minor to D major during the last ring's persistence.
- Instruments: soundfont piano lead (velocity rises per ring, a near-miss accents it). From ring 8 a harp doubles the tune an octave down. Under it are a soft string pad + pizz roots, one chord per 2/4 bar fitted to the tune (our arrangement: Dm/A7 … D/A7/D).
- Last ring: contrabass D2 + timpani D. Bloom: a rich D-major chord (strings, choir aahs, rolled piano, harp, top note D5) + a soft boom + a glass-harp D5 chime. Nothing is above D5.
- **SFX (synth):**
  - A glass SHATTER per ring, +12 ms off the notes: an inharmonic crack 0.7-2.3 kHz, a 14 ms low-passed snap, a body thump, then 6-12 glass tinkles (1.25-2.7 kHz) over 0.3 s. It grows bigger outward.
  - A soft glass "tik" on each gap-edge near-miss.
  - No hiss or whoosh. Every SFX onset is ≥ 12 ms from every note.
- -14 LUFS (master), last 1.0 s digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (0.18) `--search N --from S --jobs J --all --verify`. Physics: `--g --c0 --c1 --w0 --wk --gap0 --gap1`.

## Checks
Encoded Full HD:
- h264 yuv420p 1080x1920, 60 fps, 1496 frames (24.93 s). The last break is at 20.73 s.
- -14.00 LUFS, peak -5.39 dBFS. The last 0.5 s is digital silence. RMS/5 s: -19.9 → -17.7 → -17.1 → -14.8 → -14.0 (it builds).
- flash_check PASS (0 flashes, mean lum 0.017).
- **Loop:** pre-encode last→0 mean delta 0.542 against a normal frame step of 0.545, so the seam is one ordinary frame step. The last frame is pre-roll frame -1. `tools/check_loop.py` reports "MISMATCH" because it expects last == frame 0. Encoded seam 1.76 (an I-frame quality step, as core_drop 1.33).
- `--verify`: LEAD == source MusicXML. Top melody note D5.
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 12.5 / 20.7 / 21.8 s, plus Full HD stills at 0.45 s, 16 s and the finale. Mochi's face reads at 1:1.
- Safe zone: caption y 172-245; rings y 294-1306 (≤ 0.68 h); readout 1392.
- Render ~6 min (Full HD).

## Doubts
- Knock rate climbs (3.2 → 6.8/s), but late speeds (~3800 px/s, ~63 px/frame) make her a comet in the outer rings. Her face reads in the inner rings, at near-misses and in the finale, not mid-flight late. This is geometry: a 3.7x bigger space needs that speed for the rate to keep rising.
- The ring-break rate falls by design (outer rings take more tries). Ring 1 → 2 is a 3.1 s stretch right after the hook.
- The moving-cap kick is honest, but it can add speed spikes; seeds with vmax ≥ 4000 were rejected.

Delivered `<VIDEOS_DIR>\batch38\ring_burst.mp4`. Owner review 2026-10-16: APPROVED. 4K ship render: `output/ring_burst_ship_9x16.mp4` (seed 10181; h264 yuv420p 2160x3840, 60 fps, 1496 frames = 24.933 s; -14.00 LUFS, peak -5.39 dBFS; flash_check 0 flashes; encoded seam 1.39). The coordinator stages it.
