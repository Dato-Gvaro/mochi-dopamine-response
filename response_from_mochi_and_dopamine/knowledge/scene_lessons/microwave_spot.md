# microwave_spot — Middle of the plate or the edge: which heats EVENLY? (batch59 v1 2026-10-29; v2 batch60 2026-10-30)

- Brief: docs/BRIEF_batch59.md (v1), docs/BRIEF_batch60.md (v2: owner "good idea, needs a rework").
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\microwave_spot.mp4` (**v2**, Full HD 9:16, 16.13 s, 968 frames; output label v2b). Archive: `archive\microwave_spot_v1.mp4` (top view), `archive\microwave_spot_v2.mp4` (the same v2 build before the proof-read: "CENTRE" → "CENTER").
eview\batch59\microwave_spot.mp4` (**v2**, Full HD 9:16, 16.13 s, 968 frames; output label v2b). Archive: `archive\microwave_spot_v1.mp4` (top view), `archive\microwave_spot_v2.mp4` (the same v2 build before the proof-read: "CENTRE" → "CENTER").
- Caption (baked; `--nocap` gives the base): "~Middle~ of the plate or the ~edge~:" / "which heats ~EVENLY~?"

## v2 (2026-10-30): two microwaves seen from OUTSIDE
- **Story:** two identical microwaves stacked on shelves (Mochi top, Bolt bottom; tags MOCHI · EDGE / BOLT · MIDDLE). Frame 0: the doors are mid-swing open, each character's arm is reaching in with a frozen burrito; Mochi sets hers at the EDGE (dotted path circle), Bolt his in the MIDDLE (spin arrow). Doors shut (thunk) at 1.0-1.3 s, START beep 1.5 s, hum + oven light from 1.6 s; the plates turn behind the glass doors (mesh, light), food in a thermal view (blue frozen → cream → orange → red). Timers count 2:00 → END (x11 time-lapse).
- Banners (all literally true, proof-read): TWIN MICROWAVES · TWIN BURRITOS → 4.9 s BOLT'S IS THAWING FASTER! (his ice % drops first) → …BUT ITS CENTER SITS IN A COLD SPOT → 8.9 s HERS PASSES THROUGH THE HOT SPOTS (her ice % passes his) → 10.2 s HERS: NO ICE LEFT! → DING 12.43 s on the cadence: MOCHI'S HEATS MORE EVENLY → doors pop, each takes the food out; Bolt bites: BOLT'S BITE: FROZEN AND BOILING (face half blue with icicles, half red with steam); Mochi "HA".
- **Nerd stats (top panel, y 280-604):** TEMPERATURE: coldest to hottest bite: per burrito a min-max band over 0:00-2:00 (y 0-100 °C, WARM 40° dashed, BOILING); COLD SPOTS (below 40°) % strip under it. Inset (top-right): HOT SPOTS top view of the cavity's standing-wave field with both burritos live at their plate positions and Mochi's path circle.
- HUD y 1326-1536: COLD SPOTS (below 40 °C) big % per side (the leader's in its colour), ice %, avg °, a -20..100 °C range bar with the 40° tick, "min to max °C".
- Result at the ding: Mochi 42-69 °C, mean 61, 0 % cold, 0 % ice; Bolt -1 to 100 °C, mean 78, 16 % cold, 3.8 % ice. Cold-spot lead change 11.7 s (Bolt led 7.9-11.7 s: his ring boils first).
- Layout: ovens x 246-904 (panel at the left, door hinged right), tops y 684 / 1004, 300 high; plate 13.5 px/cm seen from 30° (y squash 0.5); characters r 58 at x 170. Key content inside x 0.10-0.84w (the open door's far edge reaches x 905).
- Sound: as v1 (Pathétique III rondo theme, quarter = 140 now) + the oven hum bed (gain 0.05), door thunks, START beeps, latch pops, the three-ding DONE bell on the cadence.
- Checks (v2b encoded): h264 High yuv420p 1080x1920 60 fps, 968 frames = 16.13 s; muxed -14.00 LUFS, peak -2.34 dBFS; last 0.5 s -166 dBFS; flash_check PASS (0); seam mean |d| 0.98 (0→1: 0.58). Frames read from the mp4: 0, 0.5, 1, 3, 6, 7.5, 9, 11, 12.6, 13.6, 15.5.
- Owner checks: is the chart readable enough at phone size (it is ~110 px tall per panel); the bite twist; Bolt "wins" cold spots 7.9-11.7 s before Mochi overtakes (banners don't claim otherwise).

## v1 (2026-10-29, archived)
- Top view into one running microwave, burritos as thermal maps, ice % HUD; the twist and music as v2.

## v1 layout
- Microwave body x 114-901, y 418-1122; turntable axis (517, 770), 22 px/cm (plate Ø 30 cm = 660 px). Burritos 10 x 5 cm (220 x 110 px), 5 mm cells.
- Characters r 70 at x 232 / 802, y 1250; the timer panel between them (y 1150-1242, "TIME-LAPSE x10").
- HUD y 1376-1554: per burrito STILL FROZEN % (the leader's in its colour) and HOTTEST °C, a -20..100 °C range bar with the 40 °C "warm" tick, and "min to max °C".
- Static camera; the plate turns at 0.66 rev per clip second (4 rpm in a x10 time-lapse). No flash.

## The physics (honest model, dt 0.05 s real)
- Field: a fixed standing-wave pattern, E² = 0.015 + 0.985 (sin(πx/6.1) sin(π(y+2.4)/6.65 + 0.88))² x a gentle 15 % modulation; hot spots ~6 cm apart (half a 12.2 cm wavelength), a cold node on the turntable axis. The second axis's period/phase were chosen (search) so the ring-averaged field over Mochi's band (r 7.5-12.5 cm) is flat to ±3.6 % while the axis is a node and r ≈ 3 cm is a hot ring: a multimode cavity is less regular than a single lattice.
- Each cell absorbs P0 E²(position now) x loss; loss = 0.20 frozen (ice + unfrozen brine) → 1.0 thawed (minus 0.25 %/°C): thawed cells run away. P0 10 W per cell at E² = 1 (~800 W absorbed in total).
- Burrito = ~60 % water: c 1.8 J/gK frozen, 3.3 thawed, latent 200 J/g; enthalpy method; 70 g each. Conduction with food diffusivity 1.4e-7 m²/s (non-food corners insulate). Boiling caps at 100 °C.
- Result at the ding: Mochi (edge) 42-69 °C, 0 % ice (gone at 9.0 s); Bolt (middle) -1.2 to 100 °C, 3.8 % ice in a core on the axis, a boiling ring ~3 cm out.

## Sound
- **Piece:** L. van Beethoven, Piano Sonata No. 8 "Pathétique" Op. 13, III. Rondo: Allegro (1798; d. 1827, PD). The 2nd movement was used before (beethoven_pathetique2); this is a different movement. Not on the banned list; not kid-coded.
- **Source:** Mutopia Project Mutopia-2013/01/08-296 (licence: Public Domain; Berners 1908), `<SOUNDFONTS_DIR>\scores\beethoven_pathetique3\pathetique-3.mid` + .rdf + SOURCE.txt (downloaded 2026-10-29); read at runtime.
- **Excerpt:** the rondo theme from its upbeat to the bar-8 cadence (beats 0-29), quarter = 150; the theme stops on the dominant and the cadence chord is voiced C major (a Picardy close) with the microwave's DING.
- **Arrangement:** piano (score), violin on the top line, clarinet an octave down very soft, pizzicato bass per half bar; cadence = timpani C, strings, harp sweep, piano chord, held strings.
- **SFX (tonal):** turntable roller clicks (4 per turn), a tick per 3 % of ice melted / per 1.5 °C while frozen / per 4 °C once thawed (rising pitch, lane per burrito), paced boiling "pops" from Bolt's ring (more as more cells boil), banner dings, the microwave's three-ding bell on the cadence, Bolt's ice-crunch bite + two lava pops.
- Mastering: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 918 frames = 15.30 s. -14.00 LUFS, peak -2.02 dBFS (measured on the muxed mp4), last 0.5 s -240 dBFS.
- RMS/s: -18.0 -18.6 -17.5 -16.9 -17.0 -16.9 -16.5 -16.7 -15.9 -15.9 -15.0 -14.8 (cadence) -15.5 -27.4 -34.2.
- SFX events/s: 12 11 8 12 13 16 14 16 10 16 17 15 5 0.
- flash_check PASS (0). Seam mean |delta| 1.09 (grey) against 0.68 between frames 0 and 1 (the plate turns and steam puffs at the seam): continuous, just under the 1.1 limit.
- Frames read from the mp4: 0.5, 3.5, 7.8, 10.0, 13.6 + a 1:1 crop of Bolt's frozen/lava face at 13.6 s.

## Doubts
- The effective frozen-food loss (0.20 of liquid water) and the field pattern are tuned values; the mechanism (fixed hot spots, ice barely absorbs, thawed spots run away, the axis never moves) is the real physics. Real microwaves also leave the centre cold.
- 4 rpm (real turntables 3-6 rpm) keeps the x10 time-lapse spin calm-ish (0.66 rev/s on screen).
- The win metric changes mid-video from "who thaws first" (Bolt) to "no ice left / every bite warm" (Mochi); banners carry it.
- "Burrito" is generic (no brand). The bite chunk covers Bolt's mouth in the twist frame.

## Args and cost
- `--p0` (10), `--ice` (0.20), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~2 s; Full HD render ~70 s at 2 encoder threads.

## Outcome
- (fill after upload)

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/microwave_spot.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 968 frames 16.13 s; -14.00 LUFS, peak -2.34 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v2b. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-06\3_microwave_spot.mp4`, 00:00 local Nov 8 (= 15:00 US East Nov 7). FHD review copy → `MochiAndBolt\archive\microwave_spot_fhd.mp4`.
