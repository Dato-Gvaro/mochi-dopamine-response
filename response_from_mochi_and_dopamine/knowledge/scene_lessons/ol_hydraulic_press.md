# ol_hydraulic_press (Dopamine.exe)
- New scene, character-free (docs/BRIEF_batch50.md, docs/BRIEF_channel2.md). Skeleton: ×2 per crush toward a named end state with a twist; concrete objects (a hydraulic press, a conveyor of everyday objects), one obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every crush makes the press ^2× STRONGER^|until something breaks ~THE PRESS~` (`^x^` = the current object's tag colour, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_hydraulic_press.mp4` (v1, Full HD, label fhd1, 14.75 s, 885 frames). No 4K yet.
- **Staging (batch58, 2026-10-29):** the 4K file moved from DopamineExe `schedule\2026-11-02\2_ol_hydraulic_press.mp4` to `schedule\2026-11-06\1_ol_hydraulic_press.mp4`, retimed to 04:00 local Nov 7 (= 19:00 US East Nov 6); its 11-02 slot went to ol_magnet_sphere (the owner wants it out sooner). File unchanged.

## World (logical 1080x1920, static camera)
- Arena: thin white frame 128-888 × 318-1226. Press centred at x 420: slate-steel crown 160-680 × 350-480 (bolts, a cream force gauge, an amber plate "MAX 400 t"), two chrome columns (192-244, 596-648), an orange cylinder, a chrome rod, a ram block and a 336-px hazard-striped platen. Bed + conveyor: belt top y 1040 (dark rubber, cleats move with it), bolster, rails and legs; a hazard-striped debris bin across the front (y 1172-1226).
- 20 objects on the belt, 330 px apart, each needing exactly 2× the one before it (ladder index k, force 2^k kg, 1 t := 2^10 kg): strawberry 1 kg, grape 2 kg, egg 4 kg, tomato 8 kg, apple 16 kg, tennis ball 32 kg, soda can 64 kg, glass bottle 128 kg, coconut 256 kg, coffee mug 512 kg, golf ball 1 t, wood block 2 t, billiard ball 4 t, concrete block 8 t, granite rock 16 t, brick 32 t, bowling ball 64 t, steel block 128 t, anvil 256 t, **diamond 512 t**. Drawn 1.3× life size (`--osc`), anvil 325 px wide.
- Each object carries a tag under it on the bed (name + strength, outline/number in an ordered "heat" hue: teal for 1 kg → green → gold → orange → red for 256 t; the diamond's tag is gold). Tags pop on the crush and dim once broken.
- Crush looks (each object-specific, all deterministic): strawberry/grape/tomato squish wide and burst (juice droplets, pulp, a flat splat + juice puddle); egg cracks (lines run down the shell), shell shards + white/yolk puddle; apple bursts into cream chunks; tennis ball squashes flat and pops (flat felt disc); soda can crumples into accordion folds to a flat disc with amber droplets; glass bottle, mug, golf ball, billiard ball, concrete block, granite rock, brick, bowling ball: cracks spread from the platen, then they shatter into material-coloured polygons (glass translucent green, mug blue glaze/white inside, etc.); wood block splits into splinters; steel block flows plastically into a wide warm-edged pancake; the anvil's horn droops, its face sags and it squats (bent anvil stays on the belt).
- Fragments: ballistic, one gravity (2,200 px/s²), three destinations: land on the belt and ride it out to the left, fall into the bin in front, or drop behind the belt.

## Rule / timeline (clip s; 126 bpm, s = beats from the theme's first downbeat)
- Crushes on the music: one per half-bar (s 6-16: grape → soda can, 0.95 s apart), one per beat (s 17-23: glass bottle → concrete block, 0.48 s), one per half-beat (s 23.5-25.5: granite → anvil, 0.24 s). Squash time 0.32 / 0.21 / 0.11 s. Breaks at 0.167, 1.12, 2.07, 3.02, 3.98, 4.93, 5.40 … 8.26, 8.50, 8.74, 8.98, 9.21, 9.45 s.
- Counter = live PRESS FORCE: rolls from the last object's strength to the current one's during each squash (×2 pill pops on each crush), 1 kg at frame 0 → 2 kg at 0.17 s → … 256 t at 9.45 s.
- Diamond (s 26 = 9.69 s): the platen lands on it and stops. Force climbs 256 → 400 t (frame limit) over 2.86 s; the frame cracks on every 8th (s 26.5-29) then every 16th (s 29.25-31.75): 17 crack events, each a new jagged segment in the left/right columns (two cracks each) or the crown, with a steel chip and a gold tip glint; the crown bows, the rod bows, the gauge needle shakes into the red.
- **Cadence 12.548 s (s 32, our G-major chord): the PRESS breaks.** Columns snap at their cracks (upper parts and the crown lift 26 px, tilt outward), the rod buckles (52 px bow), the platen snaps in two over the diamond and its halves tip and fall onto the belt either side of it, amber oil spurts from the cylinder seal, the gauge glass cracks and its needle swings loose. Diamond tag → "UNBROKEN" (gold), 5 gold glints on the diamond; counter "400 t" gold, label "THE PRESS BROKE"; meter full + goal glow; frame warms to gold. Hold → 0.6 s dissolve into the pre-roll (the strawberry's splat on the belt, the platen coming down on the grape). **14.75 s, 885 frames.**
- Events per second (crushes + strain cracks + break): 1, 1, 1, 2, 1, 2, 2, 2, 4, 4, 4, 8, 5 (cadence), then the hold.

## HUD
- Meter y 1290: log scale 1 kg → 400 t (heat-gradient fill, ticks at 1 t and 100 t, white marker), gold "FRAME LIMIT 400 t" goal from frame 0.
- Counter y 1488: force in kg / t + "×2" pill (current tag hue, pops per crush) + "PRESS FORCE".
- Watermark "DOPAMINE.EXE" right-aligned at 888, y 1256, 35 %.

## Sound
- **Music played as music:** G. Verdi, *Il Trovatore* (1853), Act II, "Vedi! le fosche notturne spoglie" (Coro di zingari, the **Anvil Chorus**); Verdi d. 1901, PD. Source: W. Dressler's piano edition, New York 1857 (Wikimedia Commons, Public Domain Mark; IA b10264954), saved at `<SOUNDFONTS_DIR>\scores\verdi_anvil_chorus\commons_dressler_1857\` + `SOURCE.txt`. The G-major theme (G–D–B, A–F♯–D, B–G–D, C–A–F♯, D–B–G, E–C–A, F♯–G, A–D–D–D) and its I–V harmony are hand-transcribed into the scene (`THEME`, `HARM`) and arranged for lib/orchestra; no MIDI is read at runtime. Two classicalmidi.co.uk sequences in the same folder were used only to cross-check pitches (not cleared for commercial use; not used in the render).
- Not on the used/banned lists (Brindisi and Verdi's Requiem Dies irae are other works), not kid-coded.
- Arrangement: violin + strings on the theme (flute 8va and trumpet join for the 2nd statement), repeated 8th-note string chords (the 1857 left hand), horns on the harmony, cello/contrabass on the beats, timpani on each half-bar, a timpani roll on D from s 29 into the cadence. One steady tempo, **126 bpm**. Cadence: our held G-major tutti (the theme ends on a half-close on D; V → I), rolled harp, celesta glints, timpani G.
- SFX (×0.60, all tonal, pitched to the chord sounding there — the crushes are the anvils of the Anvil Chorus): every crush = a low hydraulic thud on the bass note + the material's own sound: fruit = a soft "plop" glide (+ 2 ticks), egg = 3 shell ticks + plop, tennis ball = a pop, can = 4 descending clacks while it folds + a clang, glass/mug/golf/billiard = a tink cluster, coconut/wood = wood clacks, concrete/rock/brick/bowling = a 6-clack rattle, steel = two clangs, anvil = a big clang on the chord. Diamond contact = a high clang; each strain crack = a rising tonal ping + clack; the break = a G-major clang chord, a rattle down the chord, the platen halves landing (2 clangs), 5 tinks on the glints.
- `level_bed` (+3 dB crescendo, cadence +4 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux without `-shortest`.

## Checks (encoded Full HD v1)
- h264 yuv420p 1080x1920, 60 fps, 885 frames, 14.75 s. **flash_check PASS** (0 flashes, mean lum 0.022).
- **−13.98 LUFS**, peak −6.03 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.32 %. RMS per second (muxed): −19.3, −18.6, −18.6, −18.1, −18.4, −16.4, −16.8, −16.4, −15.9, −15.0, −17.2, −17.2, −16.3 (cadence), −16.1, −54.7 (tail).
- SFX events per second: 4, 5, 4, 6, 6, 10, 10, 9, 25, 13, 8, 16, 29, 16 (161 total).
- Seam (check_clip, encoded mean |Δ| last → 0): **0.627** (good band 0.12-0.72).
- Frames read from the mp4 at 0, 0.5, 1, 2, 5, 8.3, 9.1, 9.3, 11.5, 12.6, 13.5 and 14.73 s; 1:1 crops of the crush zone at 0.10 (grape squashing), 4.90 (can folded), 8.30 (concrete block shattering), 9.24 (steel pancake), 9.47 (anvil bent). Theme pitches in the rendered bed spot-checked by FFT against `THEME`.

## Doubts
- Objects are drawn 1.3× life size but still read small against the big press on a phone (grape ~86 px, anvil 325 px). The press is the hero; `--osc` raises them if the owner wants.
- The half-beat stretch (granite → anvil, 0.24 s each) is fast: the steel pancake and the bent anvil are each on screen under the platen for ~0.1 s, then ride off left (the bent anvil's horn stays visible at the left edge during the diamond phase).
- Tonnages are "real-ish" on a ×2 ladder (1 t := 1,024 kg in the ladder; brick 32 t, steel block 128 t, anvil 256 t are in the plausible range, the small ones are rounded to the ladder). A real diamond would shatter in a press; here it is the twist: it needs 512 t, the frame is rated 400 t, so the frame goes first.
- The diamond phase (2.86 s) has no crushes; its rate comes from the 17 crack events (8ths then 16ths) and the rolling counter. Events/s there 4 → 8.
- The soda can's accordion reads a little like a spring stack mid-fold.
- Music: notes from a PD 1857 piano edition, arrangement ours. The cadence chord (G major) is ours: the theme itself ends on a half-close on D.

## Flags
`--label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.60) --fin (2.0) --bpm (126) --hold (2.2) --osc (1.3)`. A still renders in < 1 s; the full FHD clip in a few minutes.

## Owner review
- 2026-10-25: approved v1 to ship as a test. 4K ship render: `output/ol_hydraulic_press_ship_9x16.mp4` (NF_SCALE 2.0, label ship, v1 settings, x264 threads 2 + rc-lookahead 12): h264 yuv420p 2160x3840 60 fps, 885 frames, 14.75 s; flash PASS (0, mean lum 0.022); −13.98 LUFS, peak −6.03 dBFS, last 0.5 s silent; seam 0.507. Frames 1 s, 8.30 s (concrete block shattering, + 1:1 crop) and 12.75 s (the press breaking) read.

## Upload draft
- Titles: "Every crush makes the press 2x stronger… until something breaks THE PRESS 💎 #satisfying #physics #shorts" · "Grape to anvil, then the diamond broke the press 💎🔨 #satisfying #physics #shorts" · "1 kg to 400 tons in 20 crushes… guess what broke first 💎 #satisfying #physics #shorts".
- Pinned comment: "the frame is only rated 400 t and the diamond needs 512… which crush was the most satisfying for you?"
