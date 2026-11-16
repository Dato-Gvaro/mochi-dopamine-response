# ol_coin_tower (DopamineEXE, channel 2)

## v4 (batch63, 2026-10-31): the CAT-BANK STEAL ending (+1.5 s)
- Owner: after the coins are down, a cat paw pops out of a little coin box (the coin-stealing cat bank toy, generic: no brand) and steals the right-most coin, "ka-chunk" + a tiny meow. Everything before 12.43 s is unchanged (sim, picture, v3 jingle: its 628 events are bit-identical, checked against the v3 script, scratchpad `ol_coin_tower_v3.py`).
- `--cat 1.5` adds the beat between the settled pile and the 0.6 s dissolve: clip **14.53 s, 872 frames** (v3 13.03). Beats (s after T0 = T_CAD + HOLD = 12.43): camera push -0.48..+0.32 (scale 0.40 -> 0.62, pan so the stolen coin sits at x 580: the camera follows the runaway coin, which stops at 12.76 s), lid cracks + eyes watch the coin +0.10, paw darts out +0.45..0.60, grab +0.63, snaps back with the coin +0.70..0.84, lid slams +0.85 (box squash + gold ticks, counter 214 -> **213** pops), smug squint peek + meow +0.95..1.28.
- The stolen coin = the right-most coin at rest (coin 205, world x 1399). The box sits on the table in WORLD coords (BOX 240x190 world px, 110 px right of the coin), so it is off-screen until the final push-in. Box teal with a paw-print emblem and a gold coin slot on the lid (hinged back-right); cat grey with pink inner ears, green slit eyes that track the coin; white paw, pink beans; the arm is a long grey noodle (toy-like).
- Screen at the cat: coin x 580, box x 688-837 (inside 0.10-0.84 w), lid/head top ~y 1000; nothing new near the HUD.
- Sound (all synthesised): `lid` (soft wooden tick), `swish` (paw dart / snap back, filtered-noise air), `coin` midi 100 at the grab, `kachunk` (latch click 'ka' + 45 ms later a hollow box thump 95->62 Hz with 235/410 Hz body modes + the coin rattling inside, low-passed), `meow` (additive kitten mew: f0 640 -> ~1000 -> 520 Hz, formants m-i-a-u, vibrato; g 0.24 = 'tiny': first try at 0.40 was louder than the spill). The bed's cadence chord has ended by ~12.75 s, so the steal plays in near-silence. Music/jingle clock kept on the v3 length (`T = T_CAD + HOLD + DISS` inside `build_events`).
- Audio test: -14.00 LUFS; RMS/50 ms around the steal: grab -19.6, kachunk -16.1, meow ~-17; silent from 13.9 s.
- **Shipped 4K** (`NF_SCALE=2.0 --label ship`): `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-10\2_ol_coin_tower.mp4` (16:00 local Nov 11 = 07:00 US East Nov 11). The v3 FHD review file → `archive\ol_coin_tower_fhd.mp4`.
- Checks (encoded 4K): h264 High yuv420p 2160x3840 60 fps, 872 frames, 14.53 s; **-14.0 LUFS**, true peak -7.4 dBFS; last 0.5 s digital silence (-inf), < -80 dBFS from 13.9 s; flash_check PASS (0); frames read at 0, 10, 11.67, 12.73, 13.08, 13.2, 13.33, 13.53, 14.17 s + 1:1 crops of the paw on the coin (f785) and carrying it (f792). Side safe zone: coin x 580, box 688-837, cat head <= ~830.
- Doubts: the box interior is filled 3% grey, a faint block shows behind the cat's head on pure black (barely visible); the stolen coin and the meow are 1.5 s after the jingle, so the loop now rests on a quiet beat instead of the spill.
- Upload: titles "Every round the coins DOUBLE… until the tower TOPPLES 🪙" · "214 gold coins vs one bell curve… then the cat took its cut 😼" · "Each gold coin lands 1.2 mm off… 214 coins later 😬" (+ ` #satisfying #physics #shorts`). Pinned: "every coin landed within a couple of mm and the bell curve still won at coin 214… and then the cat took its cut. would you have stopped at 200?"
- Flags: + `--cat (1.5)` (0 would break the cat timeline: keep it 1.5).

## v3 (batch61, 2026-10-30): the COIN-CASCADE JINGLE on the fall
- Owner on v2: "at the end I was expecting that coin jingle sound on the fall; our viewers will need it." Picture, sim, timeline and music unchanged; sound only. v2 script: scratchpad `ol_coin_tower_v2.py` (builder S session).
- New voices: `coin_wave` (a gold-coin 'ching': a disc's inharmonic modes x1, 1.51, 2.09, 2.71, 3.42, 4.2, 5.1 up to 12 kHz, the high ones short, + a 3 ms click transient) and `roll_wave` (a coin spinning down flat, Euler's-disk style: a train of tiny chings whose rate climbs 9 -> 45 Hz over 1.1 s, then a settling tink).
- The spill (612 sim hits in 10.92-11.81 s): every hit = a ching (thinned only at 5 ms, density damping 1/max(1, rate/25)^0.3; A-major pitches, table hits MIDI 88-100, pile hits 93-105), ~22% of the slow hits (< 2,500 px/s) start a roll, and a shimmer of tiny chings (up to 260/s, MIDI 98-108) follows the hit density. Before the first hit, from T_CAD + 0.15 s, a rising grinding shimmer as the column shears.
- Music under it: the bed's finale lift `--findb` 5.0 -> **-2.0** dB, so the jingle sits on top: bed vs SFX RMS 10.9-11.7 s = -24.0 vs -15.8 dB (v2: the bed was +7 dB louder and the SFX ~-22); 11.7-12.3 s = -34 vs -16.6 (the rolls ring out).
- Events: 628 (199 landing clinks unchanged + 416 chings + 13 rolls). Per second (s 10-12): 89, 350.
- Delivered `<VIDEOS_DIR>\DopamineExe\review\ol_coin_tower.mp4` (**v3**, Full HD, label v3, 13.03 s, 782 frames); v2 → `archive\ol_coin_tower_v2.mp4`. Brief said "then 4K + stage"; the coordinator asked for FHD review first, so it is NOT staged yet.
- Checks (encoded): h264 High yuv420p 1080x1920 60 fps; **-14.13 LUFS** (v2 -14.00; the louder spill shifts the master), peak -8.47 dBFS, last 0.5 s digital silence; flash PASS; seam 0.235. RMS/s (audio test): ... -17.4 (s 10), -16.4 (s 11 = the spill, the loudest second), -23.8 (rolls ring out). Frames read at 9.5, 10.6, 11.2, 12.2 s.

## v2 (batch60, 2026-10-30): all GOLD coins + nerd stats
Owner on v1: "is it worth trying? Maybe all GOLD coins and nerd stuff: the variation of a gold coin dropping perfectly, the deviation, and it drops by that rule". v2:
- **All gold coins** (one gold, a 7% per-coin brightness jitter so the edges read). The rainbow is gone.
- **The rule is pure statistics**: every coin is aimed at the centre of the coin below and lands off by eps ~ N(0, sigma = 1.2 mm) (6.5 world px on a 24 mm coin). No drift (v1 had a growing lean bias). The centres do a random walk; mirrored (eps -> -eps, same distribution) so it always tips right, away from the charts.
- **Tipping rule** (unchanged physics, now on screen): at every joint the COM of the coins above must lie over the contact patch below them. tilt = atan(dx / h) vs tipping angle = atan(edge / h) (dx = COM offset from the patch centre, edge = the patch half-width, h = the COM height above the joint). It topples when tilt > tipping angle at the WEAKEST joint (honest: a random-walk stack fails mid-height, not at the base; here joint 5).
- **On screen** (left column x 112-440, the tower moved right to x 636): (1) LANDING OFFSET histogram, 13 bins of 0.5 mm, gold bars + the stated bell curve (white) scaled to n, the newest coin's bin flashes, "each coin: N(0, sigma = 1.2 mm)" and "measured sigma = 1.15 mm (n = 213)"; (2) TILT vs TIPPING ANGLE chart over the coins (0-30 deg; gold tilt, white tipping angle; they meet at the topple), "tipping angle = atan(edge / h)"; (3) on the tower: a gold tick + "WEAKEST JOINT", the white vertical and the gold line to the COM dot ("COM"), both with a dark under-stroke; (4) meter: "TILT x deg" -> gold "TIPS AT y deg" -> "TOPPLED!", bar = tan(tilt)/tan(tipping angle).
- Seed **1416** (`--scan`-style search over pure random walks: first failure in round 4, coin #85-118 of the round): tips at **coin 214** (round-4 coin #87), joint 5, 209 coins fall. Tilt/tipping at coins 15, 45, 122, 204, 212: 14.8/65.1, 11.6/28.3, 8.0/10.4, 6.0/6.2, 5.9/5.9 deg. The cascade pans the camera 150 px left so the spill stays in frame.
- Caption unchanged: `Every round the coins ^DOUBLE^…|until the tower ~TOPPLES~` (true: 16, 32, 64, 128 per round).
- Delivered `<VIDEOS_DIR>\DopamineExe\review\ol_coin_tower.mp4` (Full HD, label v2b, 13.03 s, 782 frames); v1 archived as `archive\ol_coin_tower_v1.mp4`.
- Checks (encoded): h264 High yuv420p 1080x1920 60 fps; -14.00 LUFS, peak -7.9 dBFS, last 0.5 s digital silence; flash_check PASS; seam mean |delta| 0.23. Frames read at 0, 1.5, 4, 6, 8, 9.5, 10.2, 10.5, 11, 11.6, 12.4, 13 s; 1:1 crop of the panels + tower at 9.5 s.
- Side safe zone: charts x 112-440, tower 560-760, WEAKEST JOINT label <= 820, HUD 166-884; only cascade coins run wider.
- Doubts: the chart's tilt line is jumpy early (the weakest joint changes as coins land; honest); "edge" and "h" are not drawn as dimensions, only named in the formula; frame 0 histogram has n = 14 (sparse); coin thickness is not stated (1.1 mm at this scale).
- Flags: `--sig (6.5 world px)`, `--seed (1416)`; `--bias/--bias2` removed.
- Upload draft: "Every round the coins DOUBLE… until the tower TOPPLES 🪙 #satisfying #physics #shorts" · "Each gold coin lands 1.2 mm off… 214 coins later 😬 #satisfying #physics #shorts" · "214 gold coins vs one bell curve: guess who won 📉 #satisfying #physics #shorts". Pinned: "every coin landed within a couple of mm and the bell curve still won at coin 214… would you have stopped at 200?"

## v1 (batch59)
- Batch 59 (docs/BRIEF_batch59.md #6). A coin tower on a table. Coins drop onto the top, **every round twice as many** (16, 32, 64, 128 after a 15-coin start), each landing a hair off-centre on the coin below. The tower stands while, at EVERY level, the centre of mass of the coins above lies over the contact patch below it (the honest static condition for stacked discs). A gold dashed centre-of-mass line + dot, a TILT readout (its angle) and a BALANCE meter (the worst level, 100% = tips). Coin 226 breaks it on the cadence: the column tips over the table edge, shakes apart (slow motion ×0.5) and the coins cascade and slide across the table. Not jenga.
- Caption (baked, `--cap`; `--cap ''` = base): `Every round the coins ^DOUBLE^…|until the tower ~TOPPLES~` (the brief's "Every coin added doubles" read awkwardly; the rule is the same: the count doubles every round).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_coin_tower.mp4` (Full HD, seed 20, label fhd, **13.03 s, 782 frames**). No 4K yet.

## World (world px, y up from the table; camera maps to logical 1080x1920)
- Coin r 65, thickness 6 (a 24 mm coin ~ 20:1), drawn as short metallic cylinders (dark-edged band with a bright stripe, reeded edge when big, lit top face with a raised rim; top-face ellipse 0.22 r: camera slightly above). Tint by stacking order: copper → gold → lime → teal → blue → violet (S 0.58): the tower is an ordered rainbow.
- Table top at screen y 1168 (one thin white line, dark wood band). The base sits 80 px to the side opposite the lean so the fall stays in frame.
- Camera: scale 1.0 until the tower nears y 470, then one continuous zoom-out to 0.56 at the tip, easing to 0.38 during the cascade (the only camera move).
- HUD: meter y 1300 = "BALANCE n% · TILT x°" → gold TIPPING POINT → "TOPPLED!". Counter y 1500 = COINS + "×2 +N" round pill (pops each round). Watermark 35%.

## Model (`simulate`, seeded, exact; < 1 s CPU)
- Landing offsets: x_k = x_(k-1) + side(0.10 + 0.0068 k) + N(0, 1.2): each coin lands slightly toward the lean (the stack curves like a hand-built tower) with random scatter. Static check per coin: COM of coins j.. vs the overlap patch of coins j-1/j (level 0 = the table under coin 0).
- `--scan` picks seeds whose FIRST failure falls late in round 4 near the doubled rate: seed 20 tips at coin 226 (round-4 coin #99), level 6 (220 coins fall). Round 4's spacing is set so coin #99 lands on the cadence (0.045 beats/coin vs round 3's 0.094 = ×2.1 the rate).
- Tip: the block above level 6 rotates rigidly about the patch edge under gravity (40,000 world px/s² ≈ 0.75 g at coin scale; a 0.25 rad/s nudge from the last coin's landing); at 9° it breaks into free coins with the rotation velocity + scatter growing with height, spinning and flipping; table/pile contacts bounce (e 0.34) then slide to rest (friction), piling on a height map. Rendered at half speed from the tip (rigid lean 0.64 s on screen).

## Timeline (clip s, seed 20)
- Frame 0: 15 coins, the first round-1 coin lands at 0.17 s. Landings/s 5, 6, 8, 11, 12, 18, 24, 23, 44, 48 (rounds start at 0, 2.73, 5.45, 8.18 s). Coins at s: 15, 20, 26, 34, 45, 57, 75, 99, 122, 166, 215 → **226 at 10.23 s**.
- BALANCE at s: 4, 6, 8, 12, 16, 20, 25, 31, 38, 59, 92 → 100%; TILT 2.7° → 5.4°.
- **10.23 s TIP** (the cadence); the column leans, breaks at ~10.9 s, coins hit the table 11-12 s (cascade). Hold to 12.43 s, 0.6 s dissolve to frame 0.

## Sound
- **Music:** W. A. Mozart, Piano Sonata No. 11 in A major K. 331, I. Andante grazioso, the Tema (1783; d. 1791, PD). Mutopia `KV331_1_1_tema.mid` (Public Domain; Breitkopf & Härtel), saved at `<SOUNDFONTS_DIR>\scores\mozart_k331_tema\` + .rdf + SOURCE.txt (downloaded 2026-10-29). Bars 1-8 (score beats 0-22.5) at a steady quarter = 132 (dotted quarter 66), the A-major cadence of bar 8 = the tip. Not the banned Turkish March (that is K. 331/III); not on any used list; not kid-coded.
- Arrangement: piano (score), violin + celesta 8va on the top line, pizzicato bass per dotted quarter, a string pad from bar 5, timpani roll into the cadence; cadence = A-major strings, piano, horns, timpani A, harp sweep.
- SFX: a bright metallic clink per coin landing (inharmonic coin partials < 7 kHz) on a note the score sounds there (E5-F#6); the cascade = a lower ring with a spinning-down shimmer per table hit, clinks for coins on the pile (A-major notes). Sampled ≥ 14 ms (stack) / ≥ 12 ms (cascade), gain / (rate)^0.4. `level_bed` (+5 dB crescendo, cadence +5 dB), `audio.master(peak_db=None, reverb=0.40)`, last 0.6 s digital silence.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 782 frames, 13.03 s. **flash_check PASS** (0 flashes).
- **-14.01 LUFS**, peak -7.68 dBFS, last 0.5 s digital silence. RMS/s (audio test) -18.5, -18.2, -17.5, -17.1, -16.8, -16.8, -16.7, -16.5, -16.6, -16.7, -15.5 (cadence), -16.7 (cascade), fade. SFX events/s 5, 6, 8, 11, 12, 18, 24, 23, 37, 41, 13, 45 (cascade).
- Seam mean |delta| 0.146.
- Frames read from the mp4 at 0.5, 4, 8, 10.1, 10.6, 11.0, 11.6, 12.4 s; 1:1 crop at 9.9 s (the curved column, the COM line and dot, coins dropping onto the top).
- Side safe zone: tower and HUD inside 0.10-0.84 w; a few sliding coins of the cascade reach the left edge (decoration).

## Doubts
- Frame 0 is the calmest moment: a 15-coin stack and ~5 coins/s (each a clink on the melody); it doubles every round from there.
- The landing drift (the lean) is a modelling choice so the tower curves like a hand-built one; with pure random offsets the tower zig-zags like a snake (tried, looked wrong).
- The cascade: coin-coin contacts in the air are not modelled (coins only land on the table and on settled coins); the coins end mostly in a long low spill.
- Slow motion ×0.5 from the tip is not labelled on screen.

## Flags
`--seed (20) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (1.0) --scan a-b --hold (2.2) --slow (0.5)`. Model `--sig (1.2) --bias (0.10) --bias2 (0.0068) --g (40000) --kick (0.25) --thbreak (9)`. Clock `--bpm (132)`.

## Upload draft
- Titles: "Every round the coins DOUBLE… until the tower TOPPLES 🪙 #satisfying #physics #shorts" · "How many coins can you stack before it falls? 🪙 #satisfying #physics #shorts" · "226 coins, one tiny lean… then this happened 😬 #satisfying #physics #shorts".
- Pinned comment: "it made it to 226 coins before the lean won… would you have stopped at 200?"
