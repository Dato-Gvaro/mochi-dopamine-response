# ol_earth_drill (Dopamine.exe)
- Character-free scene (docs/BRIEF_batch51.md): drilling from the grass to the centre of the Earth through the real layers (real units, big labelled landmarks, one continuous camera move).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_earth_drill.mp4` (**v2**, Full HD, label v2fhd, 17.20 s, 1,032 frames). No 4K yet.
- Caption (baked, `--cap`; `--cap ''` = base): `^3 drills^ race to the ~CENTER~ of the Earth|Which one makes it?` (`^x^` = orange, `~x~` = gold).

## History
- **v1 (2026-10-25):** one drill, Mussorgsky "The Great Gate of Kiev" bars 105-114, 16.60 s.
  - Owner: "I don't know what's going on here."
  - The owner had removed Kiev before (siege_duel).
- **v2 (2026-10-27, the owner's idea):** a RACE.
  - Three drill heads side by side; two break on the way and one reaches the centre.
  - The early leader breaks first; the drill that starts last wins.
  - An easter-egg burrowing ship (our own design) near the core.
  - New music.
  - The v1 file is not kept in the repo (it was never approved).

## The race (v2)
- Lanes (x): STEEL TWIST 250 (blue-grey), PLASMA HEAD 508 (violet), DIAMOND CORE 766 (cyan). The winner is in the middle lane, so it reaches the centre of the concentric shells.
- **Positions.** Each drill = the winner's track s_ref(t) + lead(t) (story px).
  - STEEL: +40 → +210 px by 4.2 s.
  - DIAMOND: +20 → +130 by 5 s, then falls to +60 by its break (PLASMA closes in).
  - PLASMA: 0 (the camera reference).
  - Frame 0: 26 m / 15 m / 18 m.
- **Leaders:** STEEL from 0 s, DIAMOND from 5.00 s, PLASMA from 12.15 s. Every counter strictly increases while its drill is alive.
- **STEEL TWIST breaks at 5.00 s** (beat 14 = MIDI 1248, a syncopated tutti chord), at 392 km and 1,612 °C (steel melts ~1,450 °C).
  - It shakes harder and glows over the last 0.7 s.
  - Then: a jagged pipe stub, the bit tumbling down and melting away (1.3 s), a 34-spark burst, a red "BROKE AT 392 km" tag under the stub, and a red frozen HUD counter "BROKE · 1,612 °C" with a pop.
  - A metallic crunch (inharmonic snap pitched to the bass plus dull low-passed grains).
- **DIAMOND CORE breaks at 12.14 s** (beat 34 = MIDI 1268, the hammering D-A tutti), in the liquid outer core at 3,963 km and 4,617 °C.
  - The crown glows orange first, then cyan shards spray and the body sinks.
  - Red tag "BROKE AT 3,963 km"; crunch plus a fall of glassy D-major tinkles.
- **PLASMA HEAD reaches the CENTER at 15.00 s** (beat 42 = the concerto's final D-major chord).
  - The camera eases (Hermite, 0.544 s, speed falls monotonically) so the centre ends at y 880.
  - Its column turns gold: "6,371 km / CENTER REACHED".
  - Calm gold swell (alpha ≤ 0.42), two amber rings, gold sparks, "THE CENTER" pill.
  - Hold 1.6 s, then a 0.6 s dissolve into the pre-roll; the HUD swaps rather than double-exposing.
- **Easter egg:** our own segmented burrowing ship.
  - Design: three rounded teal hull segments with warm portholes, a gold spiral drill nose and tail fins (no film design, names or logos).
  - It drifts right → left just above the core-mantle boundary, 8.75-10.75 s, on screen ~9.0-10.3 s. Pill: "anyone home?".
  - Owner (2026-11-03): never mention or hint at the ship in pins, titles or replies; viewers discover it.

## World
- Story coordinate s (px, down); the winner's tip at screen y 740. Scroll v = 230 → 640 px/s (linear ramp, only climbs).
- **Log-ish depth.** d(s) is the smoothed (14-px Gaussian) integral of a per-segment m/px step function, solved so the winner crosses each landmark on a beat:
  - mines 3.9 km at 1.79 s;
  - Kola 12,262 m at 3.21 s;
  - Moho 35 km at 4.29 s;
  - 660 km at 6.43 s;
  - core-mantle boundary 2,891 km at 10.00 s (the hammer tutti);
  - inner core 5,150 km at 14.46 s;
  - centre at 15.00 s.
- Shells are concentric circles about the centre (warped radii); the inner core is a calm gold sphere of radius 339 px.
- The outer core and inner core were darkened from v1 (owner dislikes over-bright end frames). Mean luma of the 15.0 s frame is 65/255.
- **Layer header:** ONE label, centred on a dark pill at y 452: the layer the winner's bit is in, cross-fading over 0.2 s at each boundary. Boundaries carry left depth tags (35 / 660 / 2,891 / 5,150 km).
- Shared landmarks:
  - the deepest cave (2.2 km, between the middle and right lanes);
  - the deepest mines (3.9 km, a lit tunnel across all lanes with ore carts);
  - Kola: a gold dashed line across all lanes, "HUMANS STOPPED HERE", "Kola Superdeep Borehole · 12.2 km";
  - grass and a derrick per lane at the surface.
- **The drills:**
  - STEEL TWIST: a twist drill with travelling helical flutes and a 118° point.
  - DIAMOND CORE: a steel tube, cyan bands and a twinkling diamond-studded crown.
  - PLASMA HEAD: a ceramic heat-shield capsule with a violet ring and a short violet-pink jet; the rock at its tip glows.
  - Pipes carry tool joints in each drill's colour. The bits heat with temperature (steel → red → orange → gold) and buzz ±1.2 px.
  - Chips: 6 / 4 / 3 per tick; rock-coloured in the crust, embers in the mantle, molten droplets from the plasma.
- **HUD:**
  - three thin meter tracks (one per drill, drill colour, a red ✕ where a drill broke), ticks for mantle and core, and a gold "CENTER" glyph from frame 0;
  - per-lane columns at y 1420: name, depth (m → km), and the temperature, or "BROKE · °C" in red, or "CENTER REACHED" in gold;
  - watermark at y 1262.

## Sound
- **Music:** P. I. Tchaikovsky, Violin Concerto in D major Op. 35, III. Finale, the coda (1878; Tchaikovsky d. 1893, PD).
  - Source: full score, Mutopia #466 (Eulenburg 1920, licence Public Domain), `tchai_op35-2.mid`, saved at `<SOUNDFONTS_DIR>\scores\tchaikovsky_violin_concerto\` + `SOURCE_mutopia_466.txt`.
  - Excerpt: MIDI quarters 1234-1276 at one steady tempo (quarter = 168): the D-A tutti with scale fills, the syncopated chords, the falling/rising runs, the hammering D-A tutti, the final D-major chord (held by us).
  - Not on any used or banned list (Tchaikovsky's Piano Concerto 1 is used; this concerto is not).
- Arrangement (lib/orchestra), all 14 score parts: flute, oboe, clarinet, bassoon, 2 horns, trumpet, timpani, solo violin, strings I/II, viola, cello, contrabass (8vb). The cadence chord: strings, horns, trumpets, trombones, violin, cello/contrabass, timpani, boom. `level_bed` crescendo 5 dB, finale +3 dB.
- SFX (×0.40): the ticks are on the music grid, each owned by the next live drill in turn. Eighths to beat 16, then three per beat, then sixteenths from beat 28, so the rate climbs and the survivors take over the broken drills' ticks.
  - Per-drill tonal timbres, pitched to the bass of the moment (D/A):
    - steel: a metallic grind tick with an in-key rasp;
    - diamond: a glassy stone tick;
    - plasma: a warm "thoom" pulse.
  - Also: clinks between ticks (D pentatonic), layer thunks, 2 break crunches, 3 deep thunks on the centre.
- `audio.master(peak_db=None, reverb=0.5)`; last 0.6 s digital silence.

## Checks (encoded Full HD, v2)
- h264 yuv420p 1080x1920, 60 fps, 1,032 frames, 17.20 s.
- flash_check PASS (1 flash = the end dissolve; worst 1 s = 1; mean lum 0.074).
- −14.01 LUFS (muxed), peak −5.81 dBFS, last 0.5 s digital silence; energy above 5 kHz 0.11%.
- RMS per second: −17.7, −17.2, −17.5, −16.9, −17.1, −15.9, −16.5, −16.9, −17.2, −18.0, −15.4, −15.6, −14.7, −15.2, −15.3, −14.2 (cadence), −25.0, silent.
- Ticks per second: 6, 6, 5, 6, 5, 7, 8, 8, 9, 8, 12, 11, 11, 11, 11. SFX events per second: 6, 10, 8, 11, 11, 13, 12, 13, 13, 13, 13, 11, 13, 11, 12.
- Seam 1031→0: mean delta 3.67 vs normal steps 3.36-3.58.
- Frames read from the mp4 at 0, 0.5, 2, 5.0 and 5.4 (steel break), 9.6 (ship), 12.14 and 12.6 (diamond break), 15.0, 15.8 and 17.18 s (last frame = pre-roll).

## Doubts
- The depth scale is log-ish (warped): the bands are not to scale; the counters, tags and labels carry the real numbers.
- PLASMA HEAD is a real research idea (plasma / spallation drilling) stretched to fiction.
- The diamond's "melts ~4,000 °C+" is order-of-magnitude (high-pressure diamond).
- Every leader breaks (steel, then diamond), so the winner is the one that started last. The lead change happens at the diamond's break.
- Temperatures are rounded textbook values.

## Flags
`--label --cap --still --frame a,b --dry --sound 0 --sfx (0.40) --fin (2.0) --qpm (168) --hold (1.6) --smooth (14)`.

## Shipped (4K, 2026-10-28, batch53)
- Owner: "let's try; make the pinned comment a reference/guess about the ship from the movie" → 4K ship. `NF_SCALE=2.0 python scenes/ol_earth_drill.py --label ship` (defaults = v2).
- Encoded: h264 yuv420p 2160x3840 @ 60 fps, 1032 frames = 17.20 s. −14.01 LUFS, peak −5.81 dBFS, last 0.5 s silent. flash_check PASS (1 flash = the end dissolve, worst 1 s = 1, mean lum 0.074). Seam mean |Δ| 3.49 (the camera moves every frame; normal steps ~3.4, as in FHD).
- Frames read from the 4K mp4: 0.5 s, 9.6 s (the ship + "anyone home?"), 15.8 s (CENTER REACHED).
- Staged: `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-03\1_ol_earth_drill.mp4` (04:00 local Nov 4 = 19:00 US East Nov 3). FHD review copy → `DopamineExe\archive\ol_earth_drill_fhd.mp4`.
- New pinned comment (guess-the-reference, the film is never named): "did anyone else spot the tiny ship near the core 👀 what movie is that from".
