# shelter_water: HOSE vs a BUCKET that DOUBLES, who stores 2 WEEKS of water? (shelter pilot A, 2026-11-15, NEW)

- Brief: docs/BRIEF_shelter_pilots.md (pilot A). New file `scenes/shelter_water.py`; no lib changes.
- Gate (research/WINNING_FORMULA.md): 1 hook, 2 FILL (tank in DAYS, FULL = 2 WEEKS), 3 ×2 bucket, 5 the same dump
  again and again each 2× bigger, 6 everyday question settled by a fill/flood, 7 length, 8 overflow finale = **7**.

## Facts on screen and sources
| On screen | Source |
|---|---|
| 1 GAL = 1 DAY (one gallon per person per day) | Ready.gov "Water" and "Build a Kit": "at least one gallon of water per person per day for several days, for drinking and sanitation" |
| 2 WEEKS = 14 gal each (the FULL line) | FEMA / American Red Cross, "Food and Water in an Emergency": "Store a total of at least one gallon per person, per day. You should store at least a two-week supply of water for each member of your family." |
| 72 H (3 gal) | EU Preparedness Union Strategy (26 Mar 2025): households self-sufficient for at least 72 hours (Euronews, Reuters coverage) |
| Bucket ¼, ½, 1, 2, 4, 8 gal | the ×2 rule (not a fact claim) |

## Sim
- Volume bookkeeping is honest: particles carry gallons (bucket 0.004, hose 0.003); what lands is in the tank; an
  excess over 14 gal leaves over both rims as spill particles to a floor puddle.
- Surface: 1D damped wave field (52 columns, c 640 px/s, damping 2.2/s, zero mean, clip ±min(42, 0.45 depth)).
- Hose 1.175 gal/clip-s from sim −1.18 s; bucket trips every 1.7 s (first dump 0.30 s), pour time 0.25 + 0.13 v^0.8 s.
- Tanks 260 px wide, 50 px per gallon, rim y 526 = 2 WEEKS.

## Music
- Handel, Water Music, Alla Hornpipe (PD; IMSLP #270469 MIDI, top line −3 st, as pascal_barrel). Note per half gallon
  crossed in either tank + one per dump (strings + harp, pizz under every 2nd), glugs per dump (deeper as the bucket
  grows), soft hose plinks, splash plinks per dump (2 + 2k), D-major tutti + timpani + splash on FULL.

## Results / checks (label p1, Full HD)
- Gallons hose/bucket: 2 s 3.0/0.2 · 4 s 5.5/0.7 · 6 s 7.9/1.7 · 8 s 10.4/5.9 · 9 s 11.6/7.7.
- The 8-gal dump: lead change 9.57 s, **FULL 9.59 s** (Bolt wins), 1.72 gal over the rims to a floor puddle; Mochi ends 12.65.
- h264 yuv420p 1080x1920 60 fps, 727 f = 12.12 s; −14.01 LUFS, peak −4.66, last 0.5 s −62.4 dB; flash PASS; seam 0.38.
- Frames read: 0.3, 2.4, 5.2, 8.9, 9.45, 9.7, 10.6 (fast) + the 1 fps sheet and 1:1 crops (0.3, 3.0, 9.4, 9.75) of the encoded file.
- Delivered `<VIDEOS_DIR>/MochiAndBolt/review/shelter_water.mp4` + `shelter_water_files/`. Owner review: APPROVED 2026-11-15.

## Lessons
- Bucket particles need a small sideways speed (70 √scale px/s) or the big dumps land outside the tank.
- The hose stream takes ~0.7 s to fall 770 px: start it 1.2 s before frame 0 so the tank is not empty at frame 0.
- `orc.render` + the mixer reverb ring ~1 s: end the bed at T − 1.3 s (fade T − 1.45 → T − 1.05) to get the last 0.5 s ≤ −60 dB in the mp4.
- The lead change lands 0.02 s before FULL (an 8-gal dump is over in ~0.4 s): the overtake IS the finish.

## Doubts
- A small first bucket at frame 0; a modest overflow (honest 1.7 gal); "trip" time is a rule, not a measured walk.

## 4K (2026-11-15, approved owner)
- `<VIDEOS_DIR>/MochiAndBolt/reserve/shelter_water_4k.mp4` + `_UPLOAD.md`; FHD review copy archived in `archive/reviewed_2026-11-15/`.
