# ol_break_earth (DopamineEXE, docs/BRIEF_shorts_1115.md D2)
- New scene. An 8-rung ladder of real or round-number impacts on one Earth, measured in DINO-KILLERS against Earth's binding energy. The twist: Theia makes the Moon. The finale: an Earth twin shatters both planets to DUST.
- Caption: post-pass overlay (`--capimg` writes a transparent PNG via the scene's own draw_caption, then one ffmpeg overlay at crf 18 with the audio copied). Text: `Each impact ~BIGGER~ than the last|What does it take to ~BREAK~ the Earth?`. Base `--cap ''`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_break_earth.mp4` (FHD, seed 1, label fhd + caption overlay, 17.58 s, 1,055 frames). No 4K yet.

## Physics (`--dry` prints it)
- E = ½ μ v² in the centre-of-mass frame (μ ≈ m for small rocks). Rock 3,000 kg/m³ unless the mass is known. 1 dino-killer = 4.2×10²³ J (Chicxulub, published 3.0-4.2×10²³ J). U = 3GM²/5R = 2.242×10³² J = **530 MILLION** (red line, frame 0).

| # | impactor | m (kg) | v | E (J) | dino-killers |
|---|---|---|---|---|---|
| 1 | Chelyabinsk, 20 m (mass from Popova et al. 2013) | 1.2e7 | 19 | 2.2e15 | 0.000000005 |
| 2 | Tunguska, 60 m | 3.4e8 | 15 | 3.8e16 | 0.00000009 |
| 3 | Chicxulub, 11 km (10-15 km published) | 2.1e15 | 20 | 4.2e23 | 1 |
| 4 | 100 km rock | 1.6e18 | 20 | 3.1e26 | 750 |
| 5 | 500 km rock (ocean-vaporising size, Sleep et al. 1989) | 2.0e20 | 20 | 3.9e28 | 94,000 |
| 6 | Ceres-sized, 940 km (Ceres mass) | 9.39e20 | 20 | 1.9e29 | 450,000 |
| 7 | Theia, 6,780 km (Mars mass) | 6.42e23 | 10 | 2.9e31 | 69 MILLION |
| 8 | Earth twin | 5.97e24 | 32 | 1.5e33 | 3.6 BILLION |

- **Twin speed check, Leinhardt & Stewart (2012).** Inputs: Q*_RD = c* (4/5) π ρ1 G R_C1², with c* 1.9 and ρ1 1 g/cc. Equal masses, head-on: Q_R = v²/8. That gives Q*_RD 6.4e7 J/kg.
  - At 22.6 km/s the largest remnant is half the mass (1.8 billion dino-killers).
  - At 30.4 km/s the hit is super-catastrophic: largest remnant ≤ 10 %, 3.3 billion dino-killers.
  - Ours, 32 km/s: Q_R/Q* = 2.0, so DUST is honest.
- **Theia check (γ 0.107):** Q_R/Q'*_RD ≈ 0.04, far below disruption. That matches "STILL NOT BROKEN".
- **Binding energy vs. a collision:** U is the minimum energy; a collision wastes most of its energy as heat. Never claim "530 million breaks it".

## Clock = the score
- Holst, Mars, score beats 160-210 (bars 33-42), one 5/4 bar per rung.
- Bar lengths: 1.78, 1.71, 1.64, 1.57, 1.50, 1.45 s, then 1.45 s.
- Impacts land on bar downbeats: 0.18, 1.96, 3.67, 5.31, 6.88, 8.38 s.
- Theia lands at 9.83 s (beat 190, the bass drum entry). The twin lands at 12.73 s (beat 200, the C tutti).
- Cadence 15.63 s (beat 210, our open-C tutti). Hold 1.35 s, then a 0.6 s dissolve to frame 0.
- Rocks approach for 0.34-0.55 s before their hit. Theia approaches for 0.62 s during the zoom-out (R 300 → 115 px, 9.12-9.68 s). The twin approaches for 0.46 s.

## Look
- **Earth:** a per-pixel numpy sphere in DEVICE px, blitted under `identity_matrix` (4K-safe).
  - Texture: 2048×1024 equirect, hand-coded coarse continents (lon/lat polygons), fbm coasts, biomes, ice and banded clouds. Lit from the upper left, with a soft terminator, an ocean glint and an atmosphere rim. Cached in `output/_cache_ol_break_earth_tex_*.npz`.
  - The view is centred at 20° N. Each real site turns to the upper left before its hit.
- **Surface effects** are functions of the angular distance from the site, fading out before the next rock arrives (each hit is its own test):
  - crater + haze (3);
  - firestorm tint + flicker (4);
  - steam on the oceans + a white limb (5);
  - Voronoi magma cracks (6, Theia).
- **Theia:** clipped outside the Earth so it sinks in. 1,500 debris particles are sprayed onto a tilted disc (y × 0.26, Kepler-shaped sped-up periods). 24 % fall back, 60 % gather into the Moon (r 0.273 R_E at 3.05 R_E, just outside the Roche limit) between 1.05 and 2.15 s, and 16 % fade.
- **Twin:** both rasters are split into 156 Voronoi chunks, denser near the contact.
  - Cracks race out at 5.5 R/s. Chunks fly out (wider sideways than along the impact axis), then crumble to device-pixel grains at 0.1-1.3 s, brightened and twinkling.
  - The expansion brakes as s(a) = 1.25(1 − e^(−a/1.25)) + 0.06a.
  - The camera eases the centre of mass to the frame centre. The Moon fades into the dust.
- **Glows:** all local, ≤ 2.4 R_small (≤ 12 % of the frame), each ramping up over ≥ 0.15 s.
- **HUD:**
  - LOG meter x 872, y 1170 → 440 (10⁻⁹ → 10¹⁰), with the red line and its label from frame 0.
  - Name chip at y 1376, sub-line (size · speed · J) at y 1428, counter (log-roll 0.32 s) at y 1518, DINO-KILLERS at y 1560.
  - Stamp at y 1305; watermark at y 1222.

## Sound
- **Music:** Gustav Holst, The Planets Op. 32, "Mars, the Bringer of War" (1914-16; published 1921 by Goodwin & Tabb; Holst d. 1934; PD in the US and life+70). Score beats 160-210 (bars 33-42).
  - **SOURCE:** the notes come from `lib/scores/holst_mars.json`, extracted from the Sao Mai MusicXML (`<SOUNDFONTS_DIR>\scores\holst_mars\saomai_musicxml\`). The engraving licence is unstated; only the pitches and rhythms of the PD work are used, as in the 1921 full score (IMSLP #1014402), the same as boss_fight. Caveat as in docs/orchestra.md.
- **Arrangement:** our own, in lib/orchestra (after orchestra_pieces.holst_mars). Dynamics ramp 0.55 → 1.0 to the twin. The cadence is an open-C tutti (strings, horns, trombones, tuba, oohs, timpani C, boom, harp) after a timpani roll. No cymbal or noise riser.
- **SFX (×0.55):**
  - tonal booms on G (C for the twin), soft thumps plus glass tinks for the airbursts, and stone-bar cracks;
  - debris clinks locked to the 5/4 ostinato (0-6 per hit, rising per rung), plus ejecta landings;
  - a rising sine-blip shimmer (oceans) and a crack run (crust);
  - jet clinks plus a rising chime cluster as the Moon gathers;
  - a crack burst (the shatter), a clink per crumbling chunk, and soft tonal sand grains (no hiss).
- **Mastering:** `level_bed` (crescendo 5 dB, +3 dB after the twin), `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence.

## Checks (encoded FHD, captioned)
- h264 High yuv420p 1080x1920 @60, 1,055 frames, 17.58 s.
- -14.00 LUFS, peak -5.68 dBFS, last 0.5 s at -240 dBFS. RMS per 5 s: -19.4 / -15.6 / -15.1 / -14.7.
- flash_check PASS (0 flashes, mean lum 0.013). Seam 0.343.
- SFX events per 5 s: 61 / 242 / 375. Impact booms are within ±15 ms of the onsets in the muxed audio.
- 1:1 crops at 3.95, 8.65, 10.15, 13.0 and 13.6 s. The base caption band is clean (max luma 121, the stars).
- Render time: FHD 3.1 min, -Fast 1 min.

## Doubts
- The late dust (14.5-17 s) is dim: the planets' own colours, mostly night side and ocean. Brighter dust = `gb` in draw_shatter.
- The rungs are fast: 1.45-1.8 s each, with the stamp on screen for ~0.8-1.2 s.
- The continents are coarse polygons: they read as Earth, not as a map.

## Flags
`--seed (1) --label --cap --capimg --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --hold (1.35)`.
