# geode_crack
- New scene (batch39), built to research/simple_viral_formula.md and the BRIEF_batch25 RESEARCH RULES. This is the **CHARACTER side** of the A/B test: Bolt rides a big pivoted hammer and hits the geode; Mochi watches from the bottom-right.
- Caption (baked, `--cap`; `--cap ''` = base): `Every hit cracks it a little ^MORE^|~Until it finally OPENS~`.
- The only other text is the readout at y 326, anchored at x 410: `CRACKED n%` plus a small `HIT n`. From 85% the tail says `ALMOST!` in gold. At 100% the number is gold and the tail is gone.

## World (logical px)
- **Geode:**
  - A lumpy ellipse (rx 440, ry 318, 11 seeded harmonics) centred at x 515, resting on the floor at y 1352 with a flattened bottom. It spans x ~75-955 (~0.82 w) and y ~710-1352 (≤ 0.705 h).
  - The stone is a pre-rendered layer: a warm grey-brown radial shade, warm and cool patches, soft lit/shaded lumps, pits, grains, a dark rim and a cool rim light.
- **Hue map (one source of truth):** ~30 crystal clusters spread over the stone, with hues stepped by the golden ratio so neighbours differ. The hue at any point is a soft blend of nearby clusters (scale 30 px). Cracks, windows and the final cavity all use it, so the light leaking out at frame 0 really is the colour inside.
- **Interior** (pre-rendered layer): a crust rim, 5 agate bands, a deep-violet hollow, ~560 faceted crystal prisms (4 facets each) pointing inward, and a faint centre glow.
- **Hammer:**
  - A post at x 40. The pivot is solved so the face meets the stone top at φ −0.04 rad. The handle is 400 to the head centre, and the steel head is 92x124 with gold bands.
  - Six power lamps on the handle light up gold as hits progress.
  - Bolt (r 44) sits on the handle at 290 px, right behind the head.
- **Mochi** (r 44) stands on the floor at x 842, left of the 0.85 w strip.

## Mechanic (one model)
- **Hit energy:** hit n has E_n = 1.08^(n−1). The wind-up rises 14° → 34°, the slam shortens 0.28 → 0.18 s, and hits come faster: the interval goes geometrically 1.20 → 0.55 s. 24 hits in total. The first impact is at 0.38 s and hit 2 is at 1.58 s.
- **Split crack:** a seeded zigzag from the impact point to the bottom of the stone (664 px at s4). Each hit grows it by km·E_n·Lm, at 650 px/s.
  - km is solved so that the second-to-last hit leaves it nearly done and the last hit needs 60% of its energy to finish it. At s4: hit 12 reaches 35%, hit 22 87% (`ALMOST!`), hit 23 95%, and hit 24 completes it.
  - **`CRACKED n%` = the split crack's length / its full length.** It starts at 8% at frame 0.
- **Branch network:**
  - Budget 95·E_n px per hit: up to 3 open tips extend by 20% of the budget each, and 1 + int(0.35 E) new branches take the rest.
  - New branches spawn from the fresh part of the split crack or from older branches. 75% of the time they turn toward the emptier half of the stone.
  - Paths are zigzags of short straight segments around a slowly bending course. They stop at the stone edge. They grow at 520 px/s.
- **Chips:**
  - 6 + 2.5 E chips fly out from both edges of the hammer face each hit. They bounce off the stone outline and the floor, 240 Hz substeps.
  - Small flakes shed along the fresh cracks, one per 70 px of growth.
  - 0.40·E crystal windows open per hit. Each is a crust piece popping off (it falls in front and bounces), revealing the interior layer through a 7-gon with a hue glow and a glint.
- **Finale:**
  - The split connects (t_split = 19.66 s) and the whole crack network flares for 0.22 s.
  - The two crust halves swing open on their outer edges like doors (x-scale 1 → 0.14 with ease-in and a darkening shade), land at +0.55 s, then fade and drop.
  - Under them is the full crystal cavity: a soft bloom clipped to the stone (alpha ≤ 0.26), slow twinkles, and one sparkle per chime note.
  - Zoom goes 1.0 → 1.10, then eases back to 1.0 over the 0.9 s before the dissolve. A 0.6 s dissolve leads into the pre-roll (the hammer at the top of swing 1), so the stone "closes" and the loop restarts.
- **Cast:**
  - Bolt is determined and pumping on the lift, squashes before the slam, and hops and grins on every impact (the hop grows with E). In the finale he goes wide-eyed `wow`.
  - Mochi winces at every hit with E ≥ 1.25 and is worried from hit 20 to the split. Then she holds a `wow` to the end. Gaze is smoothed and follows the split-crack front.

## Sound (all synthesized; no music, no beds, no whoosh/hiss)
- **tok** per hit: a 5-mode stone clack at f0 = 430·E^−0.2 (430 → 305 Hz, so it gets deeper with power), plus a 105 Hz body thump (bigger with E) and a 3 ms click band-limited to 0.9-2.8 kHz.
- **Crackle:** one dry tik (950-1750 Hz, 3 modes of a few ms) per 6.5 px of total crack growth, sampled every 2 ms. Ticks closer than 12 ms merge into a fuller tik. The tick rate follows the crack growth rate, and the level is density-aware.
- **chip:** a tik per chip bounce on the stone or floor (≥ 18 ms apart). Pitch follows size and the gain follows impact speed.
- **ting** per window: a glass ping at C6-A6 drawn from a pentatonic set picked by hue.
- **Finale:**
  - The split: a 300 Hz modal crack, a 9-tik run and a 72 Hz thump.
  - Two stone-half thuds 30 ms apart (98 Hz plus a 230 Hz knock).
  - A shower of 24 clean bell chimes, C5-C6 pentatonic, 75-210 ms apart, each sparkling one crystal tip.
- Every onset is ≥ 12 ms apart. `master(reverb 0.30, peak_db −6)`. The last 1.0 s is digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --peak`. Tuning: `--hits --pow --d0 --d1 --kb --crystals`.

## Numbers (s4, default)
- 24 hits; 43 branch cracks; 19 crystal windows (3 already open at frame 0); 423 chips. Split at 19.66 s, open at 19.88 s, clip 24.78 s (1487 frames).
- 745 sound events: 24 tok, 293 crackle, 385 chip, 16 ting, 1 split, 2 thuds, 24 chimes. Minimum onset gap 12.0 ms.
- Events per 2 s: 30 40 34 51 65 67 78 78 106 137 | 52 (split + chimes) 7 0. Rate climbs to the split.

## Checks (encoded Full HD, `output/geode_crack_fhd3_9x16.mp4`)
- h264 yuv420p 1080x1920, 60 fps, 1487 frames = 24.78 s.
- -13.96 LUFS, peak -7.26 dBFS. The last 1.0 s is digital silence. RMS per 5 s: -23.7 / -23.8 / -15.9 / -18.7 / -14.5. Energy above 3 kHz is 0.62% (nothing shrill).
- flash_check PASS (0 flashes, mean lum 0.033).
- **Loop:** pre-encode, last frame → frame 0 has a mean delta of 0.009 against a normal step of 0.175. The last frame is pre-roll frame −1, during the hammer's top-of-swing hold, so the seam is invisible. Encoded seam 0.476 (good band).
- Tok onsets sit exactly on the impact frames (first at 0.380 s). The tok's 60 ms RMS is about 1.25x a crackle/chip tik.
- Encoded frames read at 0 / 0.45 / 1 / 2 / 3 / 12.4 / 19.68 (split) / 20.3 (halves swinging) / 21.5 / 23.5 s, with 1:1 crops of the impact, the split network and the reveal.
- Safe zone:
  - The caption is at y 172-245 and the readout at y ~290-330.
  - The hammer head stays below y ~330 at full wind-up.
  - The stone and Mochi are at ≤ 1352 (0.704 h), and Mochi is at x ≤ 886.
  - The geode's right edge (x ≤ 955) brushes the 0.85 w strip as decoration only.
- Delivered `<VIDEOS_DIR>\batch39\geode_crack.mp4`. The 4K ship render is still to be made after review (`NF_SCALE=2.0 --label ship`).

## Doubts
- Hits 1-3 add only ~1-2% each (honest E ∝ 1.08^n). The hook leans on the frame-0 rainbow cracks plus the first impact at 0.38 s. A higher `--pow` would front-load less, not more.
- Bolt "rides" the hammer rather than swinging it (he has no arms). It reads as his hammer, but the cause is cartoon logic.
- The geode's front crust swings open like two doors onto a cross-section: a 2D shorthand, not a true 3D split.
- Chip tiks are dense late on (385 events). They are quiet, but the owner may want fewer.


Owner review (2026-10-17): "we can try and see how it goes" -> APPROVED -> 4K, Schedule 2026-10-23 slot 1.

Owner review (2026-10-17): APPROVED ("we can try and see how it goes"). 4K ship render: `NF_SCALE=2.0 --seed 4 --label ship` -> output/geode_crack_ship_9x16.mp4 (h264 yuv420p 2160x3840, 60 fps, 1487 frames = 24.783 s; -13.96 LUFS, peak -7.26 dBFS, last 0.5 s digital silence; flash_check PASS 0 flashes; encoded seam 0.309). Left in output/ for the coordinator to stage.
