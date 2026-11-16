# block_overhang — "Stack blocks past the TABLE EDGE" / "Straight or Staircase?"

- Formula (docs/BRIEF_formula.md) on the BLOCK-STACKING (harmonic overhang) puzzle: can the top block of a stack hang COMPLETELY past a table edge? Obvious answer no; true answer yes, with 4 blocks.
  - Mochi (coral) stacks STRAIGHT and greedy: a straight column, pushed out a little more each time. 3 tries (5, 7, 9 blocks); it always tips at ½.
  - Bolt (mint) builds the HARMONIC staircase: each new block goes UNDER the stack; block j (from the top) overhangs the one below by 1/(2j) = ½, ¼, ⅙, ⅛ … Then keeps going: 57 blocks.
- **Frame 0 / goal / meter:**
  - Caption "Stack blocks past the TABLE EDGE" / "Straight or Staircase?". Rule line: "Goal: top block COMPLETELY past the edge".
  - One dashed TABLE EDGE line through both tables (same x = 560); the air past it is a faint gold hatched zone ("PAST THE EDGE").
  - Shared meter at 0.72-0.78h: OVERHANG (in blocks) 0 → 2½ with "→ ∞", gold GOAL tick at 1; a coral bar (Mochi) and a mint bar (Bolt, gold past 1), live values. A coral wall at ½ after her first tip.
  - Frame 0: Mochi's 5-column at 0.40 with its COM dot; Bolt has 1 block and the 2nd is sliding under (lands 0.10 s).
- **Honest statics:**
  - Straight column of any height: COM over the edge at overhang ½. Pushes 0.40 → 0.44 → 0.47 → 0.505 (white COM dot + plumb line, turns red past the edge). The tip is a rigid column pivoting on the table corner (θ'' = g(ε cos θ + H/2 sin θ)/I_pivot, g = 3600 px/s²), then at 0.21 rad each block goes to a scene-local 2-D rigid-box engine (SAT normal + probe points, sequential impulses with friction 0.30 and restitution 0.22, speculative contacts, position projection, sleeping). Impacts feed the clatter SFX.
  - Wobble ticks near the tip point are a small cosmetic rock about the corner (≤ 2.6°), tapping down one 16th later, twice.
  - Bolt: right end of block i in an n-stack = (H_n − H_(i−1))/2; overhang = H_n/2: 4 = 1.042 (top block 0.04 clear of the edge), 10 = 1.464, 20 = 1.799, 31 = 2.014, 57 = 2.315. Every COM sits exactly on the support corner (ideal limit); the whole-stack gold COM dot sits on the edge line (shown up to ~10 blocks). The harmonic series diverges: NO LIMIT is true.
- **Music = the clock:** W. A. Mozart, Piano Sonata K. 545, 1st mvt (1788; Mozart d. 1791). Mutopia-2013/09/01-998 MIDI, `<SOUNDFONTS_DIR>\scores\mozart_k545\K545-1.mid` (SOURCE_mutopia_998.txt; engraving CC BY-SA 3.0, notes PD).
  - Cut: bars 1-8 (theme + scale runs, vb 0-32), then the closing bars 71-73 (vb 32-43 = score beats 280-291).
  - Tempo (s/beat): 0.45 theme, 0.42-0.41 runs, 0.40 closing arpeggios, ritardando 0.56/0.66 into the final C chord.
  - Every Bolt block and every Mochi drop/push/tick lands on a score onset. Bolt: vb 0, 4, 8 (IT FLOATS on the bar-3 downbeat), 10, 12-15, then 21 blocks on the runs (gaps 1 → ½ beat), #31 on the closing tonic (vb 32), #32-#57 one per 16th of the arpeggios, NO LIMIT on the final chord (vb 41).
- **Key times** (clip s): first block 0.10; Mochi tip 1 at 1.57 (clatter 2.63); IT FLOATS 3.70; #10 7.30; Mochi tip 2 8.81 (clatter 9.98); #20 11.09; tip 3 12.56 (clatter 13.71); 2 BLOCKS 13.98; Mochi's table fades 14.2-14.8; #57 17.26; NO LIMIT 17.74; dissolve from ~20.4; clip 20.99 s (1260 frames).
- **Sound** (all in the bed; sidecar = silent markers):
  - Theme on violin + harp an octave down (mid register), runs on harp + celesta + soft strings, left hand on pizz + contrabass, half-bar string pads from bar 3, choir + horns from bar 7, brass on the closing bars; timpani on bars 5/7 and on 2 BLOCKS, a reverse-cymbal swell into 2 BLOCKS, a roll into the final C-major tutti (×0.55). `synth_plink` per melody note.
  - SFX (scene synths, no noise): a wooden tok per Bolt block (pentatonic, pitch rises with the overhang), a duller tok per Mochi block (pitch rises per level), a soft knock per push, tiny tick-ticks while wobbling, the clatter = one wood knock per engine impact (gain by impact speed), bells on IT FLOATS / 2 BLOCKS / NO LIMIT. All ≥ 12 ms apart, gain ÷ √density.
  - `peak_db=None`. Preview: −14.00 LUFS, peak −5.6 dBFS; per-second RMS −19 (theme) → −15 (runs) → −13.9 (finale); last second silent.
- **Laptop:** 1 Python process (BLAS threads 1) + x264 `-threads 2` (`Writer2`).
- **Commands:** `NF_SCALE=1.0 NF_FAST=1 python scenes/block_overhang.py --still --frame N` · `NF_SCALE=1.0 python scenes/block_overhang.py --label v1` · `--report` · `--audio` (mastered preview wav).
- **Checks** (encoded Full HD, `output/block_overhang_v1_9x16.mp4`):
  - Video: h264 yuv420p 1080x1920 at 60 fps, 1260 frames = 21.00 s.
  - Loudness: −14.00 LUFS, peak −5.57 dBFS, last 0.5 s at −74.7 dBFS. Per-5 s RMS −18.8 / −19.4 / −15.0 / −16.4 (finale second −13.9 on the preview).
  - flash_check: 0 flashes = PASS (mean luminance 0.023).
  - Loop seam: encoded mean delta 0.573 (good band); the last frames dissolve to the pre-roll state.
  - Side safe zone: key content x 0.107w-0.84w (faces at 116, meter to 866 + "→ ∞", top-block labels to ~900); only table slabs, the floor band and the gold hatch go wider.
  - Frames read (Fast stills + encoded): 0, 1.67, 2.4, 2.75, 3.75, 5, 7.3, 9.9, 10, 14, 15, 16.7, 16.9 (1:1 crop of the 54-block curve), 17.8, 18.2, 20.9 s; contact sheets of all three topples.
- **Engine lessons:** perfectly aligned stacks put every corner exactly ON the neighbour's boundary → inset probes + edge probes; per-vertex min-axis normals made leaning slabs slide up → one SAT normal per pair; full position projection hid contacts from the velocity solver (velocity ran away) → speculative contacts (1.5 px margin).
- Delivered `<VIDEOS_DIR>\batch44\block_overhang.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-19): "may work if you think so" -> decide after the early-breakouts research; if yes -> 4K Oct 26 slots 2-3.

Decision (2026-10-20): ship -> 4K, Oct 26 slot 2.
