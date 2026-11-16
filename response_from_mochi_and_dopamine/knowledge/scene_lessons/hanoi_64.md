# hanoi_64 — "Every disk DOUBLES the moves" / "Guessing or Algorithm?"

- Formula (docs/BRIEF_formula.md) on the TOWER OF HANOI legend: 64 golden disks, one move at a time, never big on small; the minimum is 2ⁿ − 1 moves, so every extra disk doubles the work.
  - Mochi (coral) GUESSES: random legal moves on 5 disks.
  - Bolt (mint) runs the ALGORITHM (the recursive solution) on the same 5 disks, then keeps going: 8, 10, then the tower grows to 64.
- **Frame 0 / rule / meter:**
  - Caption "Every disk DOUBLES the moves" / "Guessing or Algorithm?". Rule line: "Move 1 disk at a time · never big on small".
  - Ladder meter: 5 › 8 › 10 › 16 › 32 › 64? (64 = goal, gold outline). Chips turn gold when reached.
  - Both boards show a dashed gold ghost of the finished tower on peg C (the end state); peg C's label is gold.
  - Readout under Bolt's board: "2⁵ − 1 = 31 / moves for 5 disks", live for the current n.
- **Honest numbers:**
  - Bolt: closed form. After m moves, disk d has moved (m + 2^(d−1)) >> d times, one way round if n − d is even, the other if odd. Disk of move m = 1 + trailing zeros of m.
  - Mochi: seeded random walk (`RandomState(52)`), uniform among the 3 legal moves of each state, backtracks included. 97 moves; she never gets the bottom disk onto C. Same rate as Bolt for the first 31 moves, so at Bolt's solve both counters read 31.
  - Expected random-walk length for 5 disks, A → C: 4,305 moves (exact linear solve over the 243 states) vs 31.
  - 2⁶⁴ − 1 = 18,446,744,073,709,551,615 moves. At 1 move/s (Julian year 31,557,600 s) = 584,542,046,091 years = 585 BILLION YEARS = 42.4× the Universe (13.8 B years). The bars use the true ratio (2.4%).
- **Music = the clock:** J. S. Bach, Prelude in C major BWV 846 (WTC I, 1722; Bach d. 1750).
  - Source: Mutopia #5 (Mutopia-2011/09/12-5), licence Public Domain. `<SOUNDFONTS_DIR>\scores\bach_prelude_c\wtk1-prelude1.mid`, see SOURCE_mutopia_5.txt there.
  - Cut: bars 1-4 (C, Dm7/C, G7/B, C), then the coda bars 32-35 (C7/C, F/C, G7/C, final C chord). Virtual beat vb: 0-16 = score 0-16, 16-28 = score 124-136.
  - Tempo: 0.64 s/beat (one 16th = 0.16 s) to vb 24, ritardando 0.64 → 0.96 over bar 34.
  - Every 16th of the arpeggio = one event: Bolt's move (5 disks: 1 per 16th), a tower drop, a growth step, or a 64-tower move.
  - Phases: 5 disks on slots 0-30 (moves 1-31); 8 disks drop at slot 33, moves on slots 34-47 at 1, 2, 3, 4, 6, 8, 12, 16, 24, 32, 48, 64, 128, 255; 10 disks drop at 49, slots 50-62 at 1, 2, 4 … 768, 1023. Within a slot the moves are evenly spaced, so the note lands on a multiple of a power of 2 = a BIG disk's move (the ruler pattern).
  - Explosion: slots 64-95 (bars 32-33), n = 11…26, then 28, 30 … 50, 53, 56, 60, 64. Bar 34 downbeat = 2⁶⁴ − 1 lands; Bolt starts the 64 tower at 1 move per 16th. Bar 35's final C chord = 585 BILLION YEARS.
- **Key times** (clip s): first Mochi landing 0.02, first Bolt landing 0.10 (disks in flight at frame 0). 5 disks solved 4.90 (31 MOVES!). 8 disks 5.54-7.62 (peak ~800 moves/s, blur ghosts). 10 disks 8.10-10.02 (peak 1,600 moves/s). Explosion 10.34. 2⁶⁴ − 1 at 15.46. 585 BILLION YEARS at 18.54. Dissolve from 21.64, clip 22.24 s (1334 frames).
- **Staging:**
  - Mochi: smug laugh 0.15, worried from 2.2, wow at Bolt's solve, annoyed, angry through the 8-disk blur, annoyed, worried, wow at 2⁶⁴, annoyed at the end. "still lost…" from 5.3 s; her board fades at the explosion, her counter freezes at 97.
  - Bolt: laugh 1.0, a cheer per solve, worried as the tower grows, wow at 2⁶⁴ and at the finale, then laughs.
  - Finale: dark gold box "585 BILLION / YEARS! / 42× the age of the Universe" + 3 soft gold rings (no flash); the years counter rolls during bar 34 while the 64-disks bar outgrows the Universe bar.
- **Sound** (all in the bed; sidecar = silent markers):
  - Bach RH line on harp + a soft `synth_plink` per note; celesta from bar 2; LH held notes on strings_slow; contrabass + strings from bar 3; coda brass (LH +12), choir pads per bar; timpani on bar 32 and on 2⁶⁴; timpani roll over bar 34; final C major tutti (strings, choir, brass, harp roll, celesta, timpani, boom, crash; ×0.62).
  - SFX (scene synths, no noise): a crisp wood/ceramic clack per placement, pitched by disk size on the current bar's chord tones (big = low); at blur speeds only the big-disk moves clack (≤ ~2.5 per 16th). Mochi: a dull soft tick per move (no chord pitch). Drop = 3-clack cascade; growth step = a clack; a bell pair per tower solved; bells on 2⁶⁴ and the finale. All ≥ 12 ms apart, gain ÷ √density.
- **Laptop:** 1 Python process (BLAS threads 1) + x264 `-threads 2` (`Writer2`).
- **Commands:** `NF_SCALE=1.0 NF_FAST=1 python scenes/hanoi_64.py --still --frame N` · `NF_SCALE=1.0 python scenes/hanoi_64.py --label v1` · `--report` · `--search` (Mochi seeds).
- **Checks** (encoded Full HD, `output/hanoi_64_v2_9x16.mp4`):
  - Video: h264 yuv420p 1080x1920 at 60 fps, 1334 frames = 22.23 s.
  - Loudness: −14.00 LUFS, peak −5.56 dBFS, last 0.5 s at −72 dBFS. `peak_db=None`. Per-second RMS: body −18…−19, coda −15, finale chord −13.6 (pre-check on the master).
  - flash_check: 0 flashes = PASS (mean luminance 0.020).
  - Loop seam: encoded mean delta 1.02 against 0.5-0.9 for a normal step here (disks are in flight on both boards every frame); the last frame is the pre-roll at t = −1/60 s.
  - Side safe zone: content x 0.102w-0.835w at 0, 15.47 (2⁶⁴ pop), 16.7 and 20.8 s.
  - Frames read at 0, 0.27, 0.5, 3, 4.95, 7.3, 9.6, 12.5, 15.6, 18.7, 19.8 s; 1:1 crops of the 10-disk blur (9.4 s) and the finale (18.75 s).
- **v1 → v2:** "1 move" singular; the big-number and readout max widths 790 → 730 so their pop stays inside the safe zone.
- Delivered `<VIDEOS_DIR>\batch43\hanoi_64.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-19): "if you think it might work, we can try" -> my call: ship -> 4K.

Owner review (2026-10-19): APPROVED -> 4K.
- **4K render** (`--label ship`, seed 52, `peak_db=None`): `output/hanoi_64_ship_9x16.mp4`.
  - Video: h264 yuv420p 2160x3840 at 60 fps, 1334 frames = 22.233 s.
  - Loudness: −14.00 LUFS, peak −5.56 dBFS, last 0.5 s at −72.2 dBFS.
  - flash_check: 0 flashes = PASS. Seam mean delta 0.87.
