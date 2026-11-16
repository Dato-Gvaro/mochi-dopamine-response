# ol_wall_collapse (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md, docs/BRIEF_overnight_1023.md). Skeleton: a ×2 chain (every falling brick knocks loose 2 more) driven by a steady wrecking ball, toward a named end state; concrete objects (a brick wall, a steel ball on a chain), one obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every falling brick knocks loose ^2 MORE^|until the whole wall is ~DOWN~` (`^x^` = the current front brick's hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_wall_collapse.mp4` (v2, Full HD, seed 1, label fhd2, 17.37 s, 1042 frames). No 4K yet.
- Different from cannon_split (two small side-view castles shelled by cannonballs): one tall wall that fills the arena, one pendulum wrecking ball, stair-step mortar cracks, a single rubble heap, a toppling last section.

## World (logical 1080x1920, static camera)
- Arena: thin white frame 128-888 × 318-1226; the ground is its bottom line. Wall: 1,480 bricks, running bond, 18 cells × 80 rows, cell 26 × 10 px, x 392-860, y 424-1225.
- Brick look: mortar behind every standing brick (holes stay black), face inset 1.1 px, light top edge, dark bottom edge, 3 speckles. Colour = one narrow gradient by height: deep brick red (h 0.99, S 0.70, V 0.64) → terracotta → ochre at the top (h 0.09, S 0.62, V 0.80); per-brick tone ±4.5 % in 3 steps.
- Wrecking ball: R 56, brushed steel (fixed top-left light, warm brick bounce-light on the right), lug, oval chain links up to a crane trolley above the frame (y 230, hidden). Contact height y 840, chain 610 px, amplitude 0.30 rad.
- Swing = one 2/4 bar (1.579 s): θ = −A·|sin(π s)|, i.e. it rebounds off the face on every bar downbeat. The trolley glides right during the back-swing (smoothstep over 15-70 % of the bar) so every blow lands on the face's bulk (4th-nearest touching brick, then 22 px deeper; the pre-roll's first blow 8 px).
- HUD: meter y 1290 (brick gradient, white marker, "DOWN n%", gold WALL DOWN goal from frame 0); counter y 1488 "N" + "×2" pill (front hue, pops each time the count doubles) + "BRICKS DOWN"; watermark "DOPAMINE.EXE" right-aligned 888, y 1256, 35 %.

## Rule / model (exact event simulation, scenes/ol_wall_collapse.py `simulate`)
- Ball blow: every standing brick the disc overlaps falls (7-16 per blow).
- A brick that falls claims the 2 cheapest INTACT bricks: cost = distance with above ×0.55, below ×1.35 (masonry fails upward over an opening, so no long overhangs), seeded ±12 %, reach ≤ 200 px. A claimed brick shows a stair-step crack run through the mortar from its parent (0.12 s, warm white, fades by 0.4 s, alpha scaled down when dense), a gold edge glint on arrival, then hangs cracked + nudged out; it wobbles its last 0.2 s and falls at claim + D × U(0.70, 1.30), snapped up to the 16th grid.
- D is calibrated per seed (seed 1: **D 2.70 s**, pre-roll from the hit at −2.96 s) so ~75 % is down just before the cadence; everything still standing then topples ON the cadence with the ball's last blow (390 bricks): its base gives way and it crumbles straight DOWN under gravity (v2: released at rest, vy 0, a slight inward lean ≤ 45 px/s at the top, spin ±2.2 rad/s; `--crumble`). v1 tipped it as a rigid slab with ω 0.85 rad/s, which launched the top up-left; the owner saw the column "jump forward instead of falling down".
- Debris: rigid rectangles, gravity 1,800 px/s², one bounce, settle on a height map with an angle-of-repose slide (overlap 0.72 = the heap's depth toward the camera); the heap has a dark solid core so no black gaps show.

## Timeline (clip s, seed 1)
- Frame 0: whole wall standing with a dented hole at ball height, cracked bricks round it, the ball 0.2 s from its next blow (first event 0.197 s).
- Down per second: 21, 36, 57, 67, 96, 126, 156, 207, 264, 353, 444, 563, 704, 856, 1,011 → **1,480 at the cadence. Growth ×70.5.** Count doubles at 1.78, 3.36, 6.32, 8.88, 11.64, 14.41 s.
- Falls per second: 16, 21, 10, 29, 30, 30, 51, 57, 89, 91, 119, 141, 152, 155, then 469 in the last 0.41 s (topple). Busy 16ths per second: 4, 5, 4, 5 … 5.
- Ball blows (t, knocked): 0.20 (11), 1.78 (15), 3.36 (13), 4.93 (13), 6.51 (13), 8.09 (13), 9.67 (16), 11.25 (10), 12.83 (11), **14.41 cadence (8 + 390 topple)**. Trolley x 397 → 761.
- **Cadence 14.41 s** (score bar 98 downbeat, A): the last section crumbles straight down onto the heap (settled by ~15.3 s), counter rolls gold 1,480, meter 100 % + goal glow, frame warms to gold, 9 gold glints run left → right along the heap top (0.30-1.26 s after). The ball swings free through the empty space; the trolley glides back. Hold → 0.6 s dissolve into the pre-roll (t −0.6..0). 11 swings = **17.37 s, 1042 frames**: the ball is back in phase (no ghosting).

## Sound
- **Music played as music:** L. v. Beethoven, Symphony No. 7 in A major, Op. 92, II. Allegretto (1811-12; Beethoven d. 1827, PD). Source: Mutopia `BeethovenLv/O92/Symphony7_2` (Litolff edition), listed **Public Domain**; saved at `<SOUNDFONTS_DIR>\scores\beethoven_symphony7_2\` + `SOURCE_mutopia.txt` (downloaded 2026-10-24). Not on the used/banned lists, not kid-coded, no earlier scene uses it (Beethoven 5, Egmont, Ode, Moonlight 3, Rage Penny are other works).
- Score beats 175.75-194 (bars 89-98): the fortissimo tutti statement — winds, horns, trumpets and timpani on the theme's long-short-short rhythm, violin I's famous counter-melody, the string triplets — to the cadence on A. One steady tempo, **76 bpm** (Beethoven's own ♩ = 76). All 12 score parts mapped to lib/orchestra (fl, ob, cl, bn, hn, tp, timp, vln I + strings, vln II strings, vla, vc, cb). Cadence: the score's A-minor tutti chord held 2 s (strings, horns, trumpets, winds, cello/contrabass A, timpani A), rolled harp, a celesta glint run.
- SFX (×0.60, all tonal, no noise): a fired-clay "clack" (partials 1 / 2.71 / 5.4, 22 ms ring, 1 ms tonal tick at 2.9 kHz) per 16th with falls, pitched to a note the score is sounding there (E5-A6), log-scaled clusters (a rattle) as the collapse widens; each blow = a deep tonal thud (sine dropping onto the bass note in ~30 ms + octave + twelfth) + 5 lower clacks; the topple = a 0.9 s rattle down the A-minor chord, a bell on A5, chime notes on the glints. SFX events per second: 11, 12, 10, 22, 23, 30, 41, 45, 57, 58, 60, 67, 69, 64, 60, 17.
- `level_bed` (+3 dB crescendo, cadence +4 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux without `-shortest`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1042 frames, 17.37 s. **flash_check PASS** (0 flashes, mean lum 0.018).
- **−14.01 LUFS**, peak −6.04 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.41 %. RMS per second (muxed): −18.4, −17.9, −18.9, −17.8, −18.0, −18.2, −17.3, −18.2, −16.7, −16.5, −17.7, −16.1, −16.7, −17.1, −15.5 (cadence), −14.9, −22.1, silence.
- Mean relative luminance (encoded): frame 0 0.041; 7 s 0.041; 13 s 0.032; cadence 0.029; **finished heap (16.5 s) 0.026**; last frame 0.042 (= pre-roll).
- Seam: pre-encode last → 0 = 0.72 (the ball at full speed + the counter 20 → 21: a real step; 0 → 1 is 0.28). Encoded (check_clip) **1.32**, mostly H.264 noise on the fine brick texture (decoded frame 0 is itself 1.20 off its source; dissolve step 1040 → 1041 decodes at 1.41).
- Frames read from the mp4 at 0, 0.5, 1, 2, 7, 13, 14.42 (cadence), 15, 16, 16.5 and the last frame; 1:1 crops at frame 0 (ball, dented face, cracked bricks) and 7 s (stair-step cracks, loosened bricks, tumbling bricks).

## Flags
`--seed (1) --label --cap --still --frame a,b --dry --calib --audio --sound 0 --sfx (0.60) --fin (2.0) --bpm (76) --D (calibrated) --jpre (-2) --endfr (0.75) --reach (200) --upw (0.55) --fuse0/--fuse1 (0.70/1.30) --bite (22) --bite0 (8) --crumble (45) --amp (0.30) --g (1800) --rows (80)`. Calibration + sim + debris ≈ 10 s; the full FHD clip renders in ~4 min.

## Doubts
- The "2 more" rule is exact while intact bricks remain within reach, but a falling brick claims 2 while its own claim lags one fuse, so claimed ≈ 2 × fallen: from ~8-9 s the wall is all cracked/claimed and late bricks knock nothing loose (80 of 563 falls before t_c − 1.25 D got fewer than 2: 5 at 8-9 s, 29 at 9-10 s, 46 at 10-11 s; none earlier). Visually every brick that falls was cracked by someone; nobody can count at 150/s.
- Falls per second dip at 2 s (10) and are flat at 3-5 s (29-30): the early generations are still lumpy. The ball blows every 1.58 s and the music carry it; busy 16ths 4-5/5 throughout.
- Frame 0 is the whole wall + a dent + the ball 0.2 s from impact; only a few bricks are in the air (the pre-roll rubble has landed). Busy by colour/structure, not by debris.
- The last section is the ragged right edge of the wall (the far side from the ball), not a clean rectangle; it pancakes down into a small pile against the right frame line. The counter jumps to 1,480 on the cadence while that slab is still in the air (it counts bricks that left the wall).
- After the last blow the ball swings free through the empty space and partly out of the right of the frame before the trolley glides back (needed for the loop).
- Cadence chord is the score's A minor (no Picardy third): majestic, not bright.

## Owner review
- 2026-10-24, v1: liked it; fix "at the last hit the remaining column jumps forward instead of falling down" → v2: the last section crumbles straight down (only that changed; timing, ×70.5, music, checks identical: flash PASS 0, −14.01 LUFS, peak −6.04, seam 1.32). Read at 1:1 every 0.1 s from the last blow (14.40 s) to the landing (15.5 s): no upward or forward launch.

- Approved (v2). 4K ship render: `output/ol_wall_collapse_ship_9x16.mp4` (NF_SCALE 2.0, label ship, seed 1, calibrated D 2.70 / jpre −2, x264 threads 2 + rc-lookahead 12): h264 yuv420p 2160x3840 60 fps, 1042 frames, 17.37 s; flash PASS (0, mean lum 0.018); −14.01 LUFS, peak −6.04 dBFS, last 0.5 s silent; seam 1.20. Frames 0, 420, 880 read (+1:1 crop at 7 s).

## Upload draft
- Titles: "Every falling brick knocks loose 2 more… until the whole wall is DOWN 🧱 #satisfying #physics #shorts" · "One wrecking ball, 1,480 bricks, and a chain reaction 🧱💥 #satisfying #physics #shorts" · "Each brick takes 2 more with it… watch the whole wall go 🧱 #satisfying #physics #shorts".
- Pinned comment: "the ball only ever hits the left side, the cracks do the rest… which part did you think would be the last one standing?"
