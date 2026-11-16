# ol_dam_burst (DopamineEXE, channel 2)

## v2 (batch60, 2026-10-30): river from the mountain, release valve, slower
Owner on v1: "too fast; let people enjoy the ball physics; the drop from the tube looks bad (like diarrhoea); balls should come another way". v2:
- **The balls arrive as a RIVER** out of a tunnel portal in the mountain (top-left, headwall at x 112) and roll down the rock slope (39-55 deg, quadratic water drag) into the reservoir. No pipe from above.
- **Every 2 s the inflow doubles** (26 -> 52 -> 104 -> 208 -> 416 balls/s at 2, 4, 6, 8 s, on bar downbeats at 120 bpm); the river swells from a single file to a torrent. "RIVER IN n/s" label next to it. Ball r 5.0 (v1 4.5), g 900 (v1 1500): slower, bigger.
- **Release valve**: an outlet conduit through the dam's foot, a steel nozzle on the dry face aimed 35 deg up. At the first crack (6.5 s) the gate lifts (7.0 s) and blasts a jet out downstream (orifice flow v = 0.62 sqrt(2 g h), 3 files of balls): OUT 127-151/s < IN 208-416/s, so it doesn't help. Label "RELEASE VALVE / CLOSED -> OPEN! / OUT n/s" above the jet arc with a dashed leader to the valve wheel.
- Cracks 6.5 -> 9.98 s (26), **BURST 10.0 s** (beat 48, the dim7 -> D minor), 15 Voronoi chunks, the lake floods down the valley. End chord 14.0 s (beat 56, the cascade lands on D), hold 1.4 s, 0.6 s dissolve. **16.00 s, 960 frames** (v1 10.73 s).
- Caption: `Every 2 s the inflow ^DOUBLES^…|until the dam ~BREAKS~` (literally true: 26 -> 416/s in 2 s steps).
- Delivered `<VIDEOS_DIR>\DopamineExe\review\ol_dam_burst.mp4` (Full HD, seed 3, label v2b); v1 archived as `archive\ol_dam_burst_v1.mp4`.
eview\ol_dam_burst.mp4` (Full HD, seed 3, label v2b); v1 archived as `archive\ol_dam_burst_v1.mp4`.
- Numbers (seed 3): balls in view/s 315, 341, 368, 420, 473, 578, 680, 890, 1105, 1415, 1721 (burst); pressure 248 -> 639 kPa (limit = the pressure at the burst beat = 65 m of water on an 80 m dam); landings/s 31 -> 446; jet hits/s 100-134; flood 58/s at the burst, 19-37/s after.
- Checks (encoded): h264 High yuv420p 1080x1920 60 fps, 960 frames; **-14.00 LUFS**, peak -7.11 dBFS, last 0.5 s digital silence; flash_check PASS (0 flashes, mean lum 0.021); seam mean |delta| 0.263. Frames read at 0, 1, 7.1, 9.95, 10.3, 11, 12.5, 13.9, 14.5, 15.2, 15.6, 15.95 s + 1:1 crop of the valve jet (9.95 s) and the burst (10.3 s).
- Side safe zone: portal x 112, labels 300-880, dam 600-752, HUD 166-884: inside 0.10-0.84 w; only the jet/flood run off the right edge (decoration).
- Doubts: the torrent piles up the slope at x16 (granular, not a flat lake surface); after ~12.5 s the drained valley is calm for ~2.5 s before the dissolve; the counter freezes at the burst count (1,721) while the flood leaves the frame.
- Flags added: `--sbend (56)` end-chord beat, `--srcx --vriv --cd --pre`; physics defaults now `--r 5 --g 900 --q0 26 --vup 380`.
- Upload draft: "Every 2 seconds the river DOUBLES… until the dam BREAKS 🌊 #satisfying #physics #shorts" · "They opened the release valve… it wasn't enough 💥 #satisfying #physics #shorts" · "1,721 balls of water vs one concrete dam 🌊 #satisfying #physics #shorts". Pinned: "the valve was letting out 150 a second… the river was bringing in 416. would you have opened it sooner?"

## v1 (batch59)
- Batch 59 (docs/BRIEF_batch59.md #1). Side cutaway of a reservoir behind a concrete dam. A big pipe pours tiny balls (the water); **every second the inflow doubles** (x2 at frame 0 -> x32), so the jet visibly thickens (1 column -> 13 columns) and the level rises faster each second. The PRESSURE at the dam's base climbs to the DAM LIMIT, cracks spread from the wet heel, and the dam **bursts along its cracks**: 15 concrete chunks tumble out and 3,593 balls flood downstream.
- Caption (baked, `--cap`; `--cap ''` = base): `Every second the inflow ^DOUBLES^…|until the dam ~BREAKS~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_dam_burst.mp4` (Full HD, seed 3, label fhd, **10.73 s, 644 frames**). No 4K yet.

## World (logical 1080x1920)
- Reservoir x 118-560 (left bank: a rock slope from (20,300) to (196,1150)), floor y 1150. Dam = trapezoid (560,1150)-(588,600)-(640,600)-(712,1150) = "80 m". Downstream ground slopes off the right edge.
- Pipe: steel, x 330 +-97 (inner 170), mouth y 452. Balls r 4.5, drawn r x1.12 (no black seams in the packing) + a small highlight.
- Colour = the second each ball poured in (ordered sweep): the lake deep blue (4 depth shades), then teal, green, gold, orange, coral-pink (S ~0.70). The reservoir ends up layered, each layer twice the one below = the doubling made visible.
- A dashed gold LIMIT line on the dam face at the burst depth. Cracks = the interior edges of the 15 Voronoi chunks, opening from the heel outward as the pressure passes 50% -> 98.5% of the limit (each crack runs open over 0.12 s). A small warm stress glow at the heel over 60%. Burst: warm dust puffs, no flash.
- HUD: meter y 1300 = PRESSURE (kPa, rho g h of the visible water depth: per 44 px column, the top of the first under-half-full slab; median over columns; running max before the burst so splashes don't count) toward a gold DAM LIMIT -> "BROKEN!". Counter y 1500 = balls of water + "INFLOW xN" pill (pops on every doubling). Watermark 35%.

## Physics (`simulate`, seeded, deterministic; sim ~25 s, cached in output/_cache_*.pkl, `--resim`)
- PBD discs: Verlet, 8 substeps x 3 Jacobi iterations per frame, cKDTree contacts, correction / max(1, 0.45 n). One-sided terrain segments. Splash cap: no ball rises faster than 650 px/s (PBD pushes must not pump energy); speed cap 1,900 px/s; a 0.02 px noise on settled balls (no balls balancing in a perfect column on the bank).
- The jet is emitted on a lattice moving at 1,000 px/s (columns 2.25 r apart, rows >= 2.04 r): flux = columns x V / row gap = exactly the inflow. Jet balls don't push each other (a coherent stream) until they land.
- Inflow 44/s x 2^k: x2 at frame 0, doublings on score beats 36/39/42/45 (= 0.73, 1.73, 2.73, 3.73 s, every 1.00 s at 180 bpm). The source tapers to 0 over 0.5 s after the burst.
- Dam: a static convex polygon until the burst; then 15 Voronoi chunks (concrete 2.4x water) as rigid bodies: contact impulses from the balls, gravity, vertex-ground impulses (e 0.15, friction 0.5), circle-approximated chunk-chunk contacts; at the burst each gets 0.45 sqrt(2 g depth) outward.
- **The limit = the pressure reached at the burst beat** (747 kPa = 76 m of water, 95% of the dam height): the strength is a set parameter, the pressure curve is honest.

## Timeline (clip s, seed 3)
- 0.0: lake 865 balls, a single-file x2 stream, 222 kPa. Doublings 0.73 (x4), 1.73 (x8), 2.73 (x16), 3.73 (x32).
- Pressure/s 222, 244, 290, 375, 534, 667 kPa; balls/s 865, 978, 1,204, 1,652, 2,553, 3,593. Landings/s 82, 162, 336, 716, 1,597.
- Cracks open 3.05 -> 4.71 s (25 cracks). **4.73 s BURST** (beat 48, the diminished-7th -> D-minor arrival). Flood 4.8 -> ~9 s (40-57 balls/s hit the downstream ground; 96 chunk thuds).
- 8.73 s the closing D-minor chord; hold 1.4 s; 0.6 s dissolve back to frame 0. 10.73 s.

## Sound
- **Music:** L. van Beethoven, Piano Sonata No. 17 in D minor Op. 31 No. 2 **"The Tempest"**, 1st mvt (1802; d. 1827, PD). Mutopia Project `LVB_Sonate_31no2_1.mid` (Public Domain; Breitkopf & Hartel 1862-65), saved at `<SOUNDFONTS_DIR>\scores\beethoven_tempest1\` (+ .rdf). Score (MIDI quarter) beats 33.8-60 at a steady 180 bpm: the Allegro's sighing figure climbing chromatically over the rising bass (crescendo) to the dim7 -> D minor at beat 48 = the BURST, then the falling cascade; our D-minor tutti at beat 60. Not on any used list; not kid-coded; not banned.
- Arrangement: piano RH + LH (velocity crescendo to the burst), strings an octave under the RH, solo violin on the climb, cello + contrabass on the bass; timpani roll into the burst + boom, strings/horns D minor; closing chord: strings, piano, horns, timpani D, harp roll.
- SFX (x1.0): water plips per landing (>= 20 ms, pitched to the score's sounding notes G5-G6), a round low "bloop" per doubling, a tonal stone crack per crack (louder as they spread), deep thumps for chunk landings (>= 60 ms), dense lower plips for the flood (>= 14 ms). `level_bed` crescendo, `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence; own mux without `-shortest`.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 644 frames, 10.73 s. **flash_check PASS** (0 flashes, mean lum 0.026).
- **-14.00 LUFS**, peak -7.13 dBFS, last 0.5 s digital silence. RMS/s (audio test) -17.2, -16.3, -15.8, -15.6, -14.4 (burst), -14.2, -15.8, -17.2, -16.4, -16.8, silence. SFX events/s 29, 30, 31, 42, 45, 45, 35, 29, 27, 17.
- Seam mean |delta| 0.294.
- Frames read from the mp4 at 0, 0.5, 1.5, 2.5, 3.5, 4.0, 4.6, 4.8, 5.0, 5.4, 6, 7, 8.5, 9.5, 10.6 s; 1:1 crop of the dam at 4.85 s (chunks parting, layered lake behind).
- Side safe zone: pipe x 233-427, reservoir 118-560, dam 560-712, HUD 166-856, caption <= 780 px centred: inside 0.10-0.84 w. Only the flood runs off the right edge.

## Doubts
- 0-1 s is a thin single-file stream into a calm lake (the x2 rung); the jet is a solid column from ~1.7 s. Starting later (x4) would cut 1 s.
- After the burst the event rate falls (the lake drains, 4.8 -> 9 s): a dam-break ending, not a climbing rate.
- The jet plunges deep and mushrooms the coral layer into the middle (honest mixing), so the doubling layers are cleanest at ~3.5-4.2 s.
- The limit is a chosen strength (= the pressure at the burst beat).
- During the dissolve the counter ghosts (3,593 fading under 865), like ol_blade_split.

## Flags
`--seed (3) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0)`. Physics `--r (4.5) --g (1500) --sub (8) --vout (1000) --q0 (44) --lake (1000) --pipex (330) --chunks (15) --push (1.0) --vup (650)`. Clock `--bpm (180) --sb0 (33.8) --hold (1.4)`.

## Upload draft
- Titles: "Every second the inflow DOUBLES… until the dam BREAKS 🌊 #satisfying #physics #shorts" · "3,593 balls of water vs one concrete dam 💥 #satisfying #physics #shorts" · "How much water can a dam HOLD before it breaks? 🌊 #satisfying #physics #shorts".
- Pinned comment: "the inflow doubled every second and the dam didn't even last 5 of them… how many seconds would you give a real one?"

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/ol_dam_burst.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 960 frames 16.00 s; -14.00 LUFS, peak -7.11 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v2b. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-08\1_ol_dam_burst.mp4`, 04:00 local Nov 9 (= 19:00 US East Nov 8). FHD review copy → `DopamineExe\archive\ol_dam_burst_fhd.mp4`.
