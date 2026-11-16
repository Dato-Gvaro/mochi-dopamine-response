# mb_iceberg_sample: "Mochi & Bolt vs The Iceberg" (16:9 long-form SAMPLE)

Brief: docs/BRIEF_iceberg_sample.md. Review: <VIDEOS_DIR>\MochiAndBolt\review\iceberg_sample\.

## Build
- Scripted sim on the music grid. Bach Prelude in C (lib/bgm `prelude_c`, 64 bpm): the 16th arpeggio IS the hit grid. Each hit doubles the bed note on glassharp.
- Mochi = heat ticks (melt: shrink, round corners, drips that evaporate at the tool). Bolt = hits (bites cut from the bottom edge by an even-odd clip, cracks, shards).
- Rates (kg/s): L1 0.75/1.15, L2 1.6/2.6, L3 2.8/3.7. Blocks: 1x28, 2x35, 4x36 kg.
- Characters: `toon.draw_char` at sx = sy = 1 always; they lean (rot ≤ 0.12) while sliding. Melee tools fly up to strike (0.10-0.12 s up, 0.22-0.26 s back).
- A tool next to a blob must not touch it with a dark bar: it reads as an arm. Grips and handles point AWAY from the body (nail gun v1 failed this at 1:1).
- 2-tap nail gun and drill: the 2nd tap sits on the 32nd as crack SFX only (note_gain 0). Merged same-time events otherwise made L3 sound no denser than L2.

## Flash (measured)
- v1 FAILED 0:58-0:59: the berg came in with a cubic ease-out (peak ~700 px/s) while the sky darkened. A big bright shape sweeping over blue sky = UP/DN pairs over more than 25% of the cells.
- Fix: smoothstep entries (half the peak speed), berg entry 4.0 s, NO sky change. After the fix: worst 2 per 1 s (L3 four-cube entry, 34.6 s).
- Rule: never move a big light object fast over the sky AND change the background in the same second.

## Numbers (FHD v2)
See the review README.
