# ol_starry_scramble (DopamineEXE, batch64 #3)

## v1 (2026-11-01)
The Starry Night (Van Gogh, 1889, PD) as 123 × 123 = 15,129 glossy dots in a thin white square. Every FOLD is Arnold's cat map, (x, y) → (2x + y, x + y) mod 123, animated as its two shears with wrap-around (each column slides down by its index, then each row slides right by its index). Folds 1-3 read as slanted copies, then static and diagonal stripes; at fold 10 the painting appears UPSIDE DOWN; at fold 20 every dot is home. **9.95 s, 597 frames, perfect loop** (after the hold, fold 1 starts again and the last frame leads into frame 0).

- Caption (baked; `--cap ''` = base): `Every fold ^SCRAMBLES^ the painting…|until it ~COMES BACK~`. True: every fold permutes the dots; after 20 it is exactly the original (checked in code, `back exact True`).
- Chips: "fold = stretch, then wrap around" → "Arnold's cat map: back after 20 folds"; "UPSIDE DOWN?!" on fold 10 only because A^10 ≡ −I (mod 123) was verified (the grid equals the 180° rotation about cell 0, exact). Counter pill "×2.6 STRETCH" = (3+√5)/2, the map's true stretch per fold.
- Truth over brief: folds 17-19 read as diagonal stripes, not static (A^18 = A^−2 is a small shear); captions don't claim noise there.

## Model
- Image: Commons "Van Gogh - Starry Night - Google Art Project.jpg" (1280 px, PD-Art), `assets/starry_night/` (+ SOURCE.txt). Square crop x 120-1134, Lanczos to 123², HSV: S × 1.3 (cap 0.80), V → 0.22 + 0.8 V (the cypress stays visible on black). No museum name on screen.
- N choice (period ≤ 30, dots ≥ 6 px in 756 px): 84→24, 88→30, 89→22 (−I at 11), 96→24, 101→25, 116→21, 122→30 (−I at 15), **123→20 (−I at 10)**, 124→15. 123 = most detail + an exact upside-down mid-payoff.
- Dots: raster per frame in numpy (cell 6.15 px, radius 0.44 cell, radial shade + highlight), the shear = per-column / per-row fractional shift with wrap, smoothstep within each half-fold.
- Fold durations 0.42 → 0.30 s (rate climbs), +0.45 s hold on the upside-down fold; frame 0 = 10% into fold 1.

## Timeline (from frame 0)
- Folds land 0.38, 0.79, 1.20, 1.60, 1.99, … 3.87 (**fold 10: upside down**, held) · 4.68 … 7.31 · **7.61 s fold 20: back** (gold frame, shimmer sweep, chime + F-minor cadence) · hold · 9.85 s fold 1 begins again → loop.

## Sound
- Satie, Gnossienne No. 1 (publ. 1893, PD), Mutopia MIDI (`<SOUNDFONTS_DIR>\scores\satie_gnossienne1\SOURCE.txt`). One melody note per fold (its 20 first melody notes, grace notes kept, an octave down + cello 2 octaves down); left hand + chords time-warped onto the folds. Return = rich F-minor chord (strings, piano, harp roll, celesta, soft timpani).
- SFX: soft glassy tick per shear (F-minor pentatonic, +14 ms off the notes), warm chime on the return. 41 events.

## Checks (encoded, output/ol_starry_scramble_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 9.95 s; **-14.00 LUFS**, peak -6.07 dBFS, last 0.5 s digital silence; flash_check PASS (0); loop seam mean |Δ| 10.0 = the natural per-frame motion of the shear (9.8-10.9 at frames 0-2 / 594-596): seamless.
- Side safe zone: square + frame x 124-892 (0.115-0.826w), content ≤ 1211 px (0.63h).
- Stills read at 0, 1, 4, 7, 7.5, 9.9 s; 1:1 crop at 8.3 s (dots, swirl detail).

## Flags
`--n` (123), `--cropx` (120), `--label`, `--cap`, `--still --frame`, `--dry`, `--audio`, `--sfx`, `--sound 0`.

## Upload draft
- `Every fold scrambles the painting… until it comes BACK 🎨 #satisfying #physics #shorts`
- `We scrambled a famous painting 20 times. It came back 🎨 #satisfying #physics #shorts`
- `Stretch, fold, repeat: the picture returns by itself 🎨 #satisfying #physics #shorts`
- Pinned: `it was upside down at fold 10 and pure stripes at 18. how does it come back?`

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/ol_starry_scramble.py --label k4ship` (defaults) → `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-11\2_ol_starry_scramble.mp4`. h264 yuv420p 2160x3840 @60, 597 frames 9.95 s; -14.00 LUFS, peak -6.07 dBFS, last 0.5 s silent; flash PASS (0); seam 10.4 (natural shear motion, as FHD); events json bit-identical to fhd. Frames read at 1.0 / 9.5 s. FHD review file → `archive\ol_starry_scramble_fhd.mp4`.
