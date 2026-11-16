# ol_tsunami_city (DopamineEXE, batch75 #1): stills stage
- Side view: the sea sits top-left behind a sluice gate, a city slopes down at 13 deg (4 blocks: low, raised on columns, low-mid, a tall raised tower), and a deep valley on the right (x 640-900) fills toward the gold FLOOD line. Caption `Every 3 s the gate opens ^WIDER^…|until the valley ~FLOODS~` (the brief said 2 s; the 3 s period is what the sim does).
- Lessons:
  - Equal discs crystallise into hex patches and heap, so the balls are BIDISPERSE (0.85/1.15 R). Cohesion under gravity = heaps, so it is off. Noise > 0.02 boils the water.
  - In a side view every ground-level building is a weir, and a flat plain becomes a lake at sea level. Raised blocks on background columns (no collision) let the water pass under.
  - Colour each ball only after it passes the gate (tg <= t); otherwise future hues leak into the sea.
- Gate gap 14 -> 28 (f0) -> 56 -> 112 -> 224 px. FLOOD at 11.6 s, clip 14.0 s. Valley landings/s: 0,2,8,8,23,42,74,89,70,191,320,302. Nothing topples (static blocks).
- Full HD (batch75 round 2): doublings at -4, -1, 2, 5 s (frame 0 = GATE x4, the wave already over the city), FLOOD line 822. The dissolve hard-swaps the HUD. Music: Beethoven Pathetique I Allegro (Mutopia PD, newly fetched to scores\beethoven_pathetique1), FLOOD on the beat-120 C-minor arrival. 12.62 s, -14.0 LUFS, flash PASS. Delivered `review\batch75\ol_tsunami_city.mp4`.
