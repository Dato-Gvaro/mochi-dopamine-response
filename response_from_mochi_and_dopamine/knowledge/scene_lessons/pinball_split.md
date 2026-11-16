# pinball_split — Mochi's 1 FAST ball vs Bolt's ×2 SPLIT bumpers: who scores 100,000 first?

- Brief: coordinator task 2026-10-24 (batch49, docs/BRIEF_overnight_1023.md). New mechanic, new file. It borrows domino_branch's layout, HUD, faces, banners, captions and dissolve loop.
- **v3 (current).** The owner's reviews:
  - v1: "one ball and that's it? it's obvious many balls will win. Make one FAST ball."
  - v2: "the speed difference is not visually detectable." The v2 ×14 was a points multiplier; the real speed only grew ~1.3×.
  - So v3 makes the speed real: the multiplier IS the ball's real speed over Bolt's ball speed.
- Caption: "Every hit scores ~100 × speed~" / "~1 FAST ball~ or ~×2 split~:" / "who scores ~100,000~ first?".
- Two identical pinball tables, top view (violet neon panels, x 118-492 and 524-898, y 412-1292). Each has 4 pop bumpers in a diamond (r 30), two flippers (56 px), inlanes, a drain, and flat lit inserts (decoration only, nothing collides with them).
- HUD per side: a progress meter to 100,000 (y 1312), a live rule label ("FAST: ×N speed" / "SPLIT: N balls", y 1398) and the score (y 1482, gold for the leader). The faces sit between the labels.

## The rule (each side readable at a glance)

- **FAST (Mochi, coral):** one ball on a scripted, beat-locked path round the bumper diamond (~91 px a hop). Every bar her flipper fires it on the downbeat, and it lands on the other flipper on the next downbeat (mirrored every other bar). **It really speeds up**, with hits on the music grid:

  | Bars | Clip time | Hits | Real hop speed | Shown as |
  |---|---|---|---|---|
  | 0-1 | 0-3.3 s | on 8ths, 5 per bar | 454 px/s | ×1 (Bolt's balls: median ~400 px/s) |
  | 2-4 | 3.3-8.9 s | on 16ths, 9 per bar | 845 px/s | ×2 |
  | 5-7 | 8.9-14.1 s | on 32nds, 21 per bar | 1,615 px/s | ×4 (3.6× the start) |

  - **Scoring:** every hit scores 100 × her speed level (+100 / +200 / +400 pops).
  - **Visible speed:** a comet trail drawn over the last 0.16 s of real travel, so its length is the speed (~70 px at ×1, ~260 px bending round the bumpers at ×4); faint speed lines behind the ball above ×1; and a "SPEED" gauge (×1 → ×4, the needle eases over ~0.3 s at each change) in the dark corner under her left inlane.
  - **Head start:** she starts at 67,000, set so she ends on 98,600. The check asserts she leads every frame before the cadence; her smallest lead is 2,500 at 14.12 s.
- **SPLIT (Bolt, mint):** a real 2-D ball sim (gravity 1150 px/s², walls, inlanes, flippers with surface velocity, 4 substeps). A ball that touches one of his bumpers is grabbed (gold ring) and **on the next 16th of the music the bumper fires it out as TWO balls** (±60° about the contact normal, 460 px/s ±10%). A gold "×2" pops on the bumper. His balls are speed ×1: 100 a hit, no trails (median ~400 px/s). He mashes both flippers on every beat, so balls keep draining.
  - Bolt's balls do not collide with each other: with contacts on, the funnel jammed into a pile and his hit rate stopped climbing at ~85/s.
  - Colour: generation gradient blue → cyan → mint, normalised per frame (smoothed), so old lineages are blue and fresh splits mint.
- **The race:** Mochi leads from frame 0 (67,100 vs 1,500), then the doubling closes in over the last 2 s: 45,300 behind at 12 s, 10,600 at 13.8 s, 2,500 at 14.15 s. **His last ×2 wave, on the cadence, takes him past her to 100,000. She ends on 98,600.**
- **Finale:** Bolt's bumpers warm to gold and a soft light ripple runs over his balls (0.35 max lift, no flash); splitting stops. Banner "100,000! SPLIT WINS!" and, 0.3 s later, "by just 1,400!". Mochi's ball lands on her raised flipper and stays there (game over). Bolt cheers, then laughs. Mochi goes wow, then annoyed, with "again?!" from +0.45 s.
- Calm camera: static, no zoom.

## Timeline (seed 7, phase 0; clip s)

- The clip starts at sim frame 252. Frame 0 = the piece's first downbeat = a Mochi hit. The clip start is chosen so Bolt's 1,000th hit lands on the cadence. (`--search` keeps only runs where that start also puts Bolt's flips on beats.)
- **0 s:** Mochi's ball (×1, short comet) hits a bumper (+100); Bolt has 12 balls in play with "×2" pops. 67,100 vs 1,500.
- **0.5 s / 1 s / 2 s:** 67,300 / 67,500 / 67,600 vs 1,800 / 1,900 / 2,300 (Bolt 15 / 14 / 14 balls).
- Score per second (M / B, Mochi's speed, Bolt's balls): 4 s 68,600/4,100 (×2, 23); 7 s 71,600/7,800 (×2, 40); 9 s 73,400/13,900 (×4, 81); 10 s 79,000/20,200 (×4, 121); 12 s 88,200/42,900 (×4, 279); 13 s 91,000/60,600 (×4, 398); 14 s 97,800/92,900 (×4, 627).
- **CADENCE + OVERTAKE at 14.23 s:** Bolt 100,000 (675 balls), Mochi 98,600. It is the only lead change.
- Clip **15.93 s** (956 frames). The last 0.6 s dissolves into the pre-roll, and the HUD switches at the midpoint.
- **Growth:** Bolt's balls 12 → 675 (×56); his hit rate 4-5/s → ~530/s in the last 0.23 s.
- Hits per second:

  | Side | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 (0.23 s) |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Mochi | 5 | 1 | 4 | 3 | 6 | 4 | 5 | 5 | 4 | 14 | 7 | 16 | 6 | 17 | 3 |
  | Bolt | 5 | 4 | 4 | 14 | 8 | 12 | 14 | 24 | 40 | 63 | 95 | 132 | 177 | 273 | 123 |

  Mochi's per-second count alternates because each bar (1.87 s) is a rattle plus the flipper shot and the fall.
- Points per second: Mochi 0.4k → 6.8k; Bolt 0.4k → 32k (the last full second).

## Sound (music first)

- **J. S. Bach, Brandenburg Concerto No. 2 in F major, BWV 1047, 1st movement** (c. 1721; Bach d. 1750, PD).
  - Source: Mutopia piece 1680 (full-score MIDI, Bach-Gesellschaft vol. 19, Rust 1871, **Public Domain**), saved at `<SOUNDFONTS_DIR>\scores\bach_brandenburg2\mids\score.mid` with `SOURCE_mutopia_1680.txt`.
  - No other scene uses it. Not on the used or banned lists, not Chopin, not kid-coded, not circus.
- **Excerpt:** the opening ritornello, score beats 0-30.5 (bars 1-8), to its F-major cadence. Frame 0 = the piece's first downbeat. One steady tempo, quarter = 128.6 (a quarter is 28 frames, an 8th 14, a 16th 7).
- **Arrangement** (lib/orchestra, MuseScore_General): every part read from the score. Violin I on strings + the solo violin on violin, violin II, viola, cello, the continuo on harp (harpsichord stand-in) + contrabass an octave down, trumpet (the MIDI's octave, F3-G5: mid register), recorder on flute, oboe. A CC11 crescendo through the clip.
  - **Cadence (beat 30.5 = 14.23 s):** a held F-major chord on strings, horns, a short trumpet chord, cello and bass F, a rolled harp run, timpani F and a soft boom.
- **SFX:** tonal bumper dings, pitched to the tune's top line (violin I) at that moment, so they double the melody. Bell-like partials 1 / 2 / 3.9 and a 2 ms low-passed tick, nothing above 5 kHz, no noise.
  - Mochi: one clear ding per hit at pitch (8ths, then 16ths, then 32nds), slightly quieter at 32nds. Bolt: one shorter ding per 16th on which his bumpers fire, an octave down, layered 1 + log2(balls split) voices (up to 6) and louder with log2.
  - A soft woody flipper thock per flip (Mochi's flips, Bolt's beats).
- **Mastering:** domino_branch's `level_bed` (+2.5 dB crescendo, cadence `--findb 1.5`). Then `master_keep_lift()`: audio.master's room reverb (0.5) + loudness match to -14 LUFS + a 5 ms lookahead limiter at -2 dBFS. `audio.master(peak_db=None)` was measured first: its -3 dB Limiter and -1 dB drive loop flattened the cadence lift to +1.2 dB on this mix. Last 0.6 s zeroed.

## Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\pinball_split.mp4, v3)

- Video: h264 yuv420p 1080x1920, 60 fps, 956 frames = 15.93 s.
- Loudness: -14.01 LUFS, peak -1.99 dBFS. The last 0.5 s is silent (-240 dB).
- **RMS per second (muxed, stereo):** -18.4, -19.0, -18.2, -18.0, -17.8, -17.7, -17.3, -16.9, -16.3, -15.9, -16.1, -15.8, -15.7, -14.8, -14.6. No second below -19.0.
- **Finale:** 0.4 s RMS +3.65 dB over the body median. Energy above 4 kHz: 0.22%.
- Audible dings per second: 9, 4, 8, 9, 12, 11, 12, 14, 13, 22, 16, 24, 15, 25.
- flash_check: 0 flashes = PASS (mean luminance 0.011).
- **Loop seam:** check_clip mean delta 0.902 (above the 0.72 "good" edge, under the 1.1 "broken" line). It is a genuine consecutive step: frame 0 is a Mochi hit plus a Bolt ×2 fire. In v2 the same kind of in-clip step measured 0.77-0.91.
- Side safe zone: caption, panels, gauge, labels, scores and characters inside 0.10-0.84w.
- Frames read from the encoded file at 0, 0.5, 2, 7, 12, 14.25 (the overtake and finish), 14.9 and 15.9 s, plus a 1:1 crop of Mochi's table at 12 s (×4: a ~260 px zigzag comet with speed lines). Fast stills at 0, 0.5, 2, 7, 11.7, 12, 15 and 15.92 s.

## Nits / doubts

- **Bolt's balls pass through each other** (no ball-ball contacts; not cheap to fix: contacts jam the funnel and stop the climb). At the end 600+ balls overlap in a swarm.
- **The race shape is tuned; the speeds are real.** Each hit scores 100 × the real speed level, but her head start (67,000) is set from Bolt's sim so he passes her exactly on the cadence. A big head start is the price of honest scoring: her meter starts at 67% and creeps, while his races from 1.5%.
- Her speed rises in three steps (×1 / ×2 / ×4 at bar starts), not smoothly; the gauge eases between them.
- At ×4 the 32nd-note rattle (17 hits/s, ~27 px a frame) reads as a bright zigzag comet rather than a distinct ball.
- The overtake and the win are the same frame (the cadence), so there is no separate "LEAD CHANGE!" banner; the "by just 1,400!" line carries the photo finish.
- "again?!" sits between Mochi's meter and her label (touching the label's top).
- After the cadence her gauge needle falls to ×1 (the ball rests on the flipper), while her label keeps "×4 speed" (her last speed).

## Args and cost

- Defaults are the shipped values: `--seed 7 --phase 0 --layout dia4 --rb 30 --rball 8 --fl 56 --kick 460 --splita 60 --g 1150 --bb 0 --bflip 1 --mfinal 98600 --lvbars 2,5 --tend 1.70 --fin 2.0 --findb 1.5 --sfx 0.22 --timp 0.40 --boom 0.20`.
- Other args: `--search --seeds a,b --phases 0,7,14,21` (seed search; a run is usable only when "beat-aligned"), `--report`, `--cache` (pickles the table sim in output/), `--still --frame a,b`, `--audition`, `--reuse`, `--sound 0`, `--label`, `--cap`.
- Cost: sim ~5 s; Full HD render ~8 min at 2 encoder threads.
- v1 (2026-10-24, rejected): Mochi had one steady ball (100 a hit) and lost 7,800 to 100,000 after a 7 s lead change. Owner: "it's obvious many balls will win."
- v2 (2026-10-24, rejected): a ×2 → ×14 points multiplier with a real speed gain of only ~1.3×. Owner: "the speed difference is not visually detectable."
- Owner review of v3: pending.
