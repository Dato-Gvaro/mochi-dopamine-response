# ol_spiral_maze (Dopamine.exe)
- Sequel of ol_spiral_center (owner idea 2026-10-22: "a maze like that ... on the way the ball gets x2 bonus count"). New scene file, character-free (docs/BRIEF_channel2.md). Skeleton: ×2 growth toward a named end state + a rainbow brick maze eaten to the centre.
- Caption (baked, `--cap`; `--cap ''` = base): `Every gate ^DOUBLES^ the balls|until they reach the ~CENTER~` (`^x^` = swarm-front colour, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_spiral_maze.mp4` (**v2**, Full HD, seed 3, label fhdv2, 15.92 s, 955 frames). No 4K yet.
- Owner review of v1 (2026-10-23): "balls and bricks with the same colour make it hard to see where the balls are" → **v2**: every ball is one warm white #FFF6E0 (never in the brick gradient) with a 1.2 px dark outline (#0A0A12, 90%) and a soft one-frame trail (warm white 24%); at a split the parent and its twin flash white-gold (1.0, 0.86, 0.52), fading over 0.15 s. The lead-ball trails/glow (≤ 48 balls) are warm white too. Gold stays reserved for the CENTER. Sim, timing, music and everything else unchanged. (v1 tinted the balls with the brick gradient at their radius, S ×0.55.)

## World (logical 1080x1920)
- Arena: one white circle, centre (508, 800), R 392 (x 116-900, inside 0.10-0.84 w). Gold CENTER disc r 46 with a hugging glow.
- Maze: 5 concentric brick walls of 1/2/3/4/6 rows (row 9 px, 2 px row gap, corridors 26 px), bricks 13 px long, staggered: **1,350 bricks**. Openings: 2/1/1/1/0 per wall (3 bricks wide, staggered 137.5°); the 6-row inner shell has none.
- Toughness by wall (`--hp`): 1, 2, 3, 3, 4 hits. A hit that does not break dims the brick and draws a crack line.
- Colour rule: one ordered radial gradient rim → core, S 0.60-0.72, V 0.96: aqua (h .47) → azure → blue → violet → rose (h .885). Gold = the goal only (core, meter goal, CENTER word, finale glow). Balls: warm white #FFF6E0 with a thin dark outline (v2).
- ×2 gates (23): thin white rings (r 14) with "×2", on the corridor centre lines. Corridor 0 has a RUNWAY of 4 gates 0.30 rad apart right after a 1.35 rad gate-free entry stretch, then 7/5/4/4/3 evenly spread gates per corridor (minus the entry/runway window).
- HUD: depth meter y 1252 (x 170-846, gradient fill, white marker, gold CENTER goal from frame 0); counter y 1478 "N" + "BALLS" + a "×2" pill in the swarm-front colour; watermark "DOPAMINE.EXE" (900 right, 1338), 35%.

## Rule / physics (fixed dt 1/60, 4 substeps, numpy over all balls)
- Ball r 5, constant 560 px/s; ball vs brick = closest point on the brick's annular sector (2 nearest rows × 3 bricks), mirror reflection about the summed normal; arena = mirror circle. No ball-ball collisions.
- **Every ball that enters a gate it has not used becomes 2** (twins ±16°, both inherit the used-gate mask, so each gate doubles a lineage once). Physical cap 4,000 balls, beyond it a ball's weight doubles (never reached: 1,925 physical = true count).
- CENTER = the first ball within r 51 of the centre. Meter = depth (closest approach of any ball, 0 at the rim, 100% at the core).
- Seed = entry angle + heading. Seed search `--search a b` prints SCORE (centre time, end count, balls at 1/2 s, longest meter stall, late rate).
- Exponential swarm vs finite maze: the centre time is set by when the swarm outgrows the maze, so denser gates only made it faster (7-9 s). The runway gives the hook (×16 once, ~1 s), the sparse gates elsewhere set the ~13 s length.

## Timeline (clip s, seed 3)
- Frame 0 = sim frame 44 (36 frames of pre-roll for the loop dissolve): 1 ball in the outer corridor, maze intact. First ×2 at **0.25 s**.
- Balls: 1, 9 (1 s), 18 (2 s), 32, 58, 91, 132, 212, 308, 427, 618, 874, 1,281, 1,757 (13 s), **1,925 at the CENTER**.
- ×2 waves (count passes 2^k): 0.25, 0.67, 0.90, 1.84, 2.91, 4.26, 5.95, 7.48, 9.51, 11.42 s. The badge also pops (smaller) on every music beat that had a split, so it never slows.
- Events per second (splits + breaks + cracks): 37, 63, 135, 220, 279, 301, 417, 474, 531, 645, 625, 725, 863, then ~925/s in the last 0.32 s. Splits alone 8 → 475/s.
- Depth: 5, 15, 29, 29, 46, 46, 46, 49, 52, 66, 69, 73, 77, 82% (stalls ~2 s at 46% while the swarm chews wall 3).
- **CENTER 13.32 s**, 1,308 of 1,350 bricks broken. Finale: 4 px shake; a warm gold glow swells and settles (no white); 2 gold rings; a calm wave (650 px/s) crumbles the 42 bricks left (3 pieces each, drag τ 0.7 s, fade 1.2-1.7 s); every ball pours into the core along a swirl (0.5-1.6 s, accelerating) and the core grows ×1.45 as it absorbs them. Counter holds 1,925.
- Hold 2.0 s → 0.6 s dissolve into the pre-roll. **15.92 s, 955 frames.**

## Sound
- **Music played as music** (owner rule 2026-10-23): Handel, "Hallelujah" chorus, Messiah HWV 56 (1741; Handel d. 1759, PD). Source: Mutopia "Mutopia-2015/01/17-459" (Public Domain), `<SOUNDFONTS_DIR>\scores\handel_hallelujah\hallelujah-mids\combined-score.mid` + `SOURCE_mutopia_459.txt`. Not on the used/banned lists, not kid-coded, not used by any earlier scene.
- Beats 4-26 (`--b0 4`): the intro's second "Hal-le-lu-jah" (bar 2), the choir's entry at bar 4 (4.9 s) and the first phrase to its D-major cadence on beat 26. One steady tempo, **99.3 bpm**, solved so beat 26 = the CENTER hit. Gates, core and goal mark breathe on every beat.
- Arrangement (lib/orchestra): violins I/II + viola on strings, cello + contrabass (8vb), oboe doubling the sopranos, SATB on choir aahs, timpani D2 on beats 12/16/20/22/24. CENTER: held D-major chord (D3-D5) on strings + choir, trumpets D4 F#4 A4, cello/contrabass D, timpani, soft boom.
- Leveller on the bed (`level_bed`): 0.8 s RMS gain ride, the body follows a −1.5 → +1.5 dB crescendo, the cadence sits +3.5 dB above it.
- SFX (×0.40, one merged timeline ≥ 12 ms apart, gain ÷ √(rate/10)): porcelain tick per break (partials 1.25-4.3 kHz), a softer crack per hit (0.9-2.9 kHz), a tonal pop per split (sine gliding up a third on D-major pentatonic D5-B5, octave up after wave 6); burst ticks at the finale. 885 events; sounded per second 27, 41, 51, 59, 71, 66, 77, 76, 76, 78, 77, 79, 78 (saturates at the 12 ms floor from ~6 s).
- `audio.master(peak_db=None, reverb=0.5)`; last 0.6 s digital silence.

## Checks (encoded Full HD; v2 identical except where noted)
- v2: flash_check PASS (0 flashes, mean lum 0.017; mean RGB 0.070-0.095 per second), −14.01 LUFS, peak −3.63 dBFS, last 0.5 s digital silence, encoded seam 0.900 (normal 1→2 step 0.994). 1:1 crops read at 1, 6 and 10 s: every ball reads instantly against all rings.
- h264 yuv420p 1080x1920, 60 fps, 955 frames, 15.92 s. **flash_check PASS** (0 flashes, mean lum 0.017; mean RGB 0.07-0.09 per second, finale 0.093).
- **−14.01 LUFS**, peak −3.63 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.24%. RMS per second: −18.5, −18.0, −18.5, −18.2, −18.6, −17.4, −17.2, −17.2, −17.3, −16.8, −16.7, −16.5, −16.7, −14.0 (CENTER), −14.3, −42.5.
- Seam: pre-encode last→0 0.090 vs a normal step 0.095; encoded 0.848 (encoded 1→2 = 1.03, x264 grain).
- Frames read from the mp4 at 0, 0.5, 1, 2, 6.5, 13.25, 13.33, 13.83, 14.5 s and the last frame; 1:1 crops of the 1 s swarm and the breached shell at 13.25 s.
- Bug fixed during build: cairo line cap/join leaked between frames (frame 0 drawn with fresh state ≠ every later frame); `draw_world` now wraps each frame in save/restore.

## Flags
`--seed (3) --label --cap --still --frame a,b --dry --search a b --sound 0 --sfx (0.40) --fin (2.2) --b0 (4) --maxdraw (4000)`. Maze/physics (changing any changes the sim: re-run `--search`): `--rows (1,2,3,4,6) --th (9) --cw (26) --tl (13) --gapb (3) --hp (1,2,3,3,4) --opens (2,1,1,1,0) --gates (7,5,4,4,3) --runway (4) --rgap (0.30) --core (46) --br (5) --v0 (560) --split (16) --cap (4000) --leada (0.95) --leadb (1.2)`.

Owner review (2026-10-23): "balls and bricks the same colour, hard to see the balls" -> v2: balls in a distinct warm white.

Owner review (2026-10-23): "good; at the start they look like spermatozoa racing to an egg lol, maybe a pun about it" -> SHIP; the joke goes in the pinned comment only (no innuendo in titles, for ad limits).

Ship (2026-10-23): 4K staged at DopamineExe/schedule/2026-10-30 slot 1.
