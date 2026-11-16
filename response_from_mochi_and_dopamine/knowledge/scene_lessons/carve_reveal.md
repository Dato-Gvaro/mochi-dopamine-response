# carve_reveal
- New scene (batch40), built to research/simple_viral_formula.md and the BRIEF_batch25 RESEARCH RULES. It is the **CHARACTER side** of the A/B test: the characters ARE the reveal, a statue of Mochi & Bolt carved out of a rainbow block.
- Caption (baked, `--cap`; `--cap ''` = base): `Every pass carves it a little ^DEEPER^|~Until THEY appear~`.
- The only other text is the readout at y 326, anchored at x 352: `CARVED n%` plus a small tail.
  - The tail reads `PASS n` while roughing and `DETAIL PASS` (gold) during the detail and face passes.
  - It reads `ALMOST!` (gold, pulsing) during the gap pass and the release pass.
  - At 100% the number turns gold and the tail goes away.

## World (logical px)
- **Block:** x 72-958, y 520-1352 (0.82 w; floor at 0.704 h). It is made of thin wavy strata, 2-16 px thick, with pale sand lines and dark lines between them.
  - Hue runs through the rainbow with a period of 560 px, so frame 0 shows about 1.5 cycles.
  - The statue spans about one full cycle: red curl and sprout, then green faces, then a violet/pink plinth.
  - Edges glow: a rim light from the blurred alive mask, plus a hot trail behind every fresh cut.
- **Statue:** Mochi (r 195, pear body, curl) and Bolt (rounded square, sprout on a stem) stand side by side with a 44 px gap, on a plinth (x 98-918, y 1290-1352). Their faces are engraved: oval eyes, spiral pupils and a smile.
  - At frame 0 a faint white ghost outline of the statue and its faces sits inside the block, so the end state is readable.
- **Machine:** a CNC laser on a top rail at y 428. A carriage carries a telescopic rod down to the head, and a short beam and a hot spot mark the cut.
  - The big laser has a coral band; the fine laser has a gold band, a thinner beam and a smaller spot.
  - Sparks fly from the spot while it is cutting.

## Mechanic (honest material removal against the statue mask)
- **Distance field:** EDT is each block pixel's distance to the statue.
  - **Shell:** EDT ≤ 12, left for the release cut.
  - **Reach:** the big laser (radius 20) only reaches cells within 20 px of open room (EDT ≥ 32) that is connected to the outside. This is a morphological opening.
  - **Pockets:** everything else outside the shell. These are the curl, the sprout notches, the feet corners and the gap between the figures.
- **Roughing:** 22 passes. Pass k removes the reachable cells with d_k < EDT ≤ d_{k-1}.
  - The levels are quantiles, so every pass removes the same area (about 17.1k px², about 3.9% each).
  - Pass duration drops geometrically from 1.15 s to 0.55 s, so the readout speeds up.
  - The tool traces the new outline as an arch from floor-left, over the top, to floor-right, reversing direction each pass. A cell disappears when the head passes the nearest point of the path.
- **Detail passes (fine laser):**
  - Zig-zag rasters through the pockets: curl, then sprout, then feet.
  - Then face engraving: Mochi, then Bolt.
  - Then the gap between the two figures (8.8k px², 1.0 s, `ALMOST!`).
- **Release pass:** the fine laser traces the statue outline (1.1 s) and cuts the 12 px shell free. 100% lands exactly at the end of this pass.
- **Count:** `CARVED` = (rough + pocket + shell cells already cut + groove area so far) / their total.
- **Chips:** one chip per ~300 px² the big laser removes, spawned from the removed cells and coloured by the strata at that point. They fly out along the EDT gradient, bounce once or twice on the floor and fade. The fine laser adds a steady small spray at its spot.
- **Finale (T100 = 22.00 s):**
  - The kerf flares.
  - The shell breaks into 74 pieces (Voronoi along the outline) that fall top-first with a little outward push and spin, clack on the floor and fade.
  - The statue polishes: brighter, a stronger rim glow, a gloss and one slow diagonal light sweep, all clipped to the statue. A sparkle appears on each chime.
  - The view zooms 1.0 → 1.07 and eases back to 1.0 before the dissolve.
  - The laser head travels back to its frame-0 spot.
  - At +1.15 / +1.35 s the real Mochi and Bolt pop up on the rail. Mochi is proud (hop, ^^ eyes, grin, looking at her statue). Bolt is embarrassed (worried brows, wobbly mouth, sweat, blush, looking away).
- **Loop:** a 0.6 s dissolve into the pre-roll leads straight into frame 0. Pass 1 starts at −0.44 s, and the first cut is at −0.06 s, so the block is already being cut, with chips in the air, at frame 0.

## Sound
- **Melody:** Beethoven, *Ode to Joy*, bars 1-8 (30 soprano onsets).
  - **Source:** Mutopia Project id 528 ("Ode to Joy", SATB hymn setting, Public Domain): `mutopiaproject.org/ftp/BeethovenLv/ode/ode.mid`, cached at `<SOUNDFONTS_DIR>\scores\beethoven_ode\ode.mid`.
  - It is read at runtime with `orc.read_midi`, and the scene asserts that the soprano equals the verified list B B C D D C B A G G A B B A A | B B C D D C B A G G A B A G G.
  - Note p plays at the start of pass p (29 passes). Note 30, the cadence G4 over a G2 bass, lands exactly on 100%.
  - **Voicing:**
    - Soprano on soundfont piano, with the MIDI's bass note on a softer piano.
    - The hymn's inner voices as a quiet strings_slow pad.
    - On 100%: a rolled G chord (G2 D3 G3 B3 D4) on piano, a strings swell, oohs and a soft timpani G2.
    - The highest note is D5 in the melody and G5 in the chimes.
- **SFX (all synthesized; no hiss/whoosh/drill beds):**
  - **Tick train:** a clean tonal tick (a short ping, 1.08-1.32 kHz for the big laser and 1.42-1.66 kHz for the fine one, with pitch following the strata hue, plus a tiny click). There is one tick per 62 px (big) or 26 px (fine) of laser travel while it is in contact, so the rate follows the cutting speed.
  - **Chips:** a tik when a chip lands, at most one every 32 ms, with gain following speed and size.
  - **Pass reversal:** a soft modal tok, 470 Hz for the big laser and 610 Hz for the fine one, +12 ms after the note.
  - **Finale:** a clack per shell piece landing, a chime shower of 22 G-major-pentatonic bells (G4-G5), and a pop per cameo.
- Every SFX onset is ≥ 12 ms apart. The SFX bus is normalised to -21.5 LUFS under a -20 LUFS music bed, then `master(reverb 0.30, peak −6)` brings the mix to -14 LUFS. The last 1.0 s is digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --geo` (category map) `--sound 0 --peak --sfx_lufs --crf`. Tuning: `--shell --tool --d0 --d1 --dgap --dfin`.

## Numbers (seed 1, default)
- 29 passes: 22 roughing, then curl, sprout, feet, Mochi face, Bolt face, gap and release.
- Pass gaps shrink 1.15 → 0.55 s, then 0.42-0.55 s for the detail passes, then 1.0 s (gap) and 1.1 s (release).
- 100% is at 22.00 s. The clip is 26.70 s (1602 frames).
- About 1570 chips and 74 shell pieces.
- 981 sound events. Events per 2 s: 44 62 63 65 71 71 81 95 102 98 117 | 104 (finale) 8. The rate climbs up to 100%.
- `CARVED` reaches 85% after roughing, 89% after the faces and 91% after the gap. The release pass carries the last 9%.

## Checks (encoded Full HD, `output/carve_reveal_fhd1_9x16.mp4`)
- h264 yuv420p 1080x1920, 60 fps, 1602 frames = 26.70 s.
- -13.98 LUFS, peak -7.47 dBFS. The last 1.0 s is digital silence. RMS per 5 s: -16.0 / -16.1 / -17.3 / -15.6 / -17.5. Energy above 3 kHz is 0.25%.
- flash_check PASS (0 flashes, mean lum 0.066).
- **Loop:** pre-encode, last frame → frame 0 is 0.40 mean against a normal step of 0.45, so it is seamless. Encoded seam 1.57 (I-frame).
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 10 / 19.0 / 20.4 / 21.6 / 22.35 / 23.6 / 25.2 s, with a 1:1 crop of the face engraving.
  - At frame 0 the corner is already being cut, the ghost faces read, and the readout shows 1%.
  - The figures' heads emerge from ~10 s.
  - The faces are engraved at ~19 s.
  - The shell pieces fall at 22.35 s.
  - The cameo is on the rail at 23.6 s.
- **Safe zone:**
  - The caption is at y 172-245, the readout at ~300-345 and the rail at 428.
  - The cameo spans y ~300-420 at x 186-286 and 762-862.
  - The block and statue sit at ≤ 1352 (0.704 h) and x ≤ 958. Only the block's right edge and the rail ends enter the 0.85 w strip, as decoration.
- Delivered `<VIDEOS_DIR>\batch40\carve_reveal.mp4`. The 4K version has not been rendered (`NF_SCALE=2.0 --label ship` after review).

## Doubts
- The first ~4 s only shave the block's top (1 → 11%). The figures' shapes appear from ~8-10 s. The hook leans on the full rainbow frame, the ghost faces, and the laser cutting with chips from frame 0.
- The release pass jumps the readout 91 → 100% in 1.1 s, because the shell is 9% of the material.
- The spiral pupils read as "hypnotised" while they are being engraved; once done they read as pupils.
- The cameo characters are small (r 50) and appear for only the last ~3 s.
- Note per pass ignores the hymn's rhythm (the dotted B-A falls on equal steps). The tune is still recognisable.

Owner review (2026-10-17): too boring -> replaced by a 3D-printer timelapse printing the characters (print_reveal).
