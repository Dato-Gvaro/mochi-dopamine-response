# mandelbrot_dive3 — the x1,000,000,000,000 dive as ONE continuous zoom (no jumps)

- **Why:** owner on dive2 (2026-10-11): "at 11 seconds we have a jump to another view — we must ZOOM, not jump from scene to scene." dive2 skipped copy #1's dark neck with two cross-dissolves (3.6-4.5 s and 11.25-12.0 s), which read as cuts.
- **What it reuses:** new file `scenes/mandelbrot_dive3.py`; dive2, v1, lib/ and tools/ untouched. Same cached plane (`output/mandelbrot_dive_cache/`), same palette, overlays and Lacrimosa arrangement + sync as dive2 (docs/scenes/mandelbrot_dive2.md).

## One camera
Depth D(t), roll(t) and centre offset pan(D) are all smooth (monotone Hermite). There are no dissolves and no skips; the only direction change is one smooth turn.

| t (s) | music | camera |
|---|---|---|
| 0.00 | bar 3 "La-cri-mo-sa" | frame 0 = the final copy at x1T (payoff) |
| 0-2.8 | | zoom OUT fast through the deep spirals: ~2.9 ln/s, ~130 deg/s unwinding roll |
| 2.8-7.5 | bar 4 at 4.5 | still zooming out, slowing (1.6 -> 0.6 ln/s) through copy #1's rainbow "shoulder" (camera swung off-centre) |
| 7.5-9.0 | | the camera swings back on-centre, copy #1 slides in and rolls upright |
| 9.00 | bar 5 "qua" (choir re-entry) | "a copy?!": the zoom-out turns around (x207k) |
| 11.25 | "ex" | "...keep diving": back in at ~1.1-1.3 ln/s, copy #1 slides off over the camera's shoulder |
| 13.5 / 18.0 / 22.5 | bars 6 / 7 forte / 8 | deep spirals at ~1.0 ln/s, hue steps, ~36 deg/s roll |
| 24.92 | climax tutti | the final perfect copy, halo, "a PERFECT copy of the whole set!" |
| 26.25 -> end | A major chord, silent tail | eases to the end view (= frame 0) |

## The neck, crossed continuously
- **Problem:** centred on the target P, copy #1's cardioid and 2-bulb fill 55-87% of the frame at real depth 14.4-16.8 (the dull v1 stretch).
- **Offset search:** a search over centre offsets (magnitude 0-1.6 frame widths x 16 directions x 4 rolls, D 12.4-18.4, inside fraction at low res) found the open side of the cusp at c-plane angle ~120-150 deg.
  - Offset 1.0 w: 0-5% dark, worst 19-24% at D 16-16.4.
  - Offset 1.4-1.6 w: 0-0.7% dark everywhere.
- **Pan path q(D)** (frame widths, c-plane):
  - Copy #1 centred up to D 12.6.
  - 1.0 at 135 deg (13.6), 1.5 at 135 deg (14.4), 1.5 at 130 deg (16.8), 1.0 at 115 deg (17.6), 0.5 at 95 deg (18.4), 0 at 19.6.
  - The zoom's fixed point stays P; the offset is a constant fraction of the width at each depth.
  - Samples ~2.7 widths from P land ~3 px apart in the cached map: slightly soft, only in this stretch.

## Photosensitivity (one continuous zoom flashes more than a dissolve)
- **First attempt failed:** the continuous path with dive2's timing (fast rewind ~8 ln/s and plunge ~2.8 ln/s through the neck) measured 7 and 5 flashes/s (Full HD ranges).
  - The shoulder terrain has broad bright/dark rainbow bands that flip the 32x18 flash cells when zoomed fast.
- **Fix, keeping it one continuous zoom:**
  1. **Restructure:** zoom OUT to copy #1 and back IN, instead of rewind-to-the-start + plunge, so both neck legs are slow (~1.1-1.6 ln/s). The cold open is only the deep-spiral part (~2.9 ln/s, which passed in dive2).
  2. **Local luminance flattening** in D 12.9-18.8 (soft edges):
     - The 46 px low-passed luminance is pulled toward the frame mean, k = 0.35, by a smooth per-pixel gain.
     - Hue and filament detail are kept; only the broad brightness swings are compressed.
     - `--flatk` (1 = off).
- **Fast estimator** (scratch, not in the repo): the scene pipeline at 0.5 scale + overlay bands -> 32x18 cells -> flash_check's event logic. Calibrated on Full HD ranges: 9 vs 7 measured, 5 vs 5. With the fix it estimated worst 2/s for 0-10 s and 10-17 s.

## Checks (encoded Full HD, label v1 = the delivered clip)
- **Format:** h264 yuv420p 1080x1920, 60 fps, 29.65 s (1779 frames); AAC 48 kHz stereo. 285 MB.
- **Audio** (identical bed to dive2, fingerprint f2210329...): -14.01 LUFS, peak -4.66 dBFS, last 0.5 s -80.8 dBFS. Onsets on the visual keys.
- **flash_check: PASS**, 17 flashes, worst 2/s (0.88 s).
- **Continuity proof:** mean |frame-to-frame delta| over the picture (HUD rows excluded, 108x192 decode).
  - Median 9.4, p95 24.4, max 30.5. The max sits in a smooth 0.3 s plateau at 4.2 s (fastest zoom-out + pan), not a one-frame spike.
  - Former dissolve windows: 3.3-4.8 s median 24.6 / max 30.5; 11.0-12.7 s median 12.2 / max 17.1.
- **Frames read (encoded):**
  - Every 0.25 s over 3.5-4.75 s and 8.5-12.5 s (the former transition points and the turn).
  - Also 0, 0.25, 0.5, 1, 2, 3 s, mid (14.8 s), climax (24.92 s) and the last frame.
  - All one continuous zoom, all colourful. Copy #1 slides in at 7.5 s, holds upright 8.5-11 s, and slides out over the shoulder at 11.75 s.
- **Loop seam:** pre-encode 0.06 mean; encoded 2.49 (crf noise on dense detail, as dive2).
- **Render:** 36 min Full HD (--procs 6, shared machine). 4K: ~2.5-3 h, --procs 3-4, ~1 GB.

## Doubts
- Frames 0-9 s zoom OUT (from the payoff back to copy #1), and only then does the dive go in. It is one continuous camera with a single smooth turn, but the first third runs in reverse.
- The shoulder stretch (D 12.9-18.8, both ways) is flattened in brightness (k 0.35) and slightly soft (cached map sampled off-axis). It reads a little calmer and less contrasty than the deep spirals.
- Music unchanged from dive2: same tempo, half cadence and score-provenance note.

- **Delivered:** <VIDEOS_DIR>\batch27\mandelbrot_dive3.mp4 (Full HD). Owner review: pending.
- Owner review (2026-10-11): good -> APPROVED, 4K.
- **Owner (2026-10-11):** "ok I guess it's good" -> shipped in 4K.
  - NF_SCALE 2.0, label ship, `--procs 3 --chunks 150`. Resumable: 150-frame chunk mp4s are skipped when complete, then stream-copy concatenated. Added after a PC shutdown killed the first 4K run.
  - 3 h 27 min on a busy machine.
  - 2160x3840 h264 yuv420p 60 fps, 29.65 s, 823 MB. -14.01 LUFS, peak -4.66 dBFS, last 0.5 s -80.8 dBFS. flash_check PASS (worst 2/s). Encoded seam 2.07.
  - Frames 0 / 9 / 24.9 s read.
  - Staged: <VIDEOS_DIR>\Schedule\2026-10-13\1_mandelbrot_dive3.mp4 (mp4 only).
