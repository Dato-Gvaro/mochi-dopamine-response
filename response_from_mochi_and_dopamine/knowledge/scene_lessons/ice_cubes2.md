# ice_cubes2: Mixed ice or steel cubes: which keeps it COLD longer? (comment follow-up, 2026-11-08)

- **Brief:** docs/BRIEF_ice_cubes2.md. This is a new scene file, copied from ice_cubes.py, which stays bit-reproducible. lib/ and tools/ are untouched.
- **Source comment:** "How about 1 big one and 32 small ones together" (on ice_cubes, oL2XsaoHd6I).
  - The owner's condition: both cups change.
  - The nameable change: "this time: steel cubes".
- **Deliverable:** `<VIDEOS_DIR>\MochiAndBolt\review\ice_cubes2\ice_cubes2.mp4` (Full HD 9:16, 15.70 s, 942 frames, label `ic2b`). The README holds the titles and the pin.
- **v2 role swap (owner, 2026-11-08):** BOLT = the mix and wins (ep1 he had crushed; the comment asked him to add a big cube = his comeback). MOCHI = the steel: smug early, annoyed at the end.
  - Physics keys are the glasses (`S["mix"]`, `S["steel"]`); `OWNER` maps glass → blob, `GCOL` = the owner's colour. Mochi stays left (coral), Bolt right (mint), as in ep1, so the mix glass moved right.
  - Everything that names or colours a side follows `OWNER`: banners, COLDER tags, chart lines/rings, HUD blocks (steel left, mix right), caption highlights, faces, reacts, SFX pans.
  - v1 (Mochi = mix, label `ic2`) archived: `<VIDEOS_DIR>\MochiAndBolt\archive\ice_cubes2_v1_mochi_mix.mp4`.
  - Fix: `melt = max(0, 1 - m/m0)`; the lerp overshot m0 by 1 ulp → NaN corner radius (a piece could drop for a frame).
- **Caption** (baked; `--nocap` gives the base): "~Mixed ice~ or ~steel cubes~:" / "which keeps it ~COLD~ longer?"

## Story
| clip s | beat |
|---|---|
| 0.00 | Mid-air drop; the splash comes at 0.18 s. The chart and the dashed COLD LIMIT 50°F line are on screen. Banner: "BOTH FROM THE FREEZER: 0°F". |
| 1.05 / 3.0 | Mochi is smug: "STEEL NEVER MELTS!", then "NEVER WATERS DOWN!" (she hops). |
| 4.5 | Bolt goes under 50°F (gold ring) and cheers. |
| 5.0 | "STEEL STALLS AT 58°F" (coral ring at the steel's minimum); Mochi is worried. |
| 7.0 | "STEEL CAN'T MELT → NO 334 J/g"; Bolt laughs. |
| 10.2-12.3 | The small pieces vanish, one tink each. |
| 12.5 | Cadence: "BOLT'S DRINK STAYS COLDER", "49.5°F vs 70.1°F after 26 min", "MELTING ICE SOAKS UP THE HEAT", "(but his is WATERED DOWN +4 oz)". |
| 15.1-15.7 | Dissolve back to frame 0. |

- Mochi & Bolt are drawn with sx = sy = 1. watcher_pose squash is ignored (only hops and tilts), per the rest-shape rule.

## Layout
- The ep1 patio, glasses, chart box and HUD box. **US units first:** big °F readouts with small °C.
  - Chart axis: 36-82 °F, grid at 40/60/80, the COLD LIMIT dashed at 50.
- **Bolt's glass (mix, right):** the big cube floats left of centre (BIG_X -26). The small pieces pack beside it first, then below it, and re-pack as pieces vanish.
- **Mochi's glass (steel, left):**
  - The steel sits on the bottom as a 2×2×2 pile. The back row is offset (+18, -18) and darker, all drawn after the drink, with a soft contact shadow that fades in at landing.
  - The drink level is 0.29 cm higher (the sunk steel displaces 131 cm³).
  - The frost speckle and blue tint fade as the steel warms.
- **HUD:**
  - Bolt (right): ICE LEFT g + bar, "n small · +g water".
  - Mochi (left): STEEL AT °F, a cold-left bar = (T_drink − T_steel) / 43 K, "2.3 lb · +0 g water".

## Physics (real seconds, dt 1 s)
- The ep1 model: h 250 W/m²K, A = 6s² (packed ×0.75), L 334 J/g, glass UA 0.8 W/K, 300 g of tea at 25 °C, 30 °C air.
  - **The one change:** everything starts at -18 °C.
  - Each ice piece is lumped: it warms to 0 °C (c 2.09), then melts.
- **Bolt (mix):** a 60 g big cube + 32 small pieces, seeded (7) at 0.45-1.55 × the mean (60 g total).
- **Mochi (steel):** 8 cubes of 2.538 cm (one inch), the same volume as 120 g of ice = 130.9 cm³ = **1034 g** (2.28 lb); c 0.50, packed ×0.75.
  - This is generous to the steel: a tight 2×2×2 stack exposes about 0.5.
- **Results:**
  - **26 min:** 49.5 °F (9.7 °C) vs 70.1 °F (21.2 °C). The mix has 8 g of ice left and 112 g of meltwater.
  - **Mix:** coldest 42.8 °F at 10.0 min; under 50 °F from 2.78 to 26.9 min.
  - **Steel:** coldest 57.8 °F at 3.45 min (packing 0.5 → 58.9; 1.0 → 57.1); never under 50 °F.
  - **No lead change:** the ice's surface (about 331 cm²) beats the steel's larger ΔT on 232 cm².
- **Vs ep1** (same freezer start; the mix is never the best of the three):

  | | coldest | at 30 min | min under 50 °F |
  |---|---|---|---|
  | crushed | 4.3 °C | 11.3 °C | 25.7 |
  | mixed | 6.0 °C | 11.0 °C | 24.1 |
  | big cube | 8.4 °C | 10.6 °C | 20.6 |

- **Time-lapse:** PCHIP through (0.3 s, 0), (2.6 s, 1 min), (5.0 s, the steel's stall), (12.5 s, 26 min). It runs x13 → x260 and is shown live in the HUD.

## Sound
- **Piece:** Vivaldi, Winter Op. 8 No. 4, II. Largo (1725; d. 1741, PD), Mutopia #351 `winter-score-1.mid`. Beats 0-20 (bars 1-5) at quarter = 96, cadence = the E-flat tonic at 12.5 s.
- **Arrangement:**
  - The solo line on violin, with celesta an octave up (soft).
  - Violins I/II on pizz, viola on strings_slow, cello, and a harp on the half-bar bass.
  - The cadence: timpani E-flat, a strings chord + violin G5, a harp sweep, celesta, held strings.
- **SFX (tonal, on the harmony):**
  - Ice clinks plus steel clanks (inharmonic 1 / 2.40 / 3.95) on the drop.
  - Cracks from the freezer-cold ice at 0.6/1.3/2.2/3.4 s.
  - A tick per ½°F per glass (8th grid).
  - A tink per small piece gone (16th grid).
  - A soft tink per beat while the mix is under the limit.
  - Pans follow the glasses: ice 690 (right), steel 360 (left).
  - Banner dings and cadence dings.
- **Mastering:** ep1 chain: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (encoded, Full HD)
- v2 (`ic2b`): h264 yuv420p 1080x1920 @ 60 fps, 942 frames = 15.70 s; -14.01 LUFS, peak -3.07 dBFS, last 0.5 s -96 dBFS; flash_check PASS (0 flashes, mean lum 0.055). Frames read from the mp4: 0, 5.0, 13.8 s.
- v1 (`ic2`):
- h264 yuv420p 1080x1920 @ 60 fps, 942 frames = 15.70 s.
- -14.01 LUFS, peak -3.07 dBFS, last 0.5 s ≤ -90 dBFS.
- flash_check PASS (0 flashes, mean lum 0.054).
- Seam: last → first 3.91 vs adjacent 3.57 (falling ice, continuous).
- SFX events/s: 15 9 7 9 7 9 8 7 6 5 14 12 9 0.
- Frames read from the mp4: 0.0, 0.3, 0.5, 4.6, 5.0 (1:1 crop of the glasses), 7.5, 11.0, 13.8.

## Doubts
- The event rate dips to 5-6/s at 8-10 s (the mix near its minimum), then climbs with the vanishing small pieces.
- The steel never leads, so Mochi's early smugness rests on claims only.
- Mochi's straw rests on the steel pile, so it hangs mid-drink for the first 0.3 s, before the cubes land.
- The four finale lines sit tight between the caption and the chart.

## Args and cost
- `--seed` (7), `--sfx`, `--findb`, `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label` (ic2b; v1 was ic2).
- Sim ~1 s. A FAST still ~1 s. Full HD render + audio ~35 s at 2 encoder threads.

## Outcome
- (fill after upload)
