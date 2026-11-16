# pilot_parking — Bolt tries to parallel park: how many ATTEMPTS will it take? (pilots, 2026-10-28)

- Brief: docs/BRIEF_pilots.md (pilot 3). New scene file; lib/ and tools/ untouched. Characters (lib/toon), caption/banners and the sound/mastering chain copied from snowball_fort.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\pilots\pilot_parking.mp4` (**v1**, Full HD 9:16, 16.28 s, 977 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Bolt tries to ~PARALLEL PARK~:" / "how many ~ATTEMPTS~ will it take?"
- **Story (top-down street at night):** Bolt's mint car shuffles in and out of a generous gap, one attempt per bar: BONK the car behind (its hazards blink) ×8, THE BIN (knocked over, rubbish out), KERB ×2, CONE (falls over). ATTEMPT #2 → #13, 12 bumps. Attempt #14: "ONE MORE GO..." he pulls all the way out alongside the front car... and Mochi's tiny coral car nips up the lane and slides into the gap in one smooth S, stopping on the cadence: "1st TRY." HUD: ATTEMPT #14 vs MOCHI 1st TRY. Bolt's stare from his car, Mochi's smug grin.

## v2 (batch55, 2026-10-28): real parallel-parking geometry
- Owner on v1: "let's add physics. Bolt tries front-first, guessing; Mochi pulls a little forward, checks the mirrors, measures the angle and parks perfectly". Brief: docs/BRIEF_batch55.md.
- Deliverable: `MochiAndBolt\review\pilots\pilot_parking.mp4` (v2, Full HD, 16.28 s, 977 frames, label v2). v1 → `MochiAndBolt\archive\pilot_parking_v1.mp4`; v1 script kept at scratch `m55/pilot_parking_v1.py`.
- **Caption changed:** "Front-first or ~REVERSE~ in:" / "who fits the ~6.7 m~ space?" (v1's "how many ATTEMPTS will it take?" no longer has an honest answer: he gives up).
- **Same size for every car** (4.5 × 2.2 m; v1 gave Mochi a tiny car): the method wins, not the car. **The space: 6.7 m = 1.49 car lengths** (340 px), measured on the pavement from frame 0 ("SPACE 6.7 m" + a dimension line). Bicycle model: wheelbase 0.6 L, full lock 0.62 rad → minimum turning radius 3.78 m (HUD: "TURNS NO TIGHTER THAN 3.8 m").
- **Why front-first can't work (checked, not asserted):** a grid of 3,600 front-first S entries (start x/y, turn-in steer, counter-steer) finds NO pose inside the space without contact; the best leaves the rear 1.43 m out. Even a 9.1 m space fails (best 0.66 m out). Scratch scripts `m55/pk_ff.py`, `m55/pk_geom.py`.
- **Bolt (seed 220, search over 300 seeds):** attempts #3 → #11, one per bar, frame 0 is mid-move (`T_LEAD` 0.15 s). Each: turn in at a guessed steer (0.30–0.62 rad), counter-steer when his nose reaches a guessed x (kerb −80 … +45 px), stop at first contact, a red dimension "REAR OUT 1.2–2.8 m" from the parking line to his outermost corner, then he backs out along the exact same path (the bicycle model retraces) and creeps to a new start. Bumps: KERB ×2, car in front ×3, car behind ×3, THE BIN ×1 (it slides and falls over). His nose's arc is drawn dotted. At 7.56 s "FINE. YOU DO IT.": a forward S at full lock into the outer lane, where he waits and watches.
- **Mochi, the textbook (collision-checked vs both cars, the kerb and Bolt):** (1) pulls up alongside the front car, 0.6 m off it (stop 9.43 s); (2) MIRROR CHECK: a gold sight line from her right mirror to its rear bumper corner; (3) reverse at FULL LOCK to 45° (live angle readout + arc; turns mint at 45°); (4) straighten (0.77 m straight); (5) counter-steer at full lock to 0°; (6) pull forward to the middle: **1.1 m | 1.1 m**, stopping ON the cadence (13.29 s). Her rear-axle path (the two arcs + the straight) is drawn as a dotted coral guide with dots at the switch points; HUD: STEP n/6 + the step name + NEXT; at the end "1st TRY · GAPS 1.1 m | 1.1 m" with dimension lines in the gaps.
- Honest geometry note: her 45°-arc-straight-arc ends 1.9 m behind the front car; that is why the space is 6.7 m and the final gaps are 1.1 m, not the "12 cm" the owner used as an example (a two-arc park at a 3.8 m turning radius cannot end tighter than ~0.2 m behind and needs ~1.3 L).
- Sound: v1's music (Liszt) and waves; Bolt's sensor on the 16th grid while he noses in and backs out (denser near obstacles, a slow 8-sixteenth tier when far), gear clicks, the bumps as v1; his wheel-to-lock ticks on the exit; Mochi's arrival ticks, a click per step, steering ticks, a soft ding at the mirror and at 45°, her sensor quickening as she backs in, the cadence chime. SFX events/s: 11 11 12 15 9 12 12 8 6 8 3 8 10 4.
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 977 frames = 16.28 s; −14.01 LUFS, peak −1.99 dBFS, last 0.5 s digital silence; flash PASS (0, mean lum 0.07); seam last→first 1.18 vs ~1.0 between neighbouring frames at the start (he is moving on frame 0). Frames read: 0, 0.33, 4.9, 8.3, 8.6, 9.6, 10.9, 12.2, 13.6 (+ stills).
- **v2 doubts:** the event rate dips at 10 s (3/s: her slow first arc, the music carries it); Mochi's front swings out to ~0.3 m from Bolt's waiting car at 45° (correct physics, verified no contact); the parked cars and Bolt are mostly "bumps into car" (6 of 9).

## v3 (batch56, 2026-10-28): the honk-queue ending
- Owner on v2: "good, but at the end Bolt is in the middle of the road; nobody would let you stand there." Chose option 1: cars queue behind him and honk, he sheepishly backs away / waves sorry. v2 script kept at scratch `m56/pilot_parking_v2.py`.
- Deliverable: `MochiAndBolt\review\pilots\pilot_parking.mp4` (v3, Full HD, 16.88 s, 1013 frames, label v3). v2 → `MochiAndBolt\archive\pilot_parking_v2.mp4`.
- Unchanged: Bolt's 9 front-first tries, the give-up, Mochi's 6-step park and the cadence (13.29 s), caption, music.
- **What changed:**
  - **The queue:** two same-size cars (yellow C, silver D) roll up the lane behind his waiting car (x 462, overlapping his width so they can't pass; 4 px clear of Mochi's lane), cruising 8.3 m/s and braking at 3.2 m/s² to rest 0.7 m apart (C at 12.10 s, D at 12.75 s, while she counter-steers/centres). Collision-checked every frame against Mochi, Bolt and each other: no contact.
  - **After the cadence:** C HONK! (double, 13.59), D HOOONK! (long, 14.01), C again (14.41): headlights flash + gold sound arcs + a label beside each car. Bolt's face: wow → worried, looking back, sweat; at 14.24 a sheepish grin, "SORRY!" over his bonnet and a waving hand out of his window (1.25 s).
  - **The exit:** he can't back away (they block the back), so he hurries off forward (8 m/s², from 14.74) and leaves under the caption; C (15.04) and D (15.29) follow. Then the 0.6 s dissolve to frame 0.
  - HOLD 2.4 → 3.0 s (16.28 → 16.88 s).
  - "1st TRY." moved from (470, 1000) up to (520, 425) because the queue now stands there; Bolt drives under it for ~0.5 s on his way out.
- **Sound:** honks = two chord tones a third apart (C: F#4 + A#4, D: A#3 + C#4) with soft odd harmonics capped at the 5th and a 12 ms swell: friendly, in the held F-sharp chord, ~1.5 dB over the bed; brake ticks as each car stops, two falling ticks for SORRY, gear clicks as each pulls away. SFX events/s: 11 11 12 15 9 12 12 8 6 8 3 8 12 6 6 2 0.
- **v3 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 1013 frames = 16.88 s; −13.98 LUFS, peak −1.98 dBFS, last 0.5 s digital silence; flash PASS (0, mean lum 0.074); seam 1.19 (v2 1.18). Frames read from the mp4: 10.3, 13.62, 14.05, 14.45, 15.5, 16.25 (+ stills 11.0, 12.9, 13.62, 14.4, 15.2, 16.0). Side safe zone: queue, labels, wave hand all inside x 0.10–0.84w (screen 142–545).
- **v3 doubts:** the honks are pitched to the chord, so they blend more than a real horn (raised to ~1.5 dB over the bed; check by ear); his 8 m/s² getaway is brisk; D is half behind the HUD while queued; the event rate still tails off after he leaves (2/s in 15–16 s).

## SHIPPED (v3 approved, 2026-10-29)
- 4K render `--label ship` (NF_SCALE 2.0): h264 High yuv420p 2160x3840 @ 60, 1013 frames = 16.88 s; -13.98 LUFS (ebur128 -13.9), peak -1.98 dBFS, last 0.5 s digital silence; flash PASS (0 flashes, mean lum 0.074). Stills read from the 4K mp4 at 0.5, 7.2, 11.0, 13.3, 14.4 (1:1 crop: SORRY!, Mochi, gaps), 15.4 s.
- Staged: `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-05\3_pilot_parking.mp4`, slot 3 = 00:00 local Nov 7 (15:00 US East Nov 6), titles + pinned comment in that UPLOAD.md. Review FHD copy -> `MochiAndBolt\archive\pilot_parking_fhd.mp4`.

## Layout
- Fixed camera ×1.25 about world (716, 766) → screen (640, 800). Kerb x 780; parked cars A (front, blue) centre y 446 and B (behind, mauve) centre y 1086, 228 × 110 px; gap 402 px. Bin (802, 700) and cone (797, 880) at the kerb edge; lamp post, two trees (decoration).
- The drivers are drawn on the car roofs facing us (cartoon convention): Bolt r 40, Mochi r 33.
- HUD (y 1366–1526): BOLT ATTEMPT #n, BUMPS k | PARKED? NO → MOCHI 1st TRY. Key content inside x 0.10–0.84w (trees and the far pavement are decoration).

## The physics
- **Kinematic bicycle model** (rear axle, wheelbase 0.60 L, rear overhang 0.18 L): every arc is the honest path for its steering angle (≤ 0.62 rad). One attempt per bar: forward (beat 1, 30–100 px) then reverse (beat 2, 50–130 px), smoothstep speed.
- **Bolt's steering:** each move he picks the direction that straightens him up only 62 % of the time (otherwise random); magnitude random. Seed **677** chosen by a 5,000-seed search scored on: no accidental success, a bump in every attempt window, every kind of bump, the pavement things late, no gap > 1.5 s, heading |θ| < 0.95.
- **Collisions** stop a move at first contact: a wheel over the kerb (x > 776), the body vs a parked car (separating axes). The body overhang knocks the bin/cone (circle vs quad) without stopping: they get the car's velocity, slide with friction, spin and fall over.
- **Parking sensor:** while reversing, beeps on the 16th grid every 4 / 2 / 1 sixteenths as the nearest obstacle gets within 60 / 25 px.
- **Exit (#14):** pure pursuit (bicycle model) to the lane alongside car A; collision-checked (0 contacts). **Mochi:** straight up the lane then a cubic S into the gap (150 × 94 px car), timed by arc length with a soft brake ending on the cadence (13.29 s); checked against both parked cars and Bolt (0 contacts).

## Sound (music first)
- **Piece:** Franz Liszt, Hungarian Rhapsody No. 2, the friska main theme (1847; Liszt d. 1886, PD). Its back-and-forth B#–C#–B–C# figure = the shuffle. Not on any used list.
- **Source:** the LilyPond excerpt "Main theme from the friska" (8 bars, both hands) in the English Wikipedia article "Hungarian Rhapsody No. 2"; wikitext saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\liszt_rhapsody2\`.
- **Excerpt:** F-sharp major, 2/4, quarter = 140 (bar 0.857 s), the 8 bars twice (the second time tutti), cadence = bar 16 beat 2, the F-sharp chord (= Mochi parked).
- **Arrangement** (lib/orchestra): violins + flute on the theme (8vb of the piano's top line), clarinet 8vb the second time, brass stabs on the accented dotted eighths (second time), oom-pa: contrabass + tuba on 8ths 1/3, pizz chords on 2/4 (V–V–I–I–V7–V7–I–I, from Liszt's left hand); the cadence = timpani + F#-major tutti + harp sweep.
- **SFX** (tonal): parking-sensor beeps (pitched to the chord), gear clicks per move, car-on-car "donk" + 2 hazard bloops, kerb thump + tick, bin/cone "bop" + 3 rattle ticks, the pull-out clicks, Mochi's slow sensor beeps quickening into the stop, the cadence chime.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 977 frames = 16.28 s. −14.01 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −18.6 −18.6 −18.5 −17.9 −17.8 −17.6 −17.5 −16.7 −17.5 −16.9 −16.3 −16.6 −16.8 −13.3 (cadence) −13.4 −19.8.
- SFX events/s: 7 7 8 7 7 7 8 12 5 11 7 2 4 5 0 0.
- Bumps (s): 0.68 1.44 2.36 3.18 4.87 5.71 6.59 7.11 (bin) 7.17 7.27 (kerb) 9.21 (cone) 10.00.
- flash_check PASS (0 flashes, mean lum 0.07). Seam mean |Δ| 0.28 (good band).
- Frames read from the mp4: 0.5, 0.7, 1, 2, 7.15, 7.2 (1:1 crop of the bin + kerb), 9.25, 10.6, 11.6, 12.6, 13.35, 14.5, 15.6.

## Doubts
- 8 of the 12 bumps are the car behind (the honest search rarely reaches car A without spinning); the variety comes from the bin, the kerb and the cone in the second half.
- The twist is a story beat: 11–13 s has few SFX (the music carries it).
- Top-down faces on the roofs are small (r 40 / 33 px) — readable at phone size but not big.
- "Parallel parking" in a 1.76-car-length gap: generous on purpose (the joke is that he still fails).

## Args and cost
- `--seed` (677; `--seed -1` runs the search, `--search N`), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s with a fixed seed (the search ~30 s); Full HD render ~55 s at 2 encoder threads.
- Owner review (batch55): "add physics" → v2 to review.

## Outcome
- (fill after upload)
