# stack_bounce — Drop it HIGHER or STACK more balls: who hits the CEILING first? (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 3). New scene file; caption/render/sound chain copied from helmet_drop; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\stack_bounce.mp4` (**v1**, Full HD 9:16, output label v1).
- Caption (baked; `--nocap` = base): "Drop it ~HIGHER~ or ~STACK~ more balls:" / "who hits the ^CEILING^ first?".

## Story (clip times)
- A 3.0 m workshop room (wood wall, pegboards, a hanging lamp); dashed gold "CEILING 3.0 m" line = the MAX line; ruler 0-3 m. Mochi drops ONE super-ball from a magnet arm on a post; Bolt drops a stack on a guide rod from a clamp collar, always from 0.4 m, one ball more each round.
- Heights are the ball's BOTTOM above the floor everywhere (drops, apex marks, HUD), so "can't beat its drop height" reads true.
- R1 floor hits at 0.12 s (frame 0: both balls mid-fall): apex 0.81 vs 0.32 m, "MOCHI LEADS: 0.81 m vs 0.32 m".
- 2.12 s reset (magnet / collar lift, "+1 BALL" slides down the rod), R2 hits at 4.12 s: 1.62 vs 1.45 m, "MOCHI BY 17 cm"; launch tag "LAUNCH ×1.70".
- 6.37 s reset ("MAX 2.75 m" for Mochi, +1 BALL for Bolt), R3 hits at 9.12 s: Bolt's top ball leaves at 8.0 m/s ("LAUNCH ×2.85", ENERGY bars: 95 % in the top ball) and BONKs the ceiling at 9.51 s (lamp swings), ricochets onto Bolt's head (squash, stars, deadpan). Mochi's apex 2.23 m.
- 10.12 s cadence: "BOLT WINS" + "3 stacked balls: the top one would rise ×8.1 its drop" + "1 ball can't beat its drop height", ghost line "no ceiling: 3.75 m". Dissolve into the frame-0 state.

## The physics (scenes/stack_bounce.py `run_stack()`)
- 1D on the rod, dt 20 µs, impulse collisions with restitution e = 0.9 (floor, ball-ball, ceiling), gravity, drag ignored. Stack held with 5 mm gaps → the textbook chain of separate collisions.
- Sizes drawn true to the ruler (300 px/m): Mochi's ball 20 cm; Bolt's stack 29 / 20 / 13 cm, masses 9 : 3 : 1 (each 3× lighter).
- Results: Mochi 1.0 / 2.0 / 2.75 m → apex 0.81 / 1.62 / 2.23 m (e² = 81 %). Bolt 0.4 m: 1 ball 0.32 m; 2 balls launch ×1.70 (4.77 m/s) from 0.29 m → 1.45 m; 3 balls launch ×2.85 (7.98 m/s) from 0.50 m → free apex 3.75 m (rise ×8.1) → ceiling at 3.0 m (top 0.13 m ball, bonk at 4.2 m/s).
- Why Bolt drops from 0.4 m (brief: 0.5 m): with true ball sizes the launch heights count; from 0.5 m Bolt's 2-ball round would already beat Mochi's 2 m drop. 0.4 m keeps the brief's honest story (Mochi leads R1 and R2, the 3-stack wins R3).
- The ricochet sideways onto Bolt is scripted (a ceiling bounce scatters a little); the launch, apexes and bonk are the sim's.

## Sound
- **Piece:** G. Bizet, L'Arlésienne Suite No. 1, Prélude (1872; d. 1875, PD): its opening "Marche des Rois" theme (the march the brief's Suite No. 2 Farandole is built on), beats 0-30 at quarter = 180, so its own C cadence lands on "BOLT WINS"; floor hits on beats 0 / 12 / 27. Source: `<SOUNDFONTS_DIR>\scores\bizet_arlesienne_prelude\biz_arls.mid` (midiworld, note source only; SOURCE.txt). The Farandole had no PD MIDI/score reachable (flutetunes' is non-commercial).
- Arrangement: strings + violins + horns + cello on the theme, C pedal octave bass, timpani on the floor hits, C major tutti cadence.
- SFX: one soft tuned rubber-ball note per bounce / ball-ball hit (pitch locked to the theme's harmony, ≥12 ms after notes), latch clacks, lift ticks on the eighth grid, a hollow BONK on the ceiling and on Bolt's head, a short chime.

## Checks (v1 encoded, Full HD)
- h264 High yuv420p 1080x1920 @ 60 fps, 838 frames = 13.97 s. Muxed -14.00 LUFS, peak -2.16 dBFS, last 0.5 s -240 dBFS (silent).
- RMS/s: -18.4 -17.4 -17.3 -17.2 -16.6 -16.5 -16.2 -15.6 -16.1 -15.6 -13.1 (cadence) -19.6 -30.0 -40.7. SFX events/s: 4 4 12 6 8 3 10 12 6 18 10 14 17 0 (lift ticks fill the resets).
- flash_check PASS (0, mean lum 0.03). Seam mean |delta| 0.50 (good band).
- Side safe zone: rigs x 230-750, characters x 116-910 (Bolt's edge 0.843w), text inside 0.10-0.84w; the ricochet ball rolls out to ~0.92w after the bonk (decoration).
- Frames read from the mp4: 0.05, 0.6, 4.75, 8.9, 9.25, 9.55, 10.2, 11.0, 13.9; stills at 0, 0.67, 2.83, 4.67, 9.25, 9.33, 9.58, 10.0, 11.67, 12.0.

## Args
- `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## v2 (2026-11-01, owner review: "real life thing… basketball stuck at top and they try to hit it")
- `--v2`: open ceiling joists (22 cm gaps, one centred over each lane) with a basketball (24 cm) wedged in each gap; geometry puts its underside at **2.83 m**. The sim's top-ball collision now happens at the basketball's underside (TARGET) instead of the 3.0 m ceiling (same e = 0.9 rebound). Mochi's R3 drop 2.75 -> **2.55 m** so her held ball clears her basketball (apex 2.07 m, top 2.27 m: "57 cm SHORT" banner). Bolt R3: launch ×2.85 (7.98 m/s), hits the basketball at 9.47 s at **4.54 m/s** (free apex would be 3.75 m).
- Scripted (not simulated): the wedge itself and the knock-loose. The basketball then falls ballistically (start +1.1 m/s up, -0.35 m/s left, clears rod, stack and lamp), bounces e 0.78 on concrete with a low thump per bounce. The small ball's ricochet onto Bolt's head is kept. Lamp moved 610 -> 560 px (clear of the falling ball).
- Caption line 2 "who knocks their stuck ^BASKETBALL^ down?"; gold dashed line = "STUCK BALLS 2.83 m" (fades at the hit); HUD "BALL DOWN!" / "R3 HIT!".
- Weak: the falling basketball crosses the ENERGY bars for ~0.4 s.
- Deliverable `...\MochiAndBolt\review\fixes_1101\stack_bounce_v2.mp4`. 13.97 s, -13.97 LUFS, peak -2.04, silent tail, flash 0, seam 0.54. v1 -> archive/stack_bounce_v1.mp4.
- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-09` (events json byte-identical to v2fix). Full HD v2 -> archive/stack_bounce_v2.mp4.
