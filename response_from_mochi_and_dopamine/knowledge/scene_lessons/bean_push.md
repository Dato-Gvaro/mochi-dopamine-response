# bean_push — the "hand in the beans" Short: BLADE vs CUPPED HAND, seen from above (batch71, NEW)

- Brief: docs/BRIEF_batch71.md §6 (owner idea: pushing a big pile with real physics feels like a hand in beans). New file `scenes/bean_push.py`.
- First built as a SIDE view (dozer vs dustpan into a pit): with friction the pile moved as one block, the dozer filled the pit in one pass (~2 s), the scoop barely lifted anything, and balls tunnelled out. Rebuilt TOP-DOWN: blade width is the natural "1.5x WIDER" rule, and balls pile in front of the tool and roll off its ends.
- Setup: two arenas (x 112-500 / 520-904, y 330-1336), the same relaxed round heap of 773 balls (r 5.6 ±8 %, centre y 1010). BIN at the top (back wall y 330, FULL line y 450) with a sloped floor (G_BIN 900 px/s² toward the back wall, so balls past the line stay in). Tools sweep the centre lane from y 1230 up into the bin (V 420 px/s, force-limited F_LIM 6000, stall at 30 % speed → lift), lift, fly back; width W0 70 × 1.5^pass (capped at the arena).
- MOCHI: flat BLADE. BOLT: CUPPED HAND (an arc of the same width, tips leading, depth 0.32 w).
- Physics: PBD on a floor (rolling friction 7/s, rest < 30 px/s), Coulomb friction μs 0.5 / μk 0.35 ball-ball and ball-tool, ball-ball overlap corrections capped at 160 px/s of speed (a squeezed pile doesn't explode), 4 × 6 iterations, hard containment.
- FULL = ball area past the line / (bin area × PACK 0.80, the measured packing of the pressed bin: 0.79-0.86), held for 10 frames while the tool is OFF the balls (a squeezed bin doesn't count). The meter reads ≤ 99 % until FULL.
- Seed 1 result: bin % blade/cup per pass: 8/10, 14/23, 38/50, 71/77; the cup leads (banner at 10.9 s); the blade's 5th pass (×5.06) fills its bin: **MOCHI FULL at 13.33 s**; the cup's 5th pass squeezed its bin to 103 % but it settled back to 98 %.
- Music: Bizet, Carmen Prelude (PD; Mutopia #635 note data, our arrangement, as penny_double), re-timed so beat 32 (the A-major cadence) = FULL; a melody tick per group of balls crossing into a bin.
- Checks (encoded Full HD, label b71): h264 yuv420p 1080x1920 60 fps, 956 f = 15.93 s; −14.01 LUFS, peak −5.2, last 0.5 s −64 dB; flash PASS; seam 0.89 (dissolve into frame 0). Frames read 0.2, 1.5, 4.6, 7.6 (1:1 crop), 7.7, 11.0, 13.0, 13.4, 14.8.
- Doubts: no ball count in the HUD (bin % only); the melody is sparse (45 ticks, one per landing group); the loop dissolves a full bin into the frame-0 heap.
- Delivered review/batch71/bean_push.mp4. Owner review: pending.
