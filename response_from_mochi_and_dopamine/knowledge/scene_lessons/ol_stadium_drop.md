# ol_stadium_drop (DopamineEXE, BRIEF_dopa_1113 #2)
- The doubling-drop riddle, true numbers: 0.05 mL drop, 104,000,000 ft³ (AT&T Stadium, HKS fact sheet) = 58,899,040,911,360 drops = 2^45.74 → FULL at minute 45:45. Min 41 = 3.7%.
- Review copy + README (facts, sources, rung table, titles): `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_stadium_drop\`. FHD only (label fhd), 15.63 s, -14.01 LUFS, flash PASS.

## Model
- 3/4 oblique orthographic view, elevation 47°. Floor ellipse 255×113 ft (z 0) → bowl linear to rim 500×380 (z 180) → half-ellipsoid dome, height solved to 121.4 ft so the total is exactly 104e6 ft³ (bowl 53.6%).
- Water < floor film (2^29.65 drops): hemispherical drop until 5 mm high, then a 5 mm film whose AREA = V/5 mm (circle at the drop point clipped to the floor ellipse, radius from an area table). After: level from the model's cumulative volume table.
- Camera: px/ft = softmax(120 px / puddle radius, 0.70); the target slides from the drop (3, -6) to (0, 30, 150 ft) with weight (S_F/S)^0.8.
- Clock: minute k at TK[k], minute 1 = 0.34 s → minute 46 = 0.20 s (geometric). Water eases each doubling over 0.12 s; continuous from minute 45.

## Gotchas
- **pixman pattern transforms are 16.16 fixed point**: a repeating texture's matrix offset must be taken modulo the tile size, or the pattern paints one flat colour (turf fibres vanished at macro zoom).
- cairo path coords overflow past ~8M device px: huge ellipses are classified out / screen-inside / partial (`ell_state`) and screen-inside fills paint the screen rect; field rects are clipped numerically.
- The encoded seam reads 1.9 (pre-encode 1.17 vs step 1.10) because frame 0 is a fine-texture keyframe.

## Sound
- Vivaldi Summer III Presto (Mutopia 336) beats 0-54, cuts [10,15) [25,27) [31,32) → 46 virtual beats = minutes; beat 54 (G) = FULL. Bloop per doubling (G minor, pitch falls with volume), plips in the overflow.

## Flags
`--label --cap --still --frame --dry --remux --sound 0 --sfx (0.35) --fin (3.0) --dt0 (0.34) --dte (0.20) --tover (1.75) --hold (0.95) --phi (47) --sf (0.70)`
