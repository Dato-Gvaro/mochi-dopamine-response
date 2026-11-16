# rain_run — Walk or RUN in the rain: who gets WETTER? (batch54, 2026-10-28)

- Brief: docs/BRIEF_batch54.md (Mochi & Bolt 1). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from pilot_parking.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch54\rain_run.mp4` (**v1**, Full HD 9:16, 14.58 s, 875 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Walk or ~RUN~ in the rain:" / "who gets ~WETTER~?"
- **Story:** side view of a rainy plaza at dusk: cafe (start, canopy) on the left, bus shelter (finish) on the right, the same 16.4 m twice (Mochi's walkway behind, Bolt's pavement in front, road + kerb puddle below). Mochi WALKS 1.39 m/s, Bolt RUNS 4.84 m/s. Bolt's counter climbs faster (he leads "WETTER" at frame 0), he reaches the shelter at 2.63 s with 83 drops ("DRY!", HA HA); Mochi passes 83 at 2.96 s ("MOCHI'S WETTER!") and arrives at 11.05 s with 304 ("RUNNING: 73% FEWER DROPS"). A car drives by at 7.6 s and misses the puddle (Bolt flinches). On the cadence (11.58 s) a second car ploughs through the kerb puddle: SPLASH! +498 → Bolt 581 vs Mochi 304. Bolt: soaked, deadpan stare; Mochi laughs, then smug.

## Layout
- Ground lines y 770 (Mochi) / 1135 (Bolt); road 1160-1340, puddle x 640-905 at y 1186. Characters r 54 (drawn with little feet). Start x 196 (under the cafe canopy, x < 252), finish x 850 (under the shelter roof x 790-1100, y 470). 40 px = 1 m.
- HUD (y 1366-1544): "DROPS HIT (same rain, same 16 m)", per side name+method, count, a water bar, a WETTER tag on the leader, "83 rain + N splash" after the twist.
- Key content inside x 0.10-0.84w (Bolt at the finish: right edge x 904); the cafe front, shelter back and BUS sign are decoration. Static camera, calm dusk blues; no flash.

## The physics (seeded, honest)
- Rain: points falling at 9 m/s, spawned uniformly (Poisson) in x with density 8.0e-4 drops/px^2 of the side plane, per lane (independent seeds 54 / 1054, same statistics); a 3 s pre-warm fills the sky. Roofs (canopy, shelter) stop drops. A drop that enters a body circle (0.96 r) is a HIT: counted, absorbed (a tiny burst + a drip sliding down).
- Result: Mochi 304, Bolt 83 (ratio 0.27). Textbook 2D expectation n·2r·(v_rain·T + d) gives 407 / 155 without the roofs: the cover over the first and last ~1.2 m matters more to the runner, so the honest sim favours him a bit more than the formula.
- Splash: the car (16 m/s) drives through the puddle; 1000 droplets spawn along the wheel's path with vx 0.05-0.55 × car speed, vy up 170-520 px/s, real g; 498 reach Bolt's body (first +0.04 s, median +0.19 s after the cadence). Mochi (behind, 0.6 m higher) is out of reach. The car's front wheel enters the puddle 0.30 s before the cadence so the spray lands on it.
- Bolt's lead change is honest: running sweeps more drops per second (≈38/s vs ≈27/s) but spends 3.4 s in the rain vs 11.8 s.

## Sound (music first)
- **Piece:** Franz Schubert, "Die Forelle" (The Trout) D 550 (1817; Schubert d. 1828, PD). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD engraving (C.F. Peters, Band I), `forelle.mid` + rdf, saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\schubert_forelle\`. Read at runtime (voice, piano RH, piano LH).
- **Excerpt:** D-flat major 2/4, quarter = 114 (bar 1.053 s), source bars 6-16 (the first verse: "In einem Bächlein helle..."), the cadence = the tonic D-flat of bar 17 (11.58 s = the splash).
- **Arrangement** (lib/orchestra): violin on the voice line, flute 8va from bar 7, the score's piano part on piano, its rising sextuplets doubled by harp, pizz + contrabass on the left-hand bass; cadence = timpani + D-flat tutti (strings, horns, violins, piano, harp sweep).
- **SFX** (tonal): a "plip" per 16th slot holding body hits (pitched to the piano's chord, gain by count); sparse roof tinks; DRY / lead-change / arrival dings; two soft tonal car hums (Doppler); the splash = two low bloops + droplet plips.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 875 frames = 14.58 s. −14.01 LUFS, peak −1.99 dBFS, last 0.5 s digital silence.
- RMS/s: −18.5 −18.2 −17.7 −17.7 −17.4 −17.0 −17.0 −16.4 −16.2 −16.4 −15.7 −15.6 −14.2 (cadence) −17.2, then silence.
- SFX events/s: 16 17 15 11 8 9 11 9 10 8 8 13 6 0. Body hits/s (Mochi): 24 25 33 27 33 25 37 31 34 25 6.
- flash_check PASS (0 flashes, mean lum 0.04). Seam mean |Δ| 1.85 = the same as adjacent frames anywhere in the clip (1.80-1.93; the rain moves 6 px/frame), i.e. continuous.
- Frames read from the mp4: 0.5, 2.7, 2.75, 3.05, 7.75, 11.62, 11.75, 11.80, 12.2, 13.5 + a 1:1 crop of the car at the puddle.

## Doubts
- The twist is a gag on top of the physics: the HUD keeps "83 rain + 498 splash" and the banner "RUNNING: 73% FEWER DROPS" stays up, so the lesson survives the joke.
- Bolt's side is idle from 2.6 s (smug, laughing, the car-1 flinch); the action is Mochi's lane + the climbing counter.
- Mochi's hits stop at ~9.5 s when she reaches the shelter roof; 9.5-11.3 s the music and the approaching car carry it.
- Cartoon scale: the characters are ~2.7 m wide on the 40 px/m ruler (rain density is tuned for the look; the ratio is what matters).

## Args and cost
- `--seed` (54), `--dens`, `--nsplash` (1000), `--lead` (0.30), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 2 s; Full HD render ~30 s at 2 encoder threads.
- Owner review (batch55, 2026-10-28): approved as is → 4K ship.

## Outcome
- (fill after upload)

## Ship (batch55, 2026-10-28)
- Owner: approved unchanged. 4K `NF_SCALE=2.0 --label ship` (same code and seed as v1): h264 High yuv420p 2160x3840 @ 60 fps, 875 frames = 14.58 s; −14.01 LUFS, peak −1.99 dBFS, last 0.5 s silent; flash PASS (0, mean lum 0.04); seam mean |Δ| 1.63 (rain motion, as FHD 1.85). Encoded frames read at 0.3 s and the finale.
- Staged: `MochiAndBolt\schedule\2026-11-04\1_rain_run.mp4`, 08:00 local Nov 5 (= 23:00 US East Nov 4). FHD review copy → `MochiAndBolt\archive\rain_run_fhd.mp4`.
