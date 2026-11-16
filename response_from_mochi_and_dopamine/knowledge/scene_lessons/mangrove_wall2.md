# mangrove_wall2: mangrove_wall with the bottom-lane water redone (owner review 2026-11-14)

- Review: `<VIDEOS_DIR>\MochiAndBolt\review\mangrove_wall2.mp4` (+ `_files\README.md`). Built from mangrove_wall.py; v1 untouched.
- Owner: "the pouring animation at the bottom doesn't look good". v1 faults: a thin tongue that popped in fully formed, a ~60-dot spray cloud per wave, a flat see-through flood sheet, and a flood 1.42 m deep behind a crest only 0.70 m above the ground (water above the wall).

## v2 water model (drawing only; same waves and events)
- Overflow history `TH_GRID` (1/240 s) from `wall_eta`. Nappe = ballistic parcels: parcel age a has the thickness th(t−a), v0 = 150 + 7·th px/s, G_PX 1500. Contiguous runs → a sheet that grows out and detaches. Continuity thinning: half-width × v0/speed.
- `blob_union`: ONE filled path of circles (nonzero winding) = a coherent foam/water mass with no alpha stacking. Used for whitewater, the bore nose and splash plumes.
- Splash = 16 launch times × 3 fan streams; falling parcels become sparse drops (no rods). Gradient white → blue.
- Flood body: gradient fill, sheen band, surface ripples moving inland, a 5 px surge hump per R4 wave at 300 px/s, foam streaks.
- Flood capped at the brim (0.70 m): K = 0.70/1.42 scales the v1 flood_profile and the stilt sills, so the house flood times are identical. Round 4 = 30 min (q 39 l/s/m). Bolt floats from 0.55 R.

## Lessons
- A dot-particle spray reads as confetti; the union of discs reads as water.
- Check that the drawn water level is physically possible (never above the crest that holds it).

## Outcome
- (fill after review)
