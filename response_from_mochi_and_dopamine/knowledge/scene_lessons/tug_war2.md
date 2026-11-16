# tug_war2 — Doubling vs FACTORIAL (batch70)

- Brief: docs/BRIEF_batch70.md §5 = research/mochi_performance_2026-11-05.md pick 3. New file `scenes/tug_war2.py` (from tug_war.py; untouched). Caption: "Bolt: 100 people, then ~DOUBLES~" / "Mochi: ALONE, then x2, x3, x4... ~WHO WINS~?".
- THE ONE CHANGE: the rules. Bolt (drawn LEFT this time) 100 × 2^k; Mochi (RIGHT) k! — steps on the downbeats 1.1 … 9.1 s. In the code the left team keeps tug_war's role name "mochi" (early leader, loses) and the right "bolt"; `SHOW` maps them to the characters (names, colours, faces).
- Counts: 100/1, 200/1, 400/2, 800/6, 1,600/24, 3,200/120, 6,400/720, 12,800/5,040, **25,600/40,320 (step 8: "FACTORIAL PASSES!")**, 51,200/362,880.
- tug_war's model unchanged: x'' = K(right − left) − G v − BQ v|v| (K 4, G 1, BQ 0.5), sim from −2.5 s. LINES at the flag's position at T_LINE = 10.6 s (L_sim 1,191). Bolt's near miss: u = −0.84 at 8.10 s. Flag over the centre (LEAD CHANGE) 9.63 s; over Mochi's LINE 10.60 s → MOCHI WINS; Bolt's crowd flies into the pile, landing on the cadence 11.1 s.
- Crowds: one figure size for both teams (the smaller fit) and one scale for both: 1 figure = 1 person ≤ 2,500, then 10 / 100 / 1,000 people (labelled "1 figure = N people").

## Sound
- Tchaikovsky, Swan Lake "Danse napolitaine" tarantella (PD; Mutopia, arr. Sardain, public domain), score beats 82-104 at a 2/4 bar = 1 s (every step on a downbeat), its E-flat cadence = the pile landing. Our arrangement: trumpet (sounding pitch) + violin lead, strings/piano, pizz bass, hi-hat, timpani on each step, roll into the yank, E-flat tutti. tug_war's tonal SFX re-pitched to the score's harmony.

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 810 frames = 13.50 s. −13.97 LUFS, peak −5.5 dBFS, last 0.5 s silent. flash_check 0 = PASS. Seam 0.52.
- RMS/s −18.3 −17.7 −16.2 −16.7 −17.0 −15.9 −15.9 −16.5 −16.3 −17.0 −17.9 −13.6 −20.4.
- Frames read: 0, 5.0, 9.7, 10.65, 11.4, 13.0 (+ Fast stills 0-700).

## Doubts
- Sides swapped vs tug_war (Bolt left). Mochi's team is invisible-small for ~6 s (1, 1, 2, 6, 24, 120): the honest factorial; the giant counts carry it.
- The figure scale changes 3 times (10 / 100 / 1,000): the crowds re-pack on those steps.
- Tiny helpers pull as hard as big ones (tug_war's rule).

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\tug_war2.mp4`. Owner review: pending.
