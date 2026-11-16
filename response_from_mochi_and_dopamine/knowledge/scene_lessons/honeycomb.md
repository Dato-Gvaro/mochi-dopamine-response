# honeycomb — "Same wax, more HONEY" / "Squares or Hexagons?"

- The formula (docs/BRIEF_formula.md) on the HONEYCOMB CONJECTURE: why bees build hexagons. Two wooden hive frames side by side, the SAME wax budget each. Mochi (coral) builds SQUARE cells, Bolt (mint) builds HEXAGON cells. Mochi and Bolt are bees (toon + wings) hovering at their comb's building front.
- **One sentence:** same wax, more honey. Muted read: two identical WAX LEFT bars drain together, two HONEY STORED counters, Bolt's is gold (ahead by 1-2 at frame 0).
- **Honest maths (exact, edge for edge):**
  - Every cell has the same area (2601 px²): square side s = 51.0, hexagon side a = 31.64.
  - Wax charged = walls drawn. The wood frame is cut to each lattice (straight top bar + left stile for squares; zigzag top/left/right notches for hexagons), so each new square grows exactly 2 walls (bottom, right) and each new hexagon exactly 3 (lower-left, lower-right, right). That is the tiling share: every inner wall is shared by two cells.
  - Wax per cell: squares 2s = 102.0, hexagons 3a = 94.92. Ratio 1.0746 = +7.5% honey per wax.
  - Budget = 90 hexagons of wax = 8542.95 = 83.75 squares. Bolt: 90 cells = 15 full rows. Mochi: 83 cells + a half-built 84th (the last cell of her 12th row; bottom wall done, right wall 50%).
  - Both builders lay the same wax per second (one shared clock W(t)), so both bars hit EMPTY at the same instant.
  - Triangles (not shown): 116.3 wax per cell, 12% less honey than squares.
- **Music = the clock:** Chopin, Valse Op. 64 No. 1 "Minute Waltz" (1847; Chopin died 1849, PD).
  - Notes from the Mutopia MIDI, `<SOUNDFONTS_DIR>\scores\chopin_minute_waltz\chopin_valse_op64_no1.mid` (Edition Peters; Mutopia licence: Public Domain). See SOURCE.txt there.
  - Tempo map: 0.62 s/beat at beat 0, linear to 0.30 s/beat at beat 36 (eighths 0.31 → 0.15 s).
  - Bolt's hexagons complete on the eighth grid, beats 0-35.5: 66 melody onsets of the right hand + 6 grid points inside held notes (a soft harp chord tone). His 90th cell = beat 36 = our Db-major cadence (V7 → I; the score's harmony there).
  - Mochi's squares complete 7.5% slower on the same wax clock; each plays a soft harp chord tone of the score's harmony at that moment.
  - Beats 0-12 have no left hand in the score; the bed repeats the score's own beat 12-24 Db waltz pattern there.
- **Key times** (clip seconds):
  - Frame 0: Bolt 17 cells, Mochi 16, wax 78%. Bolt's 18th cell (row 3 complete) lands at 0.10 s; Mochi's 17th at 0.18 s.
  - Lead pops (+N over Bolt's counter): +3 at 3.38, +4 at 7.41, +5 at 10.72, +6 at 13.79, +7 at 16.20 s.
  - Counts M/B: 2 s 22/24, 6 s 35/38, 10 s 50/54, 14 s 68/74, 16 s 79/85.
  - 16.66 s: the wax runs out (OUT OF WAX! on both bars), the cadence chord, HEXAGONS WIN!; Mochi's wall stub sputters; Bolt's hive glows gold with a sweeping honey shimmer.
  - 16.81-17.23 s: Bolt's 7 extra cells light up one by one (celesta/harp arpeggio up the Db chord); +7 CELLS! at 17.38 s; "most honey, least wax" at 16.96 s; "bees figured this out first" + a drawn bee at 17.61 s.
  - Dissolve from 20.26 s into the pre-roll. Clip 20.86 s (1252 frames).
- **Staging:** Mochi laughs at 0.15 s, wows at +3, worries from +4, wows at the wax-out, annoyed after. Bolt laughs at +3, cheers at +5, laughs at +6, cheers and laughs (smug) at the win.
- **Sound** (all in the bed; the sidecar holds silent markers):
  - Melody on piano (Chopin's instrument) + a soft celesta double. LH: pizz chords + pizz bass, contrabass from beat 12. Strings double the tune from the climb (beat 21), horns from beat 30, a strings_slow swell over the V7 (beats 24-36). Timpani roll from beat 33.
  - Cadence: Db major on strings, choir, brass, piano, contrabass, harp roll, timpani, boom, crash (`fin` gain ×0.35, the birthday_room level).
  - SFX (scene synths, tonal, no noise): a soft waxy tik per wall (880 Hz Mochi / 980 Hz Bolt), a warm rising honey plop per filled cell, a bell chime per finished row (chord tone, ≤ C#6). All ≥ 12 ms apart, gain ÷ √density.
  - `peak_db=None` (brief).
- **Laptop:** 1 Python process (BLAS threads 1) + x264 `-threads 2` (`Writer2`).
- **Commands:** `NF_SCALE=1.0 NF_FAST=1 python scenes/honeycomb.py --still --frame N` · `NF_SCALE=1.0 python scenes/honeycomb.py` · `--report`.
- **Checks** (encoded Full HD, `output/honeycomb_v1_9x16.mp4`):
  - Video: h264 yuv420p 1080x1920 at 60 fps, 1252 frames = 20.87 s.
  - Loudness: -14.00 LUFS, peak -6.06 dBFS, last 0.5 s at -78.3 dBFS. RMS per second: body -17.6 → -16.5, cadence seconds -14.4/-14.9 (lift kept by `peak_db=None`).
  - flash_check: 1 flash (the loop dissolve at 20.65 s), worst second 1 → PASS (mean luminance 0.061).
  - Loop seam: encoded mean delta 0.524 (good band). The last frame reads 16/17 cells = frame 0.
  - Sidecar: 73 notes, 13 distinct, top pitch 16.4%; events per 5 s 18, 21, 27, 7.
  - Frames read at 0, 0.5, 8, 16.7, 17.6 s and the last frame, plus 1:1 crops of the build front at 12 s and the +7 CELLS finale at 17.6 s.
- Delivered `<VIDEOS_DIR>\batch44\honeycomb.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-19): "may work if you think so" -> decide after the early-breakouts research; if yes -> 4K Oct 26 slots 2-3.

Decision (2026-10-20, after the early-breakouts research): linear race with a small 7.5% gap = weak by the measured skeleton -> reserve.
