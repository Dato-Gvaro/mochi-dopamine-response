# ol_meteor_split (Dopamine.exe)
- New scene, character-free (docs/BRIEF_batch50.md spec, docs/BRIEF_batch51.md lessons, docs/BRIEF_channel2.md). Skeleton: ×2 per impact toward a named end state; concrete objects (meteors, a layered-rock mountain), one obvious rule, physical destruction (no slow filling).
- Caption (baked, `--cap`; `--cap ''` = base): `Every meteor that hits ^SPLITS INTO 2^|until the ~MOUNTAIN~ is GONE` (`^x^` = the newest generation's hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_meteor_split.mp4` (**v2**, Full HD, seed 1, label fhd2, 16.07 s, 964 frames; overwrote v1). No 4K yet.

## World (logical 1080x1920, static camera)
- Arena: thin white frame 128-888 × 318-1226. Flat bedrock plain (46 px, dark maroon rock texture: strata, seams, grain) along the bottom = "flat ground"; never carved, never counted. Every hit on it leaves a shallow dark crater bowl with a glowing rim that cools to a dim ember and stays (v2: the end state is a scorched crater field).
- Mountain: a 1-px rock bitmap (760 × 876), main summit x 540, two shoulders, fractal outline. Texture: folded strata coloured by altitude in RGB (deep maroon → rust → ochre → sand → slate blue-grey), dark seams every 30 px, static grain, light from the left; a snow cap (layer along the original top above a wavy snow line, with drips). Exposed tops get a 2-px lit rim; fresh crater rims glow warm orange (decay τ 0.75 s).
- Meteors: glowing heads + gradient tails, hue by generation on a warm sweep (gold 0.13 → orange → red → crimson 0.96), S 0.76. Incoming meteors (gen 0, r 13) streak in from the upper left (30° off vertical, 1,080 px/s). Each split: radius ×0.86.
- Chunks: crater debris (2-10 per crater, flung up and out) and detached overhangs fall under one gravity (1,500 px/s²) and hop down the slope up to 3 times. On rock they crumble to dust; on the bedrock 55 % of the bigger ones (≥ 3.5 px) stay as dark rubble (a thin layer, no heap).
- HUD: meter y 1290 = % MOUNTAIN LEFT (strata-gradient fill shrinking toward the gold GONE mark at the left, visible from frame 0); counter y 1488 = meteors in the air + "×2" pill (newest generation hue, pops each time the count doubles); watermark "DOPAMINE.EXE" right-aligned 888, y 1256, 35 %.

## Rule / model (scenes/ol_meteor_split.py `simulate`)
- Every impact lands on the music's 16th grid. A meteor that hits rock blasts a crater (disc of radius KCR × r, centred 0.3 rc below the surface) and splits into 2: one lands to the left, one to the right (≤ 250 px, shrinking to 60 % by the cadence), on a true ballistic arc (g 640 px/s²). Flight time is drawn from 2.85 s → 2.0 s (× U(0.62, 1.38)), shortened if the apex would leave the arena. Landing height = the rock top at landing time; a meteor on bare ground still splits (no carving).
- Steering: so the mountain shrinks AS A MOUNTAIN (lower and narrower), a child whose landing column has no rock above a shrinking envelope (original profile lowered by D(t)) is steered (p 0.95) to the nearest column that still has. Arcs are checked against the rock so nothing flies through it.
- Rock no longer connected to the ground (undercut overhangs) breaks off and falls as chunks.
- KCR is calibrated every run (`--kcr 0` default, bisection; seed 1 → 2.528) so 3 % is left just before the cadence.
- **v2 (owner: no collapse cheat, the meteors destroy it all):**
  - In the last 2.2 s every landing that would miss is steered onto the nearest remaining rock (271/271 hits on rock), so the storm chews through the core chunk by chunk.
  - Children whose landing would fall after the cadence are pulled onto it (the final volley, 314 meteors). One by one, each takes the highest rock still standing, with a 1.5× crater: 19 direct hits blast the last piece away, **0 px left over**. No slump, no crumble.
  - Meteors still in the air after the cadence burn out (fade τ 0.30 s).

## Timeline (clip s, seed 1, v2)
- Frame 0: whole mountain with 2 craters (pre-roll hits), 5 meteors in the air (2 children rising, 3 incoming); first in-clip impact 0.139 s (bar 19 downbeat).
- In the air: 5 at frame 0 → **532 before the cadence, growth ×106.** Count doubles at 0.98, 2.93, 5.42, 7.65, 9.73, 11.82 s.
- Impacts per second: 3, 5, 3, 11, 4, 16, 20, 20, 35, 42, 76, 93, 127, then 382 in the cadence second (incl. the 314-hit volley). Rock hits/s: 3, 5, 3, 11, 4, 16, 18, 20, 33, 33, 59, 88, 127, 87.
- Mountain left per second: 98, 96, 93, 90, 84, 82, 76, 70, 63, 54, 44, 34, 22, 9 % → 3 % before the cadence (a small core stub, still taking hits) → 0 on the cadence.
- **Cadence 13.47 s** (score beat 92, bar 25 downbeat, ff G minor): the volley's direct hits blast the last piece away. Meter 0 % + GONE glow, counter 532 gold + "MOUNTAIN GONE", frame warms to gold.
- End state: a flat crater field (dark bowls with glowing rims cooling to embers, rubble), warm dust rising off it, 9 gold glints along it (0.85-1.8 s after the cadence). Hold → 0.6 s dissolve into the pre-roll (t −0.6..0). **16.07 s, 964 frames.**

## Sound
- **Music played as music (epic/dramatic for meteors):** S. Rachmaninoff, Prelude in G minor, Op. 23 No. 5, "Alla marcia" (1901, pub. Gutheil 1903; Rachmaninoff d. 1943 → PD in the US (pre-1929) and life+70 countries since 2014). Source: Mutopia `RachmaninoffS/O23/rach-prelude23-05` (after the Muzyka and Gutheil editions; engraving CC BY-SA 4.0, only the notes of the PD work are used), saved at `<SOUNDFONTS_DIR>\scores\rachmaninoff_prelude_op23_5\` + `SOURCE_mutopia.txt` (downloaded 2026-10-25). Not on any used/banned list (Op. 3 No. 2 is a different work); not kid-coded.
- Score beats 67.75-94.5: bar 18's pickup, the forte march (bars 19-22: Dm, F, Cm, Gm, A7), the D pedal crescendo to ff (bar 23), the octave run down (bar 24), the ff G-minor arrival (bar 25) = the cadence. Steady **108 bpm** (Rachmaninoff's ♩ = 108).
- Arrangement (ours, lib/orchestra): the piano plays every note of both hands; violin on the top voice, strings on the RH chords, horns on the middle chord tones, trombone/tuba/cello/contrabass on the LH bass, timpani on the march's "ta-ta-TUM" bass, a timpani roll on D + tremolo strings under bar 23. Cadence: held G-minor tutti (strings, horns, trumpets, trombones, tuba, cello/bass G), rolled harp, timpani G, a soft concert bass drum boom, celesta glints.
- SFX (×0.40, all tonal, no noise): every 16th with impacts = one deep tonal thud on the bass note the score sounds there (louder for big early meteors) + crunchy rock clacks (stone-bar strike + a lower strike 7 ms later) pitched to the chord, log-scaled into a rattle as the storm thickens. Overhangs breaking off = a short descending clack run. Cadence = thuds on G1/G2, a 34-clack rattle down the G-minor chord, a bell on G5, chimes on the glints.
- `level_bed` (+3 dB crescendo, cadence +4 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux without `-shortest`. Bed pitches spot-checked by FFT at beats 68 (F4/F5/D6/F6) and 92 (G1/G2).

## Checks (encoded Full HD v2)
- h264 yuv420p 1080x1920, 60 fps, 964 frames, 16.07 s. **flash_check PASS** (0 flashes, mean lum 0.013).
- **−14.00 LUFS**, peak −5.99 dBFS, last 0.5 s digital silence.
- RMS per second (muxed): −17.8, −16.8, −17.3, −16.4, −16.5, −16.2, −15.7, −15.9, −16.2, −16.0, −15.9, −15.6, −15.5, −15.0 (cadence), −15.0, −32.4 (fade), silence.
- SFX events per second: 6, 9, 6, 21, 10, 24, 33, 32, 50, 60, 78, 84, 90, 64, 21.
- Seam (check_clip, encoded mean |Δ| last → 0): **0.573** (good band 0.12-0.72).
- Frames read from the mp4 at 0, 0.5, 1, 2 s, and across the last 3 s as 1:1 arena crops (12.5, 13.0, 13.3, 13.45, 13.5, 13.7, 14.0, 14.5, 15.0, 15.4 s):
  - 12.5 s: a narrow cratered core under the storm.
  - 13.3 s: a small stub taking direct hits.
  - 13.45-13.5 s: the volley.
  - 13.7 s: flat glowing field, chunks falling.
  - 14.5-15.4 s: crater field + rubble + rising dust + glints.
- v1 (for the record): flash PASS, −14.00 LUFS, peak −6.03 dBFS, seam 0.590.

## Flags
`--seed (1) --label --cap --still --frame a,b --dry --calib --audio --sound 0 --sfx (0.40) --fin (2.0) --bpm (108) --hold (2.0) --kcr (0 = calibrate; seed 1 → 2.528) --endleft (0.03) --tlate (2.2) --kvol (1.5) --rubble (0.55) --ta (2.85) --tb (2.00) --jit0/--jit1 (0.62/1.38) --spread (250) --aim (0.95) --shrink (0.86) --g (640) --gd (1500)`. Calibration + sim + debris ≈ 10 s; the full FHD clip renders in a few minutes.

## Doubts
- The first 3 s are the calm part: 3-5 impacts/s (big ones: crater, chunks, thud on the march beat) with 5-20 meteors in the air; the generations are still lumpy. By 5 s it is 16/s and climbing.
- The late storm is dense (450+ small meteors, near-vertical bounces): it reads as a fiery meteor storm, but it is busy. `--ta/--tb` up = fewer meteors.
- Children bounce mostly up-and-down (horizontal ≤ ~120 px/s vs ~600 px/s vertical): the split reads as two meteors rising side by side, a narrow V.
- The snow cap is carved off by ~6 s (the mountain shrinks from the top); the last piece is a small reddish core stub.
- Landings are retargeted onto rock at landing time in the last 2.2 s and in the volley (the arc is recomputed to the new column, still ballistic). Before that, ~30 % of late hits land on bare bedrock (they split without carving).
- The cadence frame is the brightest moment: ~300 meteors converge in a column on the centre, plus the ground hits around it (flash_check still 0).
- After the cadence the meteors still in the air burn out in ~0.5 s instead of landing (nothing left to hit).
- The end frame above the crater field is still mostly black sky (the mountain is gone); the glowing field, rubble, rising dust and glints carry it.
- The cadence chord is the score's G minor: majestic, not bright.

## Owner review
- 2026-10-27, v1: "interesting, but at the end the centre of the mountain is still untouched and it just collapses — make it damaged by the balls until it's gone."
- → v2: late-storm steering + the cadence volley carve the core away by direct hits (0 px left, no crumble). The end is a crater field with glowing scorch bowls, rubble, rising dust and gold glints on a 46-px textured bedrock plain. Rule, counters, music and timing are unchanged.

## Upload draft
- Titles:
  - "Every meteor that hits splits into 2… until the MOUNTAIN is gone ☄️ #satisfying #physics #shorts"
  - "5 meteors became 532 and ate a whole mountain ☄️⛰️ #satisfying #physics #shorts"
  - "Each meteor splits in 2 when it hits… watch the mountain disappear ☄️ #satisfying #physics #shorts"
- Pinned comment: "it started with 5 meteors and ended with 532… at what % did you think the mountain was done for? ☄️"

## Shipped (4K, 2026-10-28, batch53)
- Owner: "good" → 4K ship. `NF_SCALE=2.0 python scenes/ol_meteor_split.py --label ship` (seed 1; calibration kcr 2.528, 3.0% left before the cadence, the volley leaves 0 px: identical to v2).
- Encoded: h264 yuv420p 2160x3840 @ 60 fps, 964 frames = 16.07 s. −14.00 LUFS, peak −5.99 dBFS, last 0.5 s silent. flash_check PASS (0 flashes, mean lum 0.013). Seam mean |Δ| 0.405.
- Frames read from the 4K mp4: 0.5 s, 8.0 s (+ 1:1 crop of the craters), 14.5 s (crater field, 0%, 532).
- Staged: `<VIDEOS_DIR>\DopamineExe\schedule\2026-10-29\2_ol_meteor_split.mp4` (15:00 local Oct 30 = 07:00 US East Oct 30). FHD review copy → `DopamineExe\archive\ol_meteor_split_fhd.mp4`.
- Titles 1 and 3 above were 96 / 98 chars with the hashtags (☄️ is 2 code points); shortened in UPLOAD.md to "Each meteor that hits splits in 2… until the MOUNTAIN is gone ☄️" (93) and "Each meteor splits in 2 when it hits… watch the mountain vanish ☄️" (95).
