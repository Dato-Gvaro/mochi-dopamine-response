# coffee_milk — Add milk NOW or LATER: whose coffee is HOTTER in 10 min? (batch59, 2026-10-29)

- Brief: docs/BRIEF_batch59.md (Mochi & Bolt 1). New scene file, built from scenes/ice_cubes.py (chart, readouts, HUD, sound chain copied); lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\coffee_milk.mp4` (**v1**, Full HD 9:16, 13.43 s, 806 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Add ~milk NOW~ or ~LATER~:" / "whose coffee is ~HOTTER~ in 10 min?"
- **Story:** a kitchen counter, two glass mugs with thermometers, steam that follows the temperature. Frame 0: Mochi's carton is mid-pour (milk cloud swirling). Bolt keeps his coffee black and leads (HOTTER, 90 vs 74 °C) from frame 0. 1.2 s "BLACK COFFEE: HOTTER!"; 4.3 s "HOT COFFEE COOLS FASTER" + a live "BOLT'S LEAD: +x.x°C" that shrinks (11 → 7 °C); the HUD shows each cup's cooling rate (2.9 vs 1.5 °/min at the start). 8.18 s = 10:00: "BOLT ADDS HIS MILK", his number falls 68.7 → 56.6 °C and crosses below Mochi's at 8.43 s; "MILK FIRST STAYS HOTTER!" (gold ring on the chart). Cadence 10.23 s: "MOCHI WINS · 61.6 °C vs 56.6 °C". Twist: Bolt, deadpan, "*blows on it anyway*".

## v2 (batch60, 2026-10-30): literally-true banners
- Owner: "let's try, but the text is wrong". NEW RULE (BRIEF_batch60): every on-screen sentence must be literally true for BOTH sides. v1 video → `MochiAndBolt\archive\coffee_milk_v1.mp4`; v1 script at scratch `m60/coffee_milk_before.py`.
- "HOT COFFEE COOLS FASTER" → "THE **HOTTER** COFFEE COOLS FASTER" (both cups are hot; HOTTER in gold, the rest cream).
- Audit found a second false line: "MILK FIRST STAYS HOTTER!" (her cup was the COLDER one until 10:00, so it never "stayed" hotter) → "MILK FIRST ENDS UP HOTTER!".
- Proof-read, kept (true): caption "Add milk NOW or LATER: / whose coffee is HOTTER in 10 min?"; "SAME 90°C COFFEE · SAME COLD MILK" (same carton milk; Bolt's warms 5.0 → 5.8 °C by 10:00, still cold); "BLACK COFFEE: HOTTER!" (true while shown, 1.2-4.3 s); "BOLT'S LEAD: +x.x°C"; "10:00 · BOLT ADDS HIS MILK"; "MOCHI WINS / 61.6°C vs 56.6°C"; "*blows on it anyway*"; HOTTER tag on the live leader; HUD "COOLING x.x°/min", "milk: waiting/pouring/IN"; carton "5°C" (the fridge label).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\coffee_milk.mp4` (**v2**, label v2). Nothing else changed.
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 806 frames = 13.43 s; muxed -14.00 LUFS, peak -2.02 dBFS, last 0.5 s silent; flash PASS (0); seam 0.54. Frames read: 5.5 (new banner), 9.0 (ENDS UP HOTTER), 11.5 s.

## Layout
- Table y 1182. Mugs inner 200 × 257 px (7 × 9 cm), x 378 / 638, handles outward; thermometers in each (0-100 °C); characters r 56 at x 168 / 850 (key content x 112-906). Milk cartons rest in front (x 262 / 772).
- Chart x 150-870, y 410-655 (50-93 °C, 0 → 10 min, a dashed 10 min line); readouts y ~742; HUD y 1366-1544 (TIME + time-lapse, COOLING °/min bar, milk status).
- Static camera, warm calm colours, no flash.

## The physics (honest; real seconds, dt 1 s)
- 200 g coffee at 90 °C; 50 g milk at 5 °C from a 1 L carton that warms slowly in the 21 °C room (5.8 °C at 10 min).
- Heat loss = convection UA (T − 21) with UA 0.28 W/K + evaporation from the open top CE (p_sat(T) − 0.5 p_sat(21)), CE 0.30 W/kPa (steep in T); evaporated water (L 2400 J/g) leaves the mug (2-3 g). Heat capacity = water 4.18 + milk 3.93 J/gK; mixing by energy balance.
- Result: milk-now 73.8 → 61.6 °C; black 90 → 68.7 °C, + milk → 56.6 °C. Gap 5.0 °C. Why: the hotter black cup loses heat ~2× faster (2.9 vs 1.5 °/min at the start).
- Time-lapse speeds up smoothly x40 → x115 (shown live in the HUD) so the degree ticks keep coming as cooling slows.

## Sound
- **Piece:** P. I. Tchaikovsky, The Seasons Op. 37a, "January: By the Fireside" (1876; d. 1893, PD). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD, `<SOUNDFONTS_DIR>\scores\tchaikovsky_seasons_jan\Tschaikowsky-op37.1.mid` + SOURCE.txt; read at runtime.
- **Excerpt:** 3/4, quarter = 88 (bar 2.05 s): bars 1-5; Bolt's pour on the bar-5 downbeat; cadence = A major tonic (bar 6, 10.23 s).
- **Arrangement:** piano (score), violin on the top line, flute 8va very soft, cello on the bar bass, soft strings; cadence = soft timpani A, strings, harp sweep, piano chord, celesta, held strings.
- **SFX (tonal):** milk glugs (pitched blubs, no noise), spoon clinks, a degree tick per whole °C per mug (8th grid, lane pitch), a falling tick run during Bolt's pour (12 ticks), spoon tinks while Mochi leads, banner dings.
- Mastering as ice_cubes: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS), last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 806 frames = 13.43 s. -14.00 LUFS, peak -2.02 dBFS, last 0.5 s -240 dBFS.
- RMS/s: -18.6 -18.7 -17.7 -17.6 -17.1 -17.2 -16.9 -16.3 -16.4 -16.4 -13.9 (cadence) -19.2 -33.4.
- SFX events/s: 8 5 5 4 7 5 5 5 21 3 4 2 0.
- flash_check PASS (0). Seam mean |delta| 0.48 (good band).
- Frames read from the mp4: 0.5, 3.0, 8.45, 11.5 + a 1:1 crop of both mugs at 8.45 s.

## Doubts
- The lead change is late (8.4 s) by design: the whole point is that Bolt leads until the milk goes in at 10:00. The shrinking "BOLT'S LEAD" number carries the middle.
- The chart is compact; the 10-min drop is a short steep segment (the readouts carry it).
- Bolt's carton says 5 °C; the honest sim warms it to 5.8 °C by 10:00 (used in the mix).

## Args and cost
- `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~25 s at 2 encoder threads.

## Outcome
- (fill after upload)

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/coffee_milk.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 806 frames 13.43 s; -14.00 LUFS, peak -2.02 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v2. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-07\3_coffee_milk.mp4`, 00:00 local Nov 9 (= 15:00 US East Nov 8). FHD review copy → `MochiAndBolt\archive\coffee_milk_fhd.mp4`.
