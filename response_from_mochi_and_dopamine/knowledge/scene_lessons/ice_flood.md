# ice_flood — 6 kg of FLOATING ice vs 1 kg on LAND: which tank overflows? (batch72, NEW)

- Brief: docs/BRIEF_batch72.md §2-4 (IDEAS.md pick 3). New file `scenes/ice_flood.py`.
- Physics (exact, Archimedes, fresh water): tank 0.40 × 0.30 m (0.12 m²), both 5.0 mm under MAX (= 0.60 kg of new water). Mochi: 6 × 1 kg cubes floating → level change 0 exactly (the meltwater fills the displaced volume). Bolt: 1 kg block on a rock island → +8.3 mm per kg melted, capped at MAX (spills).
- Melting: dm/dt = −k · 6 s² per cube; k_air 9.86e-4 kg/(m² s) (solved so Bolt's tank overflows at clip 10.5 s), k_water = 2 × k_air. Time-lapse ×1200 (210 min at the overflow).
- Result: Bolt OVERFLOWS at 10.5 s (0.60 kg melted); Mochi then 89 % melted, level +0.0 mm (97 % melted by the end).
- Drawn: cubes ~5× their tank scale; the level scale magnified ×10 (1 mm = 10 px).
- Music: Liszt, Liebestraum No. 3 (PD; the opening theme's pitches hand-encoded), harp (+ celesta for Mochi) one note per 2.5 % melted per side; a drip per Bolt note; A-flat chord on the overflow.
- Checks (encoded Full HD, label b72): 810 f = 13.50 s; −14.00 LUFS, peak −5.2; flash PASS; seam 0.35. Frames read 0.2, 5, 6, 9, 10.55, 11.6, 12.6.
- Doubts: calm motion (melting); 13.5 s; real sea ice sits in SALT water, where meltwater raises the level a little (~2-3 % of the ice's volume); fresh water here.
- Delivered review/batch72/ice_flood.mp4. Owner review: pending.
