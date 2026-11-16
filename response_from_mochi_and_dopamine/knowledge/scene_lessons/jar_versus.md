# jar_versus — Mochi's CHAINSAW vs Bolt's ZOMBIE VIRUS (batch68)

- Brief: docs/BRIEF_batch68.md §3 (replaces press_meteor; owner: "it's about the balls; two famous things in jars of balls"). New file `scenes/jar_versus.py`; no lib/ or tools/ changes.
- Caption: "Mochi: ~CHAINSAW~ vs Bolt: ~ZOMBIE VIRUS~" / "who takes the ~WHOLE~ jar first?"; "GOAL: 100% of the jar"; rule lines "cuts every ball it touches" / "every zombie bites what it touches" (persist).

## The rules (computed, not scripted)
- Same pile in both jars: one seeded hex packing (seed 2), 322 balls, r 12-14 px, 708 contacts (4.4 per ball). Jars x 120-480 / 536-896, floor y 1300, pile top y 610.
- CHAINSAW: a vertical blade 110 px long sweeps the jar in passes (left-right-left, top band first), 280 px/s; the last band is clamped to the floor. A ball is cut the first moment the blade segment (4 px half-thickness) touches it (sampled at 600 Hz). Cut balls pop into two halves (fade in 0.75 s) + sawdust. Path-limited.
- ZOMBIE VIRUS: a vial shatters on the top-centre ball at race time 0 = patient zero. Every zombie bites every ball touching it; one bite = TAU 0.40 s × U(0.8, 1.2) per contact (seeded); a ball turns at its earliest bite = Dijkstra over the contact graph.
- Race time 0 = the blade's first touch = the vial landing. Clip = race − 0.35 s.

## Honest result
- The saw leads from 0.03 s (2 vs 1) for 10 seconds: 16/3 % at 1 s, 50/45 % at 5 s, 82/76 % at 8 s, 97/95 % at 10 s.
- **LEAD CHANGE 10.19 s** (313 vs 314 balls). Zombies reach **100 % at 10.57 s** (BOLT WINS); the saw is at 99 % and finishes at 11.03 s.
- The contagion does NOT explode exponentially (the brief's guess): in a still pile a zombie can only bite its neighbours, so the infection spreads as a wave at a near-constant ~33 bites/s after the first second (bites/s 10 27 37 38 33 32 33 33 32 31 15). It wins because the wave advances on the jar's whole width, while the saw loses time at every turn (cuts/s 50 18 35 30 28 36 22 45 20 26 9).
- Sensitivity (disclosed): seeds 1-5 → zombies win every time by 0.06-0.66 s; saw 260 px/s → zombies by 1.3 s; saw 300 px/s → the SAW wins (10.29 vs 10.57 s). The bite time and the saw speed are our rules; the race is close by nature.

## Timeline (clip 14.12 s = 847 frames)
- 0.0: saw descending into Mochi's jar, vial falling into Bolt's. 0.35: both start. ZOMBIES TAKE THE LEAD! 10.54 s; 100% INFECTED! 10.92; BOLT WINS! 11.87; the saw finishes 11.38 (100 % CUT, parked at the floor); dissolve 13.52-14.12. Zombies bounce after the win.

## Sound
- Beethoven, Symphony No. 5, 1st mvt (Mutopia #941, PD; `<SOUNDFONTS_DIR>\scores\beethoven_symphony5_1`), score quarter beats 10-36 (bar 6's motif imitations through the strings, crescendo to bar 19's ff tutti), all 12 parts mapped to lib/orchestra (flute, oboe, clarinet, bassoon, horns, timpani, violins + string doubling, viola, cello, contrabass), one global tempo so beat 36 (the ff landing) = the zombies' 100 %; + boom, swell, choir, brass, crash on it. Used once before (domino_branch, other bars).
- SFX: a glassy click per cut group, a short tonal "chomp" per bite group (≥ 12 ms apart, density-ducked). No buzz (the saw is silent apart from its cuts).

## Checks (encoded Full HD, label b68)
- h264 yuv420p 1080x1920 60 fps, 847 frames = 14.12 s. −14.01 LUFS, peak −6.17 dBFS, last 0.5 s −74.7 dBFS. flash_check 0 flashes.
- RMS/s −21.5 −15.5 −15.1 −16.3 −19.3 −19.0 −18.1 −17.6 −16.8 −16.8 −15.9 −14.5 (finish) −21.0.
- Seam: pre-encode last → first 0.119 vs an interior step 0.120 (perfect loop); encoded 1.236 (codec noise on 644 small balls through the dissolve).
- Frames read: 0, 1.0, 10.56 (lead change: 313 vs 316), 10.95 (100% INFECTED), 12.0, 14.1; Fast stills 0, 60, 300, 628, 665, 760.
- Audio was re-mixed twice on the same video (`--reuse`; video stream byte-identical): the score's soft opening was ~−26 dB in the first 5 s → note velocities lifted (0.78 + 0.22 v), CC11 from 0.88, a C-minor string tremolo + timpani roll under the first 1.5 s.

## Doubts
- Event rate is flat, not climbing: ~30 cuts/s + ~33 bites/s the whole race (both are linear processes in a still pile). The tension is the gap closing (97 vs 95 % at 10 s), not acceleration.
- Seconds 4-6 dip to −19 dB (the score's quieter bars 12-14).
- The rule numbers (saw 280 px/s, bite 0.4 s) are ours; a 7 % faster saw would win (disclosed in the README).
- Halves pass through the remaining pile as they fall (they fade in 0.75 s).

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch68\jar_versus.mp4`. Owner review: pending.
