# robot_proof: Bolt vs a REAL robot arm at balancing a pole (batch73, comment reply)

- Brief: docs/BRIEF_batch73.md §4. New file `scenes/robot_proof.py` (the brief asked for a new scene, not an episode flag, so the comment-video skill's "next episode" rule was overridden by the brief).
- Comment: @Youipi8 "WHY AM I TALKING TO A NON-SENSIENT ROBOT" (exact text). A drawn card (792 px, inside x 0.10-0.84w) with no like count or date, because those aren't known. It holds 1.2 s, then shrinks aside and fades by 1.75 s; the caption comes in after. The real screenshot (assets/comments/Youipi8.png) can replace it.
- Physics: a uniform pole on a moving pivot, θ'' = (3g/2L) sin θ − (3/2L) a cos θ, dt 1/600, seeded.
  - Robot: LQR (Q diag 50/1/8/1, R 0.05), 10 ms sensor latency, 0.05° noise, |a| ≤ 60.
  - Bolt (pole on his head): τ = 0.2 s, 0.3° noise (AR 0.97), |a| ≤ 25, a stage of ±0.35 m. His gains per length come from a grid search (`--search`). Below 3gτ²/4 no gains exist.
- Limit (Stépán 2009, Phil. Trans. R. Soc. A 367:1195): L_crit = 3gτ²/4 = 29.4 cm (τ = 0.2 s); 0.74 mm for the robot.
- Ladder: 160/100/64/40/25/16 cm (λτ 0.61 … 1.92; stabilisable only below √2).
- Result:
  - The robot holds all 6, max tilt 2.0° (its start tilt), max excursion 7 cm.
  - Bolt holds 160, 100 and 64 cm; at 64 cm he reaches his stage edge with a 21° tilt and recovers.
  - He drops 40 cm (1.28 s): the pole is above L_crit, but holding it needs more than his 0.70 m of room. He drops 25 cm (0.84 s) and 16 cm (0.76 s), both below the limit.
  - Final score: 6/6 vs 3/6.
- After a pole slips past 80°: ballistic flight of its centre and spin, landing on the floor.
- Ending (no gag): "ROBOT 6/6 · BOLT 3/6", a gold stamp "VERDICT: NOT A ROBOT" plus the 29 cm line; Bolt grins. The wall ruler fades out and a dark panel sits behind the verdict (coordinator fix).
- Audio: Sousa, El Capitan (Mutopia MIDI, PD), the top line on clarinet + pizz at 0.29 s/beat; a wood tick when each pole is placed, a double wood clack when a dropped pole lands; a C-major chord + timpani + slam at the verdict.
- Font gotcha: Segoe UI bold in cairo has no ✓ glyph (it renders a box). Draw the mark instead.
- Checks (b73B, Full HD): 984 f = 16.40 s; −14.0 LUFS, TP −5.2; flash PASS; frames read 0, 1, 5.5, 8.1, 8.44, 10.3, 14.6 s (1:1 crops of the card, Bolt's 40 cm drop and landing, the verdict).
- Delivered review/batch73/robot_proof.mp4. Owner review: pending.
