# polygon_race — "Mochi ADDS 24 sides, Bolt DOUBLES them" / "who matches 3.14159 first?" (batch68)

- Brief: docs/BRIEF_batch68.md §2 (replaces growth_race2). New file `scenes/polygon_race.py`.
- Two polygons inscribed in identical circles (R 180 px, centres x 300 / 716, y 690). Mochi: 24-gon, +24 sides a round. Bolt: triangle, x2 sides a round (Archimedes: every edge's midpoint pops out to the circle).
- The judge: perimeter / diameter of the polygon actually DRAWN, computed from its vertices every frame (so the readout climbs as vertices pop). Meter = 6 digit boxes "3.14159" per side (gold when matched, prefix match of the truncated value); GOAL line "π = 3.14159265…" from frame 0. "CLOSER TO π" under the leader.
- Head start chosen: Mochi 24 (+24). With 12 (+12) she leads only rounds 0-4 and the digit meter ties at rounds 2-3; with 24 she leads rounds 0-5.

## Honest numbers (regular polygons, end of round)
- r0 24 3.1326 / 3 2.5981 · r3 96 3.14103 / 24 3.13263 · r5 144 3.14134 / 96 3.14103 · **r6 168 3.14141 / 192 3.14145 (LEAD CHANGE)** · r7 192 / 384 (5 digits) · **r9 240 3.1415029 (5 digits) / 1,536 3.1415904 (6 digits = LOCKED)**.
- Mochi needs ≥ 1,396 sides for 6 digits: 1,416 = round 58, 49 more rounds (shown in the finale).

## Moves / animation
- Mochi's move on the bar's first half: 24 new vertices (one in every k-th edge) pop on 16ths 0-5, then all vertices slide to the regular (24k+24)-gon on 16ths 6-7. Bolt's on the second half: n midpoints pop, ≤ 8 on 16ths, more as a clockwise sweep over 1.62 beats. Pop = 0.12 s ease-out from chord midpoint to the circle (no overshoot: the readout never passes π).
- Rainbow edge ring by angle (48 hue buckets), team-tinted fill, faint dashed true circle, vertex dots shrinking with edge length, a sparkle per fresh vertex. Finale: Bolt's polygon turns gold + a ring glow.

## Timeline (clip 15.92 s = 955 frames)
- Rounds r1..r9 at 0.05 1.62 3.12 4.56 5.94 7.26 8.52 9.74 10.90 s. LEAD CHANGE 8.40 s. 3.14159 LOCKED 11.93 s, the C-major tutti 12.01 s, BOLT WINS 12.61 s, "Mochi needs 1,416 sides: 49 more rounds" from 12.9 s. Dissolve 15.32-15.92.

## Sound
- J. S. Bach, Prelude in C major BWV 846 (Mutopia #5, PD; `<SOUNDFONTS_DIR>\scores\bach_prelude_c`). Bars 1-8 = rounds 1-8, round 9 = bar 3 (G7/B), finale = C-major tutti. Accelerando 150 -> 220 bpm. Piano + harp (all), celesta (from r7), string pad (r4+), choir (r7+), horns, contrabass octave bass (r4+), timpani per bar (r7+), roll + swell into the tutti (strings, brass, choir, piano, harp sweep, tubular bell, crash). A glassy tick per popping-vertex group; pings at the lead change and the lock.
- Used once before by hanoi_64.

## Checks (encoded Full HD, label b68; the second render re-checked: same numbers, seam 0.491)
- h264 yuv420p 1080x1920 60 fps, 955 frames = 15.92 s. -14.01 LUFS, peak -5.56 dBFS, last 0.5 s -78 dBFS. flash_check 0. Seam 0.49.
- Frames read: 0, 1.0, 8.42 (lead change), 11.95 (lock), 12.7, 15.85.
- Fixes in the second render: the SIDES count now counts popped vertices only (it showed 1,536 during the last sweep); ROUND never shows 0 in the loop dissolve.

## Doubts
- From ~round 3 both shapes look like perfect circles at this size; the digits carry the race (that is the point: "looks round, isn't π yet").
- Bolt's 6th digit locks 0.08 s before the tutti (during his last sweep), so "LOCKED" and the chord land together.
Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch68\polygon_race.mp4`. Owner review: pending.
