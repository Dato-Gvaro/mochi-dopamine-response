# demolition_duel — Wrecking ball vs controlled demolition (batch32, 2026-10-14)

Caption: "Wrecking Ball vs Implosion" / "~First building to the GROUND wins~" (baked; `--nocap` = base).
Deliverable: `<VIDEOS_DIR>\batch32\demolition_duel.mp4` (Full HD, 9:16).

## Duel
- Two identical 12-floor concrete towers (4 blocks per floor), modern city at dusk.
- **Mochi = WRECKING BALL** on a telescopic crawler crane (coral). It is a pendulum: cable 160 px,
  g 1100 px/s^2, one hit every 1.24 s (the honest half period is about 1.33 s). Each hit takes
  2-3 blocks off the top (`KS`, 46 of 48 blocks in 20 hits). Hits 7 and 14 tip a 2-block slab off
  the far edge as a rigid pivot body (tips past 67°, free fall, shatters). Mochi leads 1.5 s → 23.7 s.
- **Bolt = IMPLOSION**: 12 charges, only on the columns of floors 0-3, placed bottom-up from a
  boom lift (one every 1.64 s). Wires run to the detonator. At 19.5 s it counts down 3-2-1, then
  12 pops bottom-up 0.09 s apart, a 0.25 s pause, and the tower drops. Each floor is crushed at
  the rubble line and the structure loses 14% of its speed per crush, with a 3° lean.
  Floor 12 is down at 23.70 s.
- Result: Bolt reaches the ground at 23.70 s. Mochi's 20th hit lands at 23.86 s and leaves
  **1 floor** (2 blocks). It is an honest last-second finish, not a fake.
- WHY on screen: floors-left counters with a LEADING/WINNER pill, hits vs CHARGES n/12, the dashed
  swing arc, the wires, and the "BOTTOM FLOORS ONLY?!" and "GRAVITY DOES THE WORK" banners.

## Hook / pacing
- Frame 0: the ball is mid-swing toward the tower face, with impact at 0.30 s. Bolt is placing
  charge 1. Both faces are visible (Mochi in the crane cab r31, Bolt in the basket r32).
- Events: a hit every 1.24 s, debris landings between them, and a charge clack every 1.64 s.
- Pattern breaks:
  - 1.5 s: -1 FLOOR
  - 4.75 s: "STILL 12 FLOORS?"
  - 7.7 s: TIPPED OVER
  - 10.15 s: BOTTOM FLOORS ONLY?!
  - 12.7 s: HALF GONE
  - 16.4 s: SLAB DOWN
  - 18.4 s: 12/12 ARMED
  - 3-2-1, then the pops, then IMPLOSION, then the win
- End: rubble settles and dust drifts, about a 1 s hold, then a 0.6 s dissolve to frame 0.
  Clip length is 26.30 s.
- v2 (coordinator): Bolt and the lift sat at x 0.93-0.99, under the Shorts button strip.
  - The world scale is now 1.0 (it was 1.12).
  - The lift is narrower and sits flush against Bolt's tower; the basket's right edge is ≤ x 918
    (0.85).
  - Bolt's radius is now 40 (it was 32).
  - The crane tracks are no longer cropped.

## Sound (no music, numpy synthesis)
- Each hit layers:
  - a steel clunk, a crack and a granular crunch;
  - a low thud with rumble, then a debris rain;
  - a whoosh into each hit and a cable creak on the backswing;
  - a rebar twang on every third hit.
- Every landing is a knock plus crunch, thinned to ≥45 ms apart.
- The slab tip is a low creak; the slab crash is heavy.
- A charge placement is a clack plus a soft sine bip (G6, C7 on the last one).
- The countdown is soft beeps plus a filtered riser.
- The 12 pops rise in pitch by 2.5% each.
- The implosion is a round sub boom (attack 12 ms), a 3.6 s rubble cascade, a crush knock per
  floor and a dust hiss.
- The bed is dusk wind, city hum and the crane's diesel idle.
- All onsets are ≥12 ms apart (`Onsets`). The last 1.3 s is silent.

## Lessons
- Every rubble chunk is stacked into a heightmap, so the piles grew too tall at first.
  `PACK=0.34` with a downhill walk (angle of repose ≈0.5) keeps the heaps low.
- Draw the ball AFTER the crane body: late hits (floors 0-1) swing in front of the tracks.

## Checks (v1, Full HD, 2026-10-14)
- h264 yuv420p, 1080x1920 @ 60 fps, 1578 frames = 26.30 s.
- Audio: -14.01 LUFS, peak -3.0 dBFS, last 0.5 s at -72 dBFS.
- flash_check: 0 flashes (mean luminance 0.061).
- Loop seam:
  - Before encoding, the last frame vs frame 0 is 0.0003 mean (a perfect dissolve).
  - After encoding, check_clip reads 0.80 and the decoded last frame vs frame 0 reads 1.12.
  - Normal frame-to-frame motion is 0.13-0.14.
  - So the post-encode number is quantisation drift of the last P-frame against the frame-0
    I-frame, not a content jump.
- Encoded frames read at 0, 0.3, 1, 2, 3, 13, 22.9, 23.7 and 25.5 s.

v2 recheck: -14.01 LUFS, peak -3.15 dBFS, 0 flashes, post-encode seam 0.73.

## Outcome
- (fill after upload)
- Owner review (2026-10-15): good -> APPROVED, 4K (Oct 17 slot 1).
