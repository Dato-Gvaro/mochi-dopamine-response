# ice_flood2: the SAME ice block, FLOATING or on LAND: whose beach houses flood? (batch72b, REBUILD of ice_flood)

- Brief: docs/BRIEF_batch72b.md. New file `scenes/ice_flood2.py`; `ice_flood.py` untouched.
- Why rebuilt: owner on ice_flood: "good idea, poor execution"; overflow water "magically appears at the top"; not everything should overflow.
- Model (2D cross-section per metre of coast): ice 917, fresh 1000, sea 1025 kg/m³. The block is 1.5 × 0.74 m, the same on both sides. Bolt's meltwater runs off the headland into the sea, and the level rises by meltwater volume ÷ the sea's width at that height (each flooded terrace widens the sea, so the rise slows). Mochi's floating block already displaces its weight of sea water, and its fresh meltwater needs 2.5 % more room, so her rise = 2.44 % of Bolt's.
- Drawn: levels and terrain heights ×5 (VEX solved = 5.0, labelled "heights drawn x5"); the ice is true to scale. Time-lapse; frame 0 is 4 % melted (Bolt +3.1 cm).
- Result: Bolt floods 4/4 houses at 0.68, 3.15, 6.87, 11.8 s and ends at +28.0 cm. Mochi floods 0/4 and ends at +1.9 cm.
- Fix after the first Full HD (b72b): the headland's top was ~20 cm above the sea, so it went under at ~7 s and the "land" ice ended up in the water. ROCK_TOP raised to 130 (local y), which stays above the final level (160). Character moved down onto the rock face. Shipped b72c.
- Music: Liszt, Liebestraum No. 3 (PD; theme pitches hand-encoded): a harp note every 0.4 s, a plip per drip, timpani + horns + splash on each flood.
- Checks (encoded Full HD, b72c): 960 f = 16.00 s; −14.00 LUFS, peak −6.1; flash PASS; seam 0.48. Frames read 0.05, 0.75, 3.2, 6.95, 11.9, 15.4 (+ 1:1 crop of Bolt's panel at 15.4).
- Doubts: events/5 s go 16 → 14 → 12 (the floods spread out as the sea widens); the last ~4 s have no new flood; it is a small cove (the sea is ~6.5 m wide at the start) so 1.5 m of ice can raise it 28 cm.
- Delivered: <VIDEOS_DIR>\MochiAndBolt\review\batch72b\ice_flood2.mp4. Owner review: pending.
