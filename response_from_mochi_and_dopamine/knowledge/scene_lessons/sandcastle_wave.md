# sandcastle_wave — Waves get BIGGER every beat: whose castle SURVIVES? (batch51, 2026-10-25)

- Brief: docs/BRIEF_batch51.md ("sandcastle_wave") + BRIEF_batch50 lessons. New scene file; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch51\sandcastle_wave.mp4` (**v1**, Full HD 9:16, 14.37 s, 862 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Waves get ~BIGGER~ every beat:" / "whose castle ~SURVIVES~?"
- **Twist:** the "lazy" build wins. Mochi's tall, pretty castle (104 cm, keep + 2 towers + 3 flags) is taller from frame 0 and she laughs at Bolt's low wall ("JUST A WALL?"). The waves undercut her castle tower by tower; Bolt's curved sea wall breaks every wave. The 8th wave lands on the cadence, flattens her castle and soaks her. **Bolt wins by being clever** (wall + moat), not by doubling.

## Layout
- Two stacked beach plots (1080 × 506 each): Mochi on top (y 288), Bolt below (y 852). Both get the SAME waves at the same moment. A side cut: beach on the left, sea on the right, sand at y 446 (local), still water at 452.
- Between the plots, a strip with the shared counter: "WAVE k/8", the height (10 cm → 1.71 m, climbs while each wave builds, gold for the last) and a "×1.5 EACH" pill.
- A tide pole in each plot (x 850) with cm marks (50 cm, 1 m, 1.5 m): the wave visibly rises against it.
- Mochi (x 150) left of her castle (x 222–578); Bolt (x 150) left of his small castle (x 250–370, 56 cm), a moat (x 392–448) and the SEA WALL (x 456–590, 41 cm, curved recurve face; labelled).
- A "% CASTLE LEFT" tag in each plot + HUD (y 1366–1544): "WHOSE CASTLE SURVIVES?", each side's % LEFT, rule + live height ("TALL & PRETTY · 104 cm TALL" / "SEA WALL FIRST · 56 cm TALL"), and a TALLER pill → WINNER / FLATTENED at the cadence.
- Key content inside x 0.10–0.84w; only the sea, the sun and the incoming wave bodies go wider. Calm static camera; dusk sky, sand golds, teal sea, cream foam (never white, no flash).

## The physics (honest, cartoon-scaled)
- **Sand = a 4 px cell grid.** Materials: castle sand, wall sand, loose rubble. Each castle is split into structural blocks (towers, keep, curtain segments; the wall is one block).
- **Erosion:** each wave carries an energy budget ∝ (water depth at the castle)² (`--kappa 0.065`). It is spent on exposed, submerged cells, weighted toward the sea-facing side and the foot (the swash scours hardest at the bottom, `--scour 2.5`). The wall's sand erodes at 10% of that rate (`--kwall`; compacted, and its curved face throws the water back).
- **Statics after every change:** (1) a cell needs sand under it or a supported neighbour within 7 cells in its row (wet-sand overhang); (2) within each block, every part resting on a row must have its centre of mass over its contact span, else it slumps as a whole. Failures crumble into grains that fall under gravity and pile at ~27° (wet slump) or, in moving water, are washed away. Loose rubble under moving water is carried off (`--ltr 0.10`).
- **Water:** deterministic kinematic waves (not a fluid sim). Each wave shoals, steepens and breaks from x 848 (curling lip), lands at x 578 on its downbeat as a bore of 0.45 × its height. In Mochi's plot the run-up continues around/over her castle (distance 40 + 2.6 × bore). In Bolt's plot the wall stops it: the level at the face is capped at the crest, the rest becomes spray thrown seaward plus a reflected hump. The two biggest waves overtop by a little (weir-style volume ∝ excess^1.25); that water drains into the moat (max 24 px). Bolt's castle is never touched.
- **Flags** are anchored to a top cell; they fall, then rest on the sand or float. Bolt plants a tiny mint flag at cadence + 0.55 s.
- Growth: wave height ×1.5 per beat (8 waves: 10, 15, 23, 34, 51, 76, 114, 171 cm).

## Timeline (clip s; clip = sim + 0.267)
- **0.0 s:** both castles complete, Mochi's tower flags still being planted; wave 1 (10 cm) is running in and laps both at **0.27 s** (Bolt's wall sprays).
- **0.5 / 1 / 2 s:** Mochi's second flag pops (0.25 s), wave 1's backwash; Mochi's 3rd flag + pat on the beat (1.07 s); wave 2 (15 cm) lands at 1.87. Mochi laughs, "JUST A WALL?" from 1.54 s.
- **3.47 s:** wave 3 (23 cm): first crumble, −3%. "BLOCKED!" on Bolt's wall from wave 4.
- **5.07 s:** wave 4 (34 cm): Mochi's right tower is undercut and slumps (−14%), its flag floats off.
- **6.67 s:** wave 5 (51 cm): −5%. Mochi worried.
- **8.27 s:** wave 6 (76 cm): the keep is undermined and collapses (−53%). **Lead change 8.55 s:** Bolt's 56 cm castle is now TALLER than her 51 cm stub; "THE WALL HOLDS!". Mochi "wow"; Bolt laughs.
- **9.87 s:** wave 7 (1.14 m): the run-up wraps around her remains, −9%; one tower + flag left.
- **11.47 s (cadence, bar-8 downbeat):** wave 8 (1.71 m) curls in, lands, flattens the last tower (0% at ~12.0 s), runs up and soaks Mochi (seaweed lands on her head, drips). Bolt's wall breaks it (spray curls back, a little overtopping fills the moat). "BOLT WINS!", gold glow on his castle, tiny flag (12.0 s), "FLATTENED!" over Mochi's plot. Mochi annoyed; Bolt cheers, laughs, then a smug look.
- **13.77–14.37 s:** dissolve into the pre-roll (intact castles); the HUD switches at the midpoint.

## Sound (music first)
- **Piece:** Bedřich Smetana, *Má vlast* No. 2 **"Vltava" (The Moldau)**, the main theme (1874; Smetana d. 1884, PD). A sea/water piece that swells: fits a beach showdown with rising waves. Not on any used/banned list; no other scene uses it. Not kid-coded.
- **Source:** hand-read (pitches, rhythm, chord symbols) from Wikimedia Commons "Smetana Die Moldau Hauptthema harmonisiert.png" (CC BY-SA 4.0 engraving of the PD composition; only the notes are used), saved with `SOURCE.txt` at `<SOUNDFONTS_DIR>\scores\smetana_vltava\`. Downloaded 2026-10-25.
- **Excerpt:** pickup + bars 1–8 (E minor, 6/8), one steady tempo: dotted quarter = 0.80 s (bar 1.6 s). Each wave lands on a bar downbeat; the 8th on the bar-8 cadence, voiced E **major** (the work's own E-major reprise key) for the win.
- **Arrangement** (lib/orchestra, MuseScore_General): violins on the tune an octave down; strings + oboe from bar 3; flute + horns from bar 5; Smetana-style rippling 16th arpeggios on harp (clarinet from bar 3); cello/contrabass + pizz bass; soft string pad; timpani on waves 3–7, a roll into the giant wave; cadence tutti (strings, brass, horns, violins, contrabass, timpani, harp sweep). CC11 crescendo 0.62 → 1.0.
- **SFX** (all tonal, no noise):
  - each wave: a **tonal swell** (three chord tones of its landing bar, squared attack, 6 Hz shimmer, slight upward glide) cresting on the downbeat;
  - Bolt's wall: a deep tonal **thud** on the bar's bass note + pitched spray droplets on the 16th grid (2 + k per wave);
  - Mochi's plot: a splash bloop + run-up droplets on the eighths;
  - **sand patter:** every erosion/collapse frame gathered on a 32nd grid → tiny pitched ticks on chord tones; collapses ≥ 25 cells add a low thud;
  - pats/flag pops at the start, flag landings, Mochi's soak (bloop + pat), Bolt's flag tick + a 4-note E-major ding.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 862 frames = 14.37 s.
- −13.98 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −19.7 −18.2 −18.0 −17.2 −17.5 −16.8 −17.1 −16.4 −16.0 −15.8 −15.4 −14.2 −13.7 (cadence) −17.6 (hold), then the silent tail.
- SFX events/s: 6 8 9 14 5 23 12 12 18 13 23 15 14.
- Mochi % left after each wave: 100 → 99.9 → 96.7 → 82.4 → 76.9 → 24.1 → 15.1 → 0. Bolt: 100 throughout; wall 545 → 478 cells (88%).
- flash_check PASS (0 flashes, mean luminance 0.044).
- Seam (check_clip): 0.587 mean delta encoded (within 0.12–0.72).
- Frames read from the mp4: 0, 0.5, 1, 2, 5.3, 8.45, 8.7, 11.0, 11.55, 11.7, 13.0, 13.9, 14.2; 1:1 crops of the keep before collapse (8.45), the giant wave landing (11.55) and the end state (13.0).

## Doubts
- Waves 1–2 are small (10–15 cm by design); the first 2 s rely on the flag pops, pats, laugh and the spray off Bolt's wall. Second 4 has only 5 SFX events (between waves 3 and 4).
- The cause of Bolt's win reads by ~3.5–5 s (BLOCKED! + spray vs Mochi's crumble), not in second 1.
- The giant wave's front at landing is a near-vertical polygon edge with foam blobs: readable, a bit crude at 1:1.
- The wall loses its curved lip to erosion; at the end it looks like a plain block.
- Cartoon cheats: run-up "around" Mochi's castle (3D flow drawn in 2D); the wall caps the water at its crest; the seaweed snaps onto Mochi's head; sand grains draw over her while she is soaked.
- E-major cadence is an arrangement liberty (the theme's bar 8 is E minor in the source).

## Args and cost
- Args: `--kappa 0.065`, `--scour 2.5`, `--loosew 1.3`, `--washp 0.3`, `--ltr 0.10`, `--sheetk 0.70`, `--runk 2.6`, `--kwall 0.10`, `--sfx 0.34`, `--findb 2.0`, `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--resim`, `--nocap`, `--label`.
- The simulation (~40 s) is cached as `output/sandcastle_wave_sim_<params>.pkl`; pass `--resim` after editing sim code. Full HD render ~45 s at 2 encoder threads (with a cached sim).
- Owner review: pending.

## Outcome
- (fill after upload)
