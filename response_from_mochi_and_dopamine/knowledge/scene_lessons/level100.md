# level100: RIGID metal vs BENDY plastic, LEVEL 1 → 100 of wind (batch73, NEW)

- Brief: docs/BRIEF_batch73.md §3 (the LEVEL 1-100 test Short). New file `scenes/level100.py`. Candidates + pick: review/batch73/README.md. Rule used to pick: at 1.1^99 a fixed-ratio advantage buys ~7 levels, so the smart design needs a different SCALING LAW (reconfiguration: drag ∝ v^(4/3) vs v²).
- Physics: q = ½ρU² +10 %/level; U100 = 200 km/h, so L1 = 1.8 km/h. Panel 0.60 x 0.50 m; Cd 1.17; PC 2 mm (EI 0.8, weight included; 1-1.5 mm sheets buckle/sag under their own weight). Elastica clamped at its foot, normal pressure q·Cd·(U cos θ)², 48 segments, scipy root (hybr) with continuation; N = 96 differs by 0.2 %. Shear pin 100 N (our fixture).
- Result: rigid snaps at L81 (106.3 N; L80 = 96.6 N); bendy at L100 = 84.6 N (85 %), max strain 1.31 %. Rigid at L100 would be 650 N.
- After the snap: a free rigid body (2.43 kg Al plate, penalty contact with the floor + screen, μ 0.45) hits the screen at 8.84 s and ends flat on the floor.
- Timeline: per-level durations 0.072 s (≤ L35) → 0.215 s (L81) + a 0.95 s hold → 0.125 s (L100); finale 2.45 s; 0.5 s dissolve. Frame 0 = level 2.
- Look: perspective tunnels (back wall with a 10 cm grid, a cm ruler, a ceiling lamp, a floor band, a fan + honeycomb, an exit screen), smoke streaks following an envelope (a bump ahead, the surface, a wake decay), wake eddies behind blunt bodies, a translucent curved sheet with depth, a riveted metal slab, pin-load fill bars to the red 100 N line, a level bar 1-100 with BOLT OUT · 81.
- Owner/coordinator polish (stills OK): drawn flutter (1.5 → 9 px, 9-18 Hz travelling wave; the load comes from the static shape), a 3-frame shake + pin pop at the SNAP.
- Audio: Elgar P&C No. 1 trio (Commons MIDI track 3 as note data), strings + horns + harp, one note per level ≥ 0.13 s apart; a detent click per level; low-passed wind noise crossfaded by speed; snap + clank; an A-major chord + timpani at L100.
- Checks (b73B, Full HD): 918 f = 15.30 s; −14.0 LUFS, TP −3.9; flash PASS; frames read 0, 5, 8.66, 8.85, 13, 15 s (1:1 crops at the snap, the screen hit and L100).
- Delivered review/batch73/level100.mp4. Owner review: pending.
