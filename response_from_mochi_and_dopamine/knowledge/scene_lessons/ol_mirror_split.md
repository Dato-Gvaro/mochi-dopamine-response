# ol_mirror_split — "Every mirror SPLITS the laser in 2" / "until the room is FULL of light" (Overflow Lab)

- The first Overflow Lab mirror video. It has no characters, and it follows docs/BRIEF_channel2.md.
- **Room:** a dark room with one white outline (2.5 px, 85% alpha) at x 128-888 (0.12-0.82w), y 392-1232 (≤ 0.64h). 50 glass mirrors, 44-62 px long, at least 82 px apart, with seeded angles. Each mirror is tinted by its position on a rainbow sweep, so frame 0 is already multi-hue. A laser emitter sits on the left wall.
- **Rule (optics-lite, honest):**
  - Every mirror hit splits the beam in 2: the REFLECTED child (exact: angle of reflection = angle of incidence) and the TRANSMITTED child, bent by a fixed 14° prism deflection (the sign is set per mirror).
  - Each child is one generation older, and its hue moves +0.13 round the rainbow.
  - Walls reflect without splitting, up to 3 times; then the beam stops.
- **Speed:** all light moves at the same speed, v(t) = 145·e^(0.06 t) px/s. The split rate rises exponentially to the last frame.
- **Counter:** BEAMS = 1 + the number of true splits, which is exact up to FULL.
  - After FULL the drawing is capped at 3,200 travelling fronts. Past the cap, a split draws one child carrying the weight of both.
  - The ×2 badge (in the current hue) pops each time the count doubles, at most once per 0.16 s.
- **Meter:** LIT % is the share of 6 px grid cells (126×140 = 17,640) that a beam has crossed.
  - It shows one decimal from 99%, so the last dark spots keep ticking.
  - The FULL goal mark is visible from frame 0. FULL = every cell lit.
- **Look:**
  - Each beam is a wide low-alpha ADD halo under a thin core laid with OVER, so the dense web stays rainbow instead of going white.
  - Per-line alpha falls with the number of beams alive at its birth. The first ~7 generations are drawn bold.
  - The lit floor glows: one pixel per cell, scaled up bilinearly.
  - Small 4-ray sparkles at the latest 40 splits.
  - At FULL the lattice freezes. Over 1 s it gains a +30% ADD glow, the mirrors sparkle in a wave outward from the emitter, and a "FULL!" banner pops (0.86→1.0 scale, 150 px). After that only travelling fronts are drawn.
- **v2 opening fix** (coordinator, 2026-10-21): the clip now starts **T_OFF = 4.70 s into the SAME run**. There is no re-seed and no rewind; `t_of_s` returns sim time − T_OFF. v1 (15.63 s, frame 0 = one beam) is superseded.
- **Timeline** (seed 33; clip 11.23 s = 674 f):

  | Clip time | What happens |
  |---|---|
  | Frame 0 | 26 beams, 8.0% lit, gens 6-9 alive (violet/blue/cyan/green/yellow web plus the red entry beam). A split lands at 0.04 s, then 0.05 and 0.10 s |
  | 1 s | 41 beams, 14% lit |
  | 4 s | 189 beams, 57% lit |
  | 7.93 s | **FULL** at ~2,480 beams |
  | 9.5 s | 7,993 beams |
  | 10.63 s | Dissolve to the NEW frame 0 begins |

- **Music:** Debussy, Première Arabesque (L. 66 No. 1, 1888-91; Debussy d. 1918, PD).
  - Source: Mutopia #1777 (Durand 1904 edition; the engraving licence is Public Domain), saved at `<SOUNDFONTS_DIR>\scores\debussy_arabesque1\` with SOURCE.txt. It is not on the used list and not kid-coded.
  - Cut: beats 0-20 (bars 1-5, an even stream of 60 triplet onsets: the falling arpeggios and the F#-E-D#-C#-B bass line over the dominant).
  - Each onset lands on a sampled split (greedy min gap 0.16 s → ~0.08 s, splits from 0.04 s). So the music accelerates with the light, at 0.04, 0.21, 0.40, 0.56, 0.96 … 7.80 s, close to the score's own tempo (0.139 s per onset).
  - The bar-6 E-major arrival is the cadence on FULL.
  - Arrangement: piano (both hands as written, pedal ×1.6), harp doubling the upper line from bar 3, contrabass on the bass line, a strings_slow pad per half bar from beat 0, and a soft timpani roll on the dominant into FULL.
  - Cadence (gain ×1.4): piano, strings, horns, oohs, contrabass E1/E2, a harp spread up to E6, timpani E2, a soft crash, and a rising glass arpeggio on E major.
- **SFX:** a crystalline glass ping for every split, at least 12 ms apart (555 pings).
  - Partials f0 + 1.5·f0 + 2.76·f0, with a 2.5 ms soft attack and a 4th-order low-pass at 5.8 kHz. Energy above 6 kHz is 0.01% of the total.
  - f0 is in G5-G6, tuned to a pitch class of the current half-bar's harmony.
  - Density gain is 0.055/(dens/2)^0.33. The pings fade under the cadence after FULL and stop 1.2 s before the end (556 pings in v2).
- **Checks** (v2, encoded Full HD `output/ol_mirror_split_v2_9x16.mp4`, delivered as `<VIDEOS_DIR>\channel2\ol_mirror_split.mp4`):
  - Video: h264 yuv420p 1080x1920 at 60 fps, 11.23 s.
  - Loudness: −14.00 LUFS, peak −4.5 dBFS, last 0.5 s at −57.2 dBFS. `peak_db=None`.
  - RMS: 0-1 s −22.9, 1-2 s −20.0, body (2-6 s) −17.8, the 3 s before FULL −17.5, cadence (1 s) −12.5. That is +5 dB over the approach.
  - Energy above 6 kHz: 0.006%.
  - flash_check: 1 flash (the loop dissolve) = PASS.
  - Seam mean delta: 0.464 (good band).
  - Frames read from the mp4 at 0 (1:1 crop), 1, 4, 7.95, 9.5 and 11.2 s.
- **Doubts:**
  - The first second is still ~5 dB under the body (a natural crescendo). The sim has a split lull at 0.56-0.96 s.
  - The meter sits at 99.x% for ~1.2 s (6.7-7.9 s; the honest tail of the last scattered cells).
  - After FULL the web reads as a dense, slightly pastel mesh.

- **Commands:**
  - `NF_FAST=1 python scenes/ol_mirror_split.py --still --frame 0,120,758`
  - `NF_SCALE=1.0 python scenes/ol_mirror_split.py --label v1` (one process, x264 `-threads 2`)
  - `--report`
  - `--search 0-60` (seed search: FULL time, the 90%→100% tail, early split counts)

Owner review (2026-10-21): "not so interesting, maybe later when the channel is more popular" -> reserve.
