# soda_tap — Shaken soda: does TAPPING the can help? (batch57, 2026-10-29)

## v3 (batch60, 2026-10-30): office background
- Owner on v2: "better, but why does it look like they're in jail". Brief: docs/BRIEF_batch60.md. Only `make_bg()` changed (v2 script at scratch `m60/soda_tap_before.py`); v2 video → `MochiAndBolt\archive\soda_tap_v2.mp4`.
- New background: a warm office at golden hour: a big glass wall (slim frame, two thin vertical mullions, no bars) with a dusk city skyline (lit windows, sun glow, reflections), warm painted wall darker toward the top (caption contrast), a wooden desk with drawers behind the cans, a tall potted plant (left, behind Mochi), a coffee machine with a steaming cup + a succulent on the desk (right, x 914-1068 = decoration outside the side safe zone), a plank floor.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\soda_tap.mp4` (**v3**, Full HD, label v3). Sim, story, timings, music, banners unchanged.
- **v3 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 840 frames = 14.00 s; muxed -14.00 LUFS, peak -1.93 dBFS, last 0.5 s digital silence; flash PASS (0); seam 4.68 vs 0→1 4.15 (mid-shake, as v2). Frames read: 0.3, 9.9 s (spray over the window: foam reads on the dusk sky) + stills 0.5/7.0/10.3 s.

## v2 (batch58, 2026-10-29): Bolt TAPS vs Mochi slowly ROTATES (the TV trick)
- Owner on v1: "what if one tries slowly rotating it, like the character in a famous TV show does?" Brief: docs/BRIEF_batch58.md. Edited in place; v1 script kept at scratch `m58/soda_tap_v1.py`; v1 video → `MochiAndBolt\archive\soda_tap_v1.mp4`.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\soda_tap.mp4` (**v2**, Full HD, 14.00 s, 840 frames, label v2).
- Caption: "Shaken soda: ~TAP~ it or ~ROTATE~ it?" / "Which can opens ~DRY~?". The TV show is never named (screen/titles).
- **Story:** same shake (bar 1). Bolt taps the lid 10× on beats 1+3 of bars 2-6 (TAP x10 meter); Mochi rolls her can between her palms (SLOW ROTATE ring counts turns; the COLA label and the still-stuck bubbles ride round with the wall, far-wall bubbles dimmer; faint swirl streaks = the liquid lagging). Her count drops fast (821 vs 1,446 at 0:04 real). 6.95 s "MOCHI'S CAN: SAFE ZONE" → she opens at 7.20 s (8.6 s real, 4 turns): foam to the rim, "NO SPILL!", cheer; Bolt "wow". "BOLT: STILL TAPPING..." → 9.40 s (12 s real) he opens: SPRAY!, geyser lands on him (lost 30 %), Mochi laughs. Cadence 10.4 s: "10 TAPS: -5% BUBBLES" / "SLOW ROTATING: -33%" / "ROTATE IT, DON'T TAP IT".
- **Physics v2:** as v1 (2,600 bubbles, 82 % on the walls, natural detach tau 11 s, rise 0.10 + 0.045 r² heights/s, lid tap frees top-band bubbles p 0.25). New: while the can rotates, every wall bubble gets an extra detach hazard `K_ROT` 0.20/s (`--krot`): the liquid spins up only over the Ekman time H/sqrt(nu·Omega) ~ 1 min, so the wall slides past it; the wall shear adds a drag comparable to a small bubble's buoyancy. This rate is a MODEL ASSUMPTION (~2.2× the natural rate), not a measured value. Result: Mochi 214 bubbles at 8.6 s (just waiting: 1,069; rotation freed 1,357); Bolt 686 at 12 s (no taps: 808). Time-lapse constant x1.54 (12 s real = 7.8 s clip).
- **Music:** Mendelssohn Scherzo, now bars 1-6 + bar 16's cadence (bars 5-6 are a repeat; bar 6 ends on the tonic, bar 16 = V → i). T_CAD 10.4 s, hold 3.0 s.
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 840 frames = 14.00 s; -14.00 LUFS, peak -1.93 dBFS, last 0.5 s digital silence (-240 dBFS); flash PASS (0, mean lum 0.048); seam 4.67 (mid-shake at the seam, continuous, as v1). SFX/s 8 11 21 21 22 21 22 25 12 14 13 7. Frames read from the mp4: 0.3, 4.5, 7.3, 9.9 + 1:1 crop of both cans at 5.5 s; stills at 0.5/3.3/6.3/7.2/7.8/10/10.7/11.7/13.2 s. Key content x 110-900.
- **v2 doubts:** the rotation benefit is modelled, not field-tested (tapping's non-effect IS from a field test). Mochi opens 3.4 s real before Bolt, so "rotating" beats "tapping" even with less time. The hold after the cadence (10.4-14 s) is static apart from the banners.

- Brief: docs/BRIEF_batch57.md (Mochi & Bolt 1). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from checkout_queue.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\soda_tap.mp4` (**v1**, Full HD 9:16, 16.60 s, 996 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Shaken soda: does ~TAPPING~" / "the can ~HELP~?"
- **Story:** a kitchen at night. Frame 0: both shake an x-ray cola can (thousands of bubbles swirling, BUBBLES INSIDE counters climbing, "SAME SHAKE"). Bolt then taps the lid 10 times on the beat (TAP x10 meter 0/10 → 10/10, "tap" pops); Mochi waits (WAIT 30 s ring). The counts fall almost identically. Bolt opens at 6.2 s (12 s real): SPRAY! The foam geyser goes up and comes down on him (foam cap + drips, the can loses 32 %); Mochi laughs. "10 TAPS SAVED ONLY 128 OF 2,600 BUBBLES". Mochi's count crosses the SAFE line at 11.4 s ("MOCHI'S CAN: SAFE ZONE"); at 30 s she opens on the cadence (13.6 s): the foam rises to the rim and stops, "NO SPILL!". Then "TAPPING: -5% BUBBLES / WAITING 30 s: -94% / IT'S THE WAIT, NOT THE TAP". Bolt: foam-covered, deadpan.

## Layout
- Floor y 1262. Cans 180 × 360 (bottom y 1178): Mochi's x 382, Bolt's x 626. Characters r 88 at x 198 / 812 (key content x 110-900). Floating mitten hands grip the cans; Bolt's free hand taps the lid.
- Goal meters above the cans (y ~680): WAIT 30 s ring / TAP x10 dots. HUD y 1366-1556: "TIME SINCE THE SHAKE m:ss (time-lapse x2.5)", per side count + bar with a SAFE tick (10 %), then SPRAYED! / NO SPILL!.
- Static camera; window and back counter are decoration.

## The physics (seeded, honest)
- 2,600 bubbles per can, created during the shake; 82 % stuck to a wall. A stuck bubble lets go on its own after Exp(tau = 11 s) real, then rises at (0.10 + 0.045 r²) liquid heights/s and pops at the surface.
- A tap on the LID: stuck bubbles in the top 20 % let go with p 0.25, the rest p 0.005. Over 10 taps that shakes loose 269 bubbles, but most of them would have risen anyway: at opening Bolt has 723 vs 851 without taps (128 = 5 % of 2,600).
- Opening: the pressure drop swells every bubble still in the liquid; foam ~ bubble count. Bolt (723 = 28 %) → 2,170 spray particles, ballistic (g 2000 px/s², launch 1180 px/s decaying, 0.10 rad tilt toward him), 483 land on him. Mochi (157 = 6 %) → foam rises to the rim only.
- Time-lapse: one constant factor x2.52 (30 s real between the end of the shake and Mochi's tab). Both share the same clock.
- Matches the 2021 field test (no measurable benefit from tapping); waiting is what works.

## Sound (music first)
- **Piece:** Felix Mendelssohn, Scherzo in E minor Op. 16 No. 2 (1829; d. 1847, PD). Presto, staccato, repeated-note "taps". Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD (Mutopia-2009/06/02-1653), `mendelssohn-scherzo-eminor.mid/.ly/.rdf` + SOURCE.txt at `<SOUNDFONTS_DIR>\scores\mendelssohn_scherzo_e_minor\`. Read at runtime (both staves).
- **Excerpt:** quarter = 150 (bar 1.6 s): bars 1-8 (bar 1 = the shake strokes, bars 2-4 = the 10 taps on the long repeated notes, bars 5-8 = the staccato theme under the spray), then bar 16's first half + its e4 = the cadence (13.6 s = Mochi's NO SPILL).
- **Arrangement** (lib/orchestra): bars 1-4 pizzicato + violin with a soft cello tonic/dominant pulse; bars 5-8 violin + flute on the theme, pizz + bassoon on the left hand; cadence = timpani + E-minor strings/horns, pizz button, soft held chord.
- **SFX** (tonal): shake "chk" per note in bar 1, a lid "tink" per tap, bubble-pop plips per 16th slot (pitched to the harmony, gain by count), tab double-click, the geyser's round "bloop" + plips as foam lands on Bolt, Mochi's fizz = tiny high plips (no noise), dings for SPRAY / SAFE / the cadence.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 996 frames = 16.60 s. -13.98 LUFS, peak -2.00 dBFS, last 0.5 s digital silence.
- RMS/s: -17.8 -19.4 -19.2 -17.0 -17.4 -18.3 -17.1 -17.0 -16.7 -17.2 -16.2 -16.0 -16.0 -14.4 (cadence) -16.2 -27.1, then silence.
- SFX events/s: 8 11 22 22 23 22 24 19 15 10 10 12 10 18 0.
- flash_check PASS (0 flashes, mean lum 0.05). Seam: last → first 3.95 vs adjacent shake frames 3.6-4.2 (check_clip 4.68: the cans are mid-shake at the seam, continuous motion).
- Frames read from the mp4: 0.1, 0.5, 2.0, 6.5, 7.2, 9.0, 11.6, 13.7, 14.5, 15.5 + a 1:1 crop of Bolt's foam (13.7).

## Doubts
- Bolt opens at 12 s real, Mochi at 30 s: that IS the comparison (the taps are a ritual before opening early). A viewer could call it unfair; the banners state the numbers.
- No lead change: the bubble counts fall together; the tension is "will tapping save him" and the SAFE line.
- 7.5-11.4 s is the quieter stretch (Mochi's bubbles rising, Bolt dripping, the "10 TAPS SAVED ONLY 128" banner); the SAFE-zone beat lands at 11.4 s.
- The x-ray can is giant next to the characters (cartoon scale).

## Args and cost
- `--seed` (57), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 0.5 s; Full HD render ~65 s at 2 encoder threads.

## Outcome
- (fill after upload)

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/soda_tap.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 840 frames 14.00 s; -14.00 LUFS, peak -1.93 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v3. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-07\1_soda_tap.mp4`, 08:00 local Nov 8 (= 23:00 US East Nov 7). FHD review copy → `MochiAndBolt\archive\soda_tap_fhd.mp4`.
