# jar_versus2 — CHAINSAW vs BLENDER, real physics (batch69)

- Brief: docs/BRIEF_batch69.md §1 (owner: "chainsaw and virus was an EXAMPLE ... we need PHYSICS"). New file `scenes/jar_versus2.py`, our own engine (numpy + scipy cKDTree; no new dependency).
- Caption: "Every ball a blade touches ~SPLITS~ in 2" / "~CHAINSAW~ or ~BLENDER~: who finishes first?"; "GOAL: 100% small balls".

## The rules (one rule set for both jars)
- Same pile in both jars: 27 big balls (r 36), settled once (seed 1), copied. Jars x 120-480 / 536-896, floor 1290, lid 470 (closed jars).
- A blade touch splits a ball into 2 halves (r/√2: area kept); also a ball hit with a closing normal speed > 900 px/s splits (both balls). Down to the smallest size (4 splits: 1 big = 16 small, r 9). A fresh half can split again after 0.12 s. Meter = % of ball AREA at the smallest size.
- Halves leave with 80 % of the blade's surface speed + 160 px/s apart (the blade throws them).
- Both motors start at 25 % speed and turn up to 100 % over 8 s (the same dial for both).
- CHAINSAW (Mochi): free rigid body (bar of 10 discs + motor discs), mass = 25 big balls, I = M·60²; rigid-body PBD contacts (lever arm in the generalized inverse mass) with balls and walls; chain 1,200 px/s with Coulomb friction (|f| ≤ 0.6 × normal impulse) dragging balls along the bar and kicking the saw back; the engine shakes it (seeded random force ~3,000 px/s² and torque 80 rad/s², re-drawn every 0.06 s, × the dial). Only the bar cuts.
- BLENDER (Bolt): two arms (9 discs each, reach 154 px) on a fixed axle 24 px above the floor, kinematic motor 14 rad/s × the dial.
- Engine: PBD, dt 1/240 (4 substeps/frame), 3 iterations, wall/lid restitution 0.35, a tiny seeded velocity jiggle (σ 4 px/s per substep) so perfect stacks don't freeze.

## Honest result
- The saw leads for the first second; THE BLENDER TAKES THE LEAD at ~1.1 s and finishes at race 7.38 s (100 % SMALL, BOLT WINS); the saw is at 34 % then (52 % by the clip's end).
- % small (saw/blender) per second: 5/7 9/24 15/50 18/70 21/87 26/94 34/100. Splits/s: saw 29 25 24 13 7 55 26 64 45 22; blender 66 95 108 65 40 18 12 1.
- Why: the blender sits where gravity brings every ball and throws the pile around the closed jar; the saw has to burrow and is surrounded by its own small halves. Seeds 2 / 3: blender at 8.0 / 8.2 s, saw 37 / 38 % then. Earlier tuning (no impact rule, weaker motors) had both tools stall at 94-99 % with long tails; the impact rule + the dial fixed that.

## Sound
- Rossini, The Barber of Seville overture (PD; midiworld transcription, as ol_stairs_race v1), score beats 110.5-132 (the Allegro theme) re-timed to the finish, + an E-major tutti on 100 %. A glassy click per split group (deeper for the saw's jar), density-ducked.

## Checks (encoded Full HD, label b69)
- h264 yuv420p 1080x1920 60 fps, 659 frames = 10.98 s. −14.01 LUFS, peak −5.38 dBFS, last 0.5 s −70 dBFS. flash_check pass. Seam 0.50.
- RMS/s −19.5 −20.2 −18.0 −18.5 −18.2 −18.6 −17.5 −14.0 −13.5 −22.3 (re-mixed once with `--reuse`: the first mix's body was −21 under a −11 finale).
- Frames read: 0.0, 0.8, 2.5, 5.0, 7.8, 9.0.

## Doubts
- The event rate climbs only for ~3 s in the blender jar, then falls as it runs out of big balls (the saw's rate rises in its 2nd half). The research rule "rate climbing to the end" is not met; the finish itself is fast.
- Not close: the blender wins by a lot (it reads as "the blender is the right tool").
- The engine-shake force is our model (a running chainsaw vibrates); without it the saw wedges against a wall and stops.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch69\jar_versus2.mp4`. Owner review: pending.
