# jar_versus5 — ICE: blender vs ice pick, every cube hit HARD cracks into 3 (shorts_1115 M1, 2026-11-15)

- Brief: docs/BRIEF_shorts_1115.md §M1. New file `scenes/jar_versus5.py` forked from jar_versus4 (v4 untouched, bit-reproducible).
- Nameable change: "this time it's ICE" — clear ice cubes in two tall glasses; Mochi = a BLENDER BLADE at her glass floor (continuous), Bolt = a floating ICE PICK striking from above (impacts). Rule, OVERFLOW finish, engine, Figaro = v4's.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\jar_versus5.mp4` (Full HD 9:16, label v1) + `jar_versus5_files\`.
- Caption (baked; `--cap ""` = base): "Every ice cube hit ~HARD~ cracks into 3" / "~Blender~ or ~pick~: whose glass ~OVERFLOWS~ first?"

## Scale + the one crack rule
- Glass 10 cm wide inside → **3480 px/m**. G 1600 px/s² (v4's) = real g shown in **~4.6× slow motion**; `mps(v)` maps a real m/s to sim px/s (×756).
- **V_CRACK = 2.6 m/s** (1966 px/s): a cube cracks into 3 (each 2/3 as wide, v4) when hit by a tool OR another cube at a normal speed above it. One constant for both sides.
- Pieces leave any hit at ≤ 2.9 m/s (V_MAX 2200 px/s, v4's engine cap).
- Cubes: rounded squares (half side a), collision radius = mean of in- and circumscribed radii = 1.207 a; R0 34 px (a 2.0 cm cube). Each piece turns (angle + spin, damped at rest).

## Tools
- **Blender (Mochi):** blade tip radius 0.40 × width (4 cm), plane 0.75 cm above the floor, **tip speed 20 m/s** (blenders 15-25), on v4's dial 25 % → 100 % over 8 s. Seen from the side it sweeps a disc: a piece cut by the blade plane is passed by a blade end twice per turn (probability 2ωdt/2π per substep, seeded), leaves at the blade speed at its radius (plastic hit, capped), thrown OUT toward the wall (the vortex) and cracks if that speed > V_CRACK. Flat blade (pitch 0). Crumbs of the smallest size under the plane are passed over (`--band 2`).
- **Ice pick (Bolt):** strikes at **6 m/s** (a hand pick 5-8 m/s), 9 strikes/s at 100 % on the same dial (v4's jackhammer rate). It aims at the biggest exposed crackable cube, glides there (55 % of a cycle), strikes 7 cube radii deep, cracking every crackable piece it meets head-on (normal speed > V_CRACK); a 0.2 kg pick at 6 m/s carries ~3.6 J vs ~0.1-0.3 J per cube, so the stroke drives on. The pick shoves (does not throw) the pieces it pushes aside.
- Both tools run from 0.12 s before frame 0 (`--pret`), so frame 0 is mid-action for both.

## Fill + finish
- v4's VOLUME level: (ice area inside the glass) / (width × PACK). OVERFLOW = level at the rim (the frosty line) for 20 frames.
- **PACK 1.0 (v4: 0.82), measured:** with 0.82 the HUD read 100 % while the drawn crushed pile sat ~120 px below the line (crumbs pack densely and overlap a little in the PBD). Compared the drawn pile's median top with the volume level per second (`output/tmp/mochi_1115/vtop.py`); 1.0 puts the % on the drawn pile, so OVERFLOW! appears when the ice visibly reaches the line. A median-of-surface ("visible") level was tried and dropped: the pick's craters and flying cubes made it jump ±40 %.
- **Rim y 760** (glass 530 px tall, 15 cm): with honest packing 18 crushed cubes only roughly double their visible height, so the race starts at **~36 %** (brief: ~28 %). A 28 % start never reached the rim inside 17 s.

## Engine fix (v5 only)
- PBD overlap corrections are capped at CORR_V 350 px/s, but a wall/floor clamp could cancel a correction and the leftover became a ~1700 px/s upward launch (v4's "balls fly over the caption" doubt). v5 only subtracts the part of a correction still present in the displacement. Suggestion: same one-line fix for v4-type scenes in future episodes (v4 not touched).

## Build history (what failed, for the next ice episode)
- Speed cap 2.9 m/s + a 30° pitched blade: the blender fluidised its crumbs and threw 5-12 thousand pieces over the rim (level fell to 3-12 %).
- Kicking everything under the blade: crumbs buried the blade, stall at 78 %.
- Pick that stopped at its first crack: ~1 %/s, never close.

## Seed 2 (default) — the sim's result
- Level blender/pick: 0 s 37/35 · 2 s 46/41 · 4 s 58/54 · 6 s 72/65 · 8 s 84/70 · 10 s 95/73 · **OVERFLOW (blender) 11.22 s** · pick 74 % then. Clip 14.42 s (865 f).
- Pieces 3,922 vs 1,454; cracks 2,493 vs 740; pick 103 strikes (91 cracking); 1,064 blender pieces spilled (most after the overflow).
- **No lead change** (brief asked ≥1 before 8 s): over seeds 1-9 the blender led from ~1 s in every finished run; seed 1 had the pick ahead until 4.4 s but no overflow inside 15 s. Seed search may only time, not flip, so the blender-all-the-way race ships, and the doc says so. The early seconds are close (38/37 at 0.25 s, 52/50 at 3 s).
- Outcome vs v4: v4's impact tool (Bolt) won; here the continuous tool (Mochi) wins — not the same outcome twice.

## Sound
- Music: v4's Figaro (Mozart, PD; `mozart_figaro_overture\mfig.mid`), re-timed so bar 18's D-major downbeat lands on the OVERFLOW.
- SFX (own synth): ice "tink-crack" per 12 ms group of cracks (glassy ping on the chord tone sounding in Figaro + a dry 2-tick crack; gain and ring length ∝ piece size; density-ducked), pick "tok" per strike, blade "chk" when it catches a chunk (≤ 1 per 50 ms; no motor hum), cascading table clinks rising through the chord as the winner's ice spills. Non-note sounds sit +12 ms off the crack onsets (PROTECT_NOTES; this scene mixes directly, so nothing is dropped anyway).
- Master: own −14 LUFS / −2 dBFS lift; music silent from T − 1.35 s, last 0.5 s digital silence.

## Checks (encoded Full HD, label v1)
- h264 yuv420p 1080x1920 @ 60, 865 f = 14.42 s; −14.01 LUFS (muxed, stereo), peak −1.97 dBFS, last 0.5 s −240 dB; flash_check PASS (0 flashes, mean lum 0.05); seam mean delta 0.57.
- Sound events/s 34 41 61 68 91 109 113 107 107 96 95 107 94 (silent tail); 79 % of 846 event times have a >1.2 kHz onset within 40 ms. Notes: 19 distinct, top pitch 30 %.
- Frames read every ~1 s from the mp4; 1:1 crops of both glasses at 6.0 s and of the overflow at 11.25 s.

## Doubts
- A few of Bolt's cubes still pop out of his glass on the first strikes (0.5-3 s), one up to y ~450.
- The blender blade is mostly hidden under the ice after ~2 s (only its blur and hub show).
- Seam 0.57 sits inside the good band; the dissolve hides ~4,000 pieces fading to 18 cubes.
