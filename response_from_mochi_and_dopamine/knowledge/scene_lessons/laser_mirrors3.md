# laser_mirrors3 — Trial & error (Mochi) vs CALCULATE (Bolt)

- Built from the owner's review of laser_mirrors2 (2026-10-08): "move the laser SLOWER so the viewer can catch up; let them each do it their OWN way (algorithms, maths, physics)." v1 and v2 are untouched; v3 imports only their pure helpers.
- Machine: v2's split chamber (a fixed laser, 3 big mirrors on ratchet gears, a crank per side). The characters are bigger (r 66). One crystal at a time; first to 5.
- BOTH halves get the SAME crystal (mirrored position, same route, mirrored start angles), so each crystal is a method duel. The crystals are planned on the left half with exact angles. Each mirror turns 9-36 deg; bounces per crystal: 1, 1, 2, 2, 3.
- Mochi = trial & error (bisection):
  - Steps the mirror 16 deg. Whenever the beam has gone past the goal (sign of the tracer's angle error flips), it reverses with HALF the step: 16, 8, 4 ...
  - Multi-bounce shots are searched one mirror at a time: first get the beam within 0.16 HL of the next mirror's hub, then the next mirror, and so on.
  - Each step draws an arc on the mirror rim plus its size label.
  - Moves run at 40 deg/s with an ease-out-back, a 0.20 s look between steps, and ratchet clicks every 3 deg. Click pitch rises with each halving.
- Bolt = calculate:
  - A dotted ghost of the predicted path is drawn first (0.60 s, one calculator blip per segment).
  - Then per mirror: a protractor, the dashed normal, the two equal in/out angle arcs with their degree labels, and a dashed ghost mirror at the computed angle (0.26 s, two blips).
  - Then ONE smooth crank (34 deg/s, at least 0.55 s) lands the mirror on its ghost, with one clean CLUNK.
- Measured over 200 seeds (mean time to aim):

  | Bounces | Mochi | Bolt |
  |---|---|---|
  | 1 | 1.04 s | 1.56 s |
  | 2 | 3.1 s | 2.7 s |
  | 3 | 5.6 s | 3.8 s |

  Trial & error wins the easy shots and calculating wins the multi-bounce ones.
- Each shatter shows "+1 / aimed in X.Xs", so the faster method per crystal reads on screen. Charging starts only at the lock; a beam sweeping over the crystal only glints it. Charge time 1.0 -> 0.75 s (a ring + a rising tone), then the shatter (a chime walking fur_elise +12, per the BRIEF rotation; the winning crystal gets a chord).
- s308 (default, BOLT wins as asked):
  - Faster aim per crystal: M, M, B, B, B (Mochi 1.02/0.52/3.28/3.14/4.56 s with 2/1/6/6/9 steps, Bolt 1.51/1.64/2.82/2.60/3.73 s).
  - Mochi is first to every crystal through the 4th (Mochi 2.02, 3.80, 8.27, 12.54 s; Bolt 2.51, 5.41, 9.43, 13.16 s). 4-4 at 13.16 s: LAST CRYSTAL! (a 3-bounce shot).
  - Bolt locks at 17.21 s, Mochi at 17.43 (after 9 search steps). Bolt wins 5-4 at 17.96 s with the only lead change; Mochi's crystal is at 72 % charge (it would finish 0.21 s later).
  - Clip 20.87 s (1252 frames).
- Sound: a bed built in the scene. The sidecar events carry only the glass crunch (note_gain 0), so check_clip shows "distinct 1"; regen_audio cannot rebuild the bed. Gains rise per crystal (blips, clunk, clicks).
- Loop:
  - After the win the lasers power down, the mirrors (nearest pi), cranks (nearest 2 pi) and eyes ease to frame 0 (reset_u hits 1.0 on the last frame), and the frame-0 crystals regrow.
  - Both characters return to the "determined" face 0.25 s before the seam (it is their frame-0 face).
  - Mochi's first step starts at frame 0; Bolt's ghost path starts at 0.08 s.
  - Pre-encode seam 0.029 (normal step 1.44).
- Checks (encoded Full HD): h264 yuv420p 1080x1920 60 fps; -14.01 LUFS; peak -5.39 dBFS; last 0.5 s -84 dBFS. Encoded seam 0.50. flash_check: 0 flashes = PASS.
- Args: --seed (308), --label, --cap ("a|~b~"), --melody, --search N (Bolt wins 5-4; per-crystal aim M, M, ..., B with >= 2 B; T 19.5-26 s), --still --frame.
- Other Bolt seeds: 572 (M, M, B, B, B, margin 0.31 s), 1286 (M, M, B, M, B, 3 lead changes, margin 0.89 s), 1484 (margin 0.22 s).
- Delivered <VIDEOS_DIR>\batch18\laser_mirrors3.mp4 (Full HD). Owner review: pending.
