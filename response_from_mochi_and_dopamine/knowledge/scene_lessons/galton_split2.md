# galton_split2 — 1 ball becomes 1,048,576 (batch70)

- Brief: docs/BRIEF_batch70.md §6 = research/mochi_performance_2026-11-05.md pick 4. New file `scenes/galton_split2.py` (written fresh in galton_split's look; galton_split untouched). Caption: "Bolt: ONE ball that ~SPLITS IN 2~ at every peg" / "Mochi: a firehose. First to ~FILL~ wins".
- THE ONE CHANGE: 20 rows (21 bins, 17 px). Bolt drops ONE ball; it splits at every peg: after row k exactly 2^k balls, C(k, i) at peg i; his bins get exactly C(20, j) (1,048,576). FULL = the centre bin at C(20, 10) = 184,756.
- Drawn as density: Bolt's exact per-peg counts as glows (size ~ log count), his million landing as the exact bell. Mochi's firehose = R balls/s since −13.8 s; her flight and bins = the binomial expectation + a seeded multinomial sqrt-noise. The same hop time per row on both boards: 0.40 s → 0.62 s near the bottom (one trip 9.48 s).
- Counter: "BALLS ON THE BOARD" (in flight + in bins) for both.

## Honest result
- R = 14,913 balls/s, set so Mochi leads until row 18 (1.25 × 2^18 there). Rows: 10 → 1,024 vs ~270K; 18 → 262,144 vs 327,679; **row 19 (8.75 s): 524,288 vs ~337K = LEAD CHANGE**; row 20: 1,048,576.
- The million lands 9.70 s; **FULL at 10.00 s**, "SPLIT WINS!", "1 ball -> 1,048,576", "both make the SAME bell curve" (gold dashed bell over Mochi's pile). Mochi then: ~365K on the board, centre bin ~20 % of FULL.

## Sound
- Liszt, La Campanella (PD): the theme's pitches (midiworld performance MIDI, pitches only, 8-40 s, between the high D♯ bell) walked one per row split as bells (+ an octave below, + a high D♯ tinkle between rows); a soft G♯m / D♯7 strings bed; a G♯-minor tutti (strings, horns, harp, celesta, timp) on FULL; Mochi's stream = a steady soft patter of high pentatonic ticks.

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 816 frames = 13.60 s. −14.00 LUFS, peak −8.0 dBFS, last 0.5 s −61 dBFS. flash_check 0 = PASS. Seam 0.75.
- RMS/s −18.6 −17.8 −17.3 −17.3 −17.0 −17.1 −16.3 −16.7 −16.9 −17.3 −15.7 −16.2 −26.6.
- Frames read: 0, 4.0, 8.76, 9.0 (1:1 crop), 9.75, 10.1, 11.5 (+ Fast stills).

## Doubts
- Bolt's board is nearly empty until the end (one wave): the whole fill happens in 0.3 s at 9.7 s; the drama is the counter and the widening cascade.
- Mochi's in-flight stream is a density, not individual balls (a few sparkles move); at phone size it reads as a glowing triangle.
- The Campanella notes come from a rubato performance MIDI (pitches only, our rhythm).

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\galton_split2.mp4`. Owner review: pending.
