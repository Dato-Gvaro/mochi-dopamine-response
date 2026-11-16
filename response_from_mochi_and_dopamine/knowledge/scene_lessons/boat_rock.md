# boat_rock — rocks INTO THE WATER or INTO THE BOAT: which tank overflows first? (batch72, NEW)

- Brief: docs/BRIEF_batch72.md §2-4 (IDEAS.md pick 2). New file `scenes/boat_rock.py`.
- Physics (exact, Archimedes): tank 0.50 × 0.40 m (0.2 m²), rock 1.0 L granite (2.7 kg). A sunk rock lifts the water by its volume: +5.0 mm; a rock carried by a floating boat lifts it by its weight / ρw: +13.5 mm. Rounds ×2 rocks (1, 2, 4, 8, 16), both chutes drop together (gaps 1.25/0.8/0.52/0.36/0.24 s, 0.35 s between rounds). Headroom to MAX = Bolt's rise after 24 rocks (324 mm).
- Result: BOLT OVERFLOWS on his 24th rock at 11.38 s (round 5); Mochi then +120 mm (37 %), +155 mm after all 31.
- Drawn: Bolt's boat sinks 3 px per rock (decoration; the level math is exact) and bobs; Mochi's rocks sink and pile on the floor.
- Music: Holst, Thaxted (Mutopia #527, PD), one horn+strings note per rock; a splash per Mochi rock, a wood thunk per Bolt rock; F-major chord on the overflow.
- Checks (encoded Full HD, label b72): 851 f = 14.18 s; −13.97 LUFS, peak −5.1; flash PASS; seam 0.35. Frames read 0.2, 1.6, 6.0, 10.0, 11.15, 12.3 (1:1 crop).
- Doubts: no lead change (Bolt is ahead from the first rock: the 2.7× is the whole story); the first rounds are slow (1 rock in 1.25 s, quieter audio).
- Delivered review/batch72/boat_rock.mp4. Owner review: pending.
