# ol_flag_worlds (DopamineEXE, docs/BRIEF_shorts_1115.md D1)
- New file. Mechanic from the owner's Ley Cero reference (research/reference_leycero.md): a gravity ladder that ends in a black hole, a stage meter, and an end state visible at frame 0. The LOOK is ours: no orb lattice, no 3D plate, no "wait for" line. Ours is a SHATTER ladder: a flag of 2,048 glued tiles is dropped 1 m onto the same steel plate under each world's gravity.
- Caption (overlay PNG, `--capimg`; the base is rendered with `--cap ''`): `Same flag. Same 1 m drop. ~Every world~.|Last stop: a ~BLACK HOLE~`.
- Fork sources:
  - `lib/splitdust.py` / `ol_sierpinski`: crack hairlines, glassy tinks, DUST, loop dissolve.
  - `ol_black_hole` v2: the face-on disc, then the lensed tilt (lens_raster copied).
  - `ol_flag_colours3`: paint_flag (subset copied).
  - `ol_domino_giant`: one labelled line per moment.

## World (logical 1080x1920)
- **Flag:** 64 x 32 tiles of 10 px (640 x 320, x 188-828, release top y 520), 1 m = 320 px, so the flag is 2 m x 1 m.
  - Painted from flagdata at device resolution, with a baked bevel per tile, so it reads as a glued mosaic.
  - The USA flag is drawn at 2:1, not the official 1.9:1.
- **Plate:** brushed steel, x 118-898, top y 1160, 22 px thick. It is a solid box in the sim.
- **Planet limb:** a dim limb under the plate per world, fading to black within 260 px:
  - Moon grey craters, Mars rust, Earth blue with land and clouds, Jupiter bands with the spot, Sun granulation, neutron star cyan-white.
  - It cross-fades 0.3 s at each world start.
- **HUD:**
  - WORLD row at y 362: 7 icons, spaced 118 px across x 154-862, with a gold ladder line. The black hole's gold ring is visible at frame 0.
  - Result chips at y 422.
  - One line per world at y 482 ("MOON · 0.17 g · hit in 1.11 s").
  - "1 m" bracket at x 168.
  - Counter at y 1505: PIECES, then FLAT, then SWALLOWED / 2,048.
  - Watermark at 1352.
- The black hole sits at (480, 1010), 28 px left of centre so the spiral's far tail stays nearer the safe band. Shadow r 46 px; the lensed view zooms to a shadow of 118 px.

## Physics (seeded, fixed dt; `--dry` prints the table)
- **Lattice:** one node per tile, with h/v glue bonds and diagonal shear bonds.
  - Lattice sound speed 60 m/s (soft, so the impact plays over about 1 frame). dt 0.1 ms.
  - The plate is a penalty box with friction 0.4. Tiles have contact repulsion.
  - Internal friction β = 100/s: each piece's elastic motion relaxes toward its own rigid motion. Without it the panel bounced 0.7 m off a 1 m drop.
- **ONE bond strength (EPS0 0.020)**, Weibull m = 4, scattered per bond by ONE seeded draw, so it is the same flag in every world. It was set once, on "Earth breaks it into a few dozen pieces": 0.021 gave 25, 0.020 gives 35.
  - A bond breaks past that tensile strain, or past 6x it in compression.
  - Never tuned per world: only g changes.
- **Pieces** = connected groups over the intact h/v glue, counted every frame.
- The fall before contact is analytic (real fall time).
- The flag is tilted 1.2°, so the bottom-right corner lands first. A perfectly flat landing gives unnatural horizontal strips.

| World | g (m/s²) | Fall | Impact | Sim result (seed 7) |
|---|---|---|---|---|
| Moon | 1.62 | 1.11 s | 1.8 m/s | 1 piece, 48 glue bonds cracked: **CRACKED** |
| Mars | 3.71 | 0.73 s | 2.7 m/s | **2** |
| Earth | 9.81 | 0.45 s | 4.4 m/s | **35** |
| Jupiter | 24.79 (1-bar cloud tops; no surface) | 0.28 s | 7.0 m/s | **~358-361** |
| Sun | 274 (photosphere; no surface) | 0.085 s | 23 m/s | 2,027 of 2,048: **DUST** |
| Neutron star | ~1.4e12 | 1.2 µs | ~1,700 km/s | drawn **FLAT**: a film on the flattened plate |
| Black hole | none (no floor) | - | - | **SWALLOWED 2,048 / 2,048** |

- **Jupiter and the Sun have no surface.** The plate is "a steel plate under that world's gravity" (g at the cloud tops / photosphere). Nothing on screen claims a surface.
- **The neutron star is not simulated** (no lattice can say anything at 1,700 km/s). It is drawn as the flag and plate pressed into a film, with a warm local glow and a shock along the plate.
- **The black hole is stylised:**
  - Tiles fall in a point-mass field. The flag starts on a sub-circular orbit: 0.50x the circular speed at its centre, orbital period 2.2 s there (GM 2.9e8 px³/s², start 470 px/s).
  - Differential rotation shears the flag into a striped spiral stream (a tidal-disruption stream).
  - Gas drag on the orbital speed (0.13/s, x3.5 near the horizon) is solved by bisection so the last tile crosses the horizon on the F fermata.
  - Tried first: GM solved for timing with a 170 px/s start. Everything fell nearly radially into a wedge; no spiral.
  - At 0.62x circular the spiral wraps twice, but the tail left the frame (x 1,083). At 0.42x it reads as a plunge. At 0.50x the far tail peaks at x ~1,000 (0.92 w) for ~0.5 s while the spiral itself stays inside the band.
  - The same per-bond strengths break when the tidal stretch passes them: 3,717 of 4,000 glue bonds are torn before either of their tiles reaches the horizon. That is the honest "tides tear it apart before anything is hit".
  - Not to scale: a real stellar black hole (~10 suns, horizon ~30 km) tears a 2 m object apart thousands of km out.
- **Calibration history:**
  - v0 had an explicit node-plate penalty with no side faces. A tile that slid off the plate edge and re-entered from the side got a huge upward kick, flying 17 m/s mid-air (Mars 139 pieces, Earth 35 then 57).
  - Fix: the plate is a box (push out through the nearest face), overlaps are capped at 0.35 L, and contact pairs are rebuilt every 2 steps.

## Clock = the score
- Beethoven 5 i, quarter beats; bar = 2 beats; tempo quarter = 216 (half = 108).
- Frame 0 = beat 0.5 (the first G), so the music sounds from frame 0.
- **Fermatas:**
  - bar 2 Eb held 2.0 s (the Moon's slow bounce);
  - bars 4-5 D held +0.4 s;
  - beats 34-44 broaden to 0.30 s/beat;
  - the F fermata (beat 44) is held 2.75 s (the lensed view).
- **DUMs:**

  | World | Beat | Time |
  |---|---|---|
  | Moon | 2 | 0.42 s |
  | Mars | 6 | 2.97 s |
  | Earth | 12 | 5.04 s |
  | Jupiter | 20 | 7.26 s |
  | Sun | 28 | 9.48 s |
  | Neutron star | 32 | 10.59 s |
  | Black hole tutti | 36 | 11.75 s |

  - Black-hole release on the tutti pickups (beat 34.5, 11.30 s).
  - Last tile swallowed at beat 44 (14.15 s).
- Each world's flag appears 0.28 s before its release and falls for the real fall time, so the ladder accelerates by itself. World windows: 2.4 / 2.3 / 2.4 / 2.4 / 1.2 / 0.6 s, then the black hole.
- **Clip:** 16.90 s, 1,014 frames. 0.7 s dissolve to frame 0.

## Sound
- **Music:** Beethoven, Symphony No. 5 in C minor, Op. 67, i (1807-08; d. 1827, PD).
  - SOURCE: Mutopia #941 `Symphony5_1.mid` (Breitkopf & Haertel 1862-65; the Mutopia file is Public Domain), `<SOUNDFONTS_DIR>\scores\beethoven_symphony5_1\` + `SOURCE_mutopia_941.txt`.
  - Beats 0.5-48: the motto, the imitative build, the ff tutti and the F fermata.
  - All 12 parts are mapped to the orchestra.
  - Also used by domino_branch (bars 94-122), jar_versus and ol_sand_vs_stars*. Not Dvořák iv (ol_dig_through3 on Nov 23). No Holst Mars or Valkyries with flags.
- **Arrangement:**
  - A timpani stroke under every world's DUM, and a soft boom on the neutron star.
  - The black hole: a rising oohs + slow-strings swell (C minor → F minor), then a celesta + harp rise on the lensed view.
- **Level:**
  - The ff motto keeps its own level.
  - The build is levelled with a 6 dB crescendo (ol_black_hole's level_bed).
  - The fermata fades out; the last 0.6 s are digital silence.
- **SFX (own synthesis, all partials < 6 kHz):**
  - a landing clack per world (tile on steel: click + inharmonic ring + body), lower per world (84 → 67);
  - settle clacks from the sim's new plate contacts (≥ 0.18 m/s, ≥ 35-60 ms apart);
  - glassy crack tinks from the sim's glue breaks (one per 40 ms bin, ≤ 25/s, on the sounding chord);
  - the DUST as tonal sand grains (5 ms ticks, not noise);
  - a low neutron thunk;
  - in the black hole, tiles' gulps bending DOWN (≤ 25/s) and glue tinks;
  - 8 falling chimes at the last tile.

## Neutrality rules (the series)
- One flag per episode (`--flag`), with identical physics, height and bonds. Never flag vs flag; no ranking.
- Excluded in code: Russia, Belarus, Iran (owner), Israel, Palestine, Saudi Arabia, Iraq, Afghanistan (brief). Also skip any pair in active conflict.
- No fire. The country's name is the only text about the country.
- Order after the USA: Indonesia, Brazil, Philippines, Mexico, India, Vietnam, Japan, Germany, UK.
- `paint_flag` here supports H/V/R/P/C/E/S/M/RING/L/XC. A flag that needs UJ/YY/RR/STAR_O/ARC/RAYS/TRI_O/PLUS/CHECK/SAW/HALF_E/DIAMOND (e.g. the UK's UJ) needs that op copied from ol_flag_colours3.

## Flags
- `--seed (7) --flag (USA) --label --cap --capimg --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0) --motto (1.0)`.
- Physics: `--eps (0.020) --beta (100) --cb (0.06)`.
- Clock: `--ferm1 (2.0) --ferm2 (0.40) --spb2 (0.36; v1 0.30) --holdf (2.45; v1 2.75) --hsun (1.32) --hns2 (0.75)`.
- Lens: `--shend (118)`. Black hole: `--orbt (2.64; v1 2.2) --orbf (0.46; v1 0.50) --gnear (2.5)`.
- The sim is cached in two parts: `output/_cache_ol_flag_worlds_plate_<hash>.pkl` (about 5 min, 3 worlds in parallel) and `..._bh_<hash>.pkl` (about 20 s).

## Checks v1 (encoded FHD, label fhd2, seed 7; superseded by v2 below)
- **ffprobe:** h264 High, yuv420p, 1080x1920, 60 fps, 1,014 frames = 16.90 s.
- **Audio:**
  - -14.00 LUFS, peak -6.76 dBFS, last 0.5 s digital silence.
  - RMS per 5 s: -19.3 / -18.6 / -16.3 / -16.0.
  - The ff motto keeps its level; the build is levelled with a +6 dB crescendo.
- **flash_check PASS:** 0 flashes, mean luminance 0.021.
- **Seam:** mean |Δ| 0.563.
- **Sync:** all 6 landings are within ±4 ms of the largest audio energy rise.
- **SFX events per second:** 3, 4, 2, 9, 2, 9, 0, 28, 14, 75 (Sun), 19, 24, 35, 28, 11. 263 events in total.
- **Read from the mp4:**
  - a 28-frame sheet;
  - 1:1 crops of the hook (0 s), Earth (5.6), Jupiter (7.3), Sun dust (9.52), neutron film (10.66), black-hole spiral (12.3), lensed finale (15.6) and the world row (12.8).
  - The base's caption band was checked clean.
- **Bug found at 1:1:** cairo `restore()` also restores the SOURCE. A gradient set inside save/scale/restore is dropped, and the fill uses a leftover colour: the neutron glow came out as a flat grey ellipse.
  - Fix: an elliptical gradient via `pattern.set_matrix` in normal user space.
- **4K-safe:** the limb, plate and lens rasters are device-resolution surfaces painted under `identity_matrix()`. Tile textures use a pattern matrix scaled by sc.

## Delivered (v1)
- `<VIDEOS_DIR>\DopamineExe\review\ol_flag_worlds.mp4` (FHD, captioned overlay) plus `ol_flag_worlds_files\`: README, contact sheet and crops.
- No 4K yet.
- Titles: "The USA flag dropped on every world… then a black hole 🇺🇸💀" · "Same flag, same 1 m drop: Moon → Sun → black hole 🕳️" · "Which world breaks the flag? 🇺🇸" (+ `#satisfying #physics #shorts`).
- Pinned comment: "same flag, same 1 m drop onto the same steel plate, only gravity changes. the moon only cracks it, the sun turns it to dust, and the black hole doesn't even need a floor. which flag next". The brief said "barely chips it", but the sim's Moon only cracks.
- Outcome: (fill after review / analytics)

## v2 (owner review 2026-11-15, docs/REVIEW_1115.md: "fast-forwarded on the Sun and after", "at the neutron star nothing happens")
- **The lesson:** a ladder whose stages shrink with the physics (real fall times) reads as FAST-FORWARD once the aftermath is under ~1 s. The fall may be honestly fast; the aftermath must get ≥1.5 s. Buy that time with labelled slow-motion, carried in the music by holding a chord.
- **A drawn stage with no event is dead air.** v1's neutron star (flag shows, then a "FLAT" label) got "nothing happens". Every stage needs a visible process, a live number and a result.
- **Clock:**
  - Three chords are held as fermatas: beat 28 (+1.32 s, the Sun), beat 30 (+0.64 s, the neutron fall) and beat 32 (+0.75 s, the crush). After each hold, the eighths continue in tempo.
  - Notes starting inside a held half-beat simply sound longer (`tw()` warps the score).
  - SPB2 0.36, HOLD_F 2.45. The clip is 19.91 s (1,195 frames). Moon → Jupiter keep their exact times.
- **Sun slow-mo** (`SLOWMO = {4: (8, 0.90, 0.35)}`):
  - `sim_s(w, u)` maps clip time to sim time: ×1/8 for 0.9 s, then a linear rate ramp back to 1x over 0.35 s.
  - The Sun sim records every 17 steps (1.7 ms, `FINE_PER`) with a per-frame time array `ft`. `frame_at()` picks the nearest frame, and `plan()` uses `ft` for the dt.
  - Sound events from the sim go through the inverse `clip_u()`.
  - A `SLOW-MO ×8` pill sits at y 1252 (on the limb, under the plate) while the rate is below 1.
- **Neutron star** (drawn, not simulated):
  - `SLOW-MO ×1,000,000` (1 µs = 1 s) with a live "µs after release" line. Release on beat 30, hit on the beat-32 DUM: NS_FALL = 1.195 µs, so the fall shows for 1.195 s.
  - 1/2 g t² fall with speed streaks; the counter shows SPEED live, 0 → 1,673 km/s.
  - **Crush from the bottom up** (honest: the top keeps falling at 535 px/s on screen until the front arrives; NS_CRUSH = 0.6 µs = 0.60 s).
    - Rows within d0 36 px of the front bunch 0.85x and bulge 9%.
    - The film is 2 → 8 px, white-hot with a core line, cooling over 0.9 s.
    - The plate goes 22 → 5 px.
    - 260 jets slide out along the surface, plus a local elliptical glow (alpha ≤ 0.8, ramped).
  - The counter shows FLAG HEIGHT 1.00 → 0.00 m, then FLAT / ATOM-THIN. The chip appears at hit + 0.64 s.
  - **Sound:** a tink every 10 cm fallen (t = T·sqrt(d), accelerating by itself), the thunk + clack on the DUM, a grain per crushed row + a rising tink every 2 rows, and a clack on FLAT.
- **Black-hole safe zone:**
  - The spiral's x-max came from the flag's right half swinging out in the first 1.5 s, not from the late tail.
  - Moving the hole left made it worse (a bigger orbit). Moving it right helped only a little.
  - What worked: the BH flag starts 80 px left (`BH_DX`, x 108-748) and the orbit is at 0.46x circular. The max x is 906 for the whole spiral (v1: 1,031 for 1.2 s). At 0.46x it still reads as a spiral.
  - Slowing the spiral without changing its shape: scale ORB_T with the duration (2.2 × 3.42/2.85 = 2.64). Drag is re-solved by bisection (0.085/s).
- **Bug fixed:** a tile swallowed between the frame time and the clip time was drawn parked at the hole centre, stretched by its jump speed: a "+" inside the shadow. v1 had it too. Fix: `on = sw > max(tt, k/FPS)`.
- **Sim results are unchanged** (same lattice, only the recording changed): CRACKED / 2 / 35 / 361 / 2,027. BH: 3,690 of 4,000 glue bonds torn by tides.

## Checks v2 (encoded FHD, label fhd3 + caption overlay = fhd3cap)
- **ffprobe:** h264 High, yuv420p, 1080x1920, 60 fps, 1,195 frames = 19.91 s.
- **Audio:** -14.00 LUFS, peak -6.9 dBFS, last 0.5 s digital silence.
- **flash_check:** PASS, 0 flashes (mean luminance 0.022).
- **Seam:** check_loop pre-encode EXACT (0/255). Encoded last→first 0.80, vs natural 0→1 motion 4.47.
- **Sync:** landings within ±1 ms of the largest audio rise (Sun +7 ms).
- **SFX per second:** 3, 4, 2, 9, 2, 9, 0, 28, 14, 23, 86, 8, 43, 15, 33, 31, 28, 15, 1, 0 (354 events).
- **Read from the mp4:** a 28-frame sheet, plus 1:1 crops of the Sun slow-mo (9.75, 10.30), the neutron fall / crush / flat (12.40, 12.95, 13.25) and the BH spiral (15.00).

## Delivered (v2)
- `<VIDEOS_DIR>\DopamineExe\review\ol_flag_worlds.mp4` (FHD, captioned).
- `ol_flag_worlds_files\`: README, sheet, crops, `old_v1.mp4`, and `v1\` (v1 notes and crops).
- No 4K.
- Pinned comment v2: "same flag, same 1 m drop onto the same steel plate, only gravity changes. the moon only cracks it, the sun turns it to dust, a neutron star squashes it flat in a millionth of a second, and the black hole doesn't even need a floor. which flag next".
