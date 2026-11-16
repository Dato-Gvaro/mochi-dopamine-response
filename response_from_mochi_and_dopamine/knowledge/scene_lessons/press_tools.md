# press_tools — Mochi's TRIDENT vs Bolt's SPIKE: every ball hit splits into 3

- Brief: coordinator task 2026-10-22 (batch47), from the owner's review of press_break2: "we just need some NEW TOOL… maybe spike, or trident vs spike".
- press_split2's look exactly, in press_split4's side-safe layout (stage ×0.815 about x 0.47w):
  - two violet neon chambers on black, crimson → gold balls (Mochi) and blue → mint (Bolt);
  - the counters, faces, Für Elise note per hit, banners, the dashed MAX line + OVERFLOW finale, and the dissolve loop.
- **THE ONE CHANGE is the tools.** New file; press_split2, press_break and press_break2 are untouched.
- Caption (3 lines so line 2 stays big): "Every ball ~HIT~ splits into 3" / "~Trident~ or ~Spike~:" / "which ~OVERFLOWS~ first?". Trident is coral, Spike cyan, OVERFLOWS red.

## The tools (honest difference)

- **TRIDENT (Mochi):** three prongs 62 px apart stab down together.
  - Every prong crushes every ball its tip passes into.
  - The trident only drives **150 px past its first contact (shallow)**: three short columns per strike.
  - Speeds 3300 px/s down, 4200 px/s up; it waits 0.04 s.
- **SPIKE (Bolt):** one long tapered needle on a jackhammer body.
  - It always drives **down to the floor (deep)**: it pierces the whole column under it.
  - Speeds 5000 px/s down, 6000 px/s up; it waits 0.02 s.
- Both retract only 70 px above the pile, so they are rapid jackhammers.
  - The spike's cycle lengthens as the pile gets taller, because it always goes to the floor.
  - The trident's shallow cycle stays short.
- Both walk across fixed stops: the trident over 7 stops, the spike over 9. The spike stays 50 px off the walls.
- A ball split by a strike is immune to that strike.
- **The tools pierce: there is no shaft collider.** A sideways shaft push packed balls into one-ball columns against the walls and faked an overflow. Removed.
- **Why the race turns:**
  - Early, the pile is low. The trident's three columns take more balls than the spike's one.
  - Later, the trident's shallow prongs only reach the already-crushed top layer. Its bottom row of big red balls is never touched, which is visible.
  - The spike's deep needle keeps reaching fresh big balls lower down. Smaller balls pack more per column, so every spike stroke crushes more: ×3 growth that accelerates.
- MAX line at logical y 660 (press_split2: 560, for its press's 6,561-ball piles). The tools' mixed piles fill slower.

## Seed 0 (clip time)

- The clip starts in the same sim once both chambers hold ≥ 3 balls (sim 0.62 s). The loop dissolve blends into the frames before that.
- **0 s:** both tools mid-strike. Trident chamber 5 balls (crimson → orange), spike 9 (blue → cyan). A burst is popping.
- **First split at 0.03 s.**
- **0.5 s:** 19 vs 17 balls. **1 s:** 79 vs 27, the trident leading (gold counter). **2 s:** 271 vs 91.
- **Crushes per second:**

  | Second | Trident | Spike | Total |
  |---|---|---|---|
  | 0 | 37 | 10 | 47 |
  | 1 | 96 | 32 | 128 |
  | 2 | 158 | 47 | 205 |
  | 3 | 192 | 82 | 274 |
  | 4 | 118 | 79 | 197 |
  | 5 | 68 | 155 | 223 |
  | 6 | 67 | 153 | 220 |
  | 7 | 65 | 194 | 259 |
  | 8 | 21 | 204 | 225 |
  | 9 | 57 | 157 | 214 |
  | 10 | 60 | 193 | 253 |
  | 11 | 40 | 150 | 190 |
  | 12 | 65 | 158 | 223 |
  | 13 | 23 | 121 | 144 |
  | 14 | 16 | 105 | 121 |
  | 15 | 89 | 107 | 196 |
  | 16 | 65 | 118 | 183 |

- **LEAD CHANGE at 8.37 s** (1,617 vs 1,627).
- **The SPIKE OVERFLOWS at 16.80 s** with 4,137 balls. The trident is at 2,463, with its pile top 190 px under MAX.
  - The spike snaps: the needle and body fly with chips and sparks, and the pile erupts out of the top.
  - "OVERFLOW!", then "SPIKE WINS!". Bolt cheers and laughs; Mochi shows wow, then annoyed.
- Clip **18.62 s** (1117 frames).

## Sound

- One note per crush, merged per 70 ms, walking **Für Elise**. The notes are copied from the Mutopia MIDI (piece 931, right hand, the same 54 notes as press_break); no lib MELODIES. 7–11 notes per second.
- Crunch per split, rate-capped and nudged +12 ms so it never lands on a note onset.
- **Tool ASMR** on each strike's first contact (all partials under ~5.5 kHz, no noise):
  - Trident: three staggered metallic tinks (1040 Hz ±6 %).
  - Spike: one sharper stab (1480 Hz) over a soft 170 Hz thud.
- No hiss, no creak.
- **Overflow:** clank + thunk, then the rolled A-minor cadence A1–E5 plus a pad at 3.2 (tuned against master() for +3 dB). The snap is a thunk + slam + two light glass cracks.
- Mastering: `peak_db=None`. Post-master fade so the last 0.5 s is digital silence.

## Checks (encoded Full HD, <VIDEOS_DIR>\batch47\press_tools.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 18.62 s.
- Loudness: −13.99 LUFS, peak −8.6 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second:** −17.2, −16.4, −16.1, −16.2, −16.5, −16.3, −16.3, −16.6, −16.4, −16.7, −16.5, −16.5, −16.4, −16.6, −16.6, −16.7, −15.6, −16.2. No second below −17.2 dB.
- **Finale:** momentary −11.2 LUFS, the loudest moment, +2.9 dB over the body median.
- flash_check: 0 flashes = PASS (mean luminance 0.037).
- Notes: 148, 12 distinct; top note E5 at 18 %.
- Loop seam:
  - Encoded 2.46. Pre-encode it is 2.24, and rendering sim frames 36 → 37 directly gives 2.29: a crush lands on frame 37 and both tools move 70–85 px a frame. So it is a genuine consecutive step, and the loop is seamless.
  - Normal steps at the start: 1.5, 0.96, 0.77, 1.14.
- Side safe zone, on encoded frames 0, 8.37 and 16.8 s:
  - Caption 0.106–0.831 w.
  - Stage 0.098–0.841 w (wall glow). At frame 0 a burst glow at the right wall reaches 0.856 (decoration).
  - HUD 0.124–0.813 w.
- Frames read from the encoded file at 0, 0.5, 1, 2, 5, 8.37, 16.5, 16.8, 17.2 (1:1 crop of the spike chamber), 17.67 and 18.6 s.

## Nits / doubts

- **The total crush rate peaks around 7–10 s (~250/s) and eases to ~120–200/s before the overflow.** The spike's strokes get longer as the pile deepens, and many balls are dust that can no longer split.
  - The audio stays flat-dense (notes 7–11/s, RMS −16 dB).
  - So "event rate climbing" holds for the first 3 s and the spike's rate climbs to 8 s. It is not climbing to the very end.
- The lead change at 8.4 s is mid-clip rather than late.
- **MAX is at y 660, not press_split2's 560.** At 560 the honest race ran past 24 s.
- The first sims "overflowed" from one-ball wall columns made by the shaft collider. The collider is removed and the spike's stops moved off the walls, so the overflow is now the real pile (a hill crossing MAX).
- A possibly more satisfying pair to try next: **drill vs saw** (a spinning drill bores deep; a circular saw slices a wide shallow line). Same physics hooks: deep vs wide.

## Args and cost

- Args: `--seed` (0), `--ymax` (660), `--prsp` (62), `--dtri` (150), `--tridn`, `--triwait`, `--spkdn`, `--spkwait`, `--clear` (70), `--tlimit` (26), `--label`, `--cap`, `--still --frame a,b`, `--report`.
  - `--cache` pickles/reuses the sim in output/.
  - `--reuse` re-mixes over `<name>_silent.mp4`. Rebuild it first with `ffmpeg -i <name>.mp4 -an -c:v copy <name>_silent.mp4`.
- Cost: sim about 3 min; Full HD render about 10 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\batch47\press_tools.mp4 (Full HD). Owner review: pending.

Owner review (2026-10-22): "mixed feelings but looks fun" -> ship: 4K, Oct 29 slot 1.
- **4K ship render** (2026-10-22, coordinator, v4 sim cache, no changes): `output/press_tools_ship_9x16.mp4`, h264 yuv420p 2160x3840 60 fps, 18.62 s (1117 frames), 132 MB. −13.99 LUFS, peak −8.62 dBFS, last 0.5 s silent, seam 2.39 (the genuine first-frame step), flash_check 0 = PASS. Notes and events match the Full HD.

Ship (2026-10-22): 4K staged at Schedule/2026-10-29 slot 1.
