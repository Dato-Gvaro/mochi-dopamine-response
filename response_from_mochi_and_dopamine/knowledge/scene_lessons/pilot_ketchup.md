# pilot_ketchup — Every shake... NOTHING: how many tries until it comes out? (pilots, 2026-10-28)

- Brief: docs/BRIEF_pilots.md (pilot 2). New scene file; lib/ and tools/ untouched. Characters (lib/toon), caption/banners and the sound/mastering chain copied from snowball_fort.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\pilots\pilot_ketchup.mp4` (**v1**, Full HD 9:16, 17.98 s, 1079 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Every shake... ~NOTHING~:" / "how many ~TRIES~ until it comes out?"
- **Story:** a diner table at night. Bolt holds a glass ketchup bottle upside-down over his fries: SHAKE ×12 (harder every time) → SMACK the bottom ×5 → TAP THE NECK ×14 (v1: "TAP THE 57"; removed batch55) → SQUEEZE ("GLASS DOESN'T SQUEEZE", 0.0 mm). Three single drops in all (meter 0 → 2 %). He leans in to peer at the nozzle; on Haydn's fortissimo "surprise" chord the whole bottle comes out at once ("ALL OF IT."): it buries the fries, splashes up onto Bolt (81 drops stick), floods the table (OVERFLOW 402 %). Mochi, who ate her fries one per bar, lifts her clean plate out of the flood, deadpan. Bolt's ketchup-spattered stare.

## batch55 (2026-10-28): fixes → 4K ship
- Owner: "we can try it"; the coordinator's two flags applied, nothing else changed (sim, story, timing, SFX identical).
  1. **No "57":** the neck's "57" sticker text is gone (plain glass neck); the HUD chip "TAP 57" → "TAP"; no title/pinned comment mentions it.
  2. **The pp half lifted:** `level_bed` now runs an envelope follower (0.8 s window, 0.7 s smoothing, cap ×4) over bars 9–16 (7.62 s → the chord) holding the bed at `--ppgap` dB relative to the p half's BED level. Default −3 (i.e. 3 dB OVER the p bed: the p half also carries the loud shake/smack glass knocks, so a 0 gap still sounded like a drop). `--ppgap off` = v1. The ff chord is lifted relative to the new (louder) body as before.
  - Measured on the muxed 4K mp4: short-term (3 s) loudness over 7.7–14.4 s min −15.4 LUFS (v1 −21.6), 1 s windows min −16.9 (v1 −22.5). RMS/s: −19.5 −18.0 −18.3 −17.5 −17.6 −16.1 −15.2 | −20.1 (bar 8's rest, before the pp) −17.3 −17.2 −17.3 −18.2 −18.0 −17.8 | −16.7 **−11.2 (surprise)** −14.4 −30.4. pp → ff jump 6.6 dB RMS (v1 12.6) plus the timpani/bass-drum transient; the p half came down ~1.7 dB (integrated normalisation).
  - Tried: gap +1.5 (pp −19…−21 RMS, still a dip), −1.5 (1 s min −17.8). `--findb` 4.5/6 made no difference (the chord is already at the −2 dBFS ceiling / the ×3 cap).
- 4K (`--label ship`): h264 High yuv420p 2160x3840 @ 60 fps, 1079 frames = 17.98 s; −14.00 LUFS, peak −1.95 dBFS, last 0.5 s −90 dBFS; flash PASS (0, mean lum 0.11); seam mean |Δ| 0.78. Encoded frames read at 0.5, 9.0 (+ a 1:1 crop of the bottle: no "57") and 15.3.
- Staged: `MochiAndBolt\schedule\2026-11-04\2_pilot_ketchup.mp4`, 16:00 local Nov 5 (= 07:00 US East Nov 5), PILOT. FHD review copy → `MochiAndBolt\archive\pilot_ketchup_fhd.mp4`.
- Seen at 1:1, not fixed (not asked): the upside-down "KETCHUP" word touches the label's right edge.

## Layout
- Fixed camera: world × 1.5 about (520, 1100) → screen (507, 1000) (no camera move). Table top (3/4 view) world y 1000–1236; plates on it; the characters behind the far edge (bodies clipped by the table).
- Bolt (CR 60) right, the bottle (270 × 96 px, nozzle world (600, 996)) in front of him held by two mint nubs; Mochi (CR 56) left with her plate (14 fries + a neat dollop).
- HUD (y 1350–1546): the method roster (SHAKE / SMACK / TAP 57 / SQUEEZE: active chip lit, used ones crossed out red, counts ×n) + the meter "KETCHUP ON FRIES n %" → "OVERFLOW n %". Key content inside x 0.10–0.84w.

## The physics
- **Thixotropic yield-stress ketchup.** Structure λ (1 = rested); yield stress τ_y = 1.52 λ; gravity on the column σ_g = 1.0 (normalised). Each try adds a stress pulse and breaks structure: shake 0.36 a / 1.05 % · a (a = 0.55 → 1.3 g, harder each time), smack 0.24 / 1.8 %, tap on the neck 0.04 / 0.62 %; squeeze 0 (glass). A pulse that pokes above τ_y makes a drip (`--dripk`; drops at 4.88, 5.34, 6.74 s) and breaks a little tip structure (β 0.3).
- **Delayed avalanche.** Below yield it creeps: γ̇ = C0 exp((σ − τ_y)/0.035); creep breaks structure (α γ̇ λ), so τ_y falls, the creep speeds up: λ 0.848 (5.76 s) → 0.776 (7.68) → 0.707 (11.52) → 0.674 (14.40) → 0.661 (14.80) → yield at **14.880 s = the surprise chord**. α = 60.8 is FITTED (bisection) so the avalanche lands on the chord; the tries' contributions are fixed.
- **The flood:** 563 particles (r 6.5 px) leave the nozzle over 0.8 s at ~540 px/s; position-based fluid (gravity, pair spacing with capped corrections, XSPH viscosity 0.35, floor friction, extra grip on the fries), the first hard impacts splash up (12 %), drops that reach Bolt stick (81) and slide a little.
- **Meter:** volume resting on the fries / 140 (the volume that covers them); OVERFLOW = total volume out / 140 once it runs off the plate.

## Sound (music first)
- **Piece:** Joseph Haydn, Symphony No. 94 "Surprise", II. Andante (1791; Haydn d. 1809, PD). The joke IS the piece: a quiet theme, repeated even quieter, then a fortissimo chord. Not on any used list.
- **Source:** the LilyPond excerpt (first violins, bars 1–16 with the ff chord) in the English Wikipedia article "Symphony No. 94 (Haydn)"; wikitext saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\haydn_surprise\`.
- **Excerpt:** C major, 2/4, quarter = 125 (bar 0.96 s). Bars 1–8 p (shakes on every quarter = the melody's note pairs; smacks on bar 7's eighths), bars 9–16 pp (taps on every melody note, then the squeeze), bar 16 beat 2 = the ff G-major chord + the kettledrum stroke = the pour.
- **Arrangement** (lib/orchestra): violins (8va + at pitch), flute 8va in the p half, pizz bass + soft off-beat chords (Haydn's lower strings), a string pad; the surprise = timpani G + bass drum + full strings, brass, horns, oboe, flute, contrabass, a late harp.
- **SFX** (tonal): glass knock per shake (rising with the harmony), glass "tok" + soft thud per smack, a tiny high glass tick per tap, soft grip ticks through the squeeze, a "plip" per drop, the pour: a big low plap + thud, then plaps on the 32nd grid as the ketchup lands (down the G chord), a tick + glide as Mochi lifts her plate, Mochi's fry bites.
- Mastering: the p/pp shape is kept (no crescendo levelling), the surprise lifted `--findb 3.0`; `master_keep_lift` −14 LUFS, −2 dBFS; last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 1079 frames = 17.98 s. −14.06 LUFS, peak −1.99 dBFS, last 0.5 s −90 dBFS.
- RMS/s: −17.8 −16.4 −16.7 −16.0 −16.3 −14.7 −13.6 | pp −20.2 −20.9 −21.1 −20.8 −23.2 −24.3 −23.7 | −18.2 −11.1 (surprise) −13.2 −28.7.
- SFX events/s: 7 5 5 5 6 7 10 3 5 4 5 4 5 4 6 17 12 0.
- flash_check PASS (0 flashes, mean lum 0.111). Seam mean |Δ| 0.95 (a shake lands on frame 0).
- Frames read from the mp4: 0.5, 1, 2, 5.2, 6.1, 9.0, 13.0, 14.7, 14.95, 15.3, 15.6, 16.2, 17.2 + a 1:1 crop of the flood (15.3).

## Doubts
- **The pp half is quiet** (−20…−24 dB RMS, 7.7–14.4 s): it is Haydn's own dynamic and the whole joke, but a scroller may think the sound dropped. `expr`/pizz gains can lift it.
- The **"57"** on the neck is the Heinz meme the brief asked for (a famous brand's embossing). No brand name/label shape is used (generic "KETCHUP" label with a tomato), but the owner should decide if "57" stays (it is one text string in draw_bottle).
- The Surprise theme is also used to teach beginners ("Papa Haydn"); it is not on KID_CODED_MELODIES and the framing is adult, but flag it.
- The flood is energetic (cartoon: a whole bottle in 0.8 s, splashes up to Bolt's head) and much of it ends on the table rather than on the fries (the meter on the fries peaks ~83 % then the table takes it).
- α (creep breakdown) is fitted to land the avalanche on the chord.

## Args and cost
- `--g --alpha --dripk --np --pour --pourv --splash --frict --xsph --seed --sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~5 s (fluid); Full HD render ~45 s at 2 encoder threads.
- Owner review (batch55): "we can try it" → fixes ("57", pp lift) → 4K ship.

## Outcome
- (fill after upload)
