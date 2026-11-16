# brick_tunnel
- New scene (batch38). A 90s-nostalgia hook: the classic arcade brick-breaker and its famous TUNNEL trick. No names, logos or assets. The pixel font is our own 5x7 glyph table.
- Rule: "Every brick it breaks makes the ball FASTER". Caption (baked, `--cap`): `Every brick it breaks makes the ball ^FASTER^|~Smash or TUNNEL?~`.
- Choice:
  - MOCHI · SMASH: every shot aims at the lowest brick, middle first, so she clears the wall bottom-up, one brick per shot.
  - BOLT · TUNNEL: he digs his left (inner) column. Planner score: 10 per tunnel brick, -3 per column-1 brick, -1 per other, so the tunnel stays narrow. Once the column is open, every shot is the one his forward prediction says breaks the most bricks.
- World:
  - One CRT cabinet screen (x 48-918, y 412-1360): scanlines, vignette, glare.
  - Two playfields, each 400 wide: Mochi x 62, Bolt x 502. Coral and teal neon frames, open bottom.
  - Wall: 8 x 6 rainbow neon bricks (50 x 28) at y 520-688, with a 90 px gap under the ceiling (y 430).
  - Each character balances its paddle (120 x 14, top y 1185) on its head. Eyes track the ball.

## Physics (identical for both)
- The ball is a square (half-size 8), launched at 1500 px/s, ray-cast exactly. It reflects off walls, ceiling and bricks; the axis comes from the entry face.
- Every brick: speed x1.025.
- Paddle:
  - The angle depends only on where the ball hits: angle = offset x 60 deg (offset -1..1); speed is kept.
  - Top speed 900 px/s, reaction 0.07 s after the ball turns down. Aim error is offset σ 0.035.
  - The AI plans from the exact landing prediction and picks only reachable offsets. If none is reachable it is "forced" (edge catch or miss).
- While Bolt's ball is above the wall he parks under the tunnel exit.
- Outcomes:
  - The ball passing the paddle line and leaving the field = GAME OVER.
  - First wall cleared wins.
- Seed search: `--search N --from S`.
  - Filter: Bolt wins, biggest single trip ≥ 18 bricks (`--minbig`), the loser misses within 2.2 s of the clear, clip 15-20 s.
  - Under the defaults, good seeds of 500 are 53, 229, 271, 466.
  - Tuning flags: `--v0 --grow --vp --react --aimsig --gap --rows --bh`.

## s53 (default), clip times
- Opening:
  - Mochi's ball is in flight at frame 0; her first brick breaks at 0.10.
  - Bolt launches at 0.03; his first tunnel brick goes at 0.38.
  - Bricks then break about every 0.3 s per side.
  - Mochi leads 38-41 at 4.9 s.
- Tunnel:
  - It opens at 4.40 (row-0 brick).
  - The ball gets above the wall at 5.17: TUNNEL!
  - CHAIN of 31 bricks from 5.3 to 7.8, about 0.1 s apart, with the ball speed going x1.25 → x2.56.
  - BOLT LEADS! at 5.6.
- Late game:
  - SAVED! at 8.33: a forced edge catch at offset 0.90 with the ball at x2.62.
  - x1.5 SPEED! (Mochi) at 9.3, x3 SPEED! (Bolt) at 10.9, x2 SPEED! (Mochi) at about 12.8.
  - Bolt's last 7 bricks go one or two per shot.
- Ending:
  - CLEAR! plus a 34-shard shower; BOLT WINS! and confetti at 12.78. Bolt cheers.
  - Mochi's x2.26 ball beats her paddle at 14.51 (edge -1.17). Her paddle fades.
  - Pixel GAME OVER falls on her head; bonk at 15.44.
  - She is dizzy, then gives an annoyed stare at Bolt. Bolt laughs (HA HA).
- Clip 17.00 s (1020 frames). The last 0.6 s dissolves into the pre-roll, which leads into frame 0.

## Sound (no music, no beds, no whoosh/hiss; everything synthesized here; mid/low register)
- Brick blip: a rounded soft-triangle tone with a tiny onset pitch blip, 65 ms decay.
  - Pitch per row walks up C-major pentatonic: violet bottom G3 → red top G4.
  - The cascade is a ping-pong pentatonic arpeggio, G3 to C5 and back.
- Paddle: a low bop (about 135 Hz with a drop) plus a faint click. Walls and ceiling: quiet tok (520 / 470 Hz).
- SAVED: a two-note lift. LEADS: a two-note lift.
- CLEAR: an arpeggiated C major chord plus a sub, 1.3 s.
- GAME OVER: a soft descending G3-Eb3-C3 motif. Bonk: a hollow wooden drop.
- Spectrum: 51% below 200 Hz, 48% 200-800 Hz, 0% above 2 kHz.
- Onsets ≥ 12 ms apart. `master(peak_db=-6)`. No events in the last 1.0 s; the tail fades over 0.6 s. 246 sound events.

## Flags
`--seed --label --cap 'a|~b~' --vote` (Team Mochi or Team Bolt? plus a drawn arrow at y 770, x 102-862, from win+0.6 s to the dissolve; default OFF) `--still --frame N` (-36..nf-1) `--dry --sound 0 --search`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1020 frames, 17.00 s.
- -14.00 LUFS, peak -8.0 dBFS, last 0.5 s at -56 dBFS.
- flash_check PASS (0 flashes; mean luminance 0.017).
- Seam:
  - Pre-encode, last → 0 is 0.102 against a normal step 0 → 1 of 0.102. The last frame is identical to pre-roll frame -1, so the loop is perfect.
  - check_loop prints MISMATCH because it compares last to 0 (same as edge_slide).
  - Encoded seam mean 0.60.
- Events per 5 s: 60 / 137 / 49. The only gap over 0.45 s is the GAME OVER fall (0.88 s).
- Safe zone:
  - Caption y 200-290. Labels y 378. Play content y 430-1345 (≤ 0.70h).
  - HUD (BRICKS LEFT / BALL SPEED) y 1390-1490 (≤ 0.78h).
  - Nothing important at x > 918; only the decorative bezel reaches 940.

Delivered <VIDEOS_DIR>\batch38\brick_tunnel.mp4 (no vote). Owner review: pending.

Owner review (2026-10-16): approved -> 4K (after spiral_roll2 + 2 new research videos are delivered).

Owner review (2026-10-16): APPROVED. Shipped in 4K with the vote banner ON (A/B arm) to <VIDEOS_DIR>\Schedule\2026-10-21\1_brick_tunnel.mp4.
- Render: `NF_SCALE=2.0 --seed 53 --label ship --vote`.
- Encoded 4K: h264 yuv420p 2160x3840, 60 fps, 1020 frames = 17.000 s; -14.00 LUFS, peak -8.0 dBFS, last 0.5 s at -56 dBFS; flash_check PASS (0); encoded seam mean 0.42.
- Vote banner (checked on an encoded frame at 15.8 s): x about 100-865 (<= 0.85w), y about 720-790. It sits between Mochi's remaining bricks and BOLT WINS!, so no face is covered (faces are at y 1200-1290).
