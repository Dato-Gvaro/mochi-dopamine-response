# ol_dust_mill (DopamineEXE, channel 2) — the DUST family at ~50 s, with a mill
- Brief: `docs/BRIEF_dopa_colorgun.md` section B "DUST MILL" (a test of the LENGTH lever on the one proven family, "...until it turns to DUST": ol_sierpinski 18.6K, ol_sierpinski_carpet 4.2K). Lessons from `<VIDEOS_DIR>\DopamineExe\review\ideas_2026-11-11\REFERENCE_A2aqs7IBDEw.md`: multiply (×3) never add; the end state must be visibly true; big motion at 0 s, first event < 2.5 s; rule + stake printed.
- Nameable change vs the triangle hit: **a mill does the splitting, and it runs ~50 s** (the hit is 15.5 s).
- New scene file (ol_sierpinski stays bit-reproducible). Reused from ol_sierpinski: the rainbow position map (`pos_hue`), saturation 0.75, the HUD look (meter + gold DUST mark + counter + ×3 pill + watermark), the caption look, the glass tink, the Rachmaninoff Prelude and its C#-minor DUST chord.

## Rule (what the code does)
- Every piece a blade hits splits the Sierpinski way: 3 half-size corner triangles fly off, the middle quarter falls out as glitter. A gen-6 piece (6 px) that is hit becomes its 3 gen-7 grains = DUST. 1 → 2,187 pieces (3^7), 1,093 splits. **No split without a blade contact** (swept-sector test per arm per frame, plus an arm-inside-triangle test for pieces > 40 px).
- Caption (post-render pass, family look, `--capsheet` + ffmpeg overlay, constant on every frame so frame 0 = last frame): `Every piece the blade hits ^SPLITS^ into 3|until it turns to ~DUST~` (`^` cyan, `~` gold). Bbox x 0.12-0.82 w, y 204-310.

## World (logical 1080x1920)
- Arena: thin white circle, centre (508, 800), r 396 (x 0.104-0.837 w, y 404-1196). Mill: hub r 26 + 2 tapered blades to r 175; motion blur = a fan of ghosts over the last frame's sweep + a faint swept disc (≤ 3.5% alpha).
- Triangle: side 392 (r 396 arena caps it), apex up, base 46 px above the hub, glossy rainbow (gradient in each piece's original-frame coordinates, so every piece keeps its patch of the rainbow; gloss + white hairline edge ≥ 14 px, flat colour below).
- Physics (dt 1/60, seeded): zero-g, drag 0.7/s, soft position-based collisions (r = 0.31 side, mass ∝ area), wall bounce e ≈ 0.7 on the true vertices, solid hub. Kids: spread 70 px/s + 1.25 × the blade speed along the blade + 170 px/s outward; immune 0.18 s while they leave the blade.
- **Pacing = the vortex.** Free pieces float in the ring outside the blades (a strong outward "blade wind" inside r = 175 + 0.31 side + 50 keeps them out). The mill PULLS pieces in (900 px/s², the biggest free pieces first, each free ≥ 0.9 s) so the split count follows `S*(t) = R0·τ·(e^(t/τ) − 1)`, R0 1.8/s, τ solved so S*(46 s) = 1,093. Accidental hits (a free piece knocked into a blade) are real hits and count. This is the fix for the natural cascade's tail: free physics alone always peaked mid-clip and tailed off for 5-10 s (tried: pure suction, exp ramps, a 1/(1 − t/Tc) critical vortex, a global suction controller (bursty), gen-dependent suction).
- Blades: 0.40 rev/s × e^(t/22), capped 2.6 rev/s. After DUST they slow back to 0.40 and land on the frame-0 angle (mod π) on the frame after the last (`finish_clock`).
- Dust: grains (1 per 8 px² of cut-out area + the 3 gen-7 grains of every last split) are analytic: burst out of the cut (τ 0.25-0.45 s), settle into the ring (r 209-389, area-uniform), orbit at 5-13% of the blade angle, twinkle. Additive 1.8 px splats (bincount). The glitter has its own RNG stream (physics never depends on GRAIN_A).
- Visual aids: hit spark (soft white dot, 0.14 s), the cut outline of the middle quarter (pieces ≥ 10 px, 0.22 s), motion streaks for fast pieces (4-frame lag, own colour).
- Finale: DUST = the last piece gone; a shimmer runs out through the ring (0.6 s); from +0.55 s the hub pulls the glitter in (outer grains later, tightening spiral, 0.75-1.05 s each); the hub glows gold (local radial gradient); dissolve 0.6 s into frame 0 UNDER the live mill (the blades never double).

## HUD
- Meter y 1262 (x 170-846): fill = the TRUE dust share of the original area (cut-out quarters + gen-7 grains), label "DUST n%" (100 only at DUST), quarter rungs, gold DUST mark from frame 0. Counter y 1488: 1 + 2 × splits (= 3^7 = 2,187 at DUST), "PIECES", ×3 pill (pops when the count passes 3^k and at DUST). Watermark (900 right, 1352).
- The brief's DUST % is front-loaded by geometry (the first split is already 25%); with the biggest-first pull it climbs 25 → 51% by 5 s, then ~1%/s to 100%.

## Sound
- Rachmaninoff Prelude in C-sharp minor (PD, Mutopia MIDI, the family's tune). Bar 1's bells A - G# - C# on the first 3 splits; bar 2 compressed; the Lento and the whole Agitato (to beat 170) on an accelerating tempo (τ 30 s), each score slot snapped onto a split ≥ 70 ms after the previous note; the fff motif of bar 43: A at DUST − 1.5 s, G# at − 0.75 s, the C#-minor tutti on DUST. Piano, tubular bells on the bass motif, strings, contrabass, celesta, oohs, timpani on each new generation and the motif, a timpani roll into DUST, a rising harp + celesta arpeggio for the pull-in.
- SFX: a glassy tink per split (gen 0 → 6: 560 Hz × 1.17^k, decay shortening), ≥ 12 ms apart (+ random 0-16 ms when > 80/s: no buzz), gain ÷ √(rate/10); glass glitter on DUST. `audio.master(peak_db=None, reverb=0.5)`, sfx × 0.30, last 0.6 s digital silence.

## Flags
`--seed (7) --label --still --frame a,b --dry --simonly --capsheet <png> [--cap] --sound 0 --sfx (0.30) --fin (3.0)`. Pacing: `--ttgt (46) --r0 (1.8) --apull --wind --margin --minage`. Mill: `--w0 (0.4) --tauw (22) --wmax (2.6) --blade (175)`. Dust: `--graina (8)`.

## Test clip v1 (2026-11-11): Full HD, seed 7, label fhd
- Delivered for review: `<VIDEOS_DIR>\DopamineExe\review\dust_mill\` (`ol_dust_mill.mp4` captioned, `ol_dust_mill_base.mp4` caption-less, sheet, crops, README). Caption pass: `--capsheet` PNG at the render scale + `ffmpeg overlay` (`-c:a copy`, 2 threads). Sidecars stay in `output/` (`ol_dust_mill_fhd_9x16_events.json` / `_audio.wav`).
- Timeline: first split 0.18 s; PIECES passes 3, 9, 27, 81, 243, 729 at 0.18, 1.47, 5.35, 12.17, 22.33, 33.73 s; **DUST 46.40 s**; pull-in 46.95-48.8 s; dissolve 49.50 s; **50.10 s, 3,006 frames**.
- Splits/s 3, 2, 2, 2, 2, 4, 3, 2, 5, 4, 6, ... 58, 68, 72, 70, 83, 93 → DUST (per 5 s 11, 18, 26, 39, 62, 106, 142, 223, 351, 115/1.4 s). Max gap 0.85 s. Dust area 25% (0.18 s), 55% (5 s), 73% (20 s), 89% (40 s).
- Checks (encoded): h264 High yuv420p 1080x1920 @ 60; **-14.02 LUFS**, peak -4.20 dBFS, last 0.5 s silent; **flash_check PASS** (0); seam mean |Δ| 0.43 (pre-encode: only the blades differ, < one interior frame step = seamless wrap; check_loop's "MISMATCH" is the 1-frame blade advance, by design). RMS/5 s -19.1 → -15.8 dB. Notes/s 2-4 → 11-12; 770 SFX.
- Perf: FHD render ~6 min (bincount splat; `np.add.at` made the first Fast pass ~12 min).

## Doubts / owner calls
- 50 s: the middle (8-30 s, gens 3-5) is the risk; a new ×3 rung every ~10 s there. `--ttgt 30` gives a ~34 s cut with the same look.
- DUST % is front-loaded by geometry (25% after one split). Alternative: the hit's GEN n/7 ladder (log3 of the count).
- The steered pull is invisible as a rule but every split is a real contact; free physics could not end on a climbing rate.
- Brief deviations: rainbow (family) instead of violet; side 392 not 520 (the arena); no holdout piece.

## 34 s cut (2026-11-11, coordinator: "25 s → DUST reads as padding")
- `--seed 3 --ttgt 30 --label fhd34` → `review\dust_mill\ol_dust_mill_34s.mp4` (+ `_base`, `_34s_sheet.png`). Seed 7 at ttgt 30 ends on a straggler (0.68 s gap at 31.3 s); seed 3 ends at its peak rate.
- 34.07 s, 2,044 frames; DUST 30.37 s; PIECES passes 3…729 at 0.18, 2.05, 4.83, 9.65, 16.17, 23.18 s. Splits/s … 87, 101, 109, 145, 163 → DUST; max gap 0.70 s. -14.02 LUFS, peak -3.69 dBFS; flash PASS (0); seam 0.43 (blades only).
- fluidsynth "Failed to allocate a synthesis process" ×45 (of 1,087 piano notes) at the dense end: same ~330 score slots in 30 s overrun the 1,024 voices. The 50 s cut: 0. Fix if audible: cap piano durations by local note density.
- v2 option (not built): camera push-in on the hub 1.0 → ~1.7× from ~40% of the clip, pull back at DUST to show the full glitter ring; sim/audio untouched (README has the details).

## 4K ship (2026-11-11, owner: "34 s, your pick")
- `NF_SCALE=2.0 python scenes/ol_dust_mill.py --seed 3 --ttgt 30 --label 4k34` (render ~25 min) → caption: `--capsheet output/tmp/dust_cap_4k.png` + `ffmpeg overlay, libx264 slow crf 18, -c:a copy`. Base kept: `output/ol_dust_mill_4k34_9x16.mp4`.
- Staged: `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-16\2_ol_dust_mill.mp4` (slot 16:00 local Nov 17). 2,044 frames, -14.02 LUFS, peak -3.69, flash PASS (0), seam 0.37; frames match the FHD 34 s cut. The fluidsynth voice-limit warnings recur (same 1,087 notes, same as FHD).
