# stack_sabotage3: stack_sabotage2, made stressful

- Owner review of stack_sabotage2 (2026-10-06): "good, but has potential to get more STRESSFUL". v2 is untouched. Same look, rule, 7 unique gags, WMIN 170 top floor; the changes below.
- CLOCK: from 10.0 s a tick-tock (ratchet tick, alternating size 0.6/0.05) speeds up from 0.50 to 0.18 s apart. The timer bar turns red and its glow pulses on every tick; the seconds text turns red and pops 14%. 16 ticks before the win.
- TEETER: a block landing >= 20% off its base rocks about the supporting edge with the overhang dipping. Duration 0.40 s + 0.9*(off-0.2); angle up to 0.13 + 0.7*(off-0.2) rad. A creak on each rock, a soft thunk on settle; the slice shears off only when it settles. A teeter always ends before the next block lands. The counter does not count a block until it settles.
- FINAL BLOCK: Mochi rushes it, landing 22-29% off (scripted, the seed picks the side), so it teeters. The win counts at the SETTLE: t_win = t_drop + teeter.
- LEAN (wrecking ball, amp 150): rises over 0.42 s, FREEZES at the edge for 0.50 s (2.5 px tremble), then rights itself with a damped 0.95 Hz rock. Blocks tilt along the bent tower (slope of the cantilever curve). The tower creaks while |sway| > 40 px is rising (>= 0.22 s apart).
- PANIC: from 9.5 s to the win, Mochi's sweat ramps to 1, his face goes worried/wobbly when idle, and he trembles (2.5 px at 12 Hz). He is always worried while sway > 25 px or while riding a teetering block (he rotates with it).
- PUSH-IN: zoom 1 -> 1.07 about (610, 900) from 11.5 s to the win; it eases back to 1 in the hold. UI (caption, timer, counter, banner) is not zoomed.
- Speed 430 + 720*((k-1)/19)^1.1 px/s.
- Search: keeps wins with 0.05-0.18 s spare. Score = misses, big slices, drama after the wrecking ball, non-final teeters, minus 10x spare time.
- s435 (default):
  - Gags: plane 2.11, pebble 2.95, fan 5.64, magnet 7.11, lasso 8.50, bowling 10.40, wrecking 12.45 s.
  - The lean makes level 17 TIP OFF at 13.02 s. The retry lands 80 px off and teeters 0.5 s. Level 18 teeters too. The last block lands at 14.49 s, teeters and settles at 14.91 s: 0.09 s to spare ("with 0.1 s to spare").
  - 21 attempts. Clip 18.72 s (1123 frames). Drops/5 s: 8, 12, then 8 in the last 4.9 s. All events/5 s (with ticks/creaks): 12, 42.
- Checks (encoded Full HD): h264 yuv420p 1080x1920, 60 fps. -14.00 LUFS, peak -7.27 dBFS, last 1.3 s silent. flash_check: 0 flashes = PASS. Seam: pre-encode max 4/255 on 1 px, encoded mean 0.216.
- Args: --seed (435), --label, --cap, --melody, --search N, --still --frame.
- Delivered <VIDEOS_DIR>\batch15\stack_sabotage3.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-07: Not great, but OK to fill the upload stream (Oct 11).
