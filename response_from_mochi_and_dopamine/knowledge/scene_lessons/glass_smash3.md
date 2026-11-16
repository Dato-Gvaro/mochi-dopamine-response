# glass_smash3 — 100 tiny panes, both balls fast (batch35, 2026-10-15)

- **Owner review of glass_smash2:** "smaller glass and much more; the big ball is moving very slow, make both faster". New file; glass_smash2 is untouched.
- **Look:**
  - 100 panes per lane at 34 px per 1 m gap, so about 25 are visible ahead of the ball. The camera point is x 230.
  - Panes are 190 px tall, oblique depth (22, -14), 1.2→4.5 px thick. Every 10th pane is numbered.
  - Balls: marble r 13, steel r 28. Shards per break: 5 + k/20, size 4-8 px; 70 shards in the final burst.
  - The floor chevrons flow at 1.6 m/s.
- **Physics:** same model as glass_smash (equal push, momentum shared with the shard plug, cracks weaken a pane by w × the absorbed energy). Retuned for speed and 100 panes:
  - F 0.990 N; E 0.037 → 2.78 J (power 2.48); w 2.59; e 0.656; shard mass 1.7 → 3.0 g.
  - Marble 20 g at 21.6 m/s (42 m/s at frame 0 after the push). Steel 1 kg at 3.0 m/s → 9 m/s.
- **Race (clip time):**
  - Marble: about 20 panes per second for the first 2 s, 58 panes by 3 s. It bounces at 4.2 s; every pane takes 2 hits from 5.1 s, 3 hits from 11.2 s.
  - Steel: 3 → 9 panes per second.
  - Banners: STEEL CATCHING UP! 7.7 · ONLY 10 PANES AHEAD! 10.9 · NECK AND NECK! 12.7 · LEAD CHANGE! 13.0 · STEEL BALL WINS! 14.34 (pane 100). The marble ends at 95 panes and later sticks on pane 96.
  - Length 16.25 s (975 frames). Pre-roll / dissolve 0.40 s.
- **Label:** the steel says "1 kg · heavy" (coordinator 2026-10-15: never label it slow).
- **Sound:** same palette.
  - Every contact (ping, thunk, ting) and every shatter is ducked by 1/sqrt(n/1.5) for n shatters within ±0.2 s.
  - The rumble is scaled to the steel's new speed range.
  - The loop fade is 1.1 s (power 2.2). With 0.64 s the last 0.5 s peaked at -8.7 dBFS.
- **Checks** (encoded Full HD):
  - Video: h264 yuv420p 1080x1920 60 fps.
  - Loudness: -14.03 LUFS, peak -7.40 dBFS, last 0.5 s peak -17.3 dBFS.
  - flash_check: 0 flashes, PASS.
  - Seam mean delta 6.28, the same as a normal frame step (both cameras scroll).
  - Frames read at 0, 0.5, 1, 3, 8, 13, 14.5 and 16.1 s.

Owner review (2026-10-15): "ok maybe good, let's try to ship" -> 4K Schedule/2026-10-18 slot 3 (no vote: A/B control).
