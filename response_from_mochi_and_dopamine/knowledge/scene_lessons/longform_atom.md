# longform_atom: "Every crushed ball splits into 3... from the SUN to an ATOM"

- Briefs: docs/BRIEF_longform1.md (v1/v2) and docs/BRIEF_batch58.md "Long-form v3 test" (2026-10-29). Native 16:9 long-form for Mochi & Bolt, logical 1920x1080.
- Status (2026-11-01): **the FULL crusher video (Full HD) waits on the owner** (`review\longform\longform_atom_crushers_full_fhd.mp4`, Phase 3f). Earlier: Phase 3a crusher TEST (`review\longform\longform_atom_crushers_test.mp4`; the full re-render with crushers follows only after the OK). Before that: **FULL video, Full HD, waits on the owner's review** (`review\longform\longform_atom_full_fhd.mp4`, 2026-10-31). v4 test approved with one fix (the pour free fall, done). No 4K and no upload before the owner's OK. Archived: v1, v2, v3 (`MochiAndBolt\archive\longform_atom_test_v3.mp4`) and a v4 draft render with a stroke-3 glitch (`...\archive\longform_atom_test_v4_draft.mp4`, never shown).

## Phase 3: a different CRUSHER per chapter (owner 2026-11-01, BRIEF_longform1 "Phase 3")
- Flag: `--crushers` (`CR`, `CRUSH_PLAN`, `CR_BUILT`, `tool_of(m)`). Without it every jar is the press: the delivered full video's path and caches are untouched. Crusher builds use their own caches: `output/longform_atom_build_cr_j*_s1.pkl`, `..._early_cr_s1.pkl`, frames `longform_atom_frames/deep_cr_j*`, chunks `output/longform_atom_chunks_cr/`, label `crtest`.
- What stays: the split rule (x3^(-1/3), 1 -> 3), the counter (3^n exact), the stroke plan (`timeline`), the pours/drops, the Grieg form. Only the tool that triggers a wave changes. Each tool has its own approach, contact, struggle, release, look and SFX, a "NEW CRUSHER" pill in the stage at its first stroke and a "CRUSHER: ..." HUD line; Mochi cheers each arrival, Bolt worries (weight, bomb) or laughs (vise).
- Families (how the split is triggered, all honest):
  - TOP (press, drop weight, pile driver, boot, jackhammer, juicer, mallet, microscope tip): contact under a face; the wave runs in hop order through the touching pile (the press's rule).
  - SIDE (vise, boxing glove, nutcracker, optical tweezers): jaws close from the stage edges (the column's box walls sit 45 px outside the stage, so side tools come in from there); hop order from both faces.
  - RADIAL (blast, meteor, impact probe, ultrasound, laser pulse, ion beam): a ring from a point at constant speed; every ball pops as the ring reaches it (its radius IS the pop schedule) and gets an outward kick.
  - SWEEP (steel roller, rolling pin) and SWING (wrecking ball): to build (pop order = sweep position / hop order from the impact).

### The plan, all 23 jars (coordinator 2026-11-01: 10 tools CYCLED; the owner can still change it)
- Rules: the press opens (jars 1-2) and closes (the ATOM); no tool comes back within 3 chapters (same tool >= 4 jars apart); a tool's FIRST appearance gets the "NEW CRUSHER" pill, a return gets a "CRUSHER" pill. `CRUSH_PLAN` in the scene = this table.

| Jar | Chapter (n) | Crusher | Family | First? |
|---|---|---|---|---|
| 1 | the Sun (0-5) | HYDRAULIC PRESS | top | yes (no pill: the hook) |
| 2 | -> Jupiter (5-8) | HYDRAULIC PRESS | top | |
| 3 | -> Earth (8-13) | SIDE VISE | side | NEW |
| 4 | -> the Moon (13-17) | BLAST (fuse bomb) | radial | NEW |
| 5 | -> Ceres (17-20) | DROP WEIGHT (10 tons) | top | NEW |
| 6 | -> Mimas (20-23) | METEOR STRIKE | radial | NEW |
| 7 | -> Phobos (23-31, the long one) | BOTTOM RAM (was the steel roller) | bottom | NEW |
| 8 | -> a comet (31-35) | WRECKING BALL | swing | NEW |
| 9 | -> Bennu (35-41) | SIDE VISE | side | |
| 10 | -> Dimorphos (41-44) | METEOR STRIKE | radial | |
| 11 | -> a hot-air balloon (44-50) | PILE DRIVER | top | NEW |
| 12 | -> a boulder (50-56) | WRECKING BALL | swing | |
| 13 | -> a bowling ball (56-62) | BLAST | radial | |
| 14 | -> an orange (62-65) | DROP WEIGHT | top | |
| 15 | -> marble / pea (65-71) | BOTTOM RAM | bottom | |
| 16 | -> a grain of sand (71-79) | SOUND WAVES (ultrasound probe) | radial | NEW |
| 17 | -> a dust speck (79-85) | PILE DRIVER | top | |
| 18 | -> a human cell (85-89) | LASER PULSE | radial | NEW |
| 19 | -> a bacterium (89-96) | SIDE VISE | side | |
| 20 | -> a virus (96-102) | SOUND WAVES | radial | |
| 21 | -> a ribosome (102-106) | BOTTOM RAM | bottom | |
| 22 | -> DNA width (106-113) | LASER PULSE | radial | |
| 23 | -> AN ATOM (113-121, finale) | HYDRAULIC PRESS returns (the last chord) | top | |
- Theme: industrial tools -> space impacts (meteor at Mimas and at Dimorphos) -> demolition (wrecking ball at the comet and the boulder) -> the micro/nano tools (sound waves, laser) from the sand grain down -> the press for the ATOM.
- Not built (dropped by the cycle decision): boxing glove, impact probe, giant boot, jackhammer, citrus juicer, nutcracker, rolling pin, meat mallet, microscope tip, optical tweezers, ion beam.

### Phase 3a result (2026-11-01): the crusher TEST, waits on the owner
- Command: `NF_SCALE=1.0 python scenes/longform_atom.py --crushers --jars 6 --tend 88.6 --report` (sims ~3.5 min; `LFA_EARLY=1` reuses jars 1-2 from `output/longform_atom_early_cr_s1.pkl`: 2.4 min), then `... --cache --render --review` (render 7.6 min at ~12 fps). `--tend` cuts the build at that second while keeping the FULL video's music form (`fit_form(23)`).
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\longform\longform_atom_crushers_test.mp4` (88.60 s). The full FHD and the old test are untouched.
- Content (clip s = the real opening of the new cut): 0-15 PRESS jar 1 (contact 0.47, pops 1.18 ...), 18-27 PRESS jar 2, pour; **SIDE VISE** jar 3 in the column (contacts 33.05 / 37.73 / 42.38 / 46.98 / 52.22, first pops 0.62 s later; overload by the vise at 54.8, drop 55.7); **BLAST** jar 4 (bomb lands 58.67 / 63.78 / 68.87 / 73.88, BOOM 59.27 / 64.38 / 69.45 / 74.47, ring 0.8 s; no overload, drop 77.6); **DROP WEIGHT** jar 5 in the column (contacts 80.75 / 85.68, pops 81.32 / 86.23). Every stroke made contact on plan (no MIN_STRUG delays).
- Checks on the encoded file: h264 yuv420p 1920x1080 60 fps, 5,316 frames, aac 88.597 s; **-14.01 LUFS**, peak -5.6 dBFS; flash_check **PASS** (13 flashes, worst 1 s = 2 at 27.32 s = the jar-2 break, as in the full video; the blast adds none); blackdetect **none**. Encoded frames read at every crusher's contact and pop (0.47, 1.20, 18.10, 18.72, 33.07, 33.70, 37.75, 38.37, 58.69, 59.29, 59.50, 59.75, 80.60, 80.77, 81.34, 86.25 s).
- Old path checked: `--cache --still --frame 200s` from `longform_atom_build_j23_s1.pkl` matches the delivered full video's frame (mean diff 2.4/255 = encode).
- Learned:
  - A crusher that lifts far off the pile lets it spring up ~350 px (the squeezed pile keeps overlap): the press's 150 px lift is also a LID. The drop weight lifts only LIFT too.
  - DROP WEIGHT in whole jar 2 (built, works): the pile tops out at 290 (press 335, MAX 330) and its pour left jar 3 shallow (jar 3's floor in view, "1/13 OF ALL" vs 1/3.9) at the first column strokes. So jar 2 stays the press (the brief allows the opening jars) and the weight moved to jar 5 (column, wall to wall).
  - A narrow weight (300 px) lets the pile heap around it and overflow the jar: it must span the jar / stage.
  - Side tools in the column: the box walls are 45 px off-stage, so the jaws touch off-screen and are only seen once they squeeze in (to 110 px inside the stage at 320 px/s); the pile bulges up between them (honest: squeezed sideways, it goes up).
- Weak spots (told the owner): the vise's contact itself is off-screen (seen from the squeeze on); the drop weight in the column falls only ~330 px and its "NEW CRUSHER" pill overlaps "10 TONS" for ~1 s; the column pile top is slanted (pre-existing), so the weight meets the high side first; smoke puffs read as grey discs.
- Projection, full re-render with crushers: sims ~25-30 min (as before) + FHD render ~32.8k frames at ~11 fps ~50 min = **~1.3 h FHD** (4K ~3-4 h), once the remaining tools are built (each new tool ~30-60 min to build + a stills pass).

### Phase 3b (2026-11-01): 6 more tools, owner fixes, test 2 (waits on the owner)
- Owner on test 1: "make the bomb dive into the balls and explode when it is in the middle; those side wall presses would be better with top and bottom locked walls so the balls have nowhere to go".
  - **BLAST** now lands, then DIVES `BM_DIVE` 320 px into the pile during its fuse (a disc pushing balls aside; drawn behind the balls, so the balls in front hide it), and explodes there; the ring runs out from the middle.
  - **SIDE VISE** is now a closed box: a steel LID (`VL_WAIT` 300 px above the top, down at 2,200 px/s) locks onto the pile (clank + latches, gold when locked), the column's floor is the bottom wall, and the full-height jaws close inside it. The balls cannot bulge up: they squash sideways and pop. The jaws now visibly arrive: they plough in from the stage edges and grip 25 px inside the stage (`VZ_IN`).
- New tools (all column-ready; `CR_BUILT`):
  - **METEOR STRIKE** (radial, instant): a rock with a flame trail streaks in from the upper left between contact and pop; impact fireball + ring + "IMPACT!"; kick x1.25.
  - **STEEL ROLLER** (sweep): a drum on a yoke comes down at the left and rolls across the top; a ball pops when the drum passes over its x, delayed by its depth (u = 0.65 x + 0.35 depth). It rides ON the pile (no push).
  - **WRECKING BALL** (swing): a ball on a chain swings in from the upper left (pendulum, 0.42 s), hits where it first touches, digs in 0.02 rad, pops in hop order from the hit, swings back (no collision on the way back).
  - **PILE DRIVER** (top): the drop-weight physics with a hazard-striped ram on a piston rod and two quick re-hits (bang, bang) before the big one.
  - **SOUND WAVES** (radial, ultrasound probe): a probe comes down onto the pile, hums and pings (cyan arcs), then three cyan wavefronts; kick x0.25.
  - **LASER PULSE** (radial, instant): a beam heats a spot (growing glow, rising tone), then a red-orange heat ring; kick x0.45.
- Nits fixed: the drop weight waits 600 px above the pile (a long visible free fall); its pill moved under it (y 800 for top tools); smoke puffs are soft shaded gradients; returning tools get a "CRUSHER" pill, first appearances "NEW CRUSHER".
- Learned (physics, for the next tools):
  - A tool that pushes balls UP or sideways fast (a ploughing roller, a wrecking ball swinging back through the pile, a down-only push that teleports balls) flings them into the air. The column's box is cut from the robust (1 %) pile top, so >1 % airborne balls cut the box short and the column empties (kept 111 / 5,433). Measure `kept` in the rebase lines after every new tool.
  - A wave that pops a whole vertical strip at once (all depths) geysers the column; pop order must run DOWN from the tool (hops, a ring, or the roller's depth term).
  - The roller only contacts if its ride height (`RL_SINK`) is inside the contact test.
- Debug plans: `LFA_PLAN=press,press,<tool>,...` puts tools in early jars to verify them; its caches are tagged (`_build_cr_<tag>_`, `deep_cr_<tag>_`) so they never overwrite the real plan's.
- **Test 2** `review\longform\longform_atom_crushers_test2.mp4` (80.0 s) = clip 30-110 s of a DEMO-order build (`LFA_PLAN=press,press,vise,blast,roller,meteor,press`; the real plan has the drop weight at jar 5 and the meteor at 6): `--crushers --jars 7 --tend 111 --cache --label crtest2 --window 30,110 --review` (`--window a,b` renders frames a..b, slices the audio, fades 0.25 / 1.2 s).
  - Test-2 seconds: boxed VISE lid locks ~2.8, contacts 3.10 / 7.75 / 12.40 / 17.00 / 22.23 (pops +0.6), drop 25.7; diving BLAST lands 28.67 / 33.78 / 38.87 / 43.88, BOOM 29.27 / 34.38 / 39.45 / 44.47; STEEL ROLLER contacts 50.93 / 55.88 / 60.80, rolls 51.55-52.55 / 56.53-57.47 / 61.45-62.35; METEOR streaks from 67.25 / 72.05 / 76.82, impacts 67.78 / 72.58 / 77.35.
  - Checks (encoded): h264 yuv420p 1920x1080 60 fps, 4,800 frames, aac 80.0 s; -14.01 LUFS, peak -5.8 dBFS; flash_check PASS (7, worst 1 s = 2); blackdetect none. Encoded frames read at every tool's contact and pop.

- Verified by stills (contact + pop) in a second debug build (`LFA_PLAN=press,press,wrecking,piledriver,ultrasonic,laser,press --jars 7 --tend 109`): every stroke on plan (contacts 33.07 ... 106.82). Not in test 2: WRECKING BALL, PILE DRIVER, SOUND WAVES, LASER PULSE.
- Weak spots:
  - WRECKING BALL thins the column: after its 5 strokes the box keeps 841 balls (vise ~2,100), so the next jar starts as a thin wedge (fewest in view 487). The fix to try: give it the vise's lid, or cap its push per substep.
  - STEEL ROLLER's first contact is ~0.2 s late (its pops slip off the beat by 0.24 s on stroke 1).
  - The column's pile top is slanted in several chapters (pre-existing), so tools land on the high side.
- Found: `_rng_pts` seeded skin details with `hash(str)`, which changes per process (PYTHONHASHSEED). The old full video's crater layouts can therefore differ between runs and between 30 s chunks rendered by different processes (pre-existing). Crusher builds now use `zlib.crc32` (stable); the old path is left as it was.

### Phase 3c (2026-11-01): the wrecking ball's thin column, fixed (+ the roller on the beat)
- Measured, not guessed (pile-top percentiles per frame): after a wrecking stroke the 1 % top was AIRBORNE (-108 px vs the 5 % top at 137; the vise's 90 vs 150). The column's box (rebase) and the camera both used the 1 % top, so the box was cut 760 px under flying balls (kept 841) and the camera looked into empty sky (9-108 balls in view). A one-sided swing also shoved the pile into a heap against the far wall.
- Fixes (crusher builds only; the old path keeps the 1 % top):
  - `Jar.col_top()`: the pile top = the median over 16 stage columns of each column's 3rd-highest ball. It is used for the box cut at every re-base AND for the column camera. (A plain 5 % percentile ran away: it depends on the column's depth, so the box grew deeper every stroke.)
  - The wrecking ball's push is capped at `WB_CAP` 0.8 px per PBD iteration (no flinging), and it swings in from the left and the right on alternate strokes.
  - Roller: it starts `RL_DROP` 380 px above ITS landing point, so its time to contact is exact (first pop 81.32 vs plan 81.31; was 81.55).
- Result (`LFA_PLAN=press,press,wrecking,vise,roller,press --jars 6 --tend 94`): kept per stroke 1,860-2,300 (was 841-1,800; vise ~2,100); fewest balls in view **1,431** (was 9-108; the old full video 1,331); side margin 45 px; floor margin < 10 px only at 33.0-33.8 s, where jar 3's REAL floor is in view (intended, as in the old video), so the column check's "CHECK" there is that case only.
- `review\longform\longform_atom_crushers_wrecking.mp4` (30.0 s = clip 44-74 of that build: wrecking strokes from the right at 3.0 s and the left at 8.2 s, the drop at 11.7, then the boxed vise at 14.7 / 19.8 / 24.9): h264 yuv420p 1920x1080 60 fps, 1,800 frames, aac 30.0 s; -14.01 LUFS, peak -5.7 dBFS; flash_check PASS (2, worst 1 s = 1); blackdetect none; encoded frames read at the contacts and pops.
- Still weak: the slope from jar 3's pour survives the lid-less chapters; the wrecking ball hits the high side first, so from the right it lands near the stage edge (half the ball off-stage).

### Phase 3d (2026-11-01): the slanted pile top, levelled honestly
- Measured: the slope of the pile surface at every stroke contact (a line through the 3rd-highest ball of 16 stage columns; + = rising to the right), real plan, jars 3-8 (`--crushers --jars 9 --tend 158`; script logic in this section's numbers).
- Cause (not the pour): with box WALLS, every lid-less wave grows each column by x1.44 of its own height above the box floor, so any tilt's tangent grew x1.44 per stroke (9 -> 13 -> 18 -> 26 -> 35 deg, as measured), and nothing in the jammed, damped PBD could level it. The press (and now the boxed vise's lid) flattened it each stroke, which is why the old full video never showed it. One-directional tools (roller always left -> right, meteor/laser always off-centre on one side, the wrecking ball from one side) added a steady push.
- Fixes (crusher builds only, no positions touched):
  - The column is PERIODIC in x (`Jar.per`, on at the first re-base): a window into a pile that goes on sideways. Contacts use a periodic KD-tree (boxsize) and minimum-image pair vectors; a ball leaving one side re-enters the other (with its Verlet history); the seam is 45 px off-stage. The mean slope of a periodic surface is zero, so a tilt relaxes across the seam instead of growing.
  - Off-centre and directional tools alternate sides each stroke: the roller rolls back the other way, meteor/laser impacts mirror, the wrecking ball already alternates.
- Mean |slope| per jar, before -> after (deg; max in brackets): jar 3 vise 0.3 -> 0.0; jar 4 blast 4.6 (8.4) -> 1.6 (2.3); jar 5 drop weight 11.0 (17.3) -> 3.0 (7.2); jar 6 meteor 19.9 (26.9) -> 4.8 (5.8); jar 7 roller 38.6 (44.7) -> 6.6 (11.4); jar 8 wrecking 41.7 (42.5) -> 4.2 (4.3). Kept per re-base 1,990-2,220; fewest balls in view 1,526; column check OK (floor margin 17 px).
- `review\longform\longform_atom_crushers_level.mp4` (30 s = clip 127-157 of that real-plan build: the roller alternating directions, the drop, the wrecking ball from the right then the left).

### Phase 3e (2026-11-01): the BOTTOM RAM replaces the steel roller (owner: "it goes over the balls and it's not natural to crush every ball till the bottom")
- The full render was paused (own process only); chunks 0-60 s were kept (jars 1-6 unchanged, so they stay valid) and the render resumed with the new plan.
- BOTTOM RAM (jars 7, 15, 21; the roller code stays, unused): the boxed vise's lid comes down and LOCKS on the pile, then the column's floor IS a hydraulic ram plate (hazard-striped edge, piston, opaque housing below) driven UP into the locked pile (`RAM_SQ` 120 px/s, at most `RAM_MAX` 70 px, stops when the pile pushes back). The pops run in hop order FROM THE FLOOR UP (the force goes through every ball). Sound: lid clank, a deep thump + clank on the bite, creak + hiss + servo while it strains, a hiss on release.
- The floor sits ~800 px under the pile top, so in ram chapters the camera frames lower: target = max(top + 160, min(floor - 470, top + 480)) (the plate near the view's bottom, the pile top and the lid never lost). Between strokes the zoom ramp briefly pushes the plate out of view. The column check's floor margin is negative in ram chapters by design (the plate is drawn there).
- Other surface tools checked for the roller's problem (a whole column popping at once): meteor, laser, sound waves and blast pop on a ring from their point (the blast's from deep inside), the wrecking ball in hop order from its hit, the weight/pile driver/press/vise from their faces: all travel through the pile from the contact. Only the roller (0.65 x + 0.35 depth) had it.
- `review\longform\longform_atom_crushers_ram.mp4` (30 s = clip 56-86 of `LFA_PLAN=press,press,vise,ram,wrecking,press`): ram contacts 2.67 / 7.77 / 12.85 / 17.87 (pops +0.6), drop ~21.6, the wrecking ball at 24.75. h264 yuv420p 1920x1080 60 fps, 1,800 frames; -14.01 LUFS, peak -6.0 dBFS; flash_check PASS (3, worst 1 s = 2); blackdetect none.

### Phase 3f (2026-11-01): the FULL crusher video, Full HD, waits on the owner
- `review\longform\longform_atom_crushers_full_fhd.mp4` (9:07.300) + `longform_atom_crushers_UPLOAD_notes.md` (chapters, crusher arrivals, description/title ideas; UPLOAD.md untouched). `longform_atom_full_fhd.mp4` (press-only) untouched.
- Commands: `NF_SCALE=1.0 LFA_EARLY=1 python scenes/longform_atom.py --crushers --report` (build ~40 min; `output/longform_atom_build_cr_j23_s1.pkl`, frames `deep_cr_j23_*`), then `... --crushers --cache --label full_cr --render --review --review-name longform_atom_crushers_full_fhd.mp4` (resumable 30 s chunks in `output/longform_atom_chunks_cr/`; ~4 min each at ~9-10 fps; the test-1 chunks were moved to `output/longform_atom_chunks_cr_test1/`). The render was paused for the roller -> ram swap and resumed at 60 s (chunks 0-60 s kept: jars 1-6 unchanged; seam continuous).
- Checks (encoded): h264 yuv420p 1920x1080 60 fps, 32,838 frames; aac 547.285 s (A/V 15 ms); PTS all 1/60 s; -14.01 LUFS, peak -4.1 dBFS; flash_check PASS (79, worst 1 s = 2 at 27.3 s); blackdetect none; ATOM payoff 540.30 s = the coda's last chord (+4 dB). Column: kept ~2,000-2,200 per re-base, fewest balls in view 1,472; the check's floor margin is negative only in the ram chapters (the plate is drawn there).
- Chapters unchanged from the press-only cut except "5:24 Smaller Than a Marble, Then a Pea" (was orange + marble); shortest 10.3 s.

### 4K crusher cut (2026-11-02, owner approved the FHD): staged for upload
- `NF_SCALE=2.0 python scenes/longform_atom.py --crushers --cache --label crushers_4k --render` (2 ffmpeg threads, BLAS threads 1): 158 min at 3.7-5 fps, parallel to a 4-Short 4K job. Chunks now go to `output/longform_atom_chunks_cr_x2/` (the chunk dir is scale-tagged when NF_SCALE != 1; before, a 4K run would have silently reused the FHD chunks).
- -> `MochiAndBolt\schedule\2026-11-02\4_LONG_atom_crushers.mp4` (5.0 GB): h264 yuv420p 3840x2160 60 fps, 32,838 frames, 547.300 s; aac 547.285 s (both start 0); PTS all 256/15360; -14.0 LUFS, sample peak -4.1 / true peak -2.7 dBFS (= the FHD); events + audio wav byte-identical to the FHD's; flash_check PASS (worst 1 s = 2); blackdetect none; frames at 5 / 270.5 / 541 / 59.35 s match the FHD (mean diff 0.9-4.7/255).

## FULL video (2026-10-31, BRIEF_batch63 + BRIEF_longform1 Phase 2 updated for v4)
- Command: `NF_SCALE=1.0 LFA_EARLY=1 python scenes/longform_atom.py --report` (build + column check; pickles `output/longform_atom_build_j23_s1.pkl`, frames spilled to `output/longform_atom_frames/`, ~2.3 GB), then `NF_SCALE=1.0 python scenes/longform_atom.py --cache --render` (30 s chunks in `output/longform_atom_chunks/`, resumable; joined; audio; mux). `--review` moves it to `review\longform\longform_atom_full_fhd.mp4`. `--plan` prints the jar timeline; `--still --frame 12.5s,...`; `--piece a,b`.
- `LFA_EARLY=1` reuses jars 1-2 from `output/longform_atom_early_s1.pkl` (delete it after any physics change).

### The pour fix (owner on v4: "balls don't look like free fall: they land in mid-air on something, then drop")
- Measured, not guessed (`pour_test`: per-ball vertical acceleration while >6 r above its final rest, in the world and through the camera).
- Causes, all in the pour code:
  1. **Contact damping on the ABSOLUTE velocity** (x0.93 per substep, 6 substeps): any ball touching another fell at a terminal ~120 px/s. Pour 2's median fall speed was ~400 px/s after 2 s (free fall: 6,000). That was the "lands in mid-air". Now (pour mode) damping acts on the velocity relative to the touching neighbours/floor.
  2. **A terminal speed** `V_POUR` 1,500 px/s (x0.8 when touching): replaced by adaptive substeps (fastest ball <= 2/3 r per step, up to 40) with contacts found every step: no tunnelling, no cap.
  3. **Air drag 0.999 per substep**: with 24-40 substeps it was a parachute (accel fell to 0.3 g). No drag in a pour.
  4. **The camera pulled back DURING the fall** (anchor far above): balls first rose on screen, then fell at a varying rate. Now the pull-back runs during the overload and ends exactly at the break (`pour_view`: a still view holding both jars), the fall is seen by a still camera, and the camera eases into the new jar after the landing (c2 -> c3).
  5. **The overloaded pile sprang apart at the hand-off** (`relax()` unconfined: mean overlap 0.39 r in jar 1, 0.61 r in jar 2): balls sprayed up past the plate and out through the glass. Now the relax is confined by the old walls + plate, and the pile **free-falls as one block** (a packed pile in free fall has no internal forces) until it meets the new floor; the splash and settle are simulated. Inelastic landings cancel only the RELATIVE approach velocity (cancelling the absolute one made an un-overlapping cluster hover).
- Result (world and screen): every airborne ball accelerates at exactly g (screen 2,124 / 2,411 px/s^2 = g x the held zoom) until it lands; 0 % decelerating in flight.

### The format past jar 3: one ever-deeper zoom (the "column")
- Jar 3 (n 8->13, Z 2.52 = calibrated 2.10 x 3^(1/6) for its 5 splits) takes pour 2; the camera dives into its pile, and from the first stroke on ONE column inside the pile is simulated in **screen-scale frames**: before every stroke the camera zooms x3^(1/3) about the pile top, and at that instant the state is re-based (p' = (960,540) + (p - pc) x z) and cut to the box the camera can see (+4 r; side walls 45 px outside the stage, floor below the view). The new balls are always R_TGT 6.5 px on screen; positions stay small, so 113 strokes and a 10^17 zoom have no precision problem.
- The 3rd-zoomed-stroke empty view (v4 draft) came from the old window's "rising virtual floor": gone. The hidden pile below only translates the whole column, which the camera follows, so the column frame has no rising floor. `check_window` now measures every frame (floor/side margins) and every 6th frame's balls in view.
- **Every later jar is one chapter** (20 drops): it ends on its crossing ("SMALLER THAN ..." holds until the floor gives), "JAR n IS FULL!", the press overloads, the front glass cracks (at true scale it spans the view) and shatters, and the floor gives: the whole column FREE-FALLS 1,500 px as one block into the next jar's pile (Z = 3^(k/6), exact: full -> the next jar's start level), stops dead on landing (off-screen below the view) with a camera thud. The old press lifts away; the next one waits just above the view.
- Jar 3's own floor stays real (and drawn) while its shallow pile is in view.
- Ladder with fillers (n = first split smaller): Sun 0, Jupiter 7, Earth 13, Moon 17, Ceres 20, Mimas 23, Phobos 31, a comet (5 km) 35, Bennu 41, Dimorphos 44, a hot-air balloon 50, a boulder 56, bowling ball 62, orange 65, marble 69, pea 71, sand 79, dust 85, human cell 89, bacterium 96, virus 102, ribosome 106, DNA width 113, ATOM 121.
- Real skins for all 24 objects (each with one feature that reads at r 6-10 px: Ceres' bright spot, Mimas' crater, the comet's jet, Bennu's ridge, balloon gores, bowling holes, the orange's leaf, the marble's swirl, the cell's nucleus, the virus' spikes, the DNA helix, the atom's orbits).
- Background: log-polar stars (with drop parallax) down to the boulder; then a clean lab look (cool gradient + a powers-of-ten graticule that grows with the zoom and slides with the drops), faded over 2.2 s after the boulder crossing.
- The press plate stays at TRUE scale: 40 px of the jar x the frame scale (a slab with a hot face; clamped at 6,000 px for cairo's fixed point).
- Finale: the last wave crosses the ATOM; the payoff is the coda's last chord; "SMALLER THAN AN ATOM!" rises and the card shows all 58 digits of 3^121.

### Music: Grieg, Mountain King, our long form
- The form (`set_form`): intro, the quiet block once (Grieg's own build, as v4), the tutti block twice, the high stretto block as often as needed, then the coda, laid so its last chord (score beat 348) lands on the ATOM payoff (`fit_form` iterates; 8-beat granularity).
- Tempo 84 bpm + 0.16 bpm/s (84 -> ~170 at the end). Orchestration grows per block: + contrabass, + brass, + cymbals on phrase heads, timpani every 2 beats, + flute/trombones, + bass drum, + tremolo strings and choir, timpani roll into the last chord.
- Stroke spacing has a floor falling from 4.6 s (0:35) to 3.3 s (8:40) (`gap_min`): it keeps escalating.


### Delivered (2026-10-31/11-01) and checked on the ENCODED file
- `review\longform\longform_atom_full_fhd.mp4`: **9:07.30** (32,838 frames), h264 yuv420p 1920x1080 60 fps, aac 547.285 s, 1.94 GB. Render: 18 chunks of 1,800 frames (~3 min each at 8-11 fps; the coordinator resumed it after the owner's pause, seam at frame 23,400).
- Loudness on the mux **-14.01 LUFS**, peak -3.5 dBFS; 30 s windows climb -16.5 -> -13.1 (the build). A/V diff **15 ms**. PTS: all 32,837 deltas = 256/15360 (no gaps). flash_check **PASS** (55 flashes, worst 1 s = 2 at 27.3 s; mean lum 0.068). blackdetect (0.05 s, pix_th 0.02): **none**.
- All 18 chunk seams: frame-to-frame diff at the seam within the neighbours' range (e.g. f23400 9.15 vs 8.6 median; f27000 4.74 vs 4.39); seam frames read: continuous.
- Pop sync: 598 pop groups, high-passed energy rise in the 50 ms after each: median +5.8 dB, p10 +2.7. The coda's last chord lands on the ATOM payoff (540.30 s, +4 dB step).
- Column check: side margin 45 px; floor margin >= 0 except 32.6-35.6 s where jar 3's REAL floor is in view (intended, drawn); fewest balls in view 1,331 (213.0 s, a drop).
- Build: sims ~25 min (jars 1-2 cached), max 6,561 simulated balls; frames 2.3 GB on disk.
- Chapters (crossing frame -> floor second, each >= 10 s; marble merged into orange): 0:00 Sun, 0:23 Jupiter, 0:54 Earth, 1:15 Moon, 1:32 Ceres, 1:47 Mimas, 2:26 Phobos, 2:45 comet, 3:13 Bennu, 3:28 Dimorphos, 3:57 balloon, 4:25 boulder, 4:52 bowling ball, 5:06 orange/marble, 5:32 pea, 6:05 sand, 6:30 dust, 6:47 cell, 7:16 bacterium, 7:41 virus, 7:58 ribosome, 8:26 DNA, 8:57 atom.
- UPLOAD.md (14 titles, description + chapters, pinned comment), 18 thumbnails from this build's frames (banner-free copies for composites); A/B trio 01 / 18 / 02.
- **Nits (told the owner):** the last ~5 s after the final chord are near-silent (reverb tail under the count card; an audio-only remux could hold the chord); tiny grey objects look alike (Moon/Ceres/Mimas/comet); the right HUD's longest chapter titles touch the stage edge by ~20 px; the in-zoom drop distance (1,500 px) is a visual choice.

## v4 test (2026-10-30, Phase 1d: "the balls that break the old jar drop into a BIGGER jar, physics-style")
- Command: `NF_SCALE=1.0 python scenes/longform_atom.py --review` (`--jars 3` default; `--cache` reuses the last build's sims from `output/longform_atom_build_j3_s1.pkl` - delete it after any physics change; `--piece a,b` renders clip seconds a..b silent and prints fps; `--plan`, `--calib c --r/--z`, `--still --frame`).
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\longform\longform_atom_test.mp4`.
- **Content (42.1 s):** jar 1 the Sun (5 splits, 1 -> 243), overload + cracks, the jar breaks and ALL 243 balls pour into jar 2 (x1.76 bigger, camera pulls back); jar 2 crushes on (3 splits -> 6,561, re-skins to Jupiter at n 7 with "SMALLER THAN JUPITER!"), breaks, all 6,561 pour into jar 3 (x2.10); the camera zooms INTO jar 3's pile (x4.0, then x5.8) and the press crushes on: 3^9, 3^10 = 59,049. Ends ~5 s after the last wave, pile settled.
- Timeline (clip s): jar 1 pops 1.18 / 4.01 / 6.80 / 9.56 / 12.29, payoff 14.32, break 14.99, pour landed +1.35 s. Jar 2 pops 17.66 / 20.30 / 22.91, payoff 24.86, break 25.50, pour landed +3.41 s. Jar 3: zoom-in from ~29.2, pops 31.24 (x4.0) / 35.61 (x5.8), last pop 37.15, end 42.08.
- **Fills (calibrated):** `R0_1` 161 (top at payoff 323, MAX 330); jar 2 `Z` 1.76 (top 329, chaotic: 1.74 -> 331, 1.78 -> 345); jar 3 `Z` 2.10 (analytic from jar 2's packing; the pour leaves a CONE, so the centre column is taller than the average).
- **The ball budget (the 1.5 h / 6 GB stall, fixed):**
  - Cause: the old window cull was keyed to the stroke index and skipped once the press had already started down, so jar 3 grew 6,561 -> 19,683 -> 59k -> 177k simulated balls (all stored per frame).
  - Now `SIM_CAP` 8,000. Window jars cut a BOX (`Jar.cull_box`) before every stroke, keyed by frame, once no split is pending: the column the camera will see at that stroke's zoom + 4 r + margin; balls below the view become a **virtual floor** (`fy`).
  - The hidden pile stays honest: after each wave the virtual floor rises by (3^(1/3) - 1) x the hidden share of the jar's AVERAGE height (`h_avg0`, measured over 14 bins at the first cut, so the pour's cone is not inflated), over the time until the next cut; the plate lifts ahead of it.
  - Window jars run physics x1/zoom (`Jar.kz`: gravity, speed caps, press speeds, tolerances), so motion ON SCREEN matches jar 1.
  - `check_window()` runs every build: side margin 45 px, floor margin 3 px (screen) -> the box never shows. Max simulated at once: **6,561**.
- **Physics fixes found on the way:**
  - Coincident balls (a wall corner clipping two to the same point) never separated (normal = 0/0): they now split along a hashed direction. This was the "mush" in dense jars.
  - Small balls (r < 25 px) boiled with the press_split2 tolerances: `solver_scale()` doubles the substeps (2 -> 4) and runs 12 iterations, CORR_V/damping thresholds scale with r.
  - The pour: contacts are recomputed every substep (6), terminal speed `V_POUR` 1,500 px/s (no tunnelling). The ram no longer pushes the pile (it rides at g, drawn only): pushing it squeezed balls out sideways and up at ~2,000 px/s. The overloaded pile is relaxed (positions only, 200 iterations) at the hand-off. The side glass goes 0.04 s after the floor.
  - The press of the next jar waits for its pour: `build()` probes each pour alone (press parked), measures the landing (90th-percentile speed < 150 px/s), then plans the strokes around it (`LAND`).
- **Checks** (encoded file in the review folder):
  - Video: h264 yuv420p 1920x1080, 60 fps, 42.08 s (2,525 frames), 88.7 MB; audio aac 42.07 s.
  - Loudness on the muxed mp4: **-14.0 LUFS**, true peak -4.2 dBFS. RMS per 5 s: -14.1, -13.9, -12.9, -13.3, -13.2, -13.8, -14.1, -15.3, then the end fade.
  - Onsets: 44 pop groups, high-passed energy rise in the 50 ms after each: median +10.5 dB; one group (32.5 s, jar 3's first window wave, 0.1 s after the previous group) only +0.7 dB.
  - flash_check: **PASS**, 7 flashes in 42 s, worst 1 s = 1 (15.15 s, the first break); mean luminance 0.073.
  - blackdetect (0.05 s, pix_th 0.02): **no black segments.**
  - Stills read pre-encode through both breaks/pours (14.2-17.2, 24.5-31.5 s) and every window stroke; encoded frames read at 0.5, 4.1, 13.0, 15.2, 16.0, 22.95, 25.8, 26.0, 28.5, 29.4, 30.5, 31.3/31.4, 35.7, 36.0, 38.6, 39.4, 40.5, 41.95 s, plus a 1:1 crop of a window wave (draft, 39.45 s).
- **Known issues / owner decisions before the full build:**
  - The 3rd window stroke (x8.4) is NOT in the test: in the draft its release crushed the column against the rising virtual floor and the view showed an empty frame for ~0.4 s (41.2 s of the draft). The fix is the plate-lift / floor-rise ordering; it must be solved before the full video (every later jar is a window jar).
  - Pour 2 (6,561 small balls) bursts into a loose cloud and lands as a cone after 3.4 s: reads as an explosion more than a cascade.
  - At zoom the press plate is drawn at true scale (40 px x zoom = 160-490 px thick): honest but heavy in the frame.
  - **The format past the first window jar is undecided:** a windowed pile cannot be poured whole into a bigger jar on screen. Options: (a) one ever-deepening window from jar 3 on (chapters = object crossings + a "JAR FULL -> the floor gives, the column drops into the next jar" in-window), (b) shrink-pour: the window pulls back as the next jar is revealed, drawn as a texture.
- **Perf (this laptop, another builder running):** sims: jar 1 1.2 s, jar 2 ~25 s (pour probe 1.4 s), jar 3 pour probe ~15 s + 2 window strokes ~60 s; the whole build 3.5-7.5 min. Render: 11.2 fps average at Full HD (27 fps on jar 1, 5.6 fps on the densest window frames; small balls are blitted from a sprite cache). The 42 s test: build + render + audio ~8 min.
- **Projection for the full video** (121 splits, ~2.7 s/stroke in whole jars, ~3.7-4.4 s/stroke in window jars, ~6 s per pour): **~8:00-8:30** at this pacing (Phase 2 target 8:35). Sims ~1-1.5 h (≈30 s per window stroke at <=8k balls); Full HD render ~30k frames at ~8-11 fps ≈ 50-65 min; 4K ~3-4 h. Total Full HD ~2-2.5 h.

## Music (v4): Grieg, "In the Hall of the Mountain King" (replaces Boléro)
- Why: the owner's first choice; famous, PD everywhere (1875, Grieg d. 1907), and its built-in accelerando matches the escalation. Shorts used it before (acceptable for the long video).
- Source: Mutopia #1888, Grieg's own piano arrangement (University Society 1918 edition, Public Domain), MIDI at `<SOUNDFONTS_DIR>\scores\grieg_mountain_king\`.
- Our orchestration (lib/orchestra): horns F# pedal intro, low-string pizzicato pulse throughout, bassoon theme (A1), + clarinet an octave up (A2), clarinet/oboe on F# (B), cellos+bassoon+horns+timpani (A'), tutti from beat 100 (full video).
- Tempo: 84 bpm at t=0 + 0.36 bpm/s (the piece's own stringendo stretched over the video); the theme's first note lands on the first pop. Strokes on the beat, each wave's pops on the score's note onsets, each pop group plinks the melody note it lands on. Burst: cymbal swell + boom; landing: timpani.

## The rule (honest numbers, v3)
- A hydraulic press crushes, and every crushed ball splits into 3 balls with equal total volume: radius ×3^(-1/3) = ×0.6934 per split.
- Start: **the Sun**, 1,392,700 km. d_n = 1,392,700 km × 3^(-n/3).
- Atom (~0.1 nm) at **n = 121**: d121 = 0.079 nm. 3^121 ≈ 5.39 × 10^57 balls (58 digits).
- **The balls ARE the objects.** A ball wears the skin of the smallest object on the ladder that it is not yet smaller than, so it **re-skins at the pop** that takes it under the next one (the last wave of jar 1 is born as gas giants).
- The ladder (`OBJECTS`; n = first split smaller than it):
  - Sun 0 · Jupiter (gas giant) 7 · Earth 13 · Moon 17 · Ceres (dwarf planet) 20 · asteroid Bennu (490 m) 41 · boulder (2 m) 56 · bowling ball 62 · orange 65 · marble 69 · pea 71 · grain of sand 79 · dust speck (50 µm) 85 · human cell (10 µm) 89 · bacterium 96 · virus 102 · atom 121.

## The format (v3, 2026-10-29)
- **One jar per chapter** (`build_jars()`): one per object stretch. A stretch longer than 7 splits is cut into even jars; one shorter than 3 is merged into the next one (the pea is passed inside a jar). 22 jars, 3^3 to 3^7 = 2,187 balls each.
- **Fill:** the start ball is sized so the jar's k splits fill it to MAX honestly (`R_FILL` from `--calib`): jar 1 (k=7) R0 108 px, top at payoff 337; jar 2 (k=6) R0 133, top 327. Other jars use `r_guess` (packing 0.82; it reads ~10 % small for k ≥ 6) until calibrated.
- **Physics, press, struggle, squash-pop: v2 unchanged** (press_split2 PBD, fast approach at 1,900 px/s, a struggle with area-preserving squash + stress glow + shudder + PRESSURE gauge, then the elastic pop).
- **Pacing:**
  - Stroke spacing is `bps` beats: jar 1: 4 (3.16 s), jars 2-8: 3.5, then 3. It is a floor: waves of 243+ pops push it to ~3.2 s anyway (7 snare strokes per wave).
  - First pop at 1.18 s; frame 0: the plate is already coming down onto the Sun.
- **The burst (replaces v2's hatch + chute):**
  - **Payoff:** on the first beat ≥ 0.45 s after the last pop. Banner "SMALLER THAN JUPITER!" (or "JAR FULL!" when no object is passed), MAX turns gold FULL, a rolled C-major chord, and a gold reticle on the hero ball (upper-middle of the pile).
  - **Overload:** the plate has lifted and the pile has relaxed to MAX. At payoff + 0.08 s it comes down once more and holds (no ball can split). The gauge climbs into red, the plate shudders, and cracks race over the glass from the plate (the cracks are the edges of the shard mesh).
  - **Burst at TS** (first half-beat ≥ payoff + 0.55 s): the glass breaks into ~126 triangle shards. The jar walls are the shards' neon edges and fly with them. The pile blows outward and falls, and the old press flies up and fades.
  - **The dive:** from TS + 0.06 s the camera zooms ×Z (Z = R0(next) / r(final): **×16.0 and ×11.5** in the test) over 2.0 s, a log-zoom with smoothstep, anchored on the hero ball. A tiny new jar + press assembles around the hero (fades in at 30-75 % of the dive), and at the end the new jar fills the frame at identity: no cut, no black frame.
  - The hero is blown up 90 px (new frame) during the dive, then drops into the new jar (g = 3,000 px/s²) with two bounces and a landing squash. The new press waits out of frame, then slams: that is the next chapter's first stroke.
  - Payoff → next first pop ≈ 5 s.
- **Size perception (the owner's v2 complaint):**
  - **Giant backdrop:** each jar's START object stays behind the next jar as a ghost at TRUE scale. The Sun (r 1,726 px) looms behind the Jupiter jar, and Jupiter (r 1,525 px) behind the Earth jar.
  - It is placed so its limb crosses y = 430: a curved horizon across the whole frame. It is drawn opaque over the stars, then the object at 36 % (the Sun at 64 % + a corona).
  - It IS jar k's start ball, scaled by the dive: at the burst it fades in at its original size around the hero, then balloons into the horizon. It is labelled "THE SUN, TO SCALE" (it fades 2.6 s after the landing), and the HUD keeps "BEHIND: THE SUN, TO SCALE".
  - **Powers-of-ten scale bar** (bottom centre): a round 1/2/5 × 10^n length whose bar grows through the dive and snaps (1,000,000 km → 500,000 → 200,000 → 100,000 km).
  - **Log-polar starfield:** any zoom factor slides it outward, so the dive feels like a dive and the chapters stay still. Space chapters only (later chapters: owner decision).
- **HUD:**
  - Left: the rule, SPLITS n, BALLS (+2·3^n0 per pop), "= 3ⁿ".
  - Right: CHAPTER n, FROM → TO, "1 BALL =" size in km / m / cm / mm / µm / nm, the true-scale comparison (1 ball vs the target object, both skinned), a status line ("STILL BIGGER THAN…", "SMALLER THAN…!", "THE JAR BURSTS! ZOOM ×16.0"), and "BEHIND: …".
- **Skins (lib-free, in the scene):**
  - Sun: limb-darkened gradient, granulation, spots, a corona when big.
  - Jupiter: 11 bands, turbulence lines, the Great Red Spot, sphere shading.
  - Earth: 6 continent variants, clouds, polar caps, shading, atmosphere rim.
  - Moon: maria, craters.
  - Every skin has an LOD by on-screen radius (a flat fill under 3 px). The rest of the ladder is a placeholder coloured ball (`paint_generic`); it must be drawn before the full render.
- **Characters:** as v2 per stroke. At the payoff Mochi cheers and Bolt worries through the overload; both wow at the burst; Mochi laughs and Bolt wows at the landing.

### Why the burst + dive, not the continuous powers-of-ten zoom (owner's option a, with b's scale bar)
- The press needs a jar at a FIXED scale for a whole chapter. A continuous zoom would either shrink the press out of frame or keep the balls the same size on screen, which is exactly the v2 complaint.
- The burst is a strong per-chapter payoff (cracks → shatter), and it hands over to a fast dive that reads as "we are going much smaller".
- The size comparison is direct and honest: the previous object, at true scale, stays visible behind the new jar for the whole chapter (the Sun is ~16× the Jupiter-sized start ball, Jupiter ~11× the Earth-sized one). A HUD ghost can't show that.
- From (b) we kept the persistent scale bar and the zooming starfield.

## Music v3 (superseded by Grieg in v4): Ravel, Boléro (our performance)
- **Copyright check (2026-10-29):**
  - Ravel died on 28 Dec 1937. Boléro was composed in 1928 (premiere 22 Nov 1928, Paris Opéra) and first published by Durand, Paris, in **1929** with the copyright notice.
  - **United States: public domain since 2025-01-01** (95 years from 1929 publication). Duke's Center for the Study of the Public Domain lists Boléro in its 2025 Public Domain Day class.
  - **France: public domain since 1 May 2016** (life + 70 + the French wartime extensions). EU: life + 70. It is also PD in Canada, Japan, China, New Zealand and others.
  - **Open item (flagged, not blocking):**
    - Ravel's and Benois's heirs claimed the set designer Alexandre Benois was a co-author, which would put the BALLET under copyright until 2039.
    - SACEM rejected it. The Tribunal judiciaire de Nanterre rejected it on **28 June 2024**: Ravel is the sole author, and the work "remains in the public domain".
    - The heirs filed an appeal in late Nov 2024. No appellate ruling was found as of 2026-10-29.
    - It concerns France/EU and the ballet only. US status (1929 publication) does not depend on it.
  - Our audio is our own synthesis, with no recording used. YouTube Content ID can still false-match a well-known melody; the dispute basis is "public-domain composition, own performance".
- **Note source:** the CC0 engraving by Éditions Nicolas Sceaux (2016, LilyPond; Wikimedia Commons "Bolero-ravel-nicolas-sceaux-cc0-domaine-public.pdf", CC0). It was read as page images and transcribed by hand into `THEME_A` (flute, bars 5-21), the snare ostinato and the pizzicato (score bars 1-22).
- **Arrangement (lib/orchestra, FluidSynth + MuseScore_General, MIT):**
  - Orchestra-kit snare, key 38: the 2-bar ostinato, accents on the beats, vel 0.30→0.40.
  - Pizzicato cellos (C3 + G2/G3) and violas (G3 + G4; from bar 21 C3-G3 / G3-G4 / C3).
  - Flute solo theme A from bar 5, clarinet theme A from bar 23. **76 bpm** (the printed mark; Ravel corrected it to 66 by hand).
- **Balance:**
  - The real pp opening sat 11 dB under the flute (-33 vs -22 dB RMS), so the snare (×2.2) and pizz (×1.7/×1.1) are lifted.
  - Bed per 5 s: -26, -25.5, -21.8 … -22 dB RMS (the opening is audible, and it builds when the flute enters).
- **SFX on top (all from sim events):**
  - Per pop: a squash (size-scaled), plus one C-major chord-tone plink (C5 E5 G5 C6 E6 G6 C7, walking up through the wave): the "one note per crush".
  - Per big pop (r > 40): a low thunk + a soft elastic balloon-pop (v1's glass crack is gone with the cracks).
  - Press: a short air whoosh on the fast approach; thunk + clank on contact; through the struggle a stick-slip CREAK (resonant ticks speeding up), a rising hydraulic hiss and a servo strain sweeping up; hiss on release.
  - Payoff: a rolled C-E-G-C-E plink chord. Transfer: hatch latch + clank, a chute rumble, the hatch latch shutting, rubber bounces + thunk + a C6 plink on the landing, and a soft sine riser under the camera move.
  - Master -14 LUFS via `kit.deliver(bed=...)`; the last 1.4 s fade (end of the test).

## Full video: chapter plan and estimated times (v3 pacing, `--plan`)

| Jar | From → to | Splits n | Balls in jar | Objects passed | Starts at | Bursts at |
|---|---|---|---|---|---|---|
| 1 | the Sun → Jupiter | 0→7 | 2,187 | Jupiter | 0:00 | 0:23.7 |
| 2 | Jupiter → Earth | 7→13 | 729 | Earth | 0:23.7 | 0:44.2 |
| 3 | Earth → the Moon | 13→17 | 81 | the Moon | 0:44.2 | 1:00.0 |
| 4 | the Moon → Ceres | 17→20 | 27 | Ceres | 1:00.0 | 1:11.8 |
| 5 | Ceres → (Bennu) | 20→27 | 2,187 | - | 1:11.8 | 1:35.5 |
| 6 | Ceres → (Bennu) | 27→34 | 2,187 | - | 1:35.5 | 1:59.2 |
| 7 | Ceres → Bennu | 34→41 | 2,187 | asteroid Bennu | 1:59.2 | 2:22.9 |
| 8 | Bennu → (boulder) | 41→46 | 243 | - | 2:22.9 | 2:41.8 |
| 9 | Bennu → (boulder) | 46→51 | 243 | - | 2:41.8 | 2:58.4 |
| 10 | Bennu → boulder | 51→56 | 243 | a boulder | 2:58.4 | 3:15.0 |
| 11 | boulder → bowling ball | 56→62 | 729 | a bowling ball | 3:15.0 | 3:33.9 |
| 12 | bowling ball → orange | 62→65 | 27 | an orange | 3:33.9 | 3:45.8 |
| 13 | orange → marble | 65→69 | 81 | a marble | 3:45.8 | 4:00.0 |
| 14 | marble → pea | 69→74 | 243 | a pea (at n 71) | 4:00.0 | 4:16.6 |
| 15 | pea → grain of sand | 74→79 | 243 | a grain of sand | 4:16.6 | 4:33.2 |
| 16 | sand → dust speck | 79→85 | 729 | a dust speck | 4:33.2 | 4:52.1 |
| 17 | dust speck → human cell | 85→89 | 81 | a human cell | 4:52.1 | 5:06.3 |
| 18 | human cell → bacterium | 89→96 | 2,187 | a bacterium | 5:06.3 | 5:27.6 |
| 19 | bacterium → virus | 96→102 | 729 | a virus | 5:27.6 | 5:46.6 |
| 20 | virus → (atom) | 102→109 | 2,187 | - | 5:46.6 | 6:07.9 |
| 21 | virus → (atom) | 109→115 | 729 | - | 6:07.9 | 6:26.8 |
| 22 | virus → ATOM (finale) | 115→121 | 729 | AN ATOM | 6:26.8 | (finale) |

- **Projected full length at the test's pace: ~6:57** (the ATOM payoff ~6:45, then ~12 s of finale). That is under 8:00, so no mid-rolls.
  - Same ladder at 4 beats/stroke throughout: ~7:50. At 4.5: ~8:35. At 5 (v2's opening pace): ~9:10. `bps` is per jar in `_chapter()`.
- **Gaps with no new object** (a "JAR FULL!" payoff, and the re-skin waits):
  - Ceres → Bennu (21 splits, 3 jars), Bennu → boulder (15, 3 jars), virus → atom (19, 3 jars).
  - Each still has its burst, dive and giant backdrop (the previous jar's start ball, same kind, ~11-16× bigger).
  - Candidates to fill them: a moon like Mimas (396 km, n 23), a comet nucleus (~5-10 km), a stadium-size asteroid, a hot-air balloon (~17 m, n 50), a ribosome (25 nm, n 106), DNA width (2 nm, n 113).
- Jar sims: the 2,187-ball jars take ~5 s each to simulate (the whole video is ~2 min of sims). Rendering cost: see the test numbers below.
- Music: Boléro at 76 bpm is 13:25; a ~7-9 min cut needs the intro + 7-9 theme statements, then a cut to the coda on the ATOM jar. Theme B still needs transcribing from the CC0 score.

## v3 test (2026-10-29, owner on v2: "same size ball… loses the perception of size", use real ball-shaped objects)
- Command: `NF_SCALE=1.0 python scenes/longform_atom.py --review` (`--chapters 2` is the default). `--plan` prints the full table; `--calib c --r a,b` searches a jar's fill.
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\longform\longform_atom_test.mp4`. v2 is archived as `MochiAndBolt\archive\longform_atom_test_v2.mp4`.
- **Content:** jar 1 (the Sun → Jupiter, 7 splits, 2,187 balls), burst 1, jar 2 (Jupiter → Earth, 6 splits, 729), burst 2, then the start of jar 3 (Earth → Moon): the first pop, and the clip ends 1 bar later.
- Timeline (clip time):
  - Jar 1 pops at 1.18 / 4.34 / 7.50 / 10.66 / 13.82 / 16.97 / 20.13 s; payoff 22.89; burst 23.68; dive 23.74-25.74 (×16.0); landing 25.99.
  - Jar 2 pops at 27.63 / 30.39 / 33.16 / 35.92 / 38.68 / 41.84; payoff 43.42; burst 44.21; dive 44.27-46.27 (×11.5); landing 46.50.
  - Jar 3 first pop at 48.16; end 50.53 s.
- **Checks** (encoded file in the review folder):
  - Video: h264 yuv420p 1920x1080, 60 fps, 50.53 s (3,032 frames), 43.5 MB.
  - Loudness on the muxed mp4: **-14.02 LUFS**, peak -4.8 dBFS. RMS per 5 s: -17.5, -22.1, -15.4 … -16.2.
  - Onsets: all 72 pop events show a high-passed energy rise in the 50 ms after the pop (median +7.6 dB, min +4.5).
  - flash_check: **PASS**, 3 flashes in 50 s, worst 1 s = 1 (at the burst, 23.77 s); mean luminance 0.077.
  - blackdetect (0.05 s, pix_th 0.02): **no black segments.**
  - Stills read pre-encode: 0, 1.1 (squash), 10, 20.25 (wave 7), 21.5, 23.1-23.7 (overload + cracks), and every ~0.5 s through both bursts and dives. Also read: 26, 27.5, 33, 42.7-43.7, 48.25, 50.
  - Encoded frames read: 23.2, 23.75, 24.2, 24.8, 25.4, 26.1, 43.9, 44.3, 44.9, 45.6, 46.3, 48.3 s. A 1:1 crop was read at 20.6 s (the plate on the 2,187-ball wave).
- **Cost:**
  - Sims + build ~10 s (each 2,187-ball jar ~5 s).
  - Full HD render + encode ~6 min for 3,032 frames (~8.5 fps, 2 encoder threads).
  - Full video (~7-9 min = 25-33k frames): Full HD ~50-70 min, 4K ~3-4 h.
- **Known nits / to watch:**
  - The wave under the plate still squeezes the top layer into overlapping "pillows" for ~1 s (v2's nit).
  - The calibrated R0 sits 10 % above `r_guess` for k ≥ 6. Every big jar must be `--calib`'d before the full render (the fill is otherwise short of MAX).
  - The ghost label sits mid-jar for ~2.6 s after the landing. The hero falls past it.
  - The skins past the Moon are placeholder coloured balls.
  - The starfield is space-only.

## History: v1/v2 (bowling ball → atom, 59 splits; one jar per real-object chapter, comparison objects beside the jar)
- v2 format: hatch at the jar's foot → chute → ski-jump into a physically smaller press, with a camera follow-zoom. The owner's verdict: size perception lost.


## Phase 1 test, v1 (2026-10-29; superseded)
- Command: `NF_SCALE=1.0 python scenes/longform_atom.py --review` (`--chapters 2` is the default).
- Writes `output/longform_atom_test_16x9.mp4` and moves it to `<VIDEOS_DIR>\MochiAndBolt\review\longform\longform_atom_test.mp4`.
- Timeline (clip time; bar = 2.368 s):
  - Frame 0: the plate is already on the bowling ball, squashing, with cracks growing.
  - Ch1 pops: 1.58 s (1→3), 13.42 s (→9), 25.26 s (→27, a 9-pop wave). Payoff 30.8 s, zoom 33.2-37.9 s (×3.45).
  - Ch2 pops: 40.26 s (→81 total), 49.74 s (→243). Payoff 52.1 s, zoom 54.5-59.2 s (×1.77).
  - Ch3 (golf → marble) starts. Its press comes down, and the clip ends 1 bar after its first pop (64.0 s; 3,837 frames).
- Args: `--chapters` (2), `--seed` (1), `--label` (test), `--still --frame a,b`, `--report`, `--plan`, `--calib c --r a,b`, `--reuse` (audio-only over an existing silent render), `--review` (move to the review folder).
- **Checks** (encoded file in the review folder):
  - Video: h264 yuv420p 1920x1080, 60 fps, 63.95 s (3,837 frames), 11.6 MB.
  - Loudness on the muxed mp4: **-14.02 LUFS**, peak -4.1 dBFS.
  - RMS per 5 s: -19.8, -19.3, -15.6, -16.6, -16.5, -15.9, -15.9, -16.3, -17.4, -16.9, -16.2, -15.6, -20.0 (end fade). The first 0.5 s is -19.8 dB (snare and pizz from frame 0).
  - Every pop onset lands on its event: high-passed energy rises 7-25 dB in the 50 ms after each pop.
  - flash_check: **0 flashes, PASS** (mean luminance 0.039).
  - ffmpeg blackdetect (0.05 s, pix_th 0.02): **no black segments.**
  - Encoded frames read at 0, 1.0, 1.6, 1.75, 13.5, 26.0, 30.9, 32.5, 33.6, 34.6, 35.5, 36.4, 37.3, 37.85, 38.6, 40.3, 52.2, 54.9, 55.9, 56.8, 57.7, 58.6, 59.15, 61.65 and 63.9 s. That covers both zooms at u ≈ 0.1/0.3/0.5/0.7/0.9, plus 1:1 crops of the 9-pop wave (26.6 s) and mid-zoom (35.5 s).
- **Cost:**
  - Sim + build 4.4 s; drawing ~40 fps at Full HD (≤ 27 balls). The whole test took a few minutes at 2 encoder threads.
- **Projection for the full video (~8:40 = 31,300 frames):**
  - Sims ~15 min: the 6,561-ball ATOM jar is press_split scale, ~6-8 min; the 2,187-ball jars ~3 min each.
  - Full HD ~1-1.5 h: ~26k light frames at ~20 fps, plus ~5k frames with 1-6.5k balls at ~3-5 fps.
  - 4K (`NF_SCALE` 2.0) ~3-4 h at 2 threads.
- **Known nits:**
  - Zoom 2 is only ×1.77. The honest jar fill makes zoom depth Z = R0(next) / r(final), which varies from ×1.8 to ×4 early and is much deeper late.
  - A freshly split child can overlap a neighbour for a few frames (PBD settle), the same as press_split.
  - The 2-split chapters (ch2, ch5, ch7) fill the jar with 9 big balls, which looks chunky.

## Phase 1b test, v2 (2026-10-29, superseded by v3; owner: "slow indeed", cracks "do not look good", no camera dive)
- Command: `NF_SCALE=1.0 python scenes/longform_atom.py --review` (`--chapters 5` is the default). `--remux` re-renders only the audio onto the review file (video stream copied, trimmed to the video length, no `-shortest`).
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\longform\longform_atom_test.mp4`. v1 is archived as `MochiAndBolt\archive\longform_atom_test_v1.mp4`.
- **Content:** 5 chapters (bowling ball → orange → golf ball → marble → peppercorn → grain of rice), 5 transfers, then the start of ch6. Ch6's first pop is at 60.4 s and the clip ends 1 bar later.
- Timeline (clip time):
  - Ch1 pops at 1.18 / 5.13 / 9.08 s; payoff 11.05; hatch 11.85; landing 13.60.
  - Ch2 pops at 15.39 / 19.34; payoff 20.53; hatch 21.33.
  - Ch3 pops at 25.27 / 28.82 / 32.37; payoff 33.95.
  - Ch4 pops at 38.28 / 41.85 / 45.40; payoff 47.37.
  - Ch5 pops at 51.72 / 54.87; payoff 56.05.
  - Ch6 first pop at 60.4.
  - Transfer zooms: ×3.78, ×1.65, ×3.00, ×3.79, ×1.34.
- **Checks** (encoded file in the review folder):
  - Video: h264 yuv420p 1920x1080, 60 fps, 62.77 s (3,766 frames), 17.7 MB.
  - Loudness on the muxed mp4: **-14.0 LUFS**, peak -4.7 dBFS. RMS per 5 s: -18.9, -17.8, -16.0 … -16.2, then the end fade. The first 0.5 s is -15.6 dB.
  - Onsets: all 42 pop events show a high-passed energy rise in the 50 ms after the pop (median +6.7 dB, min +2.9). The struggle creak/hiss now cuts out 70 ms before each pop, so the pop is clean. Before that cut the min was +1.1 dB.
  - flash_check: **0 flashes, PASS** (mean luminance 0.044).
  - blackdetect (0.05 s, pix_th 0.02): **no black segments.**
  - Stills read at 0, 0.33, 0.75, 1.1, 1.18-1.33 (the pop), 9.3-9.8 (the 9-ball wave), 11.7 (FULL + reticle), 12.15-14.6 (transfer 1, every ~0.25 s), 14.1-15.9 (ch2's head lowering, slamming, struggle, pop), 21.7-23.0 (transfer 2), 32.3, 57.3-61.7 (transfer 5 + ch6).
  - Encoded 1:1 crops were read at 1.0 s (squash), 1.25 s (pop), 13.3 s (ball dropping into the ×1/3.8 press) and 13.62 s (landing squash).
  - `--tcheck`: the travelling ball stays at screen x 950-1240 (the stage is 552-1368).
- **Cost:** sims + build ~10 s. Full HD render + encode ~6 min for 3,766 frames (~11 fps with the squash/glow paths, 2 encoder threads).
- **Projection for the full video at v2 pacing (~3:45 = 13.5k frames):**
  - Sims ~12-15 min (the 6,561-ball jar dominates).
  - Full HD ~35-50 min (the ch9/13/14 jars with 2-6.5k balls draw at ~3-5 fps).
  - 4K ~2-3 h at 2 threads.
- **Known nits / to watch:**
  - The first frames after a pop: the 3 children overlap and stretch (the elastic spring + PBD separating them). On the 9-ball waves, the loaded balls overlap as squashed "pillows".
  - In the ×1.3-1.7 transfers, the new press's lifted head is partly cut off by the stage window while the camera follows the ball.
  - The transfer planner is checked for every chapter (`--plan` builds all 13 plans and warns on any without clearance). Only ch1-5 are seen rendered.

