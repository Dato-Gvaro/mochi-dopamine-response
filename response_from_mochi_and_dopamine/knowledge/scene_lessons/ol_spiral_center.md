# ol_spiral_center (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). Skeleton: "rainbow brick spiral eaten to the centre" (research/early_breakouts.md), our own build: two-row brick spiral wall with a corridor, a named end state, a depth meter and a full-score note walk.
- Caption (baked, `--cap`; `--cap ''` = base): `Every brick it breaks makes it ^FASTER^|until it reaches the ^CENTER^`. Highlights in the current hue.
- Delivered: `<VIDEOS_DIR>\channel2\ol_spiral_center.mp4` (Full HD, seed 169, label fhd). No 4K yet.

## World (logical 1080x1920)
- Arena: one white circle, centre (508, 800), R 392 (x 116-900, inside 0.10-0.84 w). Gold CENTER disc r 30 with a glow that hugs it.
- Spiral: Archimedean, r = 76 + 56·φ/2π, 5.4 turns, wall = 2 rows × 11 px, corridor 32 px. Bricks 15 px long, staggered: **907 bricks**. Hue = 2 rainbow sweeps along the spiral (HSV S .85 V 1).
- Ball r 9, white with a hue trail (the path incl. bounce points, last ~0.06 s).
- HUD: depth meter y 1252 (x 170-846, rainbow fill, white ball marker, gold CENTER goal from frame 0); counter y 1478 "N BRICKS BROKEN" + "SPEED ×N" pill in the current hue; watermark "OVERFLOW LAB" 20 px, 35% alpha at (900 right, 1338). Caption/counter text has a black under-stroke so the finale shards don't hide it.

## Physics (fixed dt 1/60, substeps ≤ 2.5 px)
- Ball vs brick = oriented box, closest-point test; mirror reflection about the (summed) contact normal; arena = mirror reflection off the circle.
- Every brick touched breaks; speed ×**1.005** per brick (cap 9,000 px/s, never reached). v0 700 px/s.
- Seed = start point in the outer crescent + direction. Seed search (`--search a b`, scored on centre time 12.5-15.5 s and a monotone break rate): s169.
- Meter = depth: closest approach to the centre so far, 0 at the rim, 100% on contact with the core.

## Timeline (clip s; s169)
- Clip frame 0 = sim frame 36 (the pre-roll the loop dissolves into). Counter 6 at frame 0, first break 0.067 s.
- Breaks per second: 9, 15, 10, 25, 20, 24, 15, 15, 31, 56, 46, 68, 58, then 67 in the last 0.56 s (~120/s).
- Speed ×1.0 → ×1.2 (2 s) → ×2.1 (8.3 s) → ×4.8 (11.7 s) → **×10.2** at the CENTER.
- **CENTER hit 13.56 s** after 465 bricks. The wave (1,500 px/s) blows the other 442 out whole + 2 chips each + 28 gold core shards, with drag (τ 0.85 s), so colour hangs over the full frame; counter rolls to **907** in 0.26 s. Gold flare (no white, ≤ 0.3 s), 4 rainbow shock rings, 6 px shake.
- Hold 2.35 s → 0.6 s dissolve to the pre-roll. **16.52 s, 991 frames.**

## Sound
- **Melody:** Chopin, Étude Op. 10 No. 12 "Revolutionary", bars 1-8 (crash chords over the falling left-hand torrent), both hands = 125 score slots, read from the MIDI. Source: Mutopia "Mutopia-2018/05/15-743" (Peters/Scholtz), Public Domain; `<SOUNDFONTS_DIR>\scores\chopin_revolutionary\` + `SOURCE_mutopia_743.txt`.
- One slot per sampled break (greedy min gap shrinking 45% over the build: 6 → 13 notes/s). The run's B naturals resolve to C on the CENTER, where the étude's own final chord (bar 84, C major) sounds rolled, with strings, oohs, contrabass, timpani C3 and a boom. Strings double the RH crash chords, contrabass the low LH downbeats, timpani G2 on the bar 1/3/5 crashes.
- SFX: porcelain tick per break (3 inharmonic partials 1.25-4.3 kHz, 2 ms click, 0.5-0.8 kHz body), ≥ 12 ms apart, gain ÷ √(rate/10); burst ticks at the wave. 325 tick events. Energy > 4.5 kHz 0.08%.
- `audio.master(peak_db=None)`, `FIN_G` 2.4 (`--fin`): finale -12.8 dB RMS vs late body -15.6 (+2.8 dB). -14.01 LUFS, peak -4.8 dBFS, last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 991 frames. flash_check PASS (0 flashes).
- Seam pre-encode: last→0 mean 0.148 vs a normal step 0→1 0.136 (the loop's last frame is the predecessor of frame 0, so check_loop's "mismatch" = one step of motion, same pixel count as 0→1). Encoded 0.777 (I-frame).
- Frames read 1:1 from the mp4 at 0, 2 s, 8.3 s, the CENTER hit, burst, last.

## Flags
`--seed --label --cap --still --frame N --dry --search a b --sound 0 --sfx (0.30) --fin (2.4)`; geometry/physics `--r0 --pitch --th --tl --v0 --k --vmax --hc`. Changing any geometry/physics flag changes the sim: re-run the seed search.

Owner review (2026-10-21): "interesting" -> keep, first batch.

Owner review 2 (2026-10-22): good.

Owner review 3 (2026-10-22): "ok; if it gets successful, a sequel could be a maze like that (circle, blocks or triangular) where on the way the ball gets x2 bonus count or speed etc."

Owner review 4 (2026-10-22): ok -> Dopamine.exe schedule.
