# polygon_race2 — Mochi ADDS 2 sides, Bolt DOUBLES (batch69)

- Brief: docs/BRIEF_batch69.md §2 (owner: "Bolt's side looks good, but Mochi just has a circle with no visual effect for the eye"). New file `scenes/polygon_race2.py` (generated from polygon_race.py; polygon_race untouched).
- THE ONE CHANGE: Mochi starts as a NONAGON and adds 2 sides a round (9 → 27 over 9 rounds): a visible polygon that morphs every round (2 vertices pop, the shape relaxes to the regular n+2-gon). Bolt = polygon_race's doubling triangle (3 → 1,536). New: the gold slivers = the exact gap between each polygon and its circle (even-odd fill circle − polygon, alpha 0.75).
- Judge unchanged: perimeter ÷ diameter of the drawn polygon → π digits (6-box meter, "CLOSER TO π").
- Start/rule choice: +2 from 9 gives Mochi rounds 0-2; +2 from 8 ties at round 2 (12 vs 12); +1 from 7 leads only 2 rounds; bigger starts (16 +4) lead to round 3 but are circles to the eye again.

## Honest result
- r0 9-gon 3.0782 vs triangle 2.5981 · r1 11 3.0991 vs 6 3.0000 · r2 13 3.1111 vs 12 3.1058 (Mochi still closer) · **r3: LEAD CHANGE (clip 4.17 s)**, 24-gon 3.1326 vs 15-gon 3.1187 · r9: Bolt 1,536 = 3.1415904 (6 digits, LOCKED 11.93 s) vs Mochi 27 = 3.1345 (2 digits).
- Mochi needs 1,397 sides for 6 digits = round 694 (685 more rounds): shown in the finale.

## Sound
- Mozart, Piano Sonata K. 545, 1st mvt (Mutopia #998, PD; used once by block_overhang): bars 1-8 = rounds 1-8, bar 11 (G broken chord) = round 9, C-major tutti finale. polygon_race's arrangement (piano + harp, string pad from r4, choir/horns/timpani from r7) on the new notes.

## Checks (encoded Full HD, label b69)
- h264 yuv420p 1080x1920 60 fps, 955 frames = 15.92 s. −14.01 LUFS, peak −5.41 dBFS, last 0.5 s −78 dBFS. flash_check pass. Seam 0.51. 146 melody notes, 22 distinct.
- Frames read: 0.0, 2.0, 4.2 (lead change), 12.6 (win); Fast stills 0, 40, 200, 250, 500, 760.

## Doubts
- The lead change is at round 3 of 9 (the honest price of keeping Mochi's polygon visibly low-sided).
- From ~19 sides Mochi's facets are small (the vertex dots and slivers carry it).

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch69\polygon_race2.mp4`. Owner review: pending.
