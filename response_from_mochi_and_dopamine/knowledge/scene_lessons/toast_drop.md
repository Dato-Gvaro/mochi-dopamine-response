# toast_drop — Butter side DOWN... is it really EVERY time? (batch54, 2026-10-28)

- Brief: docs/BRIEF_batch54.md (Mochi & Bolt 2). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from pilot_parking / rain_run.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch54\toast_drop.mp4` (**v1**, Full HD 9:16, 16.73 s, 1004 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Butter side ~DOWN~..." / "is it really ~EVERY~ time?"
- **Story:** a kitchen, side view. Mochi stands on top of a 2.0 m dresser and nudges buttered toast off its edge; Bolt pushes his off the 0.75 m table, harder. 1 slice per bar each → 4 per bar (16th-note trains). Mochi's first slice lands DOWN (the myth looks true: 1/1, 100 %), then hers keep landing UP (golden pile on her coral rug) while every one of Bolt's lands DOWN (brown pile on his mint rug). A faint stroboscopic trail shows each fall's spin. Bolt's last push stops right at the edge; he climbs down, walks under the table to stare at his pile, jumps in annoyance, BONKs the underside of the table... the slice tips and lands butter-down on his foot on the cadence ("SPLAT. ON HIS FOOT."). Mochi laughs, then smug; "IT'S THE HEIGHT: ½ TURN = DOWN · 1 TURN = UP". Final: Mochi 4/38 down (11 %), Bolt 27/27 (100 %).

## Layout
- 300 px = 1 m. Floor y 1290. Dresser top y 690 (edge x 330, body face x 290), table top y 1065 (edge x 560, legs 600/790). Height stickers "2.0 m" / "0.75 m" on the furniture from frame 0.
- Slices drawn at 2× real size (66 × 13 px); characters r 58. Each slice falls in one of 10 depth rows along the edge (screen offset −3.4 px y, +1.6 px x per row) so each falls the full height to the floor (no heap on top of heap; see Doubts).
- Rugs under the two landing zones (coral x 296-412, mint x 424-572) say whose pile is whose. A landed butter-down slice shows its toasted back (brown) + a brief butter smear; butter-up shows the yellow layer on top.
- HUD (y 1366-1544): "BUTTER DOWN", per side "MOCHI · 2.0 m" / "BOLT · 0.75 m", "x / n", a red bar, "N% DOWN".
- Key content inside x 0.10-0.84w (table right end 820, Bolt ≤ 783); the window is decoration. Static camera; warm calm colours.

## The physics (seeded, honest)
- Slice 11 × 1.2 cm (I = m(L²+e²)/12), μ = 0.4. Phase 1, the hand push: slides to the edge with kinetic friction from the speed that leaves it at v0 at the edge. Phase 2, the edge: the exact Lagrange equations of a rod rocking and sliding on a corner — (I + m s²) θ'' = m g s cos θ − 2 m s s' θ', s'' = s θ'² + g sin θ − μN/m (stick/slip), N = m g cos θ − m(2 s' θ' + s θ'') — until N ≤ 0 or the end passes the corner. Phase 3: ballistic flight with constant spin until the lowest corner touches the floor (or the foot). An edge-on landing tips the way it spins.
- Seeded per slice: v0 (Mochi 0-0.55 m/s nudges, Bolt 0.35-1.0 m/s shoves), the overhang where tipping starts d0 1-8 mm. Seed 24 (search `--search N` scored on an early Mochi DOWN and ~4 total downs).
- Result: Bolt's slices leave at ~16° with ~6 rad/s → land at 92-173° (½ turn) → 26/26 down; Mochi's leave at ~49° with ~9.5 rad/s and fall 0.64 s → 273-428° (≈1 turn) → 34/38 up. Prototype check: from 0.75 m a gentle nudge gives 183-255°, a 1.5 m/s fling only 54° (so a really hard shove WOULD land butter-up; Bolt's "harder" range stays below that).
- The finale slice: pushed so it stops 1 mm behind the edge; the bonk jolts it to 3 mm past at 4 cm/s; it pivots 0.26 s, leaves at 7.3 rad/s and lands at 196° on his foot (foot top 13 px). T_BONK is solved so it lands on the cadence (13.04 s).

## Sound (music first)
- **Piece:** Franz Schubert, Moments musicaux D 780 No. 3 in F minor, "Air russe" (1823; Schubert d. 1828, PD). Sly, staccato, deadpan. Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD engraving (Sauer & Leidersdorf, Wien 1827), `MomentsNo3.mid/.ly/.rdf`, saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\schubert_moment3\`. Read at runtime (right + left hand).
- **Excerpt:** 2/4, quarter = 132 (bar 0.909 s), source bars 2-16 (the theme twice), cadence = the F-minor chord of source bar 17 (13.64 s = the splat on his foot).
- **Arrangement** (lib/orchestra): oboe on the theme's top line (staccato), the inner voice on bassoon 8vb, the second time + clarinet 8vb + violin; the left-hand oom-pa on pizzicato strings, beats on contrabass (+ bassoon the second time). Cadence: timpani + a dry pizz/strings F-minor chord, then a soft held chord.
- **SFX** (tonal): push tick, an edge click when the slice leaves the corner, butter-UP landing = a round "thup" + a tiny ding, butter-DOWN = a softer low "plap"; the hop-down thud, steps, the BONK (tonal), the final low plap. All pitched to the left hand's chord.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 1004 frames = 16.73 s. −14.00 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −18.5 −18.2 −17.9 −17.8 −17.6 −17.1 −16.9 −17.0 −16.5 −16.9 −15.9 −15.8 −16.0 −14.7 (cadence) −15.2 −25.3, then silence.
- SFX events/s: 7 7 13 15 16 21 24 26 28 24 17 20 9 3 0 (the climb; the walk/bonk beat is a story beat).
- flash_check PASS (0 flashes). Seam mean |Δ| 0.74 (good band).
- Frames read from the mp4: 0.5, 1, 2, 7, 12, 13.2 (BONK), 13.75, 15 + a 1:1 crop of the slice on his foot (13.8).

## Doubts
- Bolt is 27/27: honest for his push range, but it makes his side predictable after ~5 s; the uncertainty is Mochi's first DOWN and "will the shelf work?".
- The depth rows are a staging choice: piling every slice into one heap shortened later falls (honest too) and flipped the result for both (Mochi 14/38 down, Bolt 9/26) — it buried the lesson, so each slice gets its own floor row.
- The slice on his foot is small at phone size (drawn 1.3×, with a butter splat + a yellow smear on the foot + the banner).
- Bars 11-14 (10.5-13.6 s): Bolt's walk/bonk; Mochi keeps dropping 4 per bar, so the frame is never dead, but Bolt's counter stops.

## Args and cost
- `--seed` (24), `--search N`, `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~20 s at 2 encoder threads.
- Owner review (batch55, 2026-10-28): approved as is → 4K ship.

## Outcome
- (fill after upload)

## Ship (batch55, 2026-10-28)
- Owner: approved unchanged. 4K `NF_SCALE=2.0 --label ship` (same code and seed as v1): h264 High yuv420p 2160x3840 @ 60 fps, 1004 frames = 16.73 s; −14.00 LUFS, peak −2.00 dBFS, last 0.5 s silent; flash PASS (0, mean lum 0.08); seam mean |Δ| 0.66. Encoded frames read at 0.3 s and the finale.
- Staged: `MochiAndBolt\schedule\2026-11-04\3_toast_drop.mp4`, 00:00 local Nov 6 (= 15:00 US East Nov 5). FHD review copy → `MochiAndBolt\archive\toast_drop_fhd.mp4`.
