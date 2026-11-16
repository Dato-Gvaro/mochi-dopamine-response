# stone_skip — Flat & fast or high & hard: who SKIPS more? (batch59, 2026-10-29)

## v2 (batch60, 2026-10-30): NERD STATS
- Owner on v1: "ok, needs nerd stats" (BRIEF_batch60 NERD STATS: live numbers next to objects, labelled vectors, readable on a phone, never covering the action). v1 video → `MochiAndBolt\archive\stone_skip_v1.mp4`; v1 script at scratch `m60/stone_skip_before.py`. Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\stone_skip.mp4` (**v2**, label v2). Sim, story, timings, music, banners unchanged.
- **Stat panel per stone** (x 110-380 / 646-906, y 432-818, fonts 21-29 px): SPEED (live |v|), SPIN (Mochi 840 rpm, −4 % per skip → 516 at the 12th; "stopped" once sunk; Bolt "none"), TILT (Mochi 20°, held by the spin; Bolt's live tumble angle, the same one the drawing uses), KIN. ENERGY of a 100 g stone (Mochi 8.8 J → 0.7 J; Bolt 10.2 → 12.8 J as he falls, then "all 12.8 J into the water") + "last bounce −x.x J".
- **BOUNCE CHECK gauge** (the model's three conditions): SPIN ✓/✗, ANGLE (latest entry) < 30° ✓/✗, SPEED > 3.55 m/s with a 0-14 m/s bar, red zone below 3.55. Mochi: ✓✓✓ every skip; at the end her after-bounce speed 3.30 m/s sits in the red zone ✗ → sinks. Bolt: SPIN ✗, ANGLE 36° > 30° ✗, SPEED ✓ (he had the speed, not the spin or the angle).
- On the action: a white "v" velocity arrow on each flying stone; at each of Mochi's impacts (0.48 s) a 20° protractor (water line + the stone's plane, gold arc, "20°") and the energy that bounce cost ("−0.9 J") under the water. Mochi's stone is now DRAWN at its 20° tilt (was 7°) so the picture matches the number.
- Panels fade to 30 % while a stone (or its arrow) passes behind them (Bolt's arc at ~0.3 s and ~4.1 s); they fade out at the cadence + 0.9 s for the result + twist lines.
- Model notes: 100 g stone, 840 rpm spin and its 4 %/skip decay are illustrative assumptions (typical skipping-stone values); the 20° tilt, 30° and 3.55 m/s thresholds are the v1 model (Clanet 2004 spirit).
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 890 frames = 14.83 s; muxed -14.00 LUFS, peak -2.01 dBFS, last 0.5 s silent; flash PASS (0); seam 1.51 vs 0→1 1.13 (the pan moves; dissolve, continuous). Frames read: 0.3, 2.0, 4.2, 5.2, 10.5, 12.6 s + stills.

- Brief: docs/BRIEF_batch59.md (Mochi & Bolt 5). New scene file; caption/banner/HUD/sound chain copied from paper_plane / pool_splash; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\stone_skip.mp4` (**v1**, Full HD 9:16, 14.83 s, 890 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~Flat & fast~ or ~high & hard~:" / "who ~SKIPS~ more?"
- **Story:** a calm lake at sunset, side view; a metre rope on the water (label every 5 m). Frame 0: both stones just left the dock (Mochi crouched side-arm, Bolt overhand). "LOW + SPIN vs HIGH + HARD". Mochi's spinning stone skips (a big number pops above it per skip: 1, 2, 3…); Bolt's tumbling stone flies a high arc and leads on distance ("BOLT'S GOES WAY OUT…"). 4.97 s "PLUNK. 0 SKIPS" at 21.9 m (a flag buoy; his stone sinks with bubbles), "can her skips beat 21.9 m?". 6.18 s "SHE PASSES HIS MARK!" (gold ring, skip 5). The hops get shorter and quicker: "…PITTER-PATTER…", skip 12 at 10.86 s, and the stone sinks at 31.6 m on the cadence (11.33 s): "MOCHI WINS · 12 SKIPS · 31.6 m vs 0 · 21.9 m". Twist line: "(Bolt: 0 skips, 1 very loud PLUNK)"; Bolt's HUD portrait goes annoyed while Mochi laughs.

## Layout
- Water line y 1100, 150 px/m, lake bed y 1352. One smooth pan planned offline (Gaussian σ 0.28 s; midpoint of both stones until the plunk, then Mochi's stone + 1.4 m look-ahead; no zoom). Stones drawn 54 px wide (cartoon size), dotted trails in each colour, ripple rings per skip.
- The characters stand on the dock at frame 0 and leave the frame as the camera pans (by ~0.5 s); their faces stay in the HUD as reaction portraits (x 166 / 849).
- HUD y 1376-1554: per thrower SKIPS (big), DISTANCE (the leader's in colour), the reason line ("spin holds the tilt" / "no spin: it tumbles"), SLOW-MO x3 / REAL SPEED.

## The physics (honest model, dt 1/1200 s, real seconds)
- Mochi: 13 m/s from 0.6 m, slightly down (-1.2 m/s); first entry 15.6 deg. Bolt: 13 m/s forward + 7.5 m/s up from 1.6 m (15 m/s at 30 deg); apex 4.5 m; entry 35.7 deg.
- A skip happens if the stone spins (holds its ~20 deg tilt), the incidence is < 30 deg and the forward speed after the bounce is ≥ 3.55 m/s (Clanet et al. 2004: shallow incidence + a minimum speed). Each skip costs 10 % of the forward speed; take-off vertical speed = 0.21 x forward speed (shallow again). So the hops shrink geometrically: intervals 1.5 → 0.52 s (clip), the event rate rises.
- Result: Mochi 12 skips, 31.6 m (sinks at 3.67 m/s); Bolt 0 skips, plunk at 21.9 m. Distances from the dock edge.
- Slow motion x3 up to the cadence (the stone sinks on it), real speed after.

## Sound
- **Piece:** F. Schubert, Impromptu in A-flat D 899 No. 4 (Op. 90/4) (1827; d. 1828, PD): the opening's falling arpeggio cascades (rippling water). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project Mutopia-2008/09/28-1552 (licence: Public Domain), `<SOUNDFONTS_DIR>\scores\schubert_impromptu_d899_4\SchubertF-D899-4-Impromptu.mid` + .rdf + SOURCE.txt; read at runtime.
- **Excerpt:** score beats 3-39 (A-flat minor cascades → the C-flat = B major cadence), quarter = 190.6 (the piece's own Allegretto; set so the stone sinks on the cadence, 11.33 s).
- **Why not Invention 13 (the first pick):** the parallel DopamineEXE builder used the same bars of Bach's Invention 13 for ol_rope_bridge in this batch, so it was swapped before delivery.
- **Arrangement:** piano (all four voices), soft harp doubling the upper voices, cello + soft strings on the bar bass; cadence = timpani B, strings, harp sweep, piano chord, celesta, held strings (B major).
- **SFX (tonal):** a note per skip walking UP the harmony (the pitter-patter becomes a rising run) + droplet plips after each skip (2 → 7 as the skips crowd in), a distance tick every 2 m per stone, Bolt's deep plunk bloop, Mochi's final sink bloop, banner dings, two low sad bloops for Bolt after the result.
- Mastering: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 890 frames = 14.83 s. -14.00 LUFS, peak -2.01 dBFS (measured on the muxed mp4), last 0.5 s -240 dBFS.
- RMS/s: -17.9 -18.2 -17.3 -17.7 -17.5 -16.7 -16.2 -16.7 -15.6 -15.8 -15.7 -13.8 (cadence) -17.4 -29.4.
- SFX events/s: 9 5 8 7 10 6 10 8 7 12 14 10 2 0.
- flash_check PASS (0). Seam mean |delta| 1.09 (grey) against 0.98 between frames 0 and 1 (the pan moves at the seam): continuous.
- Frames read from the mp4: 0.5, 2.5, 5.1, 6.3, 11.6, 13.5 + a 1:1 crop of skip 11 at 10.5 s.

## Doubts
- A first version used a perspective view from behind the dock; the far skips (5-12) shrank to a few pixels near the horizon, so it was replaced by the side-on pan (stills only, never rendered).
- The skip threshold numbers (10 % loss, 3.55 m/s, 30 deg) are a tuned phenomenological model in the spirit of Clanet 2004, not a hydrodynamic sim; the outcome (low/flat/spin skips, steep/tumbling plunks) is the real physics.
- The sky above the action is calm and fairly empty (Bolt's arc uses it until 5 s).
- The characters are on screen only for the first ~0.5 s; their reactions live in the HUD portraits.

## Args and cost
- `--umin` (3.55), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~50 s at 2 encoder threads.

## Outcome
- (fill after upload)

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/stone_skip.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 890 frames 14.83 s; -14.00 LUFS, peak -2.01 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v2. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-07\2_stone_skip.mp4`, 16:00 local Nov 8 (= 07:00 US East Nov 8). FHD review copy → `MochiAndBolt\archive\stone_skip_fhd.mp4`.
