# galaxy_collision3 — two galaxies meet and SHARE their stars (batch27)

Owner review of galaxy_collision2 (2026-10-11): "PERFECT — but instead of stars kept, let's make it not about competition but about SHARING; remove the numbers."

## What it is
`scenes/galaxy_collision3.py` imports `galaxy_collision2` and changes only two hooks: `Renderer.stars` and `draw_hud`.
- Physics, visuals, camera, music, beat sync, hook and loop are identical to galaxy_collision2.
- It reuses the same sim cache (`output/galaxy_collision2_simcache_*`) and the same music-grid cache.
- **Caveat:** an edit to galaxy_collision2.py changes this scene too. Copy the file first if gc2 must change.

## Changes vs galaxy_collision2
- **Star colour = sharing.** A star keeps its ORIGIN colour (coral = Mochi's galaxy, mint = Bolt's) while it is bound to its own core.
  - Once it is shared (bound to the other core, or set free between them), it turns warm GOLD `(1.0, 0.80, 0.40)`.
  - The weights come from gc2's eased ownership mix, so stars change colour over about 0.3 s.
  - While crossing over, a star sparkles: brightness x(1 + 2.0·4w(1−w)). The exchange shows along the bridge and the tails.
  - The merged galaxy ends as a coral + mint + gold blend. The colours freeze at the merger, as before.
- **No numbers.** The counts, the "STARS KEPT" label, the lead-change banners and the winner/loser reactions are removed.
  - Caption: "Two galaxies meet" / "~and SHARE everything~".
  - After the merger, a gold "ONE GALAXY" sticker pops in.
- **Characters** (r 30, bottom):
  - Their eyes follow their own core.
  - "Wow" through the rewind and around the first pass (drop ±1.3 s), then happy.
  - They slide together over the 0.55 s before the merger and BUMP on the merger beat: they lean in, squash, and a gold 8-ray sparkle (a high-five) bursts between them.
  - Both then hop happily, side by side.
  - Positions and the bump clock are functions of the forward frame, carried across the seam, so the rewind and the loop are exact.
- **Music:** unchanged.
  - Track: Egzod, Lost Sky, Alaina Cross, "Fight In Me" [NCS Release], 1:31.066 → 2:02.505.
  - Sync: first pass + shockwave on the drop at 4.96 s; merger + bump + "ONE GALAXY" on bar 14 at 28.13 s.
  - **The video description must carry the NCS credit text** (`<VIDEOS_DIR>\music\Fight In Me\Description Text.txt`):
    ```
    Song: Egzod, Lost Sky, Alaina Cross - Fight In Me
    Music provided by NoCopyrightSounds
    Free Download/Stream: http://ncs.io/fightinme
    Watch: http://ncs.lnk.to/fightinmeAT/youtube
    ```

## Hook
Frame 0 = the blended merged galaxy (coral + mint + gold), with the two cores glowing together, Mochi and Bolt side by side and happy, and "ONE GALAXY". It then rewinds to two clean spirals already touching.

## Args
`--cap`, `--label`, `--still --frame a,b`, `--par N`, `--silent`, `--mux-only`. Everything else passes through to galaxy_collision2's args.

## Checks (Full HD v1)
- Format: h264 yuv420p 1080x1920 at 60 fps, 1886 frames = 31.43 s.
- Audio (muxed mp4): -14.02 LUFS, peak -8.14 dBFS, last 0.5 s -240 dBFS (silent from 30.13 s).
- flash_check: 0 flashes (mean luminance 0.018), PASS.
- Loop seam: encoded mean delta 1.52, against ordinary steps of 1.3-1.9 on this star texture. Pre-encode, frame 0 = the last frame's state.
- Encoded frames read at 0, 0.25, 0.5, 1, 2, 3, 4.97, 10, 18.25, 27.8, 28.2, 28.35, 28.5 and 30.5 s.
  - Gold shared stars show on the bridge and the tails.
  - At 28.2-28.5 s: the bump, the sparkle, "ONE GALAXY" and the merger ring.
- v1 fix: the high-five sparkle first sat on the faces. It was moved above the heads.
  - Frames 1507-1885 were re-rendered (from the keyframe at 1507) and stream-spliced onto frames 0-1506.
  - Join deltas are 4.00 and 4.15, against 3.5-4.1 for the neighbouring steps.
- Delivered: `<VIDEOS_DIR>\batch27\galaxy_collision3.mp4`. Owner review: pending.
- Owner review (2026-10-11): perfect, but remove the shockwave circle that keeps coming from the centre time after time (first at ~5 s); the first boom effect may stay if needed -> fix + 4K.
