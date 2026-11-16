# galaxy_collision4 — galaxy_collision3 without the centre rings (batch28 / ship)

Owner review of galaxy_collision3 (2026-10-11): "PERFECT, but when, time after time, that circle comes from the centre, it doesn't fit — remove that. If it needs some effect, you can leave that boom effect."

## Changes vs galaxy_collision3 (everything else identical)
`scenes/galaxy_collision4.py` imports galaxy_collision2 and galaxy_collision3, and reuses gc2's sim cache and music grid.
- **No rings at all.**
  - Removed: the ring light, the lensing, and the camera kicks of the later rings.
  - Also removed: the ring-triggered starburst knots, which drew a circle of pink knots.
  - The starbursts are now the compression/overlap ones only: same rule, same seed, cached in `output/galaxy_collision4_knots.npy`.
- **Drop boom (4.96 s), no circle.**
  - A core flare: +3.2 on the kick-throb channel with a 0.35 s decay, so both cores and their bloom swell, about x2.4 heat.
  - The camera kick (7 px, decays in about 0.12 s).
- **Merger (28.13 s).** A soft glow swell of the cores (rise 0.25 s, decay 1.2 s). No ring.
- Music, sync, hook, loop, caption, characters and the "ONE GALAXY" sticker are unchanged from gc3.
  - Track: Egzod, Lost Sky, Alaina Cross, "Fight In Me" [NCS Release], 1:31.066 → 2:02.505.
  - **The description must be `<VIDEOS_DIR>\music\Fight In Me\Description Text.txt` verbatim.**

## Checks
- **4K ship file** (`--label ship --par 3`, NF_SCALE 2.0, ~85 min on the shared machine): h264 yuv420p 2160x3840 at 60 fps, 1886 frames = 31.43 s, 279 MB.
  - Audio: -14.02 LUFS, peak -8.14 dBFS, last 0.5 s -240 dBFS.
  - flash_check: 0 flashes, PASS.
  - Seam mean delta 1.05.
- **Mux gotcha.** `studio.mux_audio`'s `-shortest` dropped 3 frames at 4K (1883 frames). The audio was re-muxed without `-shortest` to restore 1886.
- **Full HD review copy:** a lanczos downscale of the 4K file (crf 18, audio copied), 1886 frames, -14.02 LUFS, flash PASS.
- Encoded frames read at 0, 4.96, 5.2, 10, 28.13 and 28.5 s: no rings anywhere. The drop shows only the core flare and the kick; the merger shows a glow swell, the bump and "ONE GALAXY".
- Delivered:
  - `<VIDEOS_DIR>\batch28\galaxy_collision4.mp4` (Full HD)
  - `<VIDEOS_DIR>\Schedule\2026-10-14\1_galaxy_collision4.mp4` (4K)
