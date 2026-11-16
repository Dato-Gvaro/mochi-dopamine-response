# spiral_roll
- New scene (batch38), from the owner's reference: CodeCraftedPhysics "What was that ending?!" (1.2M views, 59 s). We kept the mechanic and made our own look, HUD and sound. Caption (baked, `--cap`): `Every shape gets ^ONE^ try|~Only one reaches the centre~`.
- World:
  - Black stage. An Archimedean spiral track: the outer wall is r = 468 - 96·φ/2π, 3.5 bricked turns, centre (520, 868). It spans x 52-988 and y 400-1290.
  - 420 thin radial bricks (120 per turn, 62% of the 3° slot). A straight lead-in from the top-left feeds the mouth at 12 o'clock.
  - One colour per try: red-orange, yellow-green, teal, blue, violet, then gold for Mochi. The new colour refills as a 0.34 s wave from the mouth to the centre.
  - Debris: 4 shards per brick fly forward and outward with drag, life 0.45-0.8 s.
- HUD row (x 88-916, y 278-390): LINE, TRIANGLE, BOLT, HEXAGON, OCTAGON, MOCHI. The current contender gets a ring in the try colour. A red X is stamped on each failure (pop 1.25x → 1x). Mochi gets a gold ring at the win. Faces appear only on Bolt and Mochi; the other shapes are plain white with a glow and a white motion trail.

## Physics (one model, E = 1 at launch, v = V0·√E, V0 = 2200 px/s, 8 substeps/frame)
- Every contender is circumradius 38 and rolls along the OUTER wall of the track.
- Polygons rotate at v/R about the front corner.
  - At each apex the centre must be lifted from the inradius to the circumradius. That costs KC·(1 − cos(π/n)), with KC 0.030.
  - If E is less than that, the polygon can't vault the corner and rocks back: STUCK.
  - Per pixel, the corner cost is KC·tan(π/2n)/2R: line 1.00, triangle 0.58, square 0.41, hexagon 0.27, octagon 0.20, circle 0.
  - Rotating at the same rate also covers less ground per second (sin(π/n)/(π/n)).
- Bricks cost EB each (all 420 bricks = 0.6). With E < EB, the shape bounces off the brick: STUCK.
- Mochi (the circle) pays bricks only. She reaches the centre with E 0.40 left and glides into the hub in 0.30 s.
- Bolt's face is drawn on whichever side of his square is most upright at his final rest. The square is symmetric, so this is free. Mochi's face stays upright, and rotating spin arcs show that she rolls.
- s7 (deterministic; the seed only changes debris):

| Contender | Turns reached (of 3.5) | Bricks | Run | Stall (clip s) | Why |
|---|---|---|---|---|---|
| Line | 0.67 | 83 | 3.05 s | 2.50 | corner |
| Triangle | 1.18 | 144 | 3.43 s | 6.37 | corner |
| Bolt | 1.62 | 197 | 4.08 s | 10.90 | corner (annoyed, camera push-in 1.42x) |
| Hexagon | 2.33 | 283 | 5.02 s | 16.80 | brick |
| Octagon | 2.87 | 349 | 5.28 s | 22.55 | brick |
| Mochi | CENTRE | 420 | 3.71 s | reaches 26.76 | E 0.40 left |

- Finale:
  - At the centre the camera zooms 2.55x over 1.45 s.
  - A soft gold glow appears. Six colour rings bloom out, one per contender colour. The walls take a gold halo.
  - Mochi is happy and squash-bounces. Bolt slides up at the bottom-left (x 168, y 1238) with an annoyed stare.
  - At 29.6 s the clip dissolves (0.6 s) into the pre-roll, with the line on the lead-in.
- Clip 30.22 s (1813 frames). Frame 0 is the line 0.55 s after launch, already in the red bricks with shards flying.

## Sound (all synthesized; no music, no beds, no whoosh/hiss, nothing shrill)
- Brick tick: a struck bar (f, a glassy 2.76f and a 4.07f, 8-45 ms) plus a soft 1.5 ms click.
  - Notes walk the C-major pentatonic C4 → A5 as the shape goes inward, with a rolling 0-2-1-3 arpeggio.
  - Ticks are thinned to one per 52 ms or more. The gain grows with the number of bricks merged into a tick.
- Tumble thud: 120 → 68 Hz plus harmonics, thinned to one per 85 ms or more. Louder as the shape slows, so the last tumbles are heard.
- Stall: a thud plus a low two-note "aww" (D3 → A2 mallet), then a woody stamp tock on the HUD X, then a soft 5-note refill run.
- Launch: pok.
- Finale: a rolled C-major chord (C2-E5, detuned pairs, low root swell), plus a glass-harp G5 chime and Bolt's plonk.
- Onsets are at least 12 ms apart. No events in the last 1.0 s. `master(peak_db=-6)`.
- Spectrum: almost nothing above 3 kHz (0.1% even in Mochi's run).

## Flags
`--seed --label --cap --vote` ("Team Mochi or Team Bolt?" at y 1130 from reach+1.0 s; default OFF) `--still --frame N` (negative = pre-roll) `--dry --sound 0`. Physics tuning: `--v0 --kc --eb`. The render raises an error if any polygon clears the track or Mochi fails, so the escalation can't silently break.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1813 frames = 30.22 s.
- -14.01 LUFS, peak -7.9 dBFS, last 0.5 s at -64 dBFS.
- flash_check PASS (0 flashes). The first bloom measured 2 flashes in 1 s; it was calmed to 6 rings, alpha 0.55, glow 0.42.
- Seam: pre-encode -1 → 0 is 0.39 against a normal step of 0.43 (−1 → 1 is 0.55), so the loop is perfect. Encoded seam 1.63 (I-frame).
- Events per 5 s: 106 / 118 / 111 / 121 / 103 / 36 (595 sound events).
- Safe zone: the caption is at y 172-245, the HUD at 278-390, and the world is clipped to y ≥ 392. The spiral ends at 1290 (0.67h). Bolt's cameo goes to about 1300.
- Render about 2 min (Full HD).

Delivered <VIDEOS_DIR>\batch38\spiral_roll.mp4. Owner review: pending.

Owner review (2026-10-16): "needs rework" — the idea is ONE shooter that tries again and again, getting further each time until EVERY brick is gone, not six contenders each abandoned after one try. Reworked as spiral_roll2 (docs/scenes/spiral_roll2.md); the review copy batch38/spiral_roll.mp4 was removed.
