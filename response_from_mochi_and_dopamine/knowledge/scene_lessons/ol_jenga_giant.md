# ol_jenga_giant — the robot pulls 2× faster every round until the tower FALLS (DopamineEXE, batch51, 2026-10-25)

- Brief: docs/BRIEF_batch51.md ("ol_jenga_giant") + BRIEF_batch50 lessons. New scene file `scenes/ol_jenga_giant.py`; lib/ and tools/ untouched. Rigid-block solver and honest statics are copied from jenga_pull / box_tower (plus a sweep-and-prune broadphase and arena walls); the HUD, caption and watermark style are copied from ol_wall_collapse.
- Deliverable: `<VIDEOS_DIR>\DopamineExe\review\ol_jenga_giant.mp4` (**v1**, Full HD 9:16, 13.58 s, 815 frames; output label v1). No 4K yet.
- The trademark word is not used anywhere on screen; "block tower" in text.
- Different from jenga_pull (Mochi & Bolt): ONE giant 50-level tower, no characters, a robot arm on a rail, a rate that doubles, a pile of pulled blocks, a mid-tower collapse into an avalanche.
- Caption (baked; `--cap ''` = base): "Every round the robot pulls ^2× FASTER^" / "until the tower ~FALLS~" (`^x^` = the current rate colour, `~x~` = gold).
  - The coordinator's line "Every pull gets 2× FASTER" was changed: if every single pull were 2× faster, the pulls would converge in ~2 s. The rate doubles every bar (a "round"), and the ×N pill shows it.

## Layout (logical 1080×1920, static camera)
- Black background, a thin white arena frame x 120–900, y 318–1236; the floor is its bottom line.
- Tower: 50 levels × 17.5 px = 875 px (top at y 361), blocks 30 × 17.5 end faces, 90 long. Centre x 340, light oblique view (KD 0.212).
  - End layers (even) show 3 end faces; bar layers (odd) show the front bar's long face.
  - Wood: one ordered gradient by height (deep cherry at the base → golden maple → pale honey at the top), sat ~0.55–0.66, ±3.5 % tone per block.
- Robot (steel + one teal accent): a rail column at x 768 with a base plate, a carriage, a two-link elbow-down arm (172 + 165 px), a wrist and two jaws.
- Pulled blocks are flicked right and fall onto a physical pile between the tower and the rail (it grows to ~y 1060).
- HUD: LEAN meter at y 1300 (green → amber → red, "LEAN x.x°", red FALLS goal mark visible from frame 0; "TOWER DOWN" after); counter y 1490 = "N" + ×N pill (×1 teal, ×2 green, ×4 amber, ×8 orange-red) + "BLOCKS PULLED"; "DOPAMINE.EXE" watermark at 35 %.
- Key content is inside x 0.10–0.84w (the arena itself is 120–900).

## Rule and physics
- Rate doubles every bar: ×1 = half notes (bar 29), ×2 = quarters (bar 30), ×4 = eighths (bar 31), ×8 = 16ths (bars 32–33). Pull 53 lands on the bar-34 downbeat. 6 pulls happen before frame 0, so holes and a pile already exist.
- Choreography:
  - ×1–×4: the arm climbs the tower (levels 5 → 43), pulling FRONT bars out along their length.
  - ×8: it zips DOWN one level per 16th (44 → 13), pulling the right end block of every end layer and the back bar of every bar layer.
  - The last pull is level 12's right block.
- **Drag:** each yank drags every level above it toward the robot. It is 0.85 px × (0.30 / 0.45 / 0.65 / 1.0 for ×1 / ×2 / ×4 / ×8), and 4.0 px for the last yank. Top drift is 39 px and the lean 2.56° at the fall.
- **Statics** (`statics`, as jenga_pull): for every interface, the centre of mass of everything above must lie over the contact patch's hull (x and depth).
  - An end layer missing its right block is supported only 15 px right of its centre.
  - The min margin is 15 px through ×1–×4 (depth, from the front bars). It falls 13.8 → 2.0 px through the ×8 run, then **−1.97 px at pull 53** (interface 12).
  - The scene asserts that 53 is the first unstable count.
- **Meter** = max(lean / lean-at-fall, (1 − margin/16)^1.2), capped at 0.97 until the fall.
- **Rocking (cosmetic):** every yank rocks the tower about its base corner, with an amplitude that grows as the margin goes.
  - **Stubborn beat:** the yank on the bar-33 downbeat (6.4 s sim, 6.58 s clip) rocks it 2.3° (the meter goes nearly full red), and it recovers while the arm keeps pulling.
  - The rocking fades out before the last pull.
- **One rigid-block sim** for the whole clip:
  - Settings: dt 1/480, 14 iterations, g 2600, block friction 0.26, floor 0.55, restitution 0.38. Depth masks: end blocks collide with everything; bars only with bars in the same slot. Arena walls are colliders.
  - Each pulled block becomes a body at its release, with a toss velocity (300–600 px/s right) and a spin.
  - At the fall, the 97 tower blocks become bodies, and the levels above 12 get a rigid tip of ω 0.30 rad/s.
  - Result: the upper tower kinks and whips right over the robot, shears into an avalanche over the pile, and spills back left against the wall. A 33-block stub stays standing.
  - Cached as `output/ol_jenga_giant_sim_<params>.pkl`; `--resim` forces a new run.

## Timeline (clip s; clip = sim + 0.18)
- **0.0:** 6 pulled, ×1, the arm mid-slide on a front bar at level 17. A 6-block pile, lean 0.1°. The block clears at 0.18.
- **0.5 / 1 / 2:** 6 → 7 (the block arcs onto the pile), then the arm travels and grips; 8 at ×2 (pill pop at 1.78); 9 at ×2, the arm climbing.
- **3.38:** ×4. **4.98:** ×8, the zipper from the top. Lean 0.5° → 2.3°, meter amber → red, creaks grow.
- **6.58:** the stubborn sway (2.3°) and a long creak; it recovers.
- **8.18 (bar-34 downbeat, ff F minor):** pull 53, TOWER DOWN, the counter turns gold. The tower kinks, whips right and crashes. Most impacts happen in 8.3–9.6; it settles by ~11.
- **10.98:** held C-minor chord, then 6 gold glints along the pile. Hold, then a 0.6 s dissolve into the pre-roll (the last frame is pure pre-roll).

## Sound (music first)
- **Piece:** L. v. Beethoven, *Coriolan* Overture, Op. 62 (1807; Beethoven d. 1827, PD). It fits "tense, when will it fall".
  - Not on any used/banned list. No other scene uses it (Egmont and the symphonies are other works). Not kid-coded.
- **Source:** Mutopia piece 57 (Mutopia-2013/02/06-57, licence **Public Domain**; Breitkopf & Härtel Gesamtausgabe). Saved at `<SOUNDFONTS_DIR>\scores\beethoven_coriolan\` + `SOURCE_mutopia.txt` (downloaded 2026-10-25).
- **Excerpt:** bars 29–35 beat 4, at one steady tempo, quarter = 0.40 s (150 bpm, the MIDI's own):
  - the pedal-point crescendo (held violin D, horn sighs, timpani/trumpet C growing);
  - the bar-34 fortissimo F-minor tremolo = the fall;
  - the falling chromatic tremolo of bar 35 = the avalanche;
  - then an added held C-minor tutti chord (strings + tremolo, horns, trumpets, winds, cello/bass C, timpani hit + roll).
- **Arrangement:** all 12 score parts mapped to lib/orchestra. Repeated 16ths are merged onto tremolo strings. Expression ramps 0.80 → 1.0.
- **SFX** (all tonal):
  - **Every pull:** a wood clack (free-bar partials 1 : 2.76 : 5.40) pitched to the harmony; its register follows the level, so the zipper is a descending clack line.
  - Jaw ticks (to ×4), stick-slip ticks on the slow slides, and creaks on pulls whose gain follows the lost margin (every beat on the ×8 run).
  - The stubborn beat gets a 1.05 s bending creak + groan; the topple a 1 s creak.
  - Every simulated impact over 130 px/s is gathered on a 32nd grid and pitched to the chord: soft low toks for the pile, crash clacks with fifths/octaves for clusters, and deep tonal thuds for big floor hits. Glint tinks follow the chord.
- **Mastering:** `level_bed` (+3 dB crescendo, `--findb 2.5`), then `audio.master(peak_db=None, reverb=0.5)`, the last 0.55 s zeroed, and a mux without `-shortest`.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080×1920 @ 60 fps, 815 frames = 13.58 s.
- **flash_check PASS** (0 flashes, mean lum 0.013).
- −14.00 LUFS, peak −6.31 dBFS (muxed), last 0.5 s digital silence.
- RMS/s: −19.7 −18.9 −18.5 −18.6 −17.4 −17.3 −16.6 −16.1 −15.3 (fall) −14.7 (avalanche) −16.0 −15.4 (chord) −19.0, then silence.
- SFX events/s: 24 15 25 23 28 27 33 32 37 50 11 14 8 0.
- Pulls/s: 2 1 3 4 5 10 10 10 2.
- Seam (check_clip, encoded): mean delta 0.519 (inside 0.12–0.72).
- Frames read from the mp4: 0, 0.5, 1, 2, 6.6, 8.3, 8.8, 9.5, 12, 13.56.
- 1:1 crops: frame 0 (the gripper holding the sliding bar, the holes, the pile) and 8.8 (the kinking tower, the pile).

## Doubts
- The tower kinks at ~level 22 rather than exactly at the failing level 12. The kick tips everything above 12, but the low friction lets the column shear and bend like a whip. It reads as "it's going", but it is less of a clean single topple.
- Part of the falling column spills LEFT, back over the stub, after it hits the right side.
- After ~11 s the scene is mostly still (the pile settled, glints, the held chord) until the dissolve: about 1.5 s with little motion.
- The tower is thin (90 px wide) to fit 50 levels at real block proportions. Its alternating layers can read as a brick wall at a glance; the holes and the sliding blocks make it read as a block tower.
- Bar-layer pulls show only as a darker recessed bar (front) or a gap on the side face (back). The clearest holes are the right-end gaps of the ×8 run.
- Cartoon cheats:
  - the drag is a scripted per-pull shift (only its consequences are computed);
  - the rocking is cosmetic;
  - the arm moves at 10 pulls/s in ×8;
  - the robot is not a collider (blocks fall in front of it).
- The ×8 round lasts 2 bars (the rate plateaus at 10/s for 3.2 s; the stubborn sway, the creaks and the crescendo carry the rise).

## Args and cost
- Args: `--dk 0.85`, `--dlast 4.0`, `--kickw 0.30`, `--mub 0.26`, `--rest 0.38`, `--sfx 0.55`, `--findb 2.5`, `--cap`, `--still --frame a,b`, `--audition`, `--report [--sim]`, `--tune` (prints the margin per pull count), `--resim`, `--reuse`, `--label`.
- Cost: the sim runs once (then cached); the Full HD render + audio took a few minutes at 2 encoder threads.
- Owner review: pending.

## Upload draft
- Titles (no trademark word):
  - "Every round the robot pulls 2× FASTER… until the tower FALLS 🤖 #satisfying #physics #shorts"
  - "A robot pulls blocks faster and faster from a 50-level tower 🪵 #satisfying #physics #shorts"
  - "It held on once… then the robot got greedy 🤖💥 #satisfying #physics #shorts"
- Pinned comment: "it swayed so hard at 6 seconds and still didn't fall… which block did you think would end it?"

## Outcome
- (fill after upload)
