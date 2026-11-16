# print_reveal
- New scene (batch41). It reworks carve_reveal after the owner's review (2026-10-17): "too boring — what if we switch to a 3D printer instead and see a fast timelapse of a 3D model generating these characters?"
- It is the **CHARACTER side** of the A/B test: the print IS Mochi & Bolt.
- carve_reveal is untouched. The statue geometry is copied from it, with Bolt's sprout standing a little taller so its tip is the last layer.
- Caption (baked, `--cap`): `Every layer builds it a little ^HIGHER^|~Until THEY appear~`.
- Readout at y 326, anchored at x 300: `LAYER n/69` plus a small `n%`.
  - On the last 3 layers it reads `ALMOST!` in gold, and the number pulses.
  - At 100% the number is gold.

## World (logical px)
- **Model:** the statue silhouette (Mochi r 195 with her curl, Bolt with his sprout, a 44 px gap, the plinth), extruded 56 px deep.
  - It is shown in a 3/4 oblique view: depth goes up-right at (0.42, −0.55) per px.
  - Each screen pixel shows the first printed point along its depth ray (20 depth steps). Faces are lit by type: front, top (lit, with infill hatching) and right side (shaded).
  - Front faces show FDM layer lines.
  - Hue follows the layer (red at the bed → violet/pink at the sprout, with an odd/even shift).
  - Fresh filament glows white-hot and cools over ~0.2 s, and a soft halo hugs the print.
  - Faces (eyes, spiral pupils, smiles) are engraved on the printed part of the front.
- **Printer:**
  - Two Z posts at x 30 and 1050, plus a top bar at y 452.
  - The X beam rides at the current layer − 70.
  - A carriage with a spinning fan, a heat break, a heater block and the nozzle tip, with an extrusion glow while it lays filament.
  - The bed is a dark plate with a faint grid, plus a front LED strip that glows warm at the finale.
- **Ghost:** above the print line, the finished model shows faintly in its own rainbow (alpha 0.22, `--ghost`), with a white outline, a back outline and the faces. The end state is readable at frame 0.

## Mechanic (honest layer-by-layer growth)
- **Layers:** 69 layers of 7.74 px, from the bed (y 1352) to the sprout tip (y 818). Each layer is the model's real cross-section at that height: one island per run of the silhouette across that layer's rows.
- **Tool path per island:** the perimeter loop first, then a zig-zag infill across the depth, spaced 8 px. Islands are joined by rapid travel, and the direction alternates each layer.
  - Every (x, depth) cell gets its filament when the nozzle reaches it on that path.
  - The nozzle position comes from the same path, so what is drawn is what is printed.
- **Frame 0** is mid-print: the plinth (8 layers = 15%) is done and still glowing, layer 9 (the feet) starts at 0.02 s, and the nozzle is moving.
- **Timelapse:** each layer's time is a geometric base, 0.46 → 0.19 s, × (0.6 + 0.4 · path length / median), clamped to 0.15-0.62 s.
  - The head layers (curl and sprout) are short, so they fly by.
  - The last 3 layers (sprout leaves and tip) hold 0.26 s each (`ALMOST!`).
  - 100% is at 18.18 s.
- **Count:** `n%` = printed cross-section volume / total.
- **Finale:**
  - The head parks up-left.
  - The bed light glows.
  - The rainbow statue brightens, with a gloss and one slow diagonal light sweep clipped to the model.
  - Sparkles land on the chimes.
  - A gentle 1.07x zoom eases back before the dissolve.
  - At +1.15 / +1.35 s the real Mochi (proud: hop, ^^ eyes, grin, looking at her statue) and Bolt (embarrassed: worried brows, wobbly mouth, sweat, blush, looking away) pop up on the top bar.
- **Loop:** a 0.6 s dissolve into the pre-roll (layer 8 being printed) leads to frame 0.

## Sound
- **Melody:** Beethoven, *Ode to Joy*, bars 1-16 (62 soprano onsets, D4-D5).
  - **Source:** Mutopia Project id 528 (SATB hymn, Public Domain), `<SOUNDFONTS_DIR>\scores\beethoven_ode\ode.mid`. It is read at runtime with `orc.read_midi` and asserted equal to the verified list.
  - One note sounds at the start of each of layers 9-69 (61 notes). Note 62, the cadence G4 over G2, lands exactly on 100% with a rolled G chord on piano, a strings swell, oohs and a soft timpani.
  - Voicing: soprano on piano, the MIDI's bass on a softer piano, inner voices as a quiet strings_slow pad.
  - Note gaps run 0.48 → 0.15 s, then 0.26 s on the last three layers.
- **Stepper "printer music":** a soft tone (sine with 2nd and 3rd harmonics and a light 9 Hz flutter). Its pitch follows the nozzle speed and stays in tune with the harmony:
  - On the perimeter it plays the bass of the current Ode note, folded into C3-B3.
  - On the infill it plays a fifth up.
  - On rapid travel it plays an octave up.
  - It is smoothed over 5 ms, sits on its own bus at −26 LUFS, and stops at 100%.
- **SFX:**
  - Step ticks: a clean pitched tick at 1.15-1.30 kHz, one per 330 px of travel and at least 12 per layer, so the rate follows the timelapse.
  - A soft Z-click (880 Hz tok) at each layer change, +12 ms after the note.
  - At the finale: a park tok, 16 G-pentatonic chimes (≤ G5) and two cameo pops.
  - The SFX bus is at −22.5 LUFS and the music bed at −20.
- `master(reverb 0.30, peak −6)` brings the mix to −14 LUFS, and the last 1.0 s is digital silence. There are no hiss, whoosh or whine beds.

## Flags
`--seed --label --cap --still --frame N --dry --sound 0 --peak --sfx_lufs --tone_lufs --ghost --crf`; timelapse `--d0 --d1`.

## Numbers (seed 1)
- Layers 1-8 (the plinth) print before frame 0. Layer 9 starts at 0.02 s, 100% is at 18.18 s, and the clip is 22.88 s (1373 frames).
- 1062 sound events (ticks, 61 Z-clicks, 16 chimes, pops, park). Events per 5 s: 300 / 361 / 333 up to 100%, then the finale.

## Checks (encoded Full HD, `output/print_reveal_fhd1_9x16.mp4`)
- h264 yuv420p 1080x1920, 60 fps, 1373 frames = 22.88 s.
- −14.00 LUFS, peak −7.88 dBFS. The last 0.5 s is digital silence (the last 1.0 s by construction). RMS per 5 s is −16.4 to −16.9. Energy above 3 kHz is 0.12%.
- flash_check PASS (0 flashes, mean lum 0.065).
- **Loop:** pre-encode, last frame → frame 0 is 0.24 mean against a normal step of 0.27, so it is seamless. Encoded seam 0.66 (good band).
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 9 / 15.5 / 17.8 / 18.6 / 20.5 s. An HD still at 8.3 s showed the glowing top layer with infill hatching and front layer lines.
- **Safe zone:**
  - The caption is at y 172-245, the readout at ~300-345 and the top bar at 452.
  - The cameo spans y ~330-445.
  - The model, bed and LED strip sit at ≤ y 1362 (0.709 h).
  - The extruded right side reaches x ~938. The right Z post (x 1050) and the beam ends sit in the 0.85 w strip as decoration.
- Delivered `<VIDEOS_DIR>\batch41\print_reveal.mp4`. No 4K version yet (`NF_SCALE=2.0 --label ship` after review).

## Doubts
- At frame 0 only the plinth is printed (orange). The multi-hue comes from the faint rainbow ghost of the finished model; a real FDM print would not show this.
- The infill zig-zag is at timelapse speed, so the nozzle reads as a fast wiggle and the hatching on the top face is subtle at phone size.
- The stepper tone is a continuous soft tone (the "printer music" feel the owner asked for). If it reads as a drone, lower `--tone_lufs` (−26 now).
- Events per 5 s peak in the middle (361) and hold 333 on the fast head layers; they do not climb strictly.

Owner review (2026-10-18): dropped.
