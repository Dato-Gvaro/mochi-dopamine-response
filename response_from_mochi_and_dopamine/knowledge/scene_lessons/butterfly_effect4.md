# butterfly_effect4 — v3 with the characters sitting at the bottom

- Built from the owner's review of butterfly_effect3 (2026-10-09): "good visuals, but the characters moving there are kind of disturbing it — let's make them sit somewhere at the bottom."
- ONLY change: v3's overlay pass. The simulation, light buffer, reveal (100 -> 1,000 -> 5,000), HUD and Moonlight Sonata soundtrack are imported from butterfly_effect3 unchanged (`v3.draw_overlays` is swapped at import; v3 stays bit-reproducible).
- Mochi and Bolt (r 30) sit side by side on a small glowing ledge at the lower left:
  - Bolt x 118, Mochi x 188, centres y 1338, ledge y 1367 with soft contact shadows.
  - Level with the label line, inside the safe zone, ≥ 100 px clear of the reach circle.
- Behaviour:
  - Eyes follow the mean tip of the 100-set.
  - WOW for 1.3 s on each count-up (bar 2 and bar 3 downbeats).
  - Happy while the cloud gathers home (collapse u 0.12-0.80), then the frame-0 smile.
  - Blinks only away from the seam. Breathing squash ±2.5 % at 10 cycles per clip (loops).
- Args: as v3 (--pose, --slow, --cap, --label, --still --frame [--warm]).
- Checks:
  - Full HD v1: h264 yuv420p 1080x1920 60 fps, 25.02 s; -14.00 LUFS, peak -2.3 dBFS, last 0.5 s -90 dBFS; flash 0 = PASS; encoded seam 0.255.
  - 4K ship: 2160x3840, same audio; flash 0 = PASS; encoded seam 0.133. Render ~75 min (sharing the CPU).
- Delivered:
  - <VIDEOS_DIR>\batch22\butterfly_effect4.mp4 (Full HD).
  - 4K staged as <VIDEOS_DIR>\Schedule\2026-10-13\1_butterfly_effect4.mp4. Owner review: pending.
- Owner review (2026-10-09): good. Scheduled for Oct 11 slot 1 (4K).
