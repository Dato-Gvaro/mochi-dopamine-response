# ol_bridge_load (Dopamine.exe)
- New scene, character-free (docs/BRIEF_batch50.md, docs/BRIEF_channel2.md). Skeleton: ×2 waves toward a named end state; concrete objects (a suspension bridge, cars, vans, trucks, tankers), one obvious rule (more weight → the bridge sags → it snaps).
- Caption (baked, `--cap`; `--cap ''` = base): `Every wave the traffic ^DOUBLES^|until the bridge ~SNAPS~` (`^x^` = the current wave's hue, `~x~` = gold). The brief's "Every second" could not be honest: a doubling count of vehicles that stay readable (car ≥ 39 px) fills three lanes after 5 waves, so the waves are ~2 s apart and the caption says "Every wave".
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_bridge_load.mp4` (v1, Full HD, label fhd1, 13.70 s, 822 frames). No 4K yet.
- Different from bridge_test 1-3 (Mochi & Bolt: arch vs truss side by side, objects dropped from the sky, a rewind loop, characters): one steel SUSPENSION bridge, traffic DRIVES on and jams, sag + hanger stress, the deck folds into a V, a dissolve loop, no characters.

## World (logical 1080x1920, static camera)
- Arena: thin white frame 128-888 × 318-1226. Black sky. Two sandstone cliffs (strata lines, a lit rim) narrowing to a teal river at y 1162.
- Bridge: towers x 192 / 840 (top y 440, steel slate, saddles, a steady red lamp), near + far main cables (far = 36 px higher, dimmer), 22 hangers 30 px apart, a 3-lane road seen slightly from above (far edge 36 px above the near edge, dashed lane lines), a truss-faced stiffening girder. Expansion joint at x 140 (glints on each axle). A round weight-limit sign "700t" at the entry.
- Vehicles (×1.25 of base size): car 37 px, van 45, truck 57, tanker 77; clean silhouettes (body gradient, dark glass, wheels per axle, tanker = cab + round tank with a highlight). Colour = wave (ordered gradient, S 0.68 V 0.86): cars blue / teal, vans green, trucks gold, tankers red-orange; back lanes darker (×0.86 / ×0.72).
- Wave labels under the girder at each wave's current x-extent, with a bracket: "1 CAR", "2 CARS", "4 VANS", "8 TRUCKS", "16 TANKERS" (3 rows, never overlap).

## Rule / model (scenes/ol_bridge_load.py)
- Waves 1, 2, 4, 8, 16 (car, car, van, truck, tanker); weights 1.5 / 3.5 / 12 / 40 t. Every vehicle's front axle hits the joint ON the score grid: cars s −18, −12, −8 (pre-roll); vans s −5, −3, −1, 1 (minims); trucks s 2-9 (quarters); tankers s 10-13 (quarters) then 14-36 (minims, lanes are filling). s = quarter beats from score bar 2.
- Drive: 330 px/s, then a 70 px constant-deceleration stop at the jam's tail (closed form). Lane = the one with most room that the previous vehicle has cleared. All 16 tankers fit (the last one's tail 6 px past the joint).
- Load = Σ weight × fraction of axles over the joint (each axle eased over 0.05 s). Limit 700 t is crossed by the 15th tanker (9.47 s); final 754.5 t.
- Sag = 34 px × (load/limit)^1.15 (+1.4 px per snapped hanger, + a 5 Hz damped bounce per axle, ≤ ~1 px), sine-shaped over the main span; the main cable's low point follows (×0.85). Hanger colour = stress (green → amber → red, S 0.68).
- Creaks: every quarter s 0-34 one central hanger shivers (3 px, gold tint, 0.4 s) with a tonal twang. Strain: 12 central hangers snap from the break point outward on s 35, 36-37.5 (8ths), 38-39.75 (16ths); each leaves a curled stub on the cable and a stub on the deck, with a gold glint.
- **Snap = s 40 = 10.797 s (bar 20's downbeat, Mozart's half cadence on D).** The main cables part at x 488: each piece blends from its taut parabola into a damped pendulum swinging from its tower top. The deck breaks at x 488: two rigid halves pivot on the towers (θ'' = 1.5 g/L cos θ, g 900 px/s² "big-scale", right half 0.07 s later), stop at 63° / 55° with a small bounce (land 11.56 / 11.64 s). Vehicles slide (μ 0.26) to the torn ends, leave with the deck's velocity + a spin, fall ballistically and sink with a splash (ring + 6 droplets, teal, no white). Vehicles on the side spans stay. Dust puffs at the break. 27 splashes, the last 1.82 s after the snap.
- Hold → 0.6 s dissolve into the pre-roll (t −0.6..0). **13.70 s, 822 frames.**

## HUD
- Meter y 1290: load / 700 t, green → amber → red gradient, white marker; gold "LIMIT 700 t" goal from frame 0, "0 t" at the left.
- Counter y 1488: load in t (one decimal under 100) + "×2" pill (current wave hue, pops on each wave) + "ON THE BRIDGE" → gold "THE BRIDGE SNAPPED" at the snap. Watermark "DOPAMINE.EXE" right-aligned at 888, y 1256, 35 %.

## Sound
- **Music played as music:** W. A. Mozart, Symphony No. 40 in G minor, K. 550, I. Molto allegro (1788; Mozart d. 1791, PD). Source: a 19th-century piano edition on Wikimedia Commons ("Symphony No.40 in G minor, K.550 (IA imslp-no40-in-g-minor-k550-mozart-wolfgang-amadeus).pdf", Public domain), saved at `<SOUNDFONTS_DIR>\scores\mozart_symphony40_1\` + `SOURCE.txt`. Bars 1-7 (the theme, violas' 8th-note chords) and 16-20 (the forte on the dominant: D / C♯°7 over a D pedal, then the half cadence on D) hand-transcribed into the scene (`THEME`, `VIOLA`, `D_CH`, `DIM_CH`); no MIDI. Not on any used/banned list; not kid-coded.
- Cut: bars 1-7 then 16-20 (bar 7 ends on D7 and bar 16 is the D pedal, so the join is seamless). One steady tempo, **minim = 116** (bar 1.034 s). Arrangement: violin + strings on the theme, viola 8ths, cello/bass minims; the forte = string tutti chords, violin/flute/oboe top line, horns on the pedal, trumpets, cello/bass D octaves (Mozart's rhythm), timpani D/A, a timpani roll into the cadence. The snap chord = bar 20's D major held 2 s (strings, horns, trumpets, winds, harp roll, contrabass D, timpani). The loop returns to the theme's pickup, as Mozart does at bar 21.
- SFX (all tonal, pitched to the chord sounding there): every axle over the joint = a rubber "thunk" (car high … tanker low, tankers 5 axles); every quarter a hanger twang, louder and higher with the stress; each hanger snap = a bright twang + a clack; the snap = a D clang chord + a low thud + a tonal rumble (D1, 7 Hz beating, no noise) + a clack run down the D chord + 2 cable "whips" (glides); the halves landing = 2 thuds; each vehicle leaving the deck = a clack; each splash = a plop.
- Mix: the music body sits 4 dB over the SFX body (`--beddb`), `level_bed` (+2.5 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux without `-shortest`.

## Checks (encoded Full HD v1)
- h264 yuv420p 1080x1920, 60 fps, 822 frames, 13.70 s. **flash_check PASS** (0 flashes, mean lum 0.010).
- **−14.01 LUFS**, peak −5.64 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.05 %. RMS per second (muxed): −20.4, −19.2, −19.5, −17.8, −18.2, −18.4, −17.9, −16.6, −16.5, −16.5, −15.1, −13.4 (snap), −15.7, −78.8 (tail).
- SFX events per second: 8, 14, 16, 22, 16, 14, 14, 14, 13, 17, 36, 24, 43 (251 total). Axle thunks per second: 5, 11, 12, 18, 12, 10, 10, 10, 10, 9.
- Load per second (t): 11.5, 18.7, 66.5, 114.5, 253, 354.5, 434.5, 514.5, 594.5, 674.5, 738.4, 754.5. Growth ×65.6 (frame 0 → snap).
- Seam (check_clip, encoded mean |Δ| last → 0): **0.576** (good band 0.12-0.72).
- Frames read from the mp4 at 0, 0.5, 1, 2, 5, 9.6, 10.82, 11.3, 12 and 13.68 s; 1:1 crops at 9.6 s (jam, hangers snapping, labels) and 11.3 s (the V fold, tankers sliding). Theme pitches in the rendered bed spot-checked by FFT against `THEME` (s 0, 1, 4, 5, 8, 10, 12, 21, 26: all within 0.2 semitone).

## Doubts
- Vehicles are small next to a 650 px bridge (car 37 px, tanker 77 px at Full HD). Bigger ones would not fit five doublings into three lanes.
- From 4 s the tankers come every minim (2/s) because the lanes are filling; the event rate is carried by the quarter-note hanger creaks, then the snaps (8ths, 16ths). Vehicles+snaps per second: 3, 3, 4, 4, 2, 2, 2, 2, 2, 5, 12.
- The counter stops at 754.5 t ~1 s before the snap (the 16th tanker is the last one that fits); the hangers snapping carry that second.
- Physics is a plausible kinematic model, not a structural solve: the deck breaks at the max-sag zone, halves pivot on the towers, the main-span hangers are assumed gone at the snap.
- "Every second" in the brief became "Every wave" (honest: waves are ~2 s apart).

## Flags
`--label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.50) --beddb (4) --fin (2.0) --bpm (116) --hold (2.9) --lim (700) --sag (34) --vsc (1.25) --g (900)`. A still renders in ~1 s; the full FHD clip in a few minutes.

## Upload draft
- Titles: "Every wave the traffic doubles… until the bridge SNAPS 🌉 #satisfying #physics #shorts" · "1 car, 2 cars, 4 vans, 8 trucks, 16 tankers… then the bridge said no 🌉 #satisfying #physics #shorts" · "The sign said 700 t. The 16 tankers didn't read it 🚛 #satisfying #physics #shorts".
- Pinned comment: "the sign at the entrance says 700 t and nobody stopped the tankers… which wave would you have closed the bridge at?"
