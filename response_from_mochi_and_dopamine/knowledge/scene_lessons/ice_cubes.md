# ice_cubes — One BIG cube or crushed ice: which keeps it COLD longer? (batch57, 2026-10-29)

- Brief: docs/BRIEF_batch57.md (Mochi & Bolt 2). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from checkout_queue / soda_tap.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\ice_cubes.mp4` (**v1**, Full HD 9:16, 13.70 s, 822 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~One BIG cube~ or ~crushed ice~:" / "which keeps it ~COLD~ longer?"
- **Story:** a summer patio at dusk. Frame 0: the ice is mid-air, falling into two glasses of iced tea (Mochi: one big cube; Bolt: a shower of crushed ice), splash at 0.18 s. A live DRINK TEMPERATURE chart draws both curves; big °C readouts sit over the glasses with a COLDER pill on the leader. Bolt's drink plunges (7.1 °C at 3 min vs 15.0 °C, "CRUSHED: COLDER, FAST!"); his pieces shrink and vanish one by one (tinks). Lead change at 6.6 s (24.9 min): "THE BIG CUBE TAKES THE LEAD!" (gold ring on the chart crossing); 7.0 s "CRUSHED ICE ALL GONE" (Bolt: NO ICE LEFT). Cadence 10.5 s (32.9 min): "MOCHI'S STILL COLDER", "12.5 °C vs 14.2 °C · 3 g of ice left", "CRUSHED = COLD FAST / BIG CUBE = COLD LONGER". Bolt annoyed, Mochi cheers.

## Layout
- Table y 1182. Glasses 7 × 12 cm at 30 px/cm (inner 210 × 360), x 362 / 655; characters r 64 at x 176 / 838 (key content x 112-902). Straws, condensation beads (count ~ how cold the drink is).
- Chart x 150-870, y 478-690 (0-26 °C, time 0 → 32.9 min). Readouts y ~768. HUD y 1366-1544: "TIME n min (time-lapse xN)", per side ICE LEFT g + bar + pieces.
- Static camera; calm dusk colours; no flash.

## The physics (seeded, honest; real seconds, dt 1 s)
- 300 g iced tea at 25 °C, patio air 30 °C. 120 g of ice each: Mochi 1 cube (5.1 cm), Bolt 64 pieces (seeded sizes 0.45-1.55 × the mean, ~1.3 cm).
- Each piece: dm/dt = h·A·T/L, h 250 W/m²K, A = 6 s² (crushed packed ×0.75 for touching faces), L 334 J/g. Meltwater joins at 0 °C. The glass gains UA 0.8 W/K × (30 °C − T). Floating ice: the drink level is constant (Archimedes).
- Result: crushed reaches 5.0 °C (min) vs the cube's 9.1 °C; the crushed pieces are gone at 26.2 min; the cube's drink is colder from 24.9 min (the last crushed slivers barely cool) and stays colder: 12.5 vs 14.2 °C at 32.9 min, cube 2.8 g left. Why: the warmer cube drink leaks in less heat from the air, so the same 120 g lasts longer.
- Time-lapse: one smooth monotone clock map (PCHIP through 0 → 2.5 min at 2.6 s, lead change at 6.6 s, end at the cadence), shown live in the HUD: x15 → x430 → x34.

## Sound (music first)
- **Piece:** Johannes Brahms, Waltz in A-flat Op. 39 No. 15 (1865; d. 1897, PD). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD (Ed. R. Joseffy), `waltz-op39-15.mid/.ly/.rdf` + SOURCE.txt at `<SOUNDFONTS_DIR>\scores\brahms_waltz15\`. Read at runtime.
- **Excerpt:** 3/4, quarter = 120 (bar 1.5 s): MIDI bars 22-28 (score bars 23-29, the theme's return), cadence = the A-flat tonic of bar 30 (10.5 s).
- **Arrangement** (lib/orchestra): piano (both hands, the score), violin on the top line, celesta 8va very soft (ice sparkle), cello on the downbeat bass, soft strings on beats 2-3; cadence = soft timpani A-flat, strings chord, harp sweep, celesta, held strings.
- **SFX** (tonal): ice clinks on the drop, a glassy tink per crushed piece vanishing (8th grid, gain by count), a degree tick per whole °C crossed per glass, early cube cracks, a soft tink per beat while the cube leads, dings on the banners and the cadence.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 822 frames = 13.70 s. -14.00 LUFS, peak -2.41 dBFS, last 0.5 s digital silence.
- RMS/s: -18.5 -18.1 -17.9 -17.6 -17.3 -17.0 -16.9 -16.1 -16.2 -16.4 -14.6 (cadence) -16.1 -28.5, then silence.
- SFX events/s: 10 11 9 7 1 5 9 8 3 4 5 0.
- flash_check PASS (0 flashes, mean lum 0.05). Seam last → first 3.67 vs adjacent 3.5-3.6 (the ice is falling at the seam: continuous).
- Frames read from the mp4: 0.5, 3.0, 5.0, 6.7, 7.4, 10.6, 13.0 + a 1:1 crop of both glasses at 5.0 s.

## Ship (batch58, 2026-10-29): owner "ok"
- 4K `NF_SCALE=2.0 --label ship` (unchanged v1): h264 yuv420p 2160x3840 @ 60, 822 frames = 13.70 s; -14.00 LUFS, peak -2.41 dBFS, last 0.5 s silent (-240 dBFS); flash PASS (0, mean lum 0.052). Frames 0.5/6.7/10.6 + 1:1 crop of the glasses at 5.0 s read.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-06\1_ice_cubes.mp4`, slot 1 08:00 local Nov 7 (= 23:00 US East Nov 6). FHD review copy → `MochiAndBolt\archive\ice_cubes_fhd.mp4`.

## Doubts
- The honest gap after the lead change is small (~1.7 °C); the ICE LEFT bars (3 g vs none) and the chart crossing carry the result.
- The lead change comes BEFORE the last crushed piece melts (the slivers barely cool), so "BIG CUBE TAKES THE LEAD" precedes "CRUSHED ICE ALL GONE" by 0.4 s.
- Event rate dips at 4 s (between the degree ticks and the vanishing pieces) and is low after the crushed ice is gone; the music carries it.
- The time-lapse is not constant (shown live in the HUD).

## Args and cost
- `--seed` (7), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~1 s; Full HD render ~45 s at 2 encoder threads.

## Outcome
- (fill after upload)
