# bolt_feast — episode of mochi_feast5: BOLT's turn to eat (PERFECT FIT)

- One nameable change: roles swapped. Mochi stomps the bag with the evil grin, Bolt eats and grows. Bolt is a rounded square, so the tank's inside is cut to his exact FULL outline: 1.9 x 1.84 r, 0.5 r bottom corners. FULL = a snug fit, corner to corner and rim to floor.
- Geometry: inner 234..846 (612 px). R_END = 306/0.95 = 322.1. TANK_TOP = FLOOR_Y - 1.84 R_END = 752.3. Bottom corner radius RC = 161. Physics corners are 10-segment arcs. Bolt is clipped to the tank's inner U, so the jolt boing (b 0.06) presses into the glass. His sprout pokes out above the rim.
- Eat test uses the rounded-rect half-width (hw_at), so nothing survives in the corners.
- Theme lemon (feast5 is peach). Bag spout is blue. Melody jolly_good_fellow (feast5 uses entertainer). william_tell was tried first: 55% of its notes are one pitch (67), so it was dropped.
- Shelves 160 px at y 960, 25 deg. Long tosses vy -300..-200 so they arc onto the right shelf.
- s1: t_end 15.87 s, 18.18 s total (TE 2.3). Bites per 5 s [22, 37, 75]. x2 1.95 s, x3 7.25, x4 12.15, FULL x5 15.87.
- TE is 2.3, not feast5's 2.1. At 2.1 the last 0.5 s of the muxed mp4 peaked at -57 dBFS (the 5-note fanfare plus the late dense bites). The pre-mux wav tail looked silent only because the mix renders 2 s past the end. Always measure the MP4.
- nudge(): melody notes keep their times. Foley and milestone chimes move in +12.5 ms steps until they clear every placed event (minimum gap 12.7 ms).
- Checks (Full HD): -14.01 LUFS, peak -7.40 dBFS, last 0.5 s -68.0 dBFS, last sound 1.80 s before the end. Seam: pre-encode frame 0 == last frame (max diff 0); encoded mean delta 0.247. flash_check 0.
- Known: the burp drops a candy onto Bolt's sprout at frame 0 (the same as feast5). It is eaten at 0.02 s.
- Made-for-kids audit 2026-10-04: children's tune replaced (now fur_elise); renders before this used a kid-coded melody.
- Owner review 2026-10-04 (batch 7): GOOD, as long as it doesn't feel like a repeat of mochi_feast5 -> schedule >=3 days after it.
- Owner review 2026-10-05: Boring; removed.
