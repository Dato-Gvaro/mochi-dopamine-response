# freezer_burst — Forgot it in the freezer: can or glass bottle, which BURSTS first? (shorts_1115 M2, 2026-11-15)

- Brief: docs/BRIEF_shorts_1115.md §M2. New file `scenes/freezer_burst.py` (ice_cubes' clock/HUD/sound-chain pattern; can and shatter art redrawn). ice_cubes untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\freezer_burst.mp4` (Full HD 9:16, label v1) + `freezer_burst_files\`.
- Caption (baked; `--nocap` = base): "~Can~ or ~glass bottle~ in the freezer:" / "which one ~BURSTS~ first?"
- Mochi = the CAN (left, red, white band, generic "COLA"); Bolt = the GLASS BOTTLE (right, green-brown longneck, cream "COLA" label). No brands.

## Model (real seconds, dt 1 s)
- 355 ml cola each (320 g water, c 4.0 J/gK), 22 °C → freezer air −18 °C, h 12 W/m²K (closed freezer, still air).
- Can: Al 0.1 mm, 13 g, 0.0323 m² (12 oz, 6.6 × 12.2 cm). Bottle: 12 oz longneck, glass 3 mm (k 1.0), 200 g, 0.043 m² (more area per ml: it cools faster).
- Ice shell grows from the walls; its conduction (k_ice 2.2) adds in series. Supercool to −3 °C, then nucleate: 2.5 K of supercooling freezes ~3 % at once (dendrite flash); the rest at −0.5 °C (sugar + CO2).
- Pressure: CO2 headspace + Henry (1.7 vol/vol/bar at 0 °C), 2.1 bar abs cold. Ice adds 0.09 × the frozen water (28.8 ml at 100 %). Headspace: can 12 ml, bottle 8 ml (neck). With headspace: gas law + redissolving CO2; without: the liquid (K 22,000 bar) against the container's give.
- Can: 0.6 ml/bar + a 6 ml dome reversal at 6.2 bar (12 oz can bottom buckle ~90 psi); seam/end fails at 7 bar. Bottle: ~0.02 ml/bar, fails at 12 bar (returnable longneck pressure rating ~12 bar / 175 psi). Values are typical published figures, not measured; the doc states them.
- **Result:** bottle 0 °C 0:42, nucleates 0:52, headspace gone 1:42, **BURSTS 1:44 at 29 % ice**. Can 0 °C 0:49, nucleates 1:00, headspace gone 2:53, dome 3:06, **BURSTS 4:01 at 70 % ice**. Bottle first in everything (no lead change; brief's title 2 order does not happen, not used).
- BURST lines on the ICE bars (29 % / 70 %) and the dials' red zones (12 / 7 bar) are from the model, from frame 0.

## Clock + story
- Vivaldi grid, q = 104 (beat 0.577 s). Time-lapse warped (PCHIP) so: bottle nucleates beat 6 (3.46 s), can beat 8 (4.62 s), bottle bursts **bar 6 downbeat (11.54 s)**, can dome beat 22 (12.69 s), can bursts **bar 7 downbeat (13.85 s)**; after that ×60. Clip 15.60 s (936 f), dissolve to frame 0 from 15.0 s. The pill shows the live ×speed.
- Frame 0: both mid-slide in from the door side, door swinging shut (warm light → blue, 0.3 s), clock 0:00; clink 0.2 s.
- Banners: "STILL LIQUID below 0°C!" → "...then it FREEZES at once", "THE BOTTLE HAS NO GIVE", "BURST!" (over the bottle), "THE CAN BULGES: +6 ml", "BURST!" (can), stamp "GLASS 1:44 · CAN 4:01".
- Bottle burst: 40 seeded shards fly and settle on the shelf; the frozen shell keeps the bottle's shape. Can: lid pops on a hinge, a slush ribbon extrudes (150 px). No slow-mo.
- Mochi/Bolt sit below the freezer (x 163 / 853, y 1292), rest shape (squash disabled).

## Sound
- Vivaldi, The Four Seasons, Winter RV 297 i. Allegro non molto (PD; Mutopia #351, `<SOUNDFONTS_DIR>\scores\vivaldi_winter\winter-mids\winter-score.mid`, read at runtime). Bars 1-6 as written at q 104 (solo violin, tremolo violins, viola, cello + bass), timpani + soft crash on the bottle burst (bar 6), F-minor chord (strings, violin, harp, timpani) on bar 7 = the can.
- SFX (synth, no hiss/whoosh): door thump, shelf clinks, 10-tink nucleation cascades, a tink per 2 % of ice on the 8th grid, can dome tok, glass shatter (26 glassy partials), seam tok + slush splort, stamp bloop.

## Checks (encoded Full HD, label v1)
- h264 yuv420p 1080x1920 @ 60, 936 f = 15.60 s; −14.01 LUFS (muxed, stereo), peak −1.98 dBFS, last 0.5 s −240 dB; flash_check PASS (0 flashes, mean lum 0.03); seam mean delta 0.34.
- SFX onsets: 43 of 53 event times (81 %) have a >1.2 kHz flux onset within 40 ms. SFX events/s 3 0 0 10 12 1 2 2 2 3 4 5 5 4 1.
- Frames read every ~1 s from the mp4; 1:1 crops: bottle shatter 11.60 s, can seam 13.95 s, nucleation 3.52 s.
- Fixes during the build: BURST! banners moved onto each container (the can's hid the seam ribbon); the dissolve switches the HUD once (was doubled text); "STILL LIQUID at −3°C" → "below 0°C" (it shows 0.9 s before nucleation, when the drinks read −1.6 °C).

## Doubts
- 4.6-10 s is a slow middle (ice % and dials creep; tinks ~2/s). Music carries it.
- After the burst only 29 % of the bottle is ice (a shell holding slush); drawn as the frozen shape standing.
- Headspace / compliance numbers are estimates; a can with less headspace bursts sooner.

## Args
- `--bpm` (104) `--sfx`, `--still --frame a,b`, `--report`, `--nocap`, `--reuse`, `--label`.

## v2 (2026-11-15 review: "the 4.6-10 s middle is slow"): `--v2`, label v2, 11.98 s
- Owner verdict on v1: OK on its own; research says mid-tier because nothing pays off until 11.5 s.
- **Same model, same real times** (bottle 1:44, can 4:01). Only the clock map changes.
- **Beat anchors (q 104):**
  - bottle nucleates on beat 3 (1.73 s); can on beat 4 (2.31 s);
  - bottle BURSTS on beat 12 = bar-4 downbeat (6.92 s);
  - can dome on beat 14 (8.08 s);
  - can BURSTS on beat 16 = bar-5 downbeat (9.23 s).
  - End tail 2.75 s; clip 11.98 s (719 f).
  - Pill speeds: ×1,250-2,350 while cooling, ×370-960 while the ice grows, ×3,000-5,200 between the bursts.
- **Score:** starts at Winter bar 3 (`SCORE_OFF` 8 beats), so the shatter is still score bar 6 and the seam is the bar-7 chord.
- **Frame 0:** `T_DOOR0` 0.15 / `T_SLIDE0` 0.12. Frame 0 is mid door-swing and mid-slide; clink at 0.08 s, door thump at 0.15 s.
  - The °C readouts fall ~35 °C/s on screen from frame 0 (22.0 → 11 °C by 0.3 s).
  - No rewind, no burst-first.
- **v1 stays the default** (bit-reproducible: 15.60 s, same anchors).
- **Checks (encoded FHD):**
  - −14.01 LUFS, peak −1.99 dBFS, tail −240 dB;
  - flash PASS (0, mean lum 0.03);
  - seam 0.51;
  - 96 % of SFX events have an onset within 40 ms;
  - SFX/s 3 9 13 3 3 4 7 3 5 3.
- **Lesson:** a time-lapse scene can be cut by re-anchoring the clock alone. Keep the events on downbeats, skip score bars at the start so the musical climax still lands on the same bar, and start frame 0 inside the setup animation (a time offset, not a rewind).
- **Doubt:** 2.3-6.9 s is still the quietest stretch (tinks ~3/s, ICE % creeping 4 → 25 %), but it is now 4.6 s instead of 6.9 s.
