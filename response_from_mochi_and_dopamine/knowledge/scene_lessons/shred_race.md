# shred_race — Every beat they shred 2× MORE sheets: Strips or Confetti, whose bin is FULL first? (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 4, wave 2). New scene file; caption/render/sound chain copied from stack_bounce; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\shred_race.mp4` (**v1**, Full HD 9:16, 14.25 s, 855 frames).
- Caption (baked; `--nocap` = base): "Every beat they shred ^2× MORE^ sheets" / "~Strips~ or ~Confetti~: whose bin is ^FULL^ first?" (true for both: both feeders double every bar).

## Story (clip times, sim values)
- Two office shredders (no brand shapes) on clear bins, dashed gold FULL line at each brim. Mochi = STRIP-CUT (35 strips per sheet), Bolt = CROSS-CUT (390 pieces per sheet). Same blank lined paper both sides, one colour per beat (8 hues), so the pile shows coloured bands that visibly squash as they settle.
- Feed doubles every bar of the music (1.5 s): 1, 2, 4 … 128 sheets, 255 in all. Top pill "SHEETS FED n" + "n/beat" badge; subline "SAME PAPER BOTH SIDES · TIME-LAPSE" (128 sheets in 1.5 s is not real-time).
- Frame 0: bar 0's sheet is through, its strips hang from the throat, confetti in the air; first ×2 at 0.25 s.
- 1.6-4.6 s "BOLT LEADS" (fresh confetti lands fluffier: 25 vs 32 kg/m³): 3.1 % vs 3.6 % at 3.25 s, 13.9 vs 14.8 % at 6.25 s.
- 7-9 s the levels are within 1 % and swap back and forth (the strips land in gulps, the confetti continuously); the 0.5 s-smoothed lead changes at **8.33 s** ("LEAD CHANGE!").
- **10.52 s Mochi's bin FULL** (222 sheets cut; Bolt at 91 %). Her head rides up 5 cm on the springy strips and strips spill over the brim. 10.75 s (bar 9's B-flat) the feed stops: "MOCHI WINS" + "same 255 sheets: tiny pieces pack down, strips spring back". Bolt's confetti keeps settling to **80 %** (density 53 kg/m³) while he stares.
- Pieces at the end: Mochi 8,925, Bolt 99,450 (11×). Dissolve 13.65-14.25 into the pre-roll.
- Brief deviations (truth over brief): the bins hold 0.4 m (not tuned to 11.8 s); exponential feed means the first 6 s are single-digit %; Bolt ends at 80 % not ~70 %.

## The physics (scenes/shred_race.py `simulate()`)
- Bin 30 × 25 × 40 cm; sheet 5 g. Each landing = a layer (mass m, density ρ) that lands at ρ0 and creeps toward ρ_eq(σ) = ρ0 + (ρmax − ρ0)(1 − e^(−σ/σ0)), σ = paper weight above per area, τ 0.55 s confetti / 0.35 s strips (compaction only). Level = Σ m/(A ρ).
- Confetti ρ0 25, ρmax 110 kg/m³, σ0 150 Pa; strips ρ0 32, ρmax 45, σ0 300 Pa (brief's starting values).
- Equilibrium capacity at FULL: strips 207 sheets, confetti 361 (×1.74). Published direction: cross-cut bins hold more shredded paper than strip-cut bins of the same volume (vendor buying guides quote 3-5× by weight; no controlled test found), e.g. https://stationery.lazada.sg/cross-cut-vs-strip-cut-shredders-which-type-should-you-buy-sg/ and https://rexel-preproduction.accobrands.com/en-lv/buying-guides/paper-shredder-buying-guide/cross-cut-paper-shredders . Our 1.74× is conservative.
- Gulps on the eighth grid (min(2^k, 8) per bar), 0.5 s through the cutters; strips drop when the sheet's tail passes, confetti sprays continuously; fall speeds 1.3 / 0.75 m/s (paper flutter). Overflow: Mochi's head lifts up to 5 cm, the rest spills.
- Pile drawn as per-bar bands with a texture squeezed by the true compaction (th / th_fresh); fresh landings form a small mound under the throat that relaxes (visual, zero-mean).

## Sound
- **Piece:** F. Chopin, Prelude Op. 28 No. 16 in B-flat minor "Presto con fuoco" (1839, PD), bars 2-8 at quarter = 160 (one bar = one feed beat), the bar-1 pickup chord at frame 0, resolving to bar 9's B-flat on the win. Source: Mutopia-2017/03/29-2176, `<SOUNDFONTS_DIR>\scores\chopin_prelude_op28_16\` + SOURCE.txt. Replaces the brief's Glinka "Ruslan" overture (no PD note data reachable: Mutopia none, IMSLP scans only, no MIDI). Not used elsewhere (grep 2026-10-31).
- Arrangement: right-hand runs folded down (≤ F5) on piano + soft strings, left-hand bass on cello + contrabass octave + piano, off-beat chords pizz (+ horns from bar 4), timpani on each doubling downbeat; B-flat major tutti cadence (Picardy) + held strings.
- SFX: a short tonal "zzip" per gulp (strips softer/longer, cross-cut buzzier), soft pitched paper ticks per landing (≥45 ms apart), a low thump when Bolt's pile slumps ≥4 mm, dings on the lead change and FULL. All ≥12 ms after notes.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 855 frames = 14.25 s. Muxed −14.00 LUFS, peak −2.00 dBFS, last 0.5 s −240 dBFS.
- RMS/s: −19.1 −18.2 −18.0 −17.6 −17.5 −17.1 −16.6 −16.2 −15.5 −15.0 −15.0 −13.5 (cadence) −25.7 −36.1. SFX events/s 10 11 14 19 34 32 32 34 33 34 29 2.
- flash_check PASS (0, mean lum 0.043). Seam mean |delta| 1.92 = the clip's own frame-to-frame motion (frames 0→1: 2.09); dissolve into the pre-roll.
- Side safe zone: bins x 135-885, heads 120-900, characters 410-610, all text inside 0.10-0.84w; the spilled strips on the floor reach the left edge (decoration).
- Frames read from the mp4: 0.05, 3.0, 8.4, 10.6, 13.0; stills at 0, 1, 2.5, 7.5, 10.0, 10.6, 11.7, 13.3.

## Args
- `--s0c`, `--s0s` (σ0 confetti/strips), `--binh` (0.40), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## v2 (2026-11-01, owner review: "maybe challenge should be whose bin can hold more?")
- Same sim, reframed (`--v2`). Caption line 2 "~Strips~ or ~Confetti~: whose bin holds ^MORE^ paper?". The honest answer flips the winner to **BOLT**: same 255 sheets, his bin takes all of them at 80 %; Mochi's is FULL at 207 sheets (10.52 s), ends holding 232 (head lifted on the springy strips) and spills 23.
- HUD density line -> "HOLDS n sheets · ρ kg/m³" (in-bin mass / 5 g). Banners: "FLUFFY AT FIRST" (Bolt's level higher early, which is now the losing side), "CONFETTI PACKS DOWN!" at the 8.33 s crossover, "FULL!" kept. Finale "BOLT WINS" + "same 255 sheets: his bin took ALL of them, hers spilled 23" + "tiny pieces pack down, strips spring back". Reactions swapped (Mochi smug then worried then annoyed stare; Bolt sweats early, cheers from the crossover). Sound unchanged.
- Deliverable `...\MochiAndBolt\review\fixes_1101\shred_race_v2.mp4`. 14.25 s, -14.00 LUFS, peak -2.00, silent tail, flash 0, seam 1.92 (= v1). v1 -> archive/shred_race_v1.mp4.
- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-09` (events json byte-identical to v2fix). Full HD v2 -> archive/shred_race_v2.mp4.
