# domino_spiral

- Rule: Mochi pushes one domino; 200 candy dominoes on a tightening spiral (2.5D boxes, 52 deg camera, kinematic topple about the front-bottom edge). Last one rings Bolt's bell -> confetti, both hop.
- Escalation: path pitch 66 -> 27 px, topple gap 0.25 s -> 0.066 s (CHAIN_S=27 s, DT_RATIO=0.27). per-5.7s falls [19, 29, 36, 48, 68].
- Rest lean angle = acos(w/pitch) (exact for a chain of equal boxes); hit angle = asin(gap/h).
- Sound: fur_elise note + soft pok per fall; bell = 84/88/91/96 chime + pop; ratchet on the rewind.
- Loop: reverse wave stand-up over 1.5 s; caption/counter alpha 0 at frame 0 and last frame.
- s1: 31.9 s, -14.0 LUFS, flash_check 0 flashes.
- Owner review 2026-10-03: Least favourite, but may work.
