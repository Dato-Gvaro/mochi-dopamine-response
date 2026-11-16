# ol_brick_breakout (DopamineEXE, channel 2)
- Batch 52 (docs/BRIEF_batch52.md). The viral "multiplying balls" brick-wall format, no game names anywhere. Rule: **every brick a ball breaks releases ONE new ball** (the brick's colour), so the balls multiply as the wall goes. End state: WALL GONE on the music's cadence; the stubborn last bricks sit in the top-right corner.
- Different from last_brick (one ball, 1,200 bricks, "even the last one") and brick_tunnel (one ball that speeds up, Mochi vs Bolt): here the ball COUNT is the mechanic.
- Caption (baked, `--cap`; `--cap ''` = base): `Every brick it breaks = ^1 MORE BALL^|until the whole wall is ~GONE~` (`^x^` = newest ball's hue, `~x~` = gold).
- **v3 (below) is the current version** (`--fig diamond`, the default). v2 = `--fig wall` (bit-identical timeline: seed 1420, 8.13 s), archived as `DopamineExe\archive\ol_brick_breakout_v2.mp4`; v1 archived as `archive\ol_brick_breakout_v1.mp4`. The v2 scene file is also at scratchpad `bD55/ol_brick_breakout_v2.py`.

## SHIPPED v3 (batch 56, 2026-10-28): owner "ok" (multi-hit bricks accepted)
- 4K: `NF_SCALE=2.0 python scenes/ol_brick_breakout.py --label ship` (defaults = v3) -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-05\1_ol_brick_breakout.mp4`, 04:00 local Nov 6 (= 19:00 US East Nov 5). FHD review copy -> `archive\ol_brick_breakout_fhd.mp4`.
- Checks (encoded 4K): h264 yuv420p 2160x3840, 60 fps, 909 frames, 15.15 s; -14.01 LUFS, peak -5.18 dBFS, last 0.5 s digital silence; seam 0.509; flash PASS (0 flashes). Events json + audio wav bit-identical to the reviewed fhd3. Frames read at 0, 1, 6, 11.2, 12.6, 15.13 s.

## v3 (2026-10-28, batch 55): a DIAMOND of bricks in the open centre
- Owner review of v2: "ended too soon. Change the classic layout? More bricks, in the centre, a bigger area, the bricks forming some figure."
- **Figure:** a cut-gem DIAMOND (table, crown 28% of the height, pointed pavilion), 194 small bricks (cell 36 x 22) on a 15 x 22 grid centred in the open arena (x 238-778, y 530-1014; arena 128-888 x 318-1226 unchanged). Icy ordered gradient table -> tip (aqua -> cyan -> sky -> blue) with alternating facet bands (lighter / darker) fanning to the tip. Not kid-coded (a gem, not a heart/star).
- **Balls from the edges:** 8 pearl balls start on the 4 arena edges (2 per side) flying inward (+-0.45 rad), V0 1000 px/s, r 9; frame 0 = sim 0.15 s (streaks visible), first break 0.17 s. Streaks kept (7 frames), their opacity eased by sqrt(40/balls) once the arena fills.
- **Same rule:** every BROKEN brick = 1 more ball (from the brick, the hitter's direction turned 14-34 deg). New in v3: **the gem is tougher inside** (bricks take hits: the outline 2, the next ring 3, deeper 4; every hit cracks it: one crack line per hit + a soft light tick). Without it 194 bricks fall in 1.7 s (the new balls chain through the dense figure).
- **The stubborn last brick = the diamond's HEART:** the deepest centre cell is pale gold and takes 24 hits, its count printed on it (24 -> 0). When <= 3 bricks stand they get a gold outline + a soft gold halo, drawn over the balls.
- HUD: "DIAMOND LEFT n%" / "DIAMOND GONE"; caption `Every brick it breaks = ^1 MORE BALL^|until the whole diamond is ~GONE~`; finale "DIAMOND GONE" (78 px).
- **Music:** Figaro overture bars 12-17 (forte tutti from frame 0) spliced at the D downbeat (beat 68) into bars 27-34 (beats 104-136: the D-pedal crescendo = the core being pounded) -> the D-major cadence at bar 35 (beat 136) = the heart breaks. 56 beats at **267.8 bpm**. Timpani D on half notes (crescendo through the pedal), roll on the cadential A. `--music c`.
- Every crack: a soft tonal "crumb" tick on a chord tone (G4-B5), sampled >= 30 ms apart, never within 14 ms of a break, gain / sqrt(rate/6).

### Timeline v3 (clip s, seed 1)
- Breaks/s 4, 8, 13, 18, 22, 22, 17, 29, 22, 23, 12, 3, 1. Balls at s 8, 12, 20, 33, 51, 73, 95, 112, 141, 163, 186, 198, 201 -> **202** (x25). Doublings 1.51, 2.83, 4.47, 7.37 s.
- 11.05 s: 3 left; 11.14 s: **only the heart left**, alone 1.41 s under ~200 balls (its count runs down).
- **12.55 s**: the heart breaks on bar 35's downbeat: gold ring, sparkles, DIAMOND GONE, counter 202 gold. Hold 2.0 s + 0.6 s dissolve. **15.15 s, 909 frames.**
- Seeds 1-4 all end on the heart (1.1-1.7 s alone, 14.5-16.2 s clips); seed 1 kept (busiest opening of the 4).

### Checks v3 (encoded Full HD, fhd3)
- h264 yuv420p 1080x1920, 60 fps, 909 frames, 15.15 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -5.18 dBFS, last 0.5 s digital silence. RMS/s -19.5, -18.5, -18.8, -18.4, -18.4, -17.3, -18.2, -17.0, -17.7, -16.8, -16.8, -17.5, -16.0, -13.9 (cadence), -26.9, silence. 846 SFX events.
- Seam mean |delta| 0.640 (in the good band).
- Frames read from the mp4 at 0, 0.3, 1, 3, 6, 9, 11.2, 12.0, 12.58, 13.3, 15.1 s; 1:1 crop at 1.0 s (cracked bricks, chunks, the "24" heart).

### Doubts v3
- **New mechanic beyond the brief:** bricks need 2-4 hits (and the heart 24). It is what makes it last 12.5 s with fast balls; the rule "every brick = 1 more ball" is unchanged.
- Breaks/s fall after 10 s (the tough core); the crack ticks on the heart keep the sound climbing.
- At 200 balls the arena is busy; the heart reads by its gold halo + number, small (36 x 22) at phone size.
- Facet shading is subtle; the silhouette carries the "diamond".

### Flags v3
`--fig (diamond|wall) --cols (15) --rows (22) --cw (36) --ch (22) --fdy (0) --r (9) --v0 (1000) --ne (8) --hp (4) --hb (2) --hpmode (depth) --core (24) --corey (-40) --f0 (9) --seed (1) --music (c)`.

### Upload draft v3
- Titles: "Every brick it breaks = 1 more ball… until the diamond is GONE 💎 #satisfying #physics #shorts" · "200 balls vs the last brick of the diamond 😤 #satisfying #physics #shorts" · "194 bricks, 8 balls… every brick makes a new ball 💎 #satisfying #physics #shorts".
- Pinned comment: "200 balls flying around and the heart of the diamond still took 24 hits… did you think it would hold?"

## v2 (2026-10-28, batch 53): fewer, FASTER balls, busy from frame 0
- Owner review of v1: "balls move kinda lazy, no engagement at start, maybe fewer balls and faster?" Same rule ("every broken brick = 1 more ball", honest elastic physics), same look, HUD, caption, stubborn last brick and WALL GONE on the chord. Changed:
  - Wall 8 x 8 = **64 bricks** (cell 95 x 34; v1 10 x 12 = 120, 76 x 26) -> 65 balls at the end (v1 121).
  - Ball speed **V0 1000 px/s** (v1 470, x2.1), radius 12 (v1 9).
  - Motion streaks: 7 frames, head opacity 0.42, width tapering 0.86 -> 0.24 of the ball (v1: 5 frames, 0.30). At 1000 px/s a streak is ~110 px long.
  - Frame 0 = 0.12 s before break 4 (`--n0 5`): **4 balls already flying**, first break at 0.11 s, 3 breaks in the first 0.5 s, 6 in the first second.
  - Music: **bars 12-17 only** (the forte tutti from frame 0, timpani D on the first frame) -> bar 18's D-major downbeat = the last brick. 24 beats at **260 bpm** (v1: bars 1-7 + 12-17, 52 beats at 275). Bars 16-17 (the cadential A, timpani roll) = the stubborn corner. `--music ab` = v1's cut.
  - Hold 2.0 s (v1 1.75).
- Seed search (`--search`, ~0.3 s per sim): 1,500 seeds at the v2 settings, kept clip 4.9-6.2 s + last brick alone >= 0.6 s + >= 5 breaks in the first second: 228, 943, **1420** (best: last brick alone 0.99 s, 3 left for 1.65 s).
- **v1 timeline/sim/sound**: `--seed 1412 --cols 10 --rows 12 --ch 26 --r 9 --v0 470 --n0 6 --hold 1.75 --music ab --trail 5 --traila 0.30` (only the streak width taper differs from v1's 2R(0.80-0.11q)); the v1 mp4 is archived at `DopamineExe\archive\ol_brick_breakout_v1.mp4`.

### Timeline v2 (clip s, seed 1420)
- Frame 0: full wall (95.3% left, bottom row pitted), 4 streaking balls, first break 0.11 s.
- Breaks/s: 6, 5, 19, 28, 2, 1. Balls at s: 4, 10, 15, 34, 62, 64 -> **65 (x16)**. Doublings at 0.75, 2.15, 2.81, 4.54 s.
- 3.88 s: 3 bricks left (gold outline); 4.44: 2 left; 4.54: **1 left** (col 0, row 0 = the top-LEFT corner) alone for 0.99 s with 64 balls flying.
- **5.53 s**: the last brick breaks on bar 18's downbeat: gold ring, sparkles, WALL GONE, counter 65 gold. Hold 2.0 s, 0.6 s dissolve into frame 0. **8.13 s, 488 frames.**

### Checks v2 (encoded Full HD, label fhd2)
- h264 yuv420p 1080x1920, 60 fps, 488 frames, 8.13 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -3.96 dBFS, last 0.5 s digital silence. RMS per second (audio test): -19.9, -19.0, -18.4, -17.9, -18.3, -15.7 (cadence), -13.5, -28.5, silence. SFX events per second 22, 22, 74, 114, 8, 9, 6.
- Seam: mean |delta| 0.496 (check_clip); luma last->0 0.375 vs a median frame step of 2.20.
- Frames read from the mp4 at 0, 0.25, 1.0, 2.4, 3.0, 4.0, 4.6, 5.5, 5.6, 6.2, 7.5, 8.1 s.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_brick_breakout.mp4` (v1 archived as `archive\ol_brick_breakout_v1.mp4`).

### Doubts v2
- **Length 8.1 s** (v1 13.7 s). Fast balls on a 64-brick wall clear it in ~5.5 s; the only ways to stretch it are a slower ball or a bigger wall (both what the owner asked to drop). Batch50's 13-18 s guideline is not met; the loop does the rest.
- The break rate falls after 4 s (the mop-up + the stubborn corner, 2 then 1 breaks/s): the cadential timpani roll carries it.
- Growth x16 (4 -> 65) is smaller than v1's x24.

## v1 notes (below)

## World (logical 1080x1920, static camera)
- Arena: thin white frame 128-888 x 318-1226 (no paddle; balls bounce off all 4 sides, none is lost).
- Wall: 10 x 12 = 120 bricks, cell 76 x 26 (collision rect inset 1.6 px), y 382-694, a 64 px gap under the ceiling. Colour by row, one calm gradient: coral (top) -> rose -> orchid -> violet -> sky blue (bottom), S 0.52-0.70, V 0.86-0.98. Rounded bricks, light top band, dark bottom edge.
- Balls: r 9, glossy (radial gradient), the brick's colour; the one original ball is pearl white. Short fading trails (last 5 frames). A new ball grows 0.45 -> 1 in 0.09 s.
- A hit brick shows dark cracks along its split lines for 3 frames, then breaks into 4 chunks (2 slanted cuts + 1 split) that fly off the contact point, fall (debris gravity 1,150 px/s^2), spin and fade in ~0.6 s, plus 6 dust specks.
- When <= 3 bricks stand they get a soft gold outline and the meter label reads "3/2/1 BRICK(S) LEFT".
- HUD: meter y 1290 (row gradient, white marker, "WALL LEFT n%", gold WALL GONE goal from frame 0); counter y 1488 "N" + "×2" pill (newest ball's hue, pops on each doubling) + "BALLS"; watermark "DOPAMINE.EXE" right 888, y 1256, 35%.

## Physics (scenes/ol_brick_breakout.py `simulate`, seeded, exact)
- Zero gravity for the balls, dt 1/60 with 4 substeps. Perfectly elastic reflections off the arena and bricks (circle-rectangle contact, normal from the closest point); perfectly elastic equal-mass ball-ball collisions (cKDTree pairs). A brick breaks on first contact.
- New ball: at the brick's centre, the hitter's outgoing direction turned by a seeded ±14-34°, base speed V0 470 px/s.
- One white ball leaves the floor at sim 0; frame 0 = sim 5.57 s (0.12 s before break 5).
- Seed search (`--search a-b`, ~0.6 s per sim): seeds 1-2200 at V0 470; kept only last-brick-alone >= 0.95 s and last brick 10.8-12.8 s into the clip (~1 in 100). 1412 = busiest opening + the last 3 in a corner.

## Timeline (clip s, seed 1412)
- Frame 0: full wall (96.7% left, bottom row pitted), 5 balls moving, first break 0.11 s.
- Breaks/s: 6, 5, 8, 4, 10, 3, 9, 21, 37, 11, 1, 1. Balls at s: 5, 11, 16, 24, 28, 38, 41, 50, 71, 108, 119, 120 -> **121 (x24.2)**. Doublings at 0.95, 2.29, 5.38, 8.15 s.
- 9.40: 3 bricks left (top-right corner), 9.43: 2 left, 10.27: **1 left** (col 9, row 0, the corner) alone for 1.07 s with 120 balls flying; 3 ball passes within 30 px in its last second.
- **11.33 s cadence**: the last brick breaks on bar 18's D-major downbeat. Gold ring runs out from the corner, gold glints on the balls it passes, 10 gold sparkles, big "WALL GONE" in gold, counter 121 gold, meter 100%, frame line warms. Hold 1.75 s, then a 0.6 s dissolve into the pre-roll = frame 0.

## Sound
- **Music played as music:** W. A. Mozart, *Le nozze di Figaro* K. 492, Overture (1786; Mozart d. 1791, PD). Notes from the midiworld.com sequence `mfig.mid`, saved at `<SOUNDFONTS_DIR>\scores\mozart_figaro_overture\` + `SOURCE.txt`. Not on any used list (BRIEF_batch50/51/52, docs/scenes/*.md), not kid-coded, not banned. Driving, fun, famous opening.
- Bars 1-7 (the pp unison string theme) + bars 12-17 (the forte tutti; bars 8-11, the winds over the same D pedal, are cut) -> bar 18 downbeat (D) = the last brick. 52 beats at one steady **275.3 bpm** (half = 138, Mozart's Presto). The tutti enters at 6.11 s, as the breaks take off; the cadential bars 16-17 (timpani roll on A) = the stubborn corner.
- Arrangement (lib/orchestra): A = violin + strings + quiet piano doubling, viola/cello/bassoon an octave below, contrabass; B = violin + strings + flute, oboe/clarinet/strings 2nd voice, horns, trumpet, viola/cello/bassoon/contrabass on the driving D octaves, timpani D on half notes. Cadence: D-major tutti held 2.1 s + harp roll, celesta glint, tubular bell D5, timpani D.
- SFX (×0.60, tonal, no noise): per break a "crunch" clack pitched to a chord tone the score is sounding (C5-G6) with a clay body, 2 small chunk clacks 14/30 ms later, and the new ball's soft glassy ping an octave up (45 ms); gains ÷ √(rate/5). Last brick = bigger crunch + D6 bell + chimes on the sparkles. SFX events/s: 23, 21, 32, 16, 40, 12, 36, 82, 142, 52, 4, 13, 2.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence; own mux without `-shortest`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 821 frames, 13.68 s. **flash_check PASS** (0 flashes, mean lum 0.013).
- **-14.01 LUFS**, peak -4.60 dBFS, last 0.5 s digital silence, energy > 5 kHz 0.14%. RMS/s (muxed): -18.4, -17.6, -17.1, -18.9, -16.9, -18.4, -16.4, -16.4, -15.9, -16.6, -17.6, -16.3 (cadence), -17.8, silence.
- Seam (check_clip): mean |Δ| **0.436**.
- Frames read from the mp4 at 0, 0.5, 1, 2, 5.5, 9.5, 10.3, 11.35, 11.75 s and the last frame; 1:1 crops at 1.0 s (cracks, chunks, new balls leaving a hole), 11.30 s (the gold-outlined last brick) and 11.75 s (WALL GONE, ring, sparkles).

## Flags
`--seed (1412) --n0 (6) --v0 (470) --r (9) --cols (10) --rows (12) --ch (26) --gap (64) --hold (1.75) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.60) --fin (2.0) --search a-b`. Sim ~0.6 s; the FHD clip renders + muxes in ~30 s.

## Doubts
- The first ~5 s are sparse (5-16 small balls, 3-10 breaks/s). That is how the doubling works (×2 at 0.95 s and 2.29 s), but the frame is mostly the wall + a few dots until ~6 s.
- Second 5 dips to 3 breaks (balls 38 -> 41) before the 21/37 burst; the break rate falls after 9 s (the mop-up, then the stubborn corner). The music carries the tension; the event rate is NOT climbing at the end.
- "Many balls almost hitting it": only ~3 pass within 30 px in its last second. With 120 balls spread evenly, the honest physics gives few near misses; the gold outline + "1 BRICK LEFT" carry the moment.
- Balls are small (r 9); r 11 found no stubborn seed in 400.
- Bars 8-11 of the overture are cut, so the theme goes straight into the forte tutti.
- Growth ×24 (5 -> 121) is modest next to ×8-per-round videos; the count is honest (1 brick = 1 ball).

## Upload draft
- Titles (≤95 chars): "Every brick it breaks = 1 more ball… until the wall is GONE 🧱 #satisfying #physics #shorts" · "1 ball, 120 bricks, every brick makes a new ball 🧱 #satisfying #physics #shorts" · "That last brick in the corner would NOT break 😤 #satisfying #physics #shorts".
- Pinned comment: "120 balls and that one corner brick still held on for a whole second… which ball did you think would get it?"
- **v2 upload draft:** titles "Every brick it breaks = 1 more ball… until the wall is GONE 🧱 #satisfying #physics #shorts" · "64 bricks, every brick makes a new ball… then ONE wouldn't break 😤 #satisfying #physics #shorts" · "That last brick in the corner would NOT break 😤 #satisfying #physics #shorts". Pinned comment: "64 balls flying around and that one corner brick still held on for a whole second… which ball did you think would get it?"
