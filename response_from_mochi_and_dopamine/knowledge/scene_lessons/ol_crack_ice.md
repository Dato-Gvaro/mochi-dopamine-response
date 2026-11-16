# ol_crack_ice (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). Skeleton: ×2 growth toward a named end state (research/early_breakouts.md). A frozen sheet is struck; every crack splits in 2 until the ice SHATTERS into rainbow-edged shards.
- Caption (baked, `--cap`; `--cap ''` = base): `Every crack ^SPLITS^ in 2|until the ice ^SHATTERS^`. Highlights in the current generation hue.
- Delivered: `<VIDEOS_DIR>\channel2\ol_crack_ice.mp4` (**v4**, Full HD, seed 7, label fhdv4, 10.90 s). Watermark "DOPAMINE.EXE" (channel renamed 2026-10-22). No 4K yet.
- Owner review of v1 (2026-10-21): "start with an empty clear view but faster cracking, to get some effect within 2 seconds and then you can go slower maybe; now it progresses very slow within 2 seconds" → v2 (clear frame 0 + burst opening).
- Owner review of v2 (2026-10-22): "looks better, but maybe nicer with less colours … a little dopamine push, some eye-candy, not too overwhelming or too colourful" → **v3 = v2 recoloured** per the BRIEF_channel2 "Colour rule" (sim, clock, opening, Chopin walk and SHATTER unchanged).

- Owner review of v3 (2026-10-22): "the first 2 seconds are ok, but at 3 or 4 seconds it goes very slow and gets boring" → **v4**: no post-burst slowdown (tips never below the burst's final 40 px/s, fork rate never drops and climbs into SHATTER at 8.2 s), a finer shard size (more forks to climb through), denser notes. Opening, colour, SHATTER and music otherwise as v3.

## v4 clock and timeline (current)
- Sim: `--ashard 1800 --afloor 400` (v3: 2,600 / 600): 2,596 cracks, 2,603 forks (26 branches), SHATTER tick 671.
- Burst 0.05 → 1.9 s as v2/v3 (461 → 40 px/s). Build: the fork rate starts at the burst's final rate RA = ρ(320)·40 and follows max(RA·e^((t−1.9)/τ), the highest rate reached so far), with τ solved for SHATTER at 8.2 s; the tip speed is never below 40 px/s (it holds 40 to ~6 s, then 45 → 85 → 170 px/s into SHATTER).
- **Forks per second: 92, 174, 194, 320, 359, 431, 441, 490, then ~510/s (8-8.2 s).**
- Cracks: 156 (1 s), 398 (2 s), 657 (3 s), 989 (4 s), 1,749 (6 s), 2,596. Meter 7% (2 s), 27% (4 s), 60% (6 s), 96% (8 s), 100% at **SHATTER 8.20 s**.
- ×2 pops: 0.27, 0.55, 0.77, 1.05, 1.53, 2.02, 3.07, 3.70, 4.83, 5.77, 6.32, 7.00, 7.38, 7.72, 7.88 s (GEN 0 → 16).
- Hold 2.1 s → 0.6 s dissolve into the clear ice. **10.90 s, 654 frames.**
- Notes: the build's gap shrinks only 35% and the burst uses the same gap (`--gb 1.0 --ga 0.35`): 11, 13, 13, 15, 15, 17, 18, 19 notes/s; the C-major cadence still lands on SHATTER.
- Checks (encoded FHD): h264 yuv420p 60 fps; flash_check PASS (0 flashes, mean lum 0.016); −14.01 LUFS, peak −4.64 dBFS, last 0.5 s digital silence; late body −16.5 dB RMS, SHATTER −13.9 (+2.6 dB); seam 0.211. Frames read from the mp4 at 0, 1, 2, 3, 4, 6, 8.18 s (98%), 8.67 s and the last frame; 1:1 crops at 4 s and 8.18 s.
- The sections below describe v2/v3 where they differ (clock, timeline, counts).

## Colour (v3)
- Cracks are coloured by **distance from the impact**: one radial gradient (a cairo RadialGradient centred on the impact, radius = R + |impact − centre|) used as the stroke source, so the web reads as calm concentric bands. Ramp (5 hues): white-cyan (h .52, S .25) → aqua (.49, .70) → blue (.58, .72) → violet (.73, .62) → soft pink (.88, .55) at the far rim, all V 1. Core = ramp 25% toward white; underlay = ramp at alpha .15-.20 (ADD). Running tips and fork glints take the ramp colour at their position.
- Shards at SHATTER are cut from the drawn sheet, so they keep their crack-edge gradient: the finale is the same calm gradient breaking apart.
- **One warm accent, gold** (1.00, .80, .35 / .92 highlight): the impact glow + ripple, the ×2 badge, the SHATTER goal mark + label, and the SHATTER release rings.
- HUD: caption highlights and the "GEN N" label take the crack-front colour (the ramp at the smoothed mean distance of the cracks born in the last 0.5 s: cyan in the burst → blue/violet in the build). Meter fill = the same ramp.
- v2 coloured by generation (hue = 0.10·gen, S .85: a full rainbow), with rainbow SHATTER rings and an ice-white goal mark.

## World (logical 1080x1920)
- Ice: one disc, centre (508, 800), R 392 (x 116-900, inside 0.10-0.84 w; y 408-1192). Glossy dark translucent blue-black: radial gradient with a fresnel-bright edge, 260 faint frost strokes, 26 static frost glints, a soft specular sheen upper left, two diagonal sheen bands and bright inner-rim glints. Thin white rim 2.5 px, 85%.
- Impact (from 0.05 s): a pit (gold glow hugging it, 26 → 42 px kick decaying τ 0.18 s, 14 hairline rays) and two thin ice-white ripple rings (ADD, out to ~140 px, 0.5 s). It stays local: no large-area flash.
- Cracks: jagged polylines (4 px steps, heading wander σ 0.11 rad with a 0.15 pull back to the base heading). Colour: see "Colour (v3)". Drawn as a soft ADD underlay (width 2.6·core + 3, alpha .15-.20) under a crisp OVER core (3.4 px × 0.87^gen, ≥ 1.2 px; colour 30% toward white). No glow discs; running tips are 1.9 px points, the newest 50 forks get a small 4-ray glint (0.2 s).
- HUD (same look as ol_spiral_center): meter y 1252 (x 170-846, rainbow fill, white marker, ice-shard SHATTER goal mark + label from frame 0, "N% CRACKED" above it); counter y 1478 "N" + "CRACKS" + a "×2" pill in the current hue with "GEN N" above it, popping (×1.3, τ 0.1 s) each time the generation front (the mean generation of the cracks born in the last 0.5 s, running max) steps up; watermark "OVERFLOW LAB" (900 right, 1338), 35%.

## Rule / sim (seeded, deterministic)
- 8 radial cracks leave the impact (seed 7: 30-80 px from the centre). **Every crack, when it ends, splits into 2:**
  - free fork: after its growth step L = max(16, 75·0.90^gen)·U(0.75,1.3), two children at ±20-43° (retries ±14-60° if blocked);
  - T-fork: a crack that runs into another crack or the rim cannot cross; its 2 children run off along both sides of the line it hit (43-69° from that line's normal), one into each of the two new cells.
  - A child is born only with ≥ 9 px of free path and only into a piece still > 600 px² (A_FLOOR). A piece > 2,600 px² that no tip can reach any more gets one branch across its middle from its boundary crack (20 of 2,244 forks).
- All tips share one speed, so the sim runs in distance ticks (1 px); geometry does not depend on the clock.
- **Meter** = share of the ice in pieces < 2,600 px² (4 px raster, 4-connected), 100% = SHATTER (tick 656). **Counter** = every crack ever born (true count).
- Totals: 2,245 cracks, 2,244 forks (908 free, 1,316 T, 20 branch), generations 0-17.

## Clock (v2)
- Frame 0 = clear ice. Impact at **0.05 s**.
- **Burst** 0.05 → 1.9 s: s(t) = 320·(1 − e^(−(t−0.05)/0.75)) / (1 − e^(−1.85/0.75)), so the tip speed falls 461 → 253 (0.5 s) → 130 (1 s) → 40 px/s (1.9 s).
- **Build**: speed = max(the burst speed easing down, τ 0.8 s; the running max of the speed that gives a fork rate R0·e^((t−1.9)/6)), with R0 solved so SHATTER lands at 12.0 s. Tip speed 18 px/s (3-8 s) → 60 (11 s) → the 1,600 cap in the last tail.

## Timeline (clip s)
- 0.00 clear glossy ice, 0 cracks. **0.05** impact: 8 rays, crunch cluster. 0.19 first forks.
- **0.5 s**: 49 cracks, gens 0-3, a red-orange-yellow star reaching ~1/3 of the radius.
- **1.0 s**: 154 cracks, gens up to 6, a red → green web over ~60% of the disc.
- **2.0 s**: 408 cracks, gens up to 9, the rainbow web out to the rim, 11% cracked.
- ×2 pops at 0.27, 0.55, 0.77, 1.08, 1.50, 1.92 (6 in the burst), then 2.83, 3.97, 6.47, 7.93, 8.80, 11.18, 11.72 s (GEN 0 → 15).
- Forks per second: **94, 175**, 106, 106, 128, 149, 149, 189, 218, 281, 307, 342 (still climbing at SHATTER).
- Cracks 408 (2 s) → 545 (3 s) → 813 (5 s) → 1,331 (8 s) → 1,976 (11 s) → **2,245**. Meter 11% (2 s) → 18% (4 s) → 31% (6 s) → 47% (8 s) → 70% (10 s) → 100%.
- **SHATTER 12.00 s.** The sheet as it stands is cut along the cracks (render-scale raster, crumbs < 40 px merged) into one sprite per cell, so the switch is seamless and every shard carries its own rainbow crack edges. A release wave (1,100 px/s, plus a thin rainbow ring) frees them from the impact outward: outward 110-360 px/s, up-kick 80-260 px/s, spin, gravity 800 px/s², an ADD edge flare (τ 0.14 s) as each breaks free; they fade below y 1120.
- Hold 1.9 s → 0.6 s dissolve into the clear ice. **14.52 s, 871 frames.**

## Sound
- **Melody:** Chopin, Étude Op. 10 No. 1 in C major (1830; Chopin d. 1849, PD), bars 1-8: the brilliant four-octave arpeggio stream over the left-hand octave bass, 124 stream slots, read from the MIDI. Source: Mutopia "Mutopia-2007/01/25-914" (Peters/Scholtz 1900), Public Domain; `<SOUNDFONTS_DIR>\scores\chopin_etude_op10_1\` + `SOURCE_mutopia_914.txt`. Not on the used list, not kid-coded, not banned.
- One slot per sampled event: slot 1 is the impact (0.05 s), then forks with a greedy min gap that is short in the burst (`--gb` 0.40 × the build's first gap) and shrinks 45% over the build. Notes per second: **14, 14**, 8, 7, 8, 9, 9, 9, 10, 12, 12, 12. The burst is a dense run of the arpeggio; the cadence still lands on SHATTER.
- Arrangement: the stream an octave down (top E6, not shrill), celesta doubles notes ≥ D4, the written LH octaves on piano + strings + contrabass, timpani on the bar-1/3/5/7 bass notes, a soft boom on the impact, a soft oohs C-major pad under bars 1-2. Bars 7-8 are the G dominant (oohs swell, timpani roll), so bar 9's C-major tonic is the cadence on SHATTER: rolled C chord (C1-C5) + strings, oohs, contrabass, timpani C3, a soft boom, a falling celesta + harp C-major cascade and 27 synthesised glass tinks (C-major chord tones, bell partials 1/2.76, 0.12-0.3 s).
- SFX: an ice "tink" per fork (2 tonal partials 1.5-2.9 kHz + 1.87×, 4% downward glide, 5-11 ms, 0.4-0.7 kHz body, 1.5 ms soft click; nothing > 5.5 kHz, no noise bed), ≥ 12 ms apart, gain ÷ √(rate/10), ×1.7 in the burst; a 7-tick crunch cluster on the impact. 629 ticks.
- `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.30, `--fin` 4.5. RMS: burst 0-2 s −18.3 dB, 2-4 s −20.9, late body 10-11.9 s −16.5, SHATTER 12-13.5 s −13.7 (+2.8 dB). Last 0.6 s digital silence.

## Checks (encoded Full HD, v3)
- h264 yuv420p 1080x1920, 60 fps, 871 frames, 14.52 s. **flash_check PASS** (0 flashes, mean lum 0.015). **−14.01 LUFS**, peak −4.32 dBFS, last 0.5 s digital silence (audio identical to v2). Seam (encoded) 0.210.
- Frames read from the mp4 at 0, 0.05, 0.5, 1, 2, 6, 11.97, 12.67 s and the last frame; 1:1 crops of the gold impact glow and the densest web.

## Checks (encoded Full HD, v2)
- h264 yuv420p 1080x1920, 60 fps, 871 frames, 14.52 s. **flash_check PASS** (0 flashes, mean lum 0.015).
- Audio (muxed mp4): **−14.01 LUFS**, peak −4.32 dBFS, last 0.5 s digital silence; energy > 6 kHz 0.02%.
- Seam (encoded): mean |Δ| **0.198**: the loop dissolves into the same clear, still ice as frame 0.
- Frames read from the mp4 at 0, 0.05, 0.5, 1, 2, 6, 11.97 (98%), 12.67 s and the last frame; 1:1 crops of the 1 s burst and the densest pre-SHATTER web. Shards fly past x 0.10-0.84 w (decoration only).

## v1 (superseded 2026-10-21; reproduce with these flags)
- Frame 0 mid-web: `--n0 6 --l0 120 --lq 0.84`, clock = never-decreasing tip speed 14 → 1,600 px/s from tick 432 (count passing 260), fork-rate target τ 5 s, SHATTER at 13.78 s, 16.30 s / 978 frames. The ice pit was baked into the ice layer. v1's clock code (`--nstart`) is replaced by the burst clock; the sim flags above reproduce v1's network.

## Flags (v4 defaults: --ashard 1800 --afloor 400 --tsh 8.2 --gb 1.0 --ga 0.35; FIN_HOLD 2.1)
`--seed (7) --label --cap --still --frame a,b,c --dry --sound 0 --sfx (0.30) --fin (4.5) --gb (0.40)`. Clock: `--sa (320) --ta (1.9) --taua (0.75) --taut (0.8) --tsh (12.0) --taur (6.0)`. Look: `--hstep (0.10)`. Sim: `--n0 (8) --l0 (75) --lq (0.90) --lf (16) --lmin (9) --ashard (2600) --afloor (600)`. Changing a sim flag changes the network: re-check the opening and the rate.

Owner review 2 (2026-10-22): "looks better but use less colours; audience = tired doomscroller wanting pleasant eye-candy" -> rework to ordered, calmer palette (see BRIEF_channel2 Colour rule).

Owner review 3 (2026-10-22): "might work" -> first batch.

Owner review 4 (2026-10-22): "first 2 s ok but at 3-4 s it goes very slow and gets boring" -> v4: no post-burst slowdown.

Owner review 5 (2026-10-22): v4 "ok" -> 4K for Dopamine.exe Oct 28.
