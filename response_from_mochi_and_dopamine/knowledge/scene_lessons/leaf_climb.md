# leaf_climb

- Owner's idea (2026-10-05): Mochi jumps up a tree leaf to leaf, and landing on the EDGE of a leaf launches him higher. Meanwhile Bolt saws the tree down. New scene, built from scratch.
- Rule: reach the golden fruit in the crown before the cut reaches 100%.
- Caption: "Reach the TOP before it falls|~Bolt is SAWING the tree~". Line 2 is the stake, not a prediction question.

## Physics (tree-local frame, dt 1/60, 8 substeps)
- Each leaf is a cantilever springboard: a rotational spring at the stem with K, I and C (damping ratio 0.075).
  - q is the tip drop (an angle).
  - A point at fraction u of the leaf moves Lg(u) = L cos(beta) (u^2 - u^3/3) per unit of q.
- Landing is a plastic collision with the leaf's effective mass at that point, I/Lg^2.
  - Tip: 0.22 x Mochi, so the leaf bends deep.
  - Near the stem the effective mass is huge, so the landing is a dead thud.
- Mochi stomps on the down-stroke (F_LEG = 2.2 mg). He leaves when the leaf is back at rest (or the rebound ends) and adds a V_POP 480 leg pop.
- Result: an edge landing launches 160-290 px. A stem landing gives a 44 px hop, then he hops further out on the same leaf.
- Leaves get springier with height (K_TIP 150 -> 50) and the spacing grows (112 + 2.2 i). So the jumps grow: 2 somersault leaps (rise >= 250) come late.
- Aim: Mochi always targets the highest reachable leaf at u ~ N(0.86, 0.05). 20% of his landings are stem misses at u 0.15-0.32.
- After a launch, the leaves wobble free. Each creak kicks every leaf, and the shudder runs up the trunk at 3200 px/s.

## Saw
- Strokes accelerate from 1.75/s to ~6/s, at 1.18% cut per stroke (+-15%).
- At 62% cut the lean pinches the blade: 0.62 s stuck, two yanks, then a steel latch snap.
- Creaks at 40/55/70/80/88/94% cut. From 55% each creak adds a lean step (total 0.061 rad).
- Sway = amp(cut) * (1 - cos)/2 at 0.45 Hz, so the kerf never closes. The kerf wedge opens honestly about the hinge on the left.
- At 100%: CRACK. The tree topples about the hinge (a'' = 7.6 sin a), lands in 1.34 s (THUD + dust wall + leaf flutter) and rebounds slightly.

## Ending (seed 23, Bolt wins)
1. Mochi's final leap toward the crown starts 0.12 s before the crack. Unhindered it would have landed at +0.42 s; by then the crown has swung away ~160 px.
2. Mochi hangs in the air for 0.40 s (worried stare at the camera), then drops 2900 px. The camera follows and the mist split closes.
3. He splats on the fallen log and goes dizzy.
4. The golden fruit flies back in, BONKs him and bounces onto Bolt's head.
5. Bolt cheers ("BOLT WINS!") and laughs. Mochi gives an annoyed stare.

## Camera and look
- One picture with a mist band at y 1060.
  - At the start and the end the frame is a single continuous view from the ground up.
  - While he climbs, the upper view follows Mochi with a critically damped spring and tracks the lean 80%, while the strip below stays on Bolt.
- The sky darkens with altitude: stars appear and a moon rises.
- Fireflies use whole cycles per clip.
- Leaves run emerald -> teal -> gold up the tree, with glow strokes, a gold rim and a sweet-spot glow at the tip that brightens with the bend.
- Golden fruit in a gold/teal crown rosette. Steel saw.
- Progress bars at 0.745-0.80 h: "MOCHI xx% CLIMBED" vs "BOLT xx% CUT".

## Sound
- mountain_king note per landing. Stem landings get a softer note plus a pok.
- Bed (built in the scene, `render_soundtrack(bed=...)`):
  - leaf boing at each launch, pitch 150-410 Hz by rise;
  - a band-noise saw rasp per stroke (tooth chatter, 60% of the stroke, push brighter than pull);
  - stick-slip wood creaks;
  - a whoosh during the fall.
- Events: crack = snap + slam; saw clank on the ground; thud = slam; splat = bounce + squash; bonk; fruit tinks; cheer arpeggio + pop.
- Silent from 26.7 s.
- `tools/regen_audio.py` cannot rebuild the bed from `_events.json`. Rerun the scene, or use the build_bed + render_soundtrack pair.
- Lesson: the first mix had the rasp at -38 dB RMS against notes at -21, so it was inaudible. The rasp gain is now 0.26 + 0.12*cut.

## Numbers (s23)
- Crack 22.76 s, thud 24.10, Mochi lands 24.90, reset at 28.44, clip 29.83 s (1790 frames).
- 25 jumps: 21 edge landings, 4 stem landings. 85 strokes.
- Landings + strokes per 5 s: 19, 23, 31, 37.
- Progress (Mochi vs Bolt): 18/12 at 5 s, 55/37 at 12 s, Mochi stalls on leaf 12 (2 stem misses), 84/85 at ~21 s, ends 95 vs 100.

## Loop
- The reset is silent and lasts 1.40 s:
  - the tree swings back up and the cut heals;
  - the sawdust pile and progress bars ease to 0;
  - Bolt walks back to the frame-0 saw pose;
  - Mochi follows a Hermite path to the state one frame BEFORE frame 0. Frame 0 is mid-air on a parabola, so the seam is one honest step.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 29.83 s.
- -14.01 LUFS, peak -7.2 dBFS, last 0.5 s -240 dBFS.
- Seam mean 0.568 (good band).
- flash_check: 0 flashes = PASS (mean lum 0.035).
- 39 notes, 20 distinct, top pitch 12.8%.

## Args and search
- Args: --seed (23), --label, --cap, --melody, --search N, --still --frame.
- `--search N` keeps seeds where the crack lands 0-0.30 s after Mochi's final leap toward the crown and no crown is reached first.
  - In the 1-30 sweep, only 23 fits.
  - Near-misses: seeds 12 and 28 crack 0.03-0.04 s into a leap to the LAST leaf (one leaf short). Seed 7 cracks 0.44 s after the crown leap.
  - Many seeds (1, 2, 5, 6, ...) are Mochi wins, which have no ending built yet.

## Delivery
- Delivered to <VIDEOS_DIR>\batch14\leaf_climb.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-06: Not what was expected: ugly leaves, bad sounds, and a sawn tree doesn't fall bit by bit. If it's worth it, use a forestry TRACTOR / tree-felling machine; otherwise leave it.
- Owner review 2026-10-06:
  - Not what he expected: the leaves are ugly and the sounds are not good.
  - A sawn tree doesn't go down bit by bit; for that, use a tractor with a tree-destroying head.
  - -> leaf_climb2 (forestry mulcher, glossy leaves, pluck/thump/tick sound).
