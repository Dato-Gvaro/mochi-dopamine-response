# sandcastle_wave2 — rematch: Mochi builds a sea wall too, 2x TALLER (batch67 wave B, 2026-11-03)

- Brief: docs/BRIEF_batch67.md clip 4. New file `scenes/sandcastle_wave2.py` (copy of sandcastle_wave; the original is untouched).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch67\sandcastle_wave2.mp4` (Full HD 9:16, 14.37 s, 862 frames; label b67).
- Caption (baked): "Rematch: her wall is ~2x TALLER~" / "whose castle ~SURVIVES~?"

## THE ONE CHANGE
- Mochi copies Bolt's idea: a sea wall in front of her tall castle, but STRAIGHT and 2x as tall as his (192 px vs 96 px = 87 vs 44 cm) from about the same sand (528 vs 545 cells), so 44 px thick. Her castle is ep. 1's, moved 28 px inland (curtain trimmed to x 532). Waves, sand rules, Bolt's plot: ep. 1's.

## Physics changes (all flags/args; same rules for both walls)
- `walled(side, k)`: wave k meets a standing wall. Mochi's waves are decided at T_K[k] − 0.05 (M_WALLED); a walled wave uses Bolt's ep. 1 water model (approach clipped at the wall, pile + reflection, level capped at the crest, erosion budget × KAPPA_WALL, only cells x ≥ 540). Once her wall has fallen (crest < half its height: M_TFALL), later waves use ep. 1's run-up model over her castle.
- Water acts on both walls from x 548 (ep. 1's line for Bolt). `--faceown` (her outer 12 px only) makes her wall HOLD — but that rule cannot follow the face as it is undercut (the face x is the wall's top-right cell), so it is an artifact; the default is the honest one.
- Bolt's lane is bit-for-bit ep. 1's physics (wall 545 → 478 cells, moat 24 px).

## Result (honest)
- Waves 1-6 blocked by both walls. Mochi's wall is undercut at its foot and collapses during wave 6 (sim 8.07, clip 8.33): "HER WALL FELL!".
- Wave 7 (1.14 m) runs up over her castle: 100 → 74.5 %. Wave 8 (1.71 m, the cadence) flattens it: 0 % (keep down at sim 11.33). Bolt 100 % → BOLT WINS again.
- Sensitivity: wall thickness 40/44/48 px → topples in wave 6 every time.

## Sound
- Vivaldi, Summer RV 315 Presto "the storm" (Mutopia #336 note data, `<SOUNDFONTS_DIR>\scores\vivaldi_summer\summer-mids\summer-score-2.mid`), score bars 10-17 (violin I, violin II in canon, viola as held tremolo, cello) + our G-minor tutti on bar 18 = wave 8. Bar = 1.60 s (ep. 1's wave grid). Ep. 1 used Vltava.
- SFX as ep. 1, chord-fitted to Gm | Cm Cm | Eb Eb | Gm Gm | Gm; Mochi's walled waves get a wall thud instead of the splash; win chime G minor.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 862 frames = 14.37 s. −14.01 LUFS, peak −2.00 dBFS, last 0.5 s silent.
- RMS/s −18.6 −18.1 −18.5 −17.9 −17.7 −17.0 −16.9 −16.9 −15.7 −16.0 −15.6 −14.1 −13.9 −18.2. SFX events/s 6 7 5 6 2 11 10 7 13 7 26 17 17.
- flash_check 0 flashes. Seam 0.598.
- Frames read from the encoded files: 0.5, 2.0, 8.25, 8.45, 8.8, 10.1, 11.7, 14.2; 1:1 crops of the wall failing (8.30 / 8.40 / 8.55).

## Doubts
- Second 4 has only 2 SFX events (both walls just block small waves).
- The wall "topples" as a column of grains (the model turns a failed block into grains), not a rigid fall.
- First 2 s: small waves as in ep. 1; the hook is Mochi's "MINE'S 2x TALLER!".

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/sandcastle_wave2.py --still --frame 10,130,520`
- `NF_SCALE=1.0 python scenes/sandcastle_wave2.py --label b67` (sim ~40 s cached in output/, render ~3 min)
