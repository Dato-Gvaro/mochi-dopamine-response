# neon_trails4 — Wall Hugger vs Cutter (batch29, 2026-10-12)

## RETIMED (2026-10-12, coordinator: the slow 8th-note start would fail the hook rule)
- **Speed:** the bikes now ride the 16ths from GO (9.3 cells/s at 140 bpm). There is no slow phase; the music opens straight into the driving groove (hook bar → 1 build bar → the drop at 3.43 s).
- **Game:** a longer game was needed, so seeds were re-searched on 20x24 and 22x24 with a widened draw (seeds ≥ 100000: any rim start, free thresholds). **Seed 100056 on 22x24:**
  - **CUT OFF:** at step 28 (3.75 s) Bolt's CUTTER slices 354 of Mochi's 471 reachable cells, just after the drop.
  - **Lead:** Bolt leads on SPACE for the whole race.
  - **Finish:** Mochi's WALL HUGGER fills her 117-cell box without wasting a cell. Bolt traps himself inside his own zig-zag lattice and hits a wall at step 145 (16.29 s, on the final chord, a half-bar landing). Mochi has 0 cells left: **by ONE STEP**.
  - **Late lead change:** at step 143, only 0.2 s before the crash. It is too late for a readable banner; the SPACE bar flips instead.
- **Clip:** T = 20.03 s at 140 bpm.
- **Checks:**
  - LUFS -14.03, peak -2.49 dBFS, last 0.5 s -90.3 dBFS.
  - flash_check 0.
  - Seam: post-encode 0.581, pre-encode 0.0546 (normal 0.0556), exact.
- **Doubt:** about 45 % of the arena is still empty at the end (the cut-off half is never re-entered). The 1-step finish and speed came first.
- The original seed-409 notes below are history (that seed is too short at 16ths).


Built from the owner's review of neon_trails3: "the song is better, but their movement is not — let them do different approaches and a challenge over which approach is better." v1-v3 are untouched; the music ("Night Drive 140") and the look are kept.

## Duel (16x21, seed 409; real rules, deterministic)
- **MOCHI "WALL HUGGER":** straight while the move keeps ≥ 0.8 of the best room; otherwise she turns toward the bigger space. She makes long rim runs, then tight U-turn pillars (rectilinear and patient).
- **BOLT "CUTTER":** a 45° zig-zag, alternating one cell on each of two headings. A blocked heading reflects like a light ray, so his diagonals bounce across the middle and slice the arena. He leaves the pattern only to survive (room < 0.85 of the best).
- **Story:**
  1. "CUT OFF! -67 cells" at 8.79 s and "CUT OFF! -76 cells" at 12.21 s: the CUTTER leads early.
  2. The music's drop lands at 13.71 s.
  3. "MOCHI TAKES THE LEAD!" at 15.11 s.
  4. Bolt hits a wall at 17.14 s, on the final A minor: "WALL HUGGER beats CUTTER by ONE STEP!" (Mochi has 0 cells left).
- **Search:** ~2.5k seeds per board on 14x19, 16x21 and 18x22, keeping finishes with ≤ 10 cells margin. Seed 409 has the clearest early-cutter / late-hugger swing and the best line art.

## Look
- Rule names float above each bike.
- One slim SPACE bar (Voronoi territory). On frame 0 it shows the final split, and it blends to 50/50 during the de-rez.
- Low light walls, white-hot heads; same synthwave sky as v1-v3.
- Frame 0 = the finished line art: bouncing diagonal chevrons plus rim and pillars. It de-rezzes to the start by 0.72 s; "GO!" at 0.86 s.

## Music
- "Night Drive 140", ORIGINAL (from neon_trails3), A minor, 140 bpm.
- **Clock:** the bikes ride the 8ths before the drop and the 16ths after it. The drop is placed at the bar nearest the turning point, with at least two bars of 16ths.
- **Layout:** hook bars → 2-bar build (snare roll, riser) → drop → a climb on E → the final A minor on the loser's crash.
- Every turn is a pluck on the grid.

## Checks (<VIDEOS_DIR>\batch29\neon_trails4.mp4, Full HD, 20.90 s)
- h264 yuv420p 1080x1920, 60 fps, 1254 frames.
- Pre-encode seam 0.0524, equal to the normal frame delta of 0.0529, so the loop is exact.
- flash_check: 0 flashes.
- LUFS -14.02, peak -2.92 dBFS, last 0.5 s -90.3 dBFS; post-encode seam 0.611 (good band).

## Args
- `--seed 409 --cols 16 --rows 21` (defaults), `--bpm 140`.
- `--still --frame ...`, `--silent`, `--audio-only`, `--report`.

## Doubts
- **The early phase is slow.** Before the drop (0.9-13.7 s) the bikes ride 8ths at 4.7 cells/s; the 16ths come in the last 3.4 s.
- **About 45 % of the arena stays empty at the end.** The cut-off areas are never used.

## Owner review
- pending
- Owner review (2026-10-12): ok (the opening rewind is the intended hook) -> APPROVED, 4K (Oct 15 slot 3).
