# checkout_queue — 3 full carts or 6 baskets: which line is FASTER? (batch54, 2026-10-28)

- Brief: docs/BRIEF_batch54.md (Mochi & Bolt 3). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from pilot_parking / rain_run.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch54\checkout_queue.mp4` (**v1**, Full HD 9:16, 16.53 s, 992 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~3 full carts~ or ~6 baskets~:" / "which line is ~FASTER~?"
- **Story:** a supermarket, side view, checkout 1 (Mochi, top) and checkout 2 (Bolt, bottom). Both buy one carton of milk. Mochi queues behind 3 full carts (19/20/17 items); Bolt behind 6 baskets (6/6/7/7/6/5). Items glide down the belt and beep through the scanner, carts/baskets empty item by item, customers pay (badge "PAY") and walk out, the line shuffles up. HUD race = ITEMS AHEAD (Bolt's logic): Bolt leads from frame 0 (36 vs 55), "MOCHI'S LINE PULLS AHEAD!" 5.5 s, "BOLT'S LINE BACK IN FRONT!" 6.8 s, PRICE CHECK in Mochi's line 7.7-9.0 s (item stuck with a "?", amber lamp, cashier on the phone; Bolt laughs), "MOCHI'S LINE PULLS AHEAD!" 9.7 s. Mochi pays and steps out on the cadence: "MOCHI'S OUT FIRST! 5:36 vs 5:52"; Bolt out 0.67 s later, wow → annoyed stare. "EVERY PERSON = ~40 s TO PAY / FEWER PEOPLE WINS".

## Layout
- Floors y 840 (checkout 1) / 1255 (checkout 2); counter x 490-902, belt 500-760, scanner 775, bag 820, register + cashier ~862-890 (cashier = decoration). Queue slots: carts x 620/475/330, Mochi 185 (carts drawn 0.82× in front of their owners); baskets every 76 px from 620, Bolt at 164. Characters r 50, customers r 41 (muted colours), item-count badge over each customer.
- HUD (y 1366-1544): "WAITED m:ss (time-lapse x25)", per side "MOCHI · 3 CARTS" / "BOLT · 6 BASKETS", big ITEMS AHEAD (→ "OUT 5:36"), PEOPLE AHEAD.
- Banners in the clear band y 345-530 above checkout 1. Key content inside x 0.10-0.84w (Bolt x 114-214; the cashier/lamp reach x 910, decoration). Static camera; muted shelves.

## The sim (seeded, honest, real seconds)
- Per customer: fixed time U(30, 50) s (18 % before the first scan = stepping up / unloading start, the rest = pay + receipt after the last scan); per item U(2.0, 3.4) s. Mochi's/Bolt's own milk: 2.6 s + 38 s (identical). Price check in Mochi's line: U(26, 34) s before a seeded item of customer 2 or 3 (here 31.3 s, customer 3).
- Seed 2072 (search `--seed -1 --search N`, scored on: Mochi wins by ~9 s real, items-ahead leader sequence Bolt → Mochi → Bolt → Mochi with ≥1.3 s between flips, the price check ~7 s). Mochi done 335.6 s, Bolt 352.1 s (margin 16.5 s = 0.67 s of clip).
- Honest odds: over 400 seeds Mochi's line wins 335 (84 %) — with the price check in her line. Expected values: 3×40 + 56×2.7 ≈ 271 s (+31 s check) vs 6×40 + 37×2.7 ≈ 340 s.
- Time-lapse: one constant factor ×24.7, chosen so Mochi pays on the cadence; frame 0 = 12 s into the wait (both belts already moving).

## Sound (music first)
- **Piece:** W. A. Mozart, *Ein musikalischer Spass* (A Musical Joke) K. 522, I. Allegro (1787; Mozart d. 1791, PD) — a joke piece (clumsy horns), bustling, "shop-music" bright. Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD edition, `k522-mv1.mid/.ly/.rdf`, saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\mozart_musical_joke\`. All 5 parts read at runtime.
- **Excerpt:** F major 4/4, quarter = 144 (bar 1.667 s), source bars 6-13 (the tonic chords, the triplet runs, the held horn notes), cadence = the F-major chords of bar 14 (13.33 s = Mochi pays).
- **Arrangement** (lib/orchestra): the score's own scoring — horns, violin I, violin II, viola, cello + contrabass; cadence: timpani + three F-major horn/string chords + a soft held chord.
- **SFX** (tonal): a scanner "bip" per 16th slot holding scans (per lane, pitched to the chord: checkout 1 higher, checkout 2 lower), card "bip-bip" per payment, two step ticks per shuffle, the price-check "boo-bop" (low, soft), lead-change dings, the cadence chime.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 992 frames = 16.53 s. −14.00 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −18.7 −18.8 −17.9 −18.0 −17.5 −17.9 −17.6 −16.5 −17.5 −17.3 −16.5 −16.8 −16.0 −14.6 (cadence) −16.7 −30.6, then silence.
- SFX events/s: 16 10 9 9 15 14 10 13 4 17 9 7 7 8 0.
- flash_check PASS. Seam: pre-encode last → first 0.51 vs adjacent 0.33 (continuous); encoded check_clip 0.92 (I-frame coding noise).
- Frames read from the mp4: 0.5, 2, 5.6, 6.85, 6.9, 8.0 (+1:1 crop of the price check), 9.8, 13.4, 15.5.

## Doubts
- The race metric is ITEMS AHEAD (what Bolt believes); the real finish is decided by the payments, which the HUD shows as PEOPLE AHEAD + the "PAY" badges. A viewer might read the lead changes as noise; the final banners spell the lesson.
- Event rate dips at 8 s (the price check: 4 events) — it is the stall, on purpose; it does not climb at the end (the lines run out of items).
- Customers are generic recoloured blobs (the toon bodies); the cashier is too.
- The time-lapse (×25) is stated in the HUD; the WAITED clock keeps running after Mochi leaves.

## Args and cost
- `--seed` (2072; `-1` + `--search N`), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 0.1 s (search 4000 seeds ~5 s); Full HD render ~25 s at 2 encoder threads.
- Owner review (batch55, 2026-10-28): approved as is → 4K ship.

## Outcome
- (fill after upload)

## Ship (batch55, 2026-10-28)
- Owner: approved unchanged. 4K `NF_SCALE=2.0 --label ship` (same code and seed as v1): h264 High yuv420p 2160x3840 @ 60 fps, 992 frames = 16.53 s; −14.00 LUFS, peak −2.00 dBFS, last 0.5 s silent; flash PASS (0, mean lum 0.05); seam mean |Δ| 0.76. Encoded frames read at 0.3 s and the finale.
- Staged: `MochiAndBolt\schedule\2026-11-05\1_checkout_queue.mp4`, 08:00 local Nov 6 (= 23:00 US East Nov 5). FHD review copy → `MochiAndBolt\archive\checkout_queue_fhd.mp4`.
