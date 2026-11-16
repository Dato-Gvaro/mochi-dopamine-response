# ol_paint_drip (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md, docs/BRIEF_overnight_1023.md). Skeleton: ×2 per ledge (every drip that lands on a ledge splits in 2) toward a named end state; concrete objects (glossy paint drips, a wall, ledges), one obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every drip that hits a ledge ^SPLITS^ in 2|until the wall is ~COVERED~` (`^x^` = the front band's hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_paint_drip.mp4` (**v2: calm painted colours**, Full HD, seed 3, label fhd2, 16.15 s, 969 frames). No 4K yet.
- **v1 → v2 (coordinator, owner rule 5 "never over-bright", 2026-10-24):** the v1 end frame was a full-wall, full-brightness rainbow and the yellow-green bands read neon. v2 changes colour only (timing, ×54, music, finale unchanged): one deep colour per band, warm red → orange → gold, then teal → azure → blue → indigo (yellow-green skipped; it only shows inside the 24 px blend at the gold/teal ledge row), HSV value 0.60-0.78, sat 0.58-0.74, 8 % deeper toward each band's bottom; drip heads lifted (+0.17 value, gloss) so they pop; the white sheen lines on the streaks removed (`--sheen` restores them). Mean luminance of the covered end frame (15.33 s): full frame 0.209 → **0.153**, wall 0.604 → **0.419** (p95 0.81 → 0.56). Frame 0 / last frame (= pre-roll): 0.092 → 0.071.

## World (logical 1080x1920, static camera)
- Wall x 140-876 (inside 0.10-0.84 w), y 336-1200, thin white frame (85 %). Bare wall = 3.5 % white + a faint 13 % primer of each band's final colour (the end state is readable from frame 0).
- A paint pipe along the top (red paint inside) with 2 nozzles (x 324, 692, tips y 382); the next drop swells at each tip and lets go on the grid.
- 7 bands (generation 0-6, each 0.85× the height of the one above: 178 → 78 px) and 6 ledge rows laid out as a binary tree: row g's ledges are centred on the gen g-1 runs, half-length = half the gen-g spacing (92, 46, 23, 11.5, 5.75, 2.9 px). Runs: 2 → 4 → 8 → 16 → 32 → 64 → 128.
- Drips: glossy beads (radial gradient + specular), r 14 × 0.75^g; a landing bead squashes, the two halves slide to the ledge ends and run down. Streaks: one colour per band (`BAND_HSV`: red, orange, gold, teal, azure, blue, indigo; V 0.60-0.78), blended over ±12 px at each ledge row; heads lifted +0.17 value. (v1: hue by height 0.00 → 0.76, S 0.76, V 0.93, white sheen lines.) No random per-object colour.
- HUD: meter y 1290 (rainbow fill, white marker, "WALL n %" left, gold COVERED goal from frame 0); counter y 1488 "N" + "×2" pill (front-band hue, pops on every split step) + "DRIPS"; watermark "DOPAMINE.EXE" right-aligned 876 at y 1230, 35 %.

## Rule / model (closed form, no integration)
- Nozzles release on the music grid: one scout drop at beat −10, quarters from −6, eighths from −2, 16ths from beat 0, stop on the cadence. Every band takes exactly 3 beats (2.5 s), so every split lands on the eighth/16th grid. Splits are synchronous across a row.
- Each split hands its halves a seeded share p = 0.5 ± 0.07; a run's width factor = (share × n)^0.4 (runs are not twins).
- Streak width at height y = spacing × min(1.3, f × (a_g + K_g × P(y,t)) × taper): P = drips that have passed y (smooth over 0.15 s), a_g = bead radius / spacing, K_g = K × (spacing/5.75)^−0.25, taper 0.7→1 from the ledge end (gen 0: none). K is solved so everything below the top band is covered 0.6 s before the cadence; the top band's factor M0 (0.0837, solved) makes the two big pours meet exactly on the cadence. So the wall covers top-down band by band, and the LAST bare patch is the slot between the two pours (x ≈ 504, y ≈ 545): 54 px wide at T−2 s, 27 at T−1, 12.5 at T−0.5, closed on the cadence.
- Counter = every drip that has run on the wall (nozzle drops + both halves of every split).

## Timeline (clip s, seed 3)
- Frame 0: front entering band 3 (16 heads), bands 0-2 streaked (red/orange, yellow, green, teal heads), wall 19 %, 72 drips; first split step at t = 0.
- 0.5 s: 76 drips, 22 %. 1 s: 92, 27 %. 2 s: 150, 37 %. 6.5 s: ~600, 74 %, bottom band reached at 6.67 s.
- Drips per second: 72, 92, 150, 200, 262, 444, 548, 810, 1,040, 1,318, 1,820, 2,260, 2,826, 3,520, 3,898 (end). **×54.1.**
- Cover % per second: 19, 28, 37, 46, 55, 63, 71, 78, 85, 92, 96, 98, 99.3, 100 at 13.33.
- Bands fully covered at 2.6, 4.75, 6.85, 8.55, 10.7, 12.75 s (bands 1-6); band 0 (the last slot) at 13.33.
- Splits per second (run-level): 12, 24, 20, 26, 56, 78, 126, 110, 134, 120, 342, 278, 342, 188 (last 0.33 s).
- **Cadence 13.33 s** (bar 5 downbeat): the slot closes; gold sparkle + 2 gold rings there, counter gold 3,898, meter 100 % + goal glow, frame warms to gold, a calm light sweep down the wall (1.2 s); beads soak in (fade 0.7 s), nozzles stop. Hold 2.2 s → 0.6 s dissolve into the pre-roll (t −0.6..0). **16.15 s, 969 frames.**

## Sound
- **Music played as music:** J. S. Bach, Air from Orchestral Suite No. 3 in D, BWV 1068 ("Air on the G string", c. 1730; Bach d. 1750, PD). Sources: Mutopia, both listed **Public Domain**: `BachJS/BWV1068/bach_air_bmv_1068` (flute + guitar → the melody) and `BachJS/BWV1068/air-tromb` (trombone quartet, Ross Keenum → inner voices + the octave-walking continuo; its voices trade places at beat 6, stitched back in `score_notes`). Saved at `<SOUNDFONTS_DIR>\scores\bach_air_bwv1068\` + `SOURCE_mutopia.txt` (downloaded 2026-10-24). The orchestral Mutopia engraving is CC BY-SA, NOT used. Not on the used/banned lists, not kid-coded, no earlier scene uses it.
- Beats 0-16 (bars 1-4: the held F#, the turn, the sequence over the walking bass, V → I into D on the bar-5 downbeat = the last slot closes). One steady tempo, **72 bpm**.
- Arrangement (lib/orchestra): melody on strings_slow + solo violin; 2nd violins strings_slow; viola; cello + contrabass 8vb on the walking bass; the bass eighths doubled quietly on pizz + harp 8va (the split grid you hear). Cadence: held D-major chord (strings D2-F#5, horns), rolled harp, celesta glint, cello/contrabass D, soft timpani D.
- SFX (×0.40): one tonal paint "plink" per ledge row per split step (sine with a 16 % up-glide, chord tone of the score's harmony, deeper rows higher: D5 → ~F#6, 7 ms apart = a little falling arpeggio, density-scaled); a soft low blop at the nozzles on each beat and when drips first reach the floor; a bell tink on the last slot + a rising D-major chime run on the sweep. No noise. SFX events per second: 6, 5, 7, 9, 9, 16, 15, 17, 19, 17, 26, 24, 27, 18 (0.33 s), 3.
- `level_bed` (+3 dB crescendo, cadence +4 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux WITHOUT `-shortest` (`studio.mux_audio` dropped the last 2 dissolve frames on v0 → broken seam 1.59).

## Checks (encoded Full HD v2; v1 identical except mean lum)
- h264 yuv420p 1080x1920, 60 fps, 969 frames, 16.15 s. **flash_check PASS** (1 flash, in the dissolve at 15.65 s; mean lum 0.049, v1 0.101).
- **−14.01 LUFS**, peak −4.88 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.18 %. RMS per second (muxed): −19.0, −18.2, −18.5, −17.6, −17.7, −17.6, −17.0, −16.9, −16.8, −16.6, −16.3, −15.9, −15.8, −14.8 (cadence), −14.2, −29.3, silence.
- Seam (encoded, mean |Δ| last → 0): 1.13 (v1 1.18) — frame 0 is a split step (beat 0); ordinary on-beat steps in the same file measure 0.90-1.46, off-beat 0.19-0.45.
- v2 frames read from the mp4 at 0, 2, 7, 13.33 (cadence), 13.47 (finale crop 1:1) and the last frame. v1: 0, 0.5, 1, 2, 6.5, 12.5, 13.2, 13.35, 13.8, 15.5 s; 1:1 crops: a top-row split (frames 150/153: the drop lands, two halves on the ledge), the bottom bands at 12.5 s, the last slot at 13.17 s, the finale sparkle at 13.43 s.

## Flags
`--seed (3) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (0.40) --fin (2.0)`. Model: `--bpm 72 --db 3 --bfirst -10 --bq -6 --b8 -2 --bsw 0 --S 2 --ng 7 --r0 14 --hr 0.85 --amp 0.07 --fexp 0.4 --beta 0.25 --t0 0.7 --t0n 1.0 --tn 1 --lead 0.6 --m0 (auto) --tint 0.13 --count total|active`. The sim is cached in `output/ol_paint_drip_*_sim.pkl` (key includes every model flag).

## Doubts
- The top band is the slowest to cover (two pours, 368 px apart, x M0 = 0.08): it stays half bare while the lower bands fill, so the last patch is at the top, not at the floor. Chosen so the last patch is visible (the bottom band's gaps are ≤ 5.75 px).
- Frame 0 has the lower ~45 % of the wall still bare (only the primer tint and ledge dashes): the ×54 counter needs the front to travel bands 3 → 6 during the clip.
- Meter reads 99 % for the last ~1.3 s (the shrinking slot); the finale sparkle/rings are modest in size.
- The Air at 72 bpm is calm, not "hype"; it is the most recognisable steady-tempo PD piece not yet used.
- The bottom two bands are a fine dotted texture of tiny beads (2.5-3.3 px) — reads as shimmer, not individual drips.

## Upload draft
- Titles: "Every drip that hits a ledge splits in 2… until the wall is COVERED 🎨 #satisfying #physics #shorts" · "2 drips became 3,898 and painted the whole wall 🎨 #satisfying #physics #shorts" · "Splitting paint drips until the wall is fully covered 🖌️✨ #satisfying #physics #shorts".
- Pinned comment: "2 nozzles, 6 rows of ledges and every drip doubles… the gap at the top was the last to go. which colour band filled fastest for you?"
