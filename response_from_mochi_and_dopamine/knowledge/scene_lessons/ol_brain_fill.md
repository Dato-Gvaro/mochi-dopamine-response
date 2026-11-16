# ol_brain_fill (DopamineEXE, batch62 #2)

## v1 (2026-10-31)
A side-view brain outline (frontal lobe left; 6 deep folds; a cerebellum lobe joined to the brainstem by a 35 px neck; a dead-end brainstem). Zero gravity, every ball at a constant 450 px/s, elastic bounces. Every wall hit spawns one copy beside the ball along the wall, if it fits. It runs until every part of the brain holds a ball: FULL, then a "neurons firing" sweep front → back.

- Caption (baked; `--cap ''` = base): `Every wall hit makes ^1 MORE^ ball…|until the ~BRAIN~ is full` (the brief's "Every ball that hits a wall makes 1 MORE…" shrank to an unreadable size on one line; same rule, shorter). True: every wall hit spawns a copy (when there is room for one), and the run reaches FULL.
- **Deviations (truth over brief):** speed 450 px/s, not 900 (at 900 the count went ×16 in 1 s and FULL came at ~5 s); FULL at 7.13 s, not 9.8 (the clip is 9.33 s, in the 9-13 s band). Music: the owner's NCS track "Waiting" (the brief's listed option) instead of Nessun dorma: no PD source of the Turandot Act III score could be fetched (IMSLP captcha; the classicalmidi Turandot files are Acts I-II only and © the sequencer), and the owner prefers his own tracks.

## Model (`simulate`, seeded, ~15 s CPU)
- Geometry: Catmull-Rom outline (53 control points, corners at the neck/brainstem kept sharp), gyral bumps (5 px, λ 62 px) on the cerebrum arc and underside; 6 fold walls (Sylvian, central, precentral, frontal, parieto-occipital, occipital) + 2 short folia walls in the cerebellum, all with a 5 px wave. Whole brain shifted 12 px left: x 128-905 (0.12-0.84w), y 405-1160 (0.21-0.60h).
- Walls rasterised at 1 px; nearest-wall lookup by an exact Euclidean distance transform (scipy, with indices). Ball r 5; 4 substeps/frame; ball-ball PBD (2 iterations, cKDTree) + equal-mass elastic exchange; speeds renormalised to V (constant-speed balls).
- Spawn: on a wall hit, try ±(2r + 0.6) along the wall tangent (random side first); valid if inside, ≥ r from every wall and no ball within 2r. The copy gets the parent's velocity mirrored along the wall (≥ 0.2 V tangential).
- FILLED % = share of the brain's 20 px cells (reachable area ≥ 40% of the cell, 935 cells) that hold a ball centre at that frame. FULL = first frame at 100%; the meter then latches at 100%.
- Seed **12**, pre-roll 80/60 s (frame 0 = 7 balls, next spawn 0.02 s; the pre-roll is set so FULL lands on the track's 4-bar line). Seed scan (FULL / first cerebellum entry, sim time from 1 ball): 5 7.72/6.08, 8 7.97/6.55, 10 8.50/6.60, 11 8.52/6.83, **12 8.45/6.87**, 13 7.10/5.40, 14 6.83/4.63, 15 8.75/4.93.

## Timeline (seed 12)
- 0 s 7 balls · 1 s 24 · 2 s 81 · 4 s 918 (55%) · 5.55 s the first ball squeezes through the neck into the empty cerebellum · 6 s 2,452 (92%) · 6.63 s 98%: "LAST GAP" tag (the cell that was the last one empty, in the temporal lobe under the Sylvian fissure) · **7.13 s FULL, 2,987 balls** · sweep · 9.33 s end (3,361 balls). Dissolve 0.6 s into frame 0. **560 frames.**

## Screen
- Balls: hue by x (orange → gold → green → cyan → violet, S 0.75), cerebellum magenta; gloss dot, dark rim; newborn white ring; trails while < 60 balls.
- Meter y 1300 "BRAIN FILLED n%" → gold "BRAIN FULL 100%", FULL mark from frame 0. Counter y 1500 BALLS (gold at FULL) + "×2" pill that pops on every doubling. Watermark 35%.

## Sound
- "Waiting" (Syn Cole, KAZHI, NCS), from 0:49.762 (the drop at 0:49.784; 135.01 BPM grid from `output/mirror_duel3_musicgrid.json`): FULL lands on the downbeat 4 bars after the drop (0:56.895). Fade out over 1.05 → 0.55 s before the end, digital silence after. **Its Description Text must go in the description:**
  ```
  Song: Syn Cole, Kazhi - Waiting
  Music provided by NoCopyrightSounds
  Free Download/Stream: http://ncs.io/s_waiting
  Watch: https://ncs.lnk.to/s_waitingAT/youtube
  ```
  (Same song as Mochi's mirror_duel3; different channel.)
- Glassy click per spawn (≤4 per frame, gain density-scaled), MIDI 72-86; a 14-note rising glassy run with the sweep. 1,465 events.

## Checks (encoded mp4)
- h264 yuv420p 1080x1920 60 fps, 9.33 s; **-14.02 LUFS**, peak -7.51 dBFS, last 0.5 s digital silence; flash_check PASS (0); seam mean |Δ| 0.180.
- Stills read at 0, 0.5, 2, 4, 5.5, 6.9, 7.0, 7.13, 7.5, 7.8 s; 1:1 crops (encoded) of the neck at 5.67 s and the frontal lobe at 7.33 s.

## Flags
`--seed` (12), `--v` (450), `--pre` (80/60), `--hold` (1.6), `--tmax`, `--scan a,b`, `--resim`, `--dry`, `--audio`, `--still --frame`, `--cap`.

## Upload draft
- `Every wall hit makes 1 more ball… until the brain is full 🧠 #satisfying #physics #shorts`
- `Can multiplying balls fill every fold of a brain? 🧠 #satisfying #physics #shorts`
- `7 balls, 1 rule, 2,987 balls later the brain is full 🧠 #satisfying #physics #shorts`
- Pinned: `the little bit under the big fold was the last spot to fill. did you spot the gap?`
- Description: the NCS text above (required).
