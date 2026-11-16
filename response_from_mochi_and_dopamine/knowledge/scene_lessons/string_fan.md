# string_fan — Every round the weight DOUBLES: 200 strings or 50, whose weight DROPS first? (batch64, 2026-11-01)

- Brief: docs/BRIEF_batch64.md (Mochi & Bolt 2). New scene file; caption/HUD/render/master chain copied from stack_bounce; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch64\string_fan.mp4` (**v1**, Full HD 9:16, output label v1). 14.98 s.
- Caption (baked; `--nocap` = base): "Every round the weight ^DOUBLES^" / "~200 strings~ or ~50~: whose weight ^DROPS^ first?".

## Story (clip times)
- One steel beam, two rigs on the SAME thread (~10 kg each). Mochi: 200 strings tied by eye (slack 0-16 cm), a blue droopy cloud. Bolt: 50 strings on a jig (within 2 mm), straight. Each rig: load bar -> slotted-weight hanger; the rider sits on the plate stack and hops as each plate slides in under them.
- LOAD (bar + hanger + rider + plates) 15 / 30 / 60 / 120 / 240 kg, plates set down at 0.10 / 2.41 / 4.72 / 7.02 / 9.33 s (every 2 bars of the polka). Pre-roll 0.6 s (frame 0 = rider mid-hop, plate 1 arriving).
- 3.1 s "ONLY 15 OF MOCHI'S 200 ARE PULLING"; 5.2 s "ALL 50 OF BOLT'S 50 ARE PULLING".
- 7.31 s Mochi's first snap (the 3rd-shortest, a weak 7.2 kg string): "SNAP! ONE OF HER SHORTEST STRINGS". Her hottest string 8.4 kg in R4.
- R5 (9.33 s): Mochi's bundle unzips 199 -> 0 (real 0.35-0.96 s after the plate). SLOW-MO ×4 (labelled) over the last 0.42 s real (clip 9.97-11.64), so the stack lands on the crash mat ON the cadence (11.64). Mochi dizzy -> annoyed stare; Bolt laughs ("HA").
- Bolt holds all 50, hottest 5.3 kg. 12.1 s chips "200 strings held LESS than 50" / "equal lengths share the load". Dissolve 14.39-14.99 into the pre-roll.

## The physics (`run_rig()`)
- Fiber-bundle model (Peirce 1926, Daniels 1945), 1D bar dynamics, dt 50 µs. Thread k = 98.1 N / 3 cm (10 kg at 3 % on 1 m), Kelvin-Voigt eta 10 ms, Weibull strengths m = 8, mean 10 kg; snap when stretch > own break stretch. Load sharing = Σ k·max(0, x − s_i) over intact strings; avalanches emergent.
- Each plate is set down over 0.3 s (same for both). Tested: dropping plates (step load) overshoots so much Bolt loses 11-19 strings in R5 — rejected as the protocol, documented here.
- Seeds: Mochi 9, Bolt 1, slack range 0.16 m (scan: S 0.15-0.16 makes most seeds fail in R5 only; 0.12-0.14 hold 240 kg). Results: Mochi snaps/round [0,0,0,1,199], taut strings ~10-34 of 200; Bolt [0,0,0,0,0], hottest 0.6/0.9/1.5/2.8/5.3 kg. Mochi falls 28 cm onto the mat (x end 28.4 cm).
- Tension colour = force / own breaking force: blue (slack) -> green -> gold -> red.

## Sound
- **Piece:** J. & J. Strauss, Pizzicato-Polka (1869, PD). Strain A (8 bars) hand-read from the 1886 Kunkel Bros. piano print, archive.org b10241449 (`<SOUNDFONTS_DIR>\scores\strauss_pizzicato_polka\`, SOURCE.txt). Quarter = 104; pizzicato strings + harp doubling, oom-pah pizz bass + contrabass, timpani on each plate; bar 9 (G7) under the unzip, our own C major cadence at 11.64 s.
- SFX: tonal iron clank per plate, one harp-like pluck per snap (harmony-locked, rising with the unzip, merged ≤1/60 ms, ≥12 ms after notes), a soft low thud + clank at the mat.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 899 frames = 14.98 s. Muxed -14.00 LUFS, peak -2.00 dBFS, last 0.5 s -240 dBFS.
- flash_check PASS (0). Seam mean |delta| 0.90 (rider mid-hop + plate sliding at the seam: motion, dissolve into the pre-roll).
- SFX events/s 2 0 2 0 2 0 0 3 0 11 14 6 0 0 0 (climbs into the unzip; R1-R4 carried by the polka bed).
- Side safe zone: rigs/bars x 138-882, text inside 0.10-0.84w; beam posts at 0.09/0.84w and sliding plates are decoration. Content ≤0.66h; banners 0.70h; HUD 0.72-0.81h.
- Frames read from the mp4: 0.03, 1.0, 3.3, 7.4, 7.5, 9.9, 10.8, 11.4, 12.5, 14.95.

## Args
- `--slack` (0.16), `--mseed` (9), `--bseed` (1), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## v2 (2026-11-01, owner review: "text is misleading")
- Text only, same sim (`--v2`; v1 still reproducible without it). Caption "~200 SLOPPY strings~ vs ~50 PERFECT strings~" / "Every round the weight ^DOUBLES^: whose ^DROPS^ first?". HUD names "MOCHI · UNEVEN" / "BOLT · ALL EQUAL". Banners "UNEVEN LENGTHS: ONLY 15 OF 200 PULL" (R2) / "EQUAL LENGTHS: ALL 50 OF 50 PULL" (R3).
- Finale: "uneven strings: only 34 carried the load" / "equal strings: all 50 shared it". 34 (not the owner's 15) = the most of her 200 ever taut before the 240 kg plate (`peak_taut_mochi()`, R4); 15 is only the R2 count. Truth over brief.
- Deliverable `<VIDEOS_DIR>\MochiAndBolt\review\fixes_1101\string_fan_v2.mp4` (label v2fix). 14.98 s, -14.00 LUFS, peak -2.00, last 0.5 s silent, flash 0, seam 0.88. v1 -> archive/string_fan_v1.mp4.
- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-09` (events json byte-identical to v2fix). Full HD v2 -> archive/string_fan_v2.mp4.
