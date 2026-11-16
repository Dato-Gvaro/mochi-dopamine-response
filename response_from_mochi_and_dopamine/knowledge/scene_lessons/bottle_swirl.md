# bottle_swirl: SWIRL it or just FLIP it? (batch73, NEW; replaces honey_straws)

- Brief: docs/BRIEF_batch73.md §1 (owner idea, the Naked Scientists demo). New file `scenes/bottle_swirl.py`.
- Measured totals: Naked Scientists "Hurricanes in a Lemonade Bottle", 2 L bottle: ~20 s inverted, ~10 s swirled. Mechanism: Caquas, Pastur & Genty, Phys. Rev. Fluids 9, 064701 (2024).
- Model (no CFD): outflow q(t) drives everything. Bolt: 65 glugs over 20.0 s (3.25/s, duty 0.55, blunt trapezoid slugs, 31 cm³ each). Mochi: 5 glugs to 1.55 s (155 cm³), then a vortex at 228 cm³/s (0.25 s ramp, 0.5 s taper) → empty at 10.0 s. Orbital swirl motor 0-1.5 s; air core grows 1.0 → 1.6 s.
- Geometry: bottle profile solved to 2.12 L brimful (2 L fills 32.8 cm of 34.8); beaker r 6 cm, 2 L at 17.7 cm; 15 px/cm. Bubble = that glug's water volume; stream width = 2√(q/(πv)) with v = 60 cm/s + g·τ; beaker level = volume out.
- Clip: 1.5x real time (labelled), frame 0 = real 0.7 s; Mochi EMPTY at 6.20 s, Bolt at 12.87 s; hold 1.8, dissolve 0.5 → 15.17 s.
- Music: Schubert D 774 voice line (Mutopia PD, new to the channel; <SOUNDFONTS_DIR>\scores\schubert_auf_dem_wasser\), one harp note per 0.1 L poured by either side; a gloop per glug; a flow-following hiss; chord + timpani on each EMPTY.
- Coordinator still review: OK; asked for a more visible vortex → core radius 0.46-0.6 cm (+ white edge), tracers alpha 0.85 / 4.5 px.
- Checks (encoded Full HD, b73a): 910 f = 15.17 s; −14.01 LUFS, peak −6.3; flash PASS; seam 0.43; events/5 s 24 → 10 → 6 (Mochi finishes mid-clip).
- Doubts: falling event rate after Mochi's finish; the glug rhythm is modelled; 1.5x playback.
- Delivered: <VIDEOS_DIR>\MochiAndBolt\review\batch73\bottle_swirl.mp4. Owner review: pending.
