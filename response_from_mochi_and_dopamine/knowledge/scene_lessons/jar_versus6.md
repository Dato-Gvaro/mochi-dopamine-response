# jar_versus6: ICE, blender vs ice pick WITH A COMEBACK (owner review 2026-11-15, M1 rework)

- **Source:** fork of `scenes/jar_versus5.py` (v5 untouched). Owner verdict on v5: no race (blender led all the way), the pick "jumps weirdly", gold ice disliked. Decision: one try with real blender physics.
- **Deliverable:** `<VIDEOS_DIR>\MochiAndBolt\review\jar_versus6.mp4` (Full HD 9:16, label v6) + `jar_versus6_files\`.
- **Caption** (baked; `--cap ""` = base): "Every ice cube hit ~HARD~ cracks into 3" / "~Blender~ or ~pick~: whose glass ~OVERFLOWS~ first?" (v5's).

## The blender's weakness: the ice BRIDGES over the blade (JAMMED)
- **Rule** (one set of constants for both glasses, `Balls.update_bonds`, once per frame):
  - Crushed ice of gen >= `SNOW_GEN` 4 (pieces <= 4 mm) packs like snow.
  - A packed crumb has >= 3 contacts (pieces, walls or floor) and is not flying (< 400 px/s). After 0.25 s packed (`T_SINTER`) it sinters to the crumbs it touches.
  - A sintered cluster touching BOTH walls is an arch. It is locked: held on the walls, it does not fall and gives in contacts like a wall (infinite mass).
  - Cubes and chunks never sinter. They rest on the arch.
- **Breaking bonds:**
  - The blade knocks out any locked piece its plane cuts.
  - The pick's steel frees whatever it touches.
  - A hit harder than V_CRACK cracks a locked piece (or knocks a crumb loose).
  - Vibration: each locked piece with nothing under it (the hollow's ceiling) shakes loose at `VIB_RATE` 1.0/s × the dial.
- **What the sim then does:**
  - The blender's fines sink around the blade and pack.
  - Once a packed layer spans the glass, the chunks above sit on it, out of reach.
  - The blade (flat, v5 geometry: it acts only on pieces its plane cuts) spins in a ~26 px slot under the arch. The slot is full of churning powder of the smallest size (~130 crumbs), which cannot crack further.
  - Splits/s collapse to ~0 and the level freezes.
  - The vibration erosion never breaks the arch in the tested runs (no late surge). The sim gives none, and nothing fakes one.
- **Label honesty:** the brief's working name was "AIR POCKET: the blade spins in air". The sim's slot is full of powder, not air, so the on-screen label is **"JAMMED!" + "ice bridged over the blade"** (with a spinning-blade icon).
  - It shows while an arch spans over the blade and nothing crackable is in the blade's plane: `air_pockets()`, 5.33-14.97 s in seed 4.
  - Mochi worried, Bolt laughs; a soft two-note fall on the chord.
- **Tested and not used:** up-angled wings sweeping 1.5 cm (`--band 3`). The blender overflows at 4.4 s with no jam and no race. v5's flat blade stays: a documented geometry, not chosen post hoc.

## Engine fixes (v6; all apply to both glasses)
- **Wall tunnelling.** A crumb at 9 px/substep crossed the 6 px glass and counted as "spilled". It looked like spray and leaked thousands of pieces. The side of the wall now comes from where the piece started the substep.
- **Floor-clamp launch.** A pick-shove cancelled by the floor clamp became a ~5,000 px/s launch (v5's whole cubes over the rim). Inner-wall and floor clamps are contacts now, not velocity; restitution 0.35 sets the bounce.
- **Correction pumping.** The CORR_V cap (350 px/s) was per substep, so a piece held in a packed pile gained +350 px/s every substep and the pile was pumped up. It is now a cap on the TOTAL speed a contact push gives.
- **Pick fragments.** A pick WEDGES a cube apart: its pieces spread at SEP_V. v5 flung them down at 0.8 × 6 m/s into a pile that could not give.
- **Result:** in the first 8 s the highest piece in Bolt's glass is a chip 54 px above the rim (v5: cubes to y≈450). The ~100 pieces spilled before the finish are fines once the glass is >88 % full.

## The pick (smooth, believable)
- **One stroke cycle, no teleports:**
  - MOVE: smootherstep glide plus a small lift arc. Peak ≤ `GLIDE_V` (4 m/s mapped = 50 px/frame); the measured max is 49 px/frame (v5: ~137-180 px/frame and off the top of the frame).
  - WIND: a 22 px raise in 0.035 s.
  - STRIKE: 6 m/s, 75 px/frame (the real strike).
  - WITHDRAW: straight back up its channel to 34 px above the surface, eased in-out, peak = the strike speed.
- **Aim:** only RESTING pieces count for the target and the hover height (v5 aimed over flying cubes and leapt off-frame). Biggest gen first, then least buried, then nearest (`TRAVEL_W` 5 px per px of travel).
- **Rate:** set by its own motion (~3.3 strikes/s at full dial; 48 strikes in the race). The dial asks 9/s, but a smooth stroke cannot go faster.
- **Withdraw shove:** while pulling out or gliding, the spike shoves crumbs sideways only (no riding up the tip).

## Look
- **Ice** is the same clear pale-cyan in both glasses: 5 shades (0.62-0.85, 0.86-0.96, 0.98-1.0), alpha 0.58-0.86, white edges, inner facet, glint.
  - Fines blend toward snow-white. Sintered (arch) crumbs are packed-snow white, so the bridge is visible.
  - Crack glints are icy white/cyan. No gold anywhere on the ice.
- **Sides** are told apart by the rim (side-colour lip + bulbs), label, gauge and character colour: Mochi coral (1.0, 0.52, 0.45), Bolt teal (0.33, 0.80, 0.72).

## Timing knobs (shared; none can change who wins)
- Both tools run 2.0 s before frame 0 (`--pret`), so frame 0 is mid-race at 50 / 47 %.
- Dial 40 % → 100 % over 4 s (`--l0 0.4 --tramp 4`).
- Finale 2.0 s: OVERFLOW! 0.8 s, BOLT WINS! 0.65 s, dissolve 0.6 s.

## Outcome across seeds (pret 2.0, l0 0.4, tramp 4)

| Seed | Winner | Overflow | Lead change |
|---|---|---|---|
| 1 | pick | 17.50 s | |
| 2 | **blender** | 5.45 s (overflowed before the arch formed) | |
| 3 | pick | 15.15 s | 12.2 s |
| 4 | pick | 14.97 s | 13.37 s |
| 5 | pick | 15.22 s | 12.12 s |
| 6 | pick | 17.37 s | |
| 7 | pick | 16.08 s | 11.8 s |
| 8 | pick | 15.53 s | |

- The pick wins 7/8: the majority outcome. Seed 4 is picked for TIMING only (the earliest finish keeps the clip ≤ 17 s).
- Earlier configs (pret 0.12-1.5, tramp 4-5) also gave the pick in every seed tried (1-5). One exception: pret 3.0 with seed 2, where the blender overflowed at 5.2 s.

## Seed 4 (default): the sim's result
- **Level blender/pick (%):** 0 s 50/47 · 2 s 66/56 · 4 s 84/65 · 5 s 92/71 · **JAMMED 5.33 s at 93 %** · 8 s 93/82 · 10 s 93/88 · 12 s 93/93 · **PICK TAKES THE LEAD 13.37 s** · **pick OVERFLOWS 14.97 s**, blender 93 %.
- Clip 16.98 s (1019 f).
- Cracks 1,371 vs 1,396; pick 48 strikes in the race (all cracking).
- Pick splits/s climb to the end: 21 → 142.

## Sound
- v5's chain: Figaro re-timed so bar 18's D-major downbeat lands on the OVERFLOW (14.97 s); crack tinks, pick toks, blade chks, overflow clinks.
- New: a two-note fall at the jam.
- Music silent from T − 0.95 s; last 0.5 s digital silence.

## Doubts
- **Meter vs picture (main doubt).**
  - Both glasses LOOK heaped to the OVERFLOW line from ~6-7 s (the blender's chunks ride on the arch over the hollow; the pick's mid-size pieces pack loosely). The volume meter reads 78-99 % meanwhile.
  - The winner does not depend on the definition: by volume the pick wins; by literal spill the pick's glass sheds chips from ~9 s and the blender's never spills.
  - Alternative for the owner: finish on the first visible spill (~10 s, a ~12-13 s clip), with the meters then reading ~90 %.
- Verification: pre-encode seam 0.000 (the last frame redraws frame 0); post-encode 0.95 is x264 noise in the dense ice.
- The blender is frozen for 9.6 s (5.3-15 s). Only its powder churns under the arch while the pick climbs. Is that tension, or a dead half of the screen?
- The lead change comes late (13.37 s, 1.6 s before the finish): a last-second comeback, not a mid-video overtake.
- The jam's "slot" is thin (~26 px); the label carries the explanation.
- 1 seed in 8 gives the blender the win before it jams. That is honest (a race), but titles that name a winner must match this seed.

## Args
- `--seed` (4), `--pret` (2.0), `--l0` (0.4), `--tramp` (4), `--tail` (2.0), `--vib` (1.0), `--snowgen` (4), `--sinter` (0.25), `--packn` (3), `--vfly` (400).
- `--band` (1 = flat plane, all pieces; 3 = 1.5 cm sweep, tested), `--glide` (4.0), `--travel` (5.0), `--pickv` (6.0).
- `--nopacked`/`--relslip` (rejected rest criteria), `--dbgpop`, `--still --frame a,b`, `--report`, `--resim`, `--label`.

## Build history (what failed)
- **Absolute-speed sintering** (speed < 60 px/s): PBD jitter keeps crumbs at ~0.15 m/s, so no arch until the blender had already died.
- **Slip-anchor sintering:** an arch only at ~11 s.
- **Relative-slip sintering:** at 9 s.
- **Packed (contact count):** the arch at ~6 s. Kept.
- **Blade passing over dust** (`--band 2`, v5): the blender stalled at 87 % in its own dust bed at ~10 s, with no bridge. The blade now throws dust too.
- **Hand-speed glide** (2 m/s, 25 px/frame): the pick needed 19-22 s. 40 px/frame: 17.6 s. 50 px/frame + nearer aim: 15-17.5 s.

## v6b: the tight cut (owner 2026-11-15): RIM meter + end on the first visible spill
- **Why:** the volume meter read 78-99 % while both glasses already LOOKED heaped to the line from ~6 s; the blender sat frozen 9.6 s.
- **Meter (`rim_meter`, `--meter rim`, default; `--meter vol` = v6):** the median of the per-6 px-column pile top (all pieces inside the glass) vs the OVERFLOW line, smoothed 31 frames centred. Same rule both glasses. Post-processed from the cached sim: physics identical.
  - A speed filter ("resting only") from frame diffs is NOT usable: piece order changes on splits/culls.
- **Finish:** the first frame with >= `SPILL_N` 3 pieces outside the glass walls at once (lone thrown chips at 1.1 s and 6.5 s are 1 piece). The meter shows 100 % from that frame; before it, capped at 99.4 % (seed 4: 0.17 pt of cap).
- **Seed 4:** frame 0 66/71 (the pick's loose chunks stack tall) · blender lead 2.45 s · JAMMED 5.33 s at 89 % · PICK TAKES THE LEAD 5.75 s · pick 96-99 % from 6 s · **first spill 9.13 s** (f547, 5 pieces) · clip **11.13 s** (668 f). Blender never spills.
- The surface meter is noisier than volume: the leader's gold flips once for 0.17 s at ~1.4 s.
- Figaro is re-timed to the earlier finish: 52 beats in 9.13 s = ~340 qpm (v6: 208).
- Lesson: measure the meter on what is DRAWN (pile top) before shipping a "fill" race; packed volume lags a loose pile by 10-20 points.
- **Music for the 9.13 s finish (`--music cut`, default; `--music v6` = old):** Figaro bars 1-5 + 15-17 → bar-18 D downbeat on the OVERFLOW = 32 quarters = ~210 q/min. The full v6 cut (52 quarters) ran ~340 q/min on the shorter race: too fast (coordinator). Keep the tempo ~208 ±10 % by choosing the bar count, never by stretching. Timpani in the cut-out bars are dropped (they mapped to wrong times).

## 4K ship (2026-11-15, approved)
- `NF_SCALE=2.0 python scenes/jar_versus6.py --label 4k` -> `reserve\jar_versus6_4k.mp4` + `_UPLOAD.md`. 2160x3840, 668 f, -14.01 LUFS / -1.99 dBFS, flash 0, seam 0.64; frames vs FHD mean diff 0.97-1.38.
