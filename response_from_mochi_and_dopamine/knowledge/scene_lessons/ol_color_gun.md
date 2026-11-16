# ol_color_gun (DopamineEXE)
- New scene, character-free. Brief: `docs/BRIEF_dopa_colorgun.md` §A (owner decisions 2026-11-11: end state ALL GOLD COINS, US "COLOR", no characters, meter = glyphs/swatches only).
- Caption (post-pass, `--caption-pass`): `Every shot = a new ^COLOR^ or more ~SIDES~|until it's ALL `GOLD` COINS` (`^` current hue, `~` white ×1.10, backtick = gold). Base renders with `--cap ''`.
- Test delivery: `<VIDEOS_DIR>\DopamineExe\review\colorgun\` (FHD, seed 3). No 4K yet.

## World (logical 1080x1920)
- Tank x 130-885, y 490-1258, white 2.5 px 85%. 800 pieces: jittered hex lattice 25 × 32 (pitch 29.5 × 23.7, jitter ±3 px), seeded rotations.
- Colour ladder #4050FF → #AF40FF → #FF40EF → #FF7040 → #FF9F40 → #FFD940 (rel. luminance 0.14, 0.20, 0.31, 0.33, 0.46, 0.71: one-way brightening). Sides ladder 3, 4, 5, 6, 8, circle; circumradius 13.8 / 13.0 / 12.6 / 12.3 / 12.1 / 12.0.
- Gold + circle = a COIN (dark-gold rim + inner ring + highlight).
- Guns: hubs (290, 444) / (790, 444), bodies 90 × 60 ABOVE the rim, barrel 44 px (tip at the rim, never over the pieces). The hub window shows the NEXT ammo (hue disc / white glyph; a coin from 11.2 s). Labels COLOR / SHAPE ABOVE the bodies (the brief said under; under would sit on the rim).
- HUD: 8 chips (swatch / glyph, firing order) at y 1300 + gold-coin goal chip at x 862; progress line y 1340 = CHANGES / 8,000; counter y 1468 + ×N pill (latest colour); watermark (880 right, 1364).

## Mechanic
- Shots (fire): C1 −1.62 (lands −1.40), S1 −0.55 (lands −0.30), C2 1.70 ×2, S2 3.90 ×2, C3 5.85 ×4, S3 7.60 ×4, C4 9.15 ×8, S4 10.50 ×8, barrage 11.70-11.82 16 + 16 = ×32.
- Landing points: farthest-point sampling (best of 40) among pieces already at the previous rung of that ladder; C1 (395, 885) left of centre, S1 (440, 850) inside it. Finale points = k-means 16 per ladder; each gun sweeps its 16 in angle order.
- **Front schedule (the rate gate):** constant-speed fronts give a CHANGES/s curve that falls 43% between shots (a disc's rate drops once it hits the walls). Fix: every wave spreads over 4 shot intervals (`SPAN_K`) with coverage rate ∝ u^0.7 (1−u) (`BUMP_A/B`); its first 45 px run at 110 px/s (`R_YOUNG`, `V_MIN`) so each landing visibly pops. Fronts stay circles (a common radius-vs-time per wave). Overlapping bumps sum to a curve that only climbs.
- Finale fronts: constant speed solved so the last flip = `--tgold` (12.4 s → 424 px/s). 12.2 s (the brief) needs ~1,030 px/s: too fast to read as a wave.
- Catch-up: rung k plays when the earliest front of rung ≥ k arrives; a skipped rung is a 0.06 s step (~980 steps, all counted). 800 × 10 = 8,000 exact.
- Flips: colour crossfade 0.10 s; shape = 120-sample vertex morph 0.14 s + 60° spin + 1 → 1.22 → 1 pulse; shockwave 3 px push from the front's source, spring τ 0.2 s; rim highlight 30% white for 2 frames on the flipped piece only; front ring 1 px 20% white clipped to its (arrival-weighted) Voronoi cell.
- Payoff: glint sweep 12.4-12.9; coin Y-axis flip ripple from the centre (start 12.92 → 13.67, 0.42 s each); twinkles (10% of coins) to 14.3; dissolve 14.4 → 15.0 into frame 0. 900 frames.

## Rate gate (`--dry`, seed 3)
- CHANGES/s (1 s window): 0 s 131, 1 s 239, 2 s 308, 3 s 382, 4 s 413, 5 s 432, 6 s 450, 7 s 467, 8 s 494, 9 s 535, 10 s 614, 11 s 632, barrage ~2,850. Max fall vs running max before ALL GOLD 6.7% (gate 15%). PASS.
- The brief's ≥ 1,500/s by 11 s is impossible on this budget: 1,600 changes (C5 + S5) must happen in the finale, so at most 6,400 fit before 11.8 s (a linear climb from 200/s tops out ~870/s). Measured 632/s at 11 s.
- CHANGES at frame 0: 83 (brief ≈ 108).

## Sound
- Melody: Grieg, In the Hall of the Mountain King (1875, PD), Mutopia 1888 MIDI (`<SOUNDFONTS_DIR>\scores\grieg_mountain_king\`), NOT the bank entry. One 2-bar phrase per shot interval, the shot on the downbeat: bars 21-22, 23-24, 25-26, 27-28, 29-30, 31-32, 47-48 (beats 84 … 124, 188). Eighths 7/s → 13/s (the piece's accelerando). Barrage = grace G# A A# into the hammered D/B chord; ALL GOLD = rolled B-minor tutti (`--fin` 2.5).
- Orchestration builds per phrase: pizz (+octave to ≥ B3) + bassoon → + clarinet → + strings + piano → + horns on the bass → + brass; contrabass + pizz bass; timpani on downbeats from C2, every beat in the last phrase; a roll 11.2-11.7, another + string tremolo 11.82 → ALL GOLD (fills the hole before the chord).
- SFX: glass tik per flip (partials 1 / 2.32, < 5.5 kHz), pitch = the current bass chord's tones rising with the front's radius (S ladder an octave lower), ≤ 40/s (25 ms gap), panned by x, nudged +12 ms off melody notes, gain ≥ 0.32 in the barrage. COLOR gun = soft thoomp (sine 130 → 55 Hz + 500 Hz puff), SHAPE gun = wooden clack; barrage = 10-hit alternating roll. Coin ripple: chings (< 7.5 kHz, LP 8 kHz) ~25/s + harp / celesta B-minor cascade. Glint: glass tings.
- `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.42; last 0.55 s digital silence.
- `--regen-audio <mp4>` rebuilds the soundtrack onto an existing render.

## Flags
`--seed 3 --label --cap --still --frame a,b --dry --sound 0 --sfx 0.42 --fin 2.5 --tgold 12.4 --c1 -1.4 --s1 -0.3 --vmin 110 --ryoung 45 --caption-pass <base> --out <file> --regen-audio <mp4>`.

## Lessons
- Constant-speed circular fronts in a box can't hold a rising change rate across overlapping waves; schedule coverage per wave (a smooth bump over several intervals) and keep the radius common per wave so it still reads as a front.
- A pure bump starts too slowly to see the landing: give the young front a fixed speed first.
- Coins must flip about the screen Y axis: reset the piece's random rotation once it is a circle.
- Dense 800-piece texture: the post-encode seam mean delta reads ~1.2-1.7 at 540p from H.264 noise alone, though the pre-encode seam is EXACT (check_loop 0/255). Judge the seam pre-encode.

## Checks (encoded Full HD, label fhd2, seed 3)
- h264 yuv420p 1080x1920, 60 fps, 900 frames, 15.00 s. Encoder forces a keyframe on the last frame (`-force_key_frames expr:eq(n,899)`): the base seam mean delta drops 0.98 → **0.65**; captioned (2nd generation) 0.87. Pre-encode seam EXACT (check_loop 0/255).
- Audio (muxed): **−13.98 LUFS**, peak −4.7 dBFS, last 0.5 s digital silence, > 6 kHz 0.10%. RMS/s −20.7 → −14.5 (11 s); ALL GOLD 12.5 s −14.5 (the 12.0-12.25 s window −17.7, a short breath before the chord after the roll + tremolo fill).
- 112/112 melody notes, all 7 gun shots and ALL GOLD within 25 ms of a measured onset. Sidecar: 500 pitched events, 33 distinct, top 15%.
- **flash_check PASS**: 1 flash, worst 1/s (13.65 s, the coin ripple).
- Frames read from the encoded mp4: contact sheet every 0.5 s, key frames 0 / 2 / 6 / 7.75 / 10 / 11.5 / 12.4 / 13.33 s, 1:1 crops at 2.0 s (C2 landing), 4.17 s (S2 landing), 10 s (busiest) and 11.87 s (barrage slugs in flight).

## Doubts (for the owner)
- The shape waves are subtle from afar: pentagon / hexagon / octagon at r ≈ 12 look alike on a phone. The colour waves carry the read.
- Orange (C4) vs coral (C3) is a small step: it's the brief's ladder.

## v2 (`scenes/ol_color_gun2.py`, coordinator review 2026-11-11; v1 file untouched)
- Why: at 800 pieces (r ≈ 12) pentagon/hexagon/octagon blurred on a phone; indigo → violet and coral ↔ orange were too close; the coin-flip ripple read as a black bullseye; frame 0's front was weak.
- 396 pieces (18 × 22, pitch 40.6 × 34.5, lattice x 152-863 / y 512-1236), circumradius 20.5 / 19.2 / 18.6 / 18.3 / 17.6. `NR = 4` rungs per ladder.
- Colours #3D4BFF → #D83CE6 → #FF5038 → #FF9420 → #FFD940 (rel. luminance 0.132, 0.235, 0.273, 0.425, 0.713: still one-way brightening; hues 236° → 294° → 8° → 31° → 48°). Sides 3 → 4 → 5 → 6 → circle (`--sides`; octagon dropped, it read as the circle).
- Shots: C1 lands −2.60 (frame 0 = a 94-piece magenta disc, crisp edge, moving), S1 −0.50, C2 1.90 ×2, S2 4.20 ×2, C3 6.30 ×4, S3 8.20 ×4, barrage 9.90-10.02 8 + 8 = ×16; ALL GOLD 10.60 (final fronts 616 px/s). CHANGES 396 × 8 = 3,168.
- Payoff: glint 10.6-11.1, then a bright slow shimmer sweep corner to corner (each coin +38% toward white once, 0.45 s, over 1.0 s), twinkles, dissolve 12.8 → 13.4. 804 frames. No dark ripple.
- Front ring 30% white, 1.6 px. Music phrases bars 21-22, 23-24, 25-26, 29-30, 47-48. Barrage tiks ≥ 0.45 gain, roll ×0.55 (no hole before the chord).
- Checks (encoded FHD, label fhd1): h264 yuv420p 1080x1920 60 fps 804 frames 13.40 s; −13.98 LUFS, peak −5.5, tail silent; 77/78 notes + all guns + ALL GOLD on onsets (≤ 25 ms); flash_check PASS (1 flash, worst 1/s); seam pre-encode EXACT, encoded 0.57 base / 0.77 captioned; CHANGES/s max fall 5.9% (74 → 259/s → ~1,300 barrage).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\colorgun\ol_color_gun_v2.mp4` (+ base, sheets, 1:1 crops). README says watch v2.

## v3 (`scenes/ol_color_gun3.py`, overnight 2026-11-12, brief docs/BRIEF_overnight_1112.md §1; v1/v2 untouched)
- Owner on v2: never shape AND colour at once; faster; more objects; a hit = a shockwave through the whole field, COLOUR then SHAPE alternating; first hit + wave by ~1 s; distinct hues; shapes must read.
- 572 pieces (22 x 26). Waves C S C S C S C, hits x1 x1 x2 x2 x4 x4 then a x8 gold barrage. Per piece the changes follow the wave order, >= 0.10 s apart (`GAP`; a faster wave bends behind the slower one).
- Colours #3D4BFF → #D83CE6 → #FF4A3A → #26E0FF → #FFD940 (rel. luminance 0.13 / 0.24 / 0.27 / 0.61 / 0.71, monotone). Shapes triangle → square → star → circle (radial-function morph from vertex lists).
- Each wave: young front 330 px/s for 70 px, then a coverage bump over 1.45 fire intervals. Shockwave = ring (colour or white) + 0.12 s brighten + scale pop (shape 1.42) + 6 px outward kick.
- Fires C1 lands −0.40 (frame 0 = a magenta disc), S1 1.00, C2 2.85, S2 4.55, C3 6.05, S3 7.35, barrage 8.50; ALL GOLD 9.45; dissolve 11.45 → 12.05.
- Music: Mountain King phrases bars 21-32 (beats 84-124), one per wave.
- Checks (FHD): 12.05 s, −13.99 LUFS, peak −5.4, flash PASS (1), seam 0.65 base. Changes/s 191 → 354 → 408 → 828; max fall 16% (1.9 s).
- Lesson: the shape waves need their own pop (bigger scale + white glint + thicker ring), or they vanish next to the hue waves.

## v4 (`scenes/ol_color_gun4.py`, 2026-11-12b, brief docs/BRIEF_1112b.md §1; v1-v3 untouched)
- Owner on v3: "why are u ignoring my request". The shape gun fired while the colour wave was still spreading. Rule: STRICTLY sequential waves, never two alive at once.
- 13 waves, one hit each, C/S alternating. `simulate()` asserts:
  - each shot fires 0.10-0.21 s after the previous wave's LAST change;
  - its first change comes after that;
  - DUR shrinks every wave.
- Timeline is pure (`timeline()`, module level):
  - sweep DUR 0.80 → 0.34 s, geometric;
  - gap 0.16 → 0.10 s;
  - slug flight is a fixed schedule, 0.14 → 0.09 s, so fire-to-fire shrinks monotonically. With distance-based flight it did not.
- Colours: silver → red → orange → yellow → green → blue → purple → gold (#FFB51F, deeper than yellow #F4EE3A).
- Shapes: tri → square → star → plus → diamond → heart → circle. Diamond, heart and circle are drawn upright (ROTF = 0).
- Lesson: a 4-point sparkle reads as a 5-point star at pile size, so it was replaced by an upright card-suit diamond.
- Checks (FHD): 12.20 s, −14.0 LUFS, TP −4.3; flash PASS (2, worst 1/s); seam exact pre-encode, 0.94 base / 1.18 captioned. Per-cycle CHANGES/s 520 → 1,023, gold 1,331.
