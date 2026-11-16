# ol_rupert_drop (DopamineEXE, batch62 #4)

## v1 (2026-10-31)
A Prince Rupert's drop (head 12 mm across, curling 26 mm tail) on a steel anvil, seen through crossed circular polarisers (black field, stress fringes in interference colours). A 0.5 kg drop hammer hits the head 5 times, every hit's peak force 2× the last (0.5 → 8 kN): nothing. Then side cutters snip the tail: a crack front runs to the head at 1,800 m/s and the whole drop turns to glitter in 18 µs (SLOW-MO ×100,000), then falls onto the anvil (SLOW-MO ×10).

- Caption (baked; `--cap ''` = base): `Every hit is ^2× HARDER^…|can ANYTHING break this ~GLASS~?` True: each hit's peak force doubles (model values), and the answer (a snip) is shown.
- Banners: "NOT A SCRATCH" + "lab tests: it survives a 15,000 N squeeze"; finale "the TAIL was / its weak spot". Name on screen once: "PRINCE RUPERT'S DROP" (engraved on the anvil) + a 5 mm scale bar.

## Published numbers (verified 2026-10-31)
- Surface compression 400-700 MPa; the head survives 15,000 N between tungsten-carbide platens; survives "impact with a small hammer": Aben, Anton, Õis, Viswanathan, Chandrasekar & Chaudhri, Appl. Phys. Lett. 109, 231903 (2016) (abstract quoted by Purdue's 2017 release, purdue.edu/newsroom/releases/2017/Q2/research-solves-centuries-old-riddle-of-prince-ruperts-drops.html). On screen: "SKIN: up to 700 MPa (squeezed tight)", "15,000 N squeeze".
- Crack front up to 1,900 m/s, finger-like bifurcations (Chandrasekar & Chaudhri, Phil. Mag. B 70, 1195 (1994)); Purdue: "more than 4,000 mph" (= 1,790 m/s). On screen: "CRACK FRONT 1,800 m/s".
- NOT published (model values, not labelled as measured): the hammer forces (Hertz contact, below), the fragment speeds, the drop's exact size.

## Model (`simulate`, ~20 s CPU, cached)
- Geometry: head circle r 120 px (1 mm = 20 px) at (330, 800) ∪ a tapered tube (r 70 → 3.5 px, e-folding 95 px) along a curling centreline (600 px), smooth-min union (k 22).
- Fringes: retardation δ (nm) = head rings 40 + 2,496·s²√(1−s²) (s = r/R) blended with the tail 260 + 1,150·√(1−s²)·√(a/40); colour = Michel-Lévy (I(λ) = sin²(πδ/λ) integrated over 400-700 nm with 3 Gaussian channels), S capped 0.80. A hit adds a Flamant point-load term 15,000·F[kN]·cosθ/r (circles tangent at the contact) that decays with τ 0.16 s (visual afterglow of a µs event).
- Hammer: m 0.5 kg; Hertz steel-on-glass (E* 55.1 GPa, R 6 mm): ½mv² = (8/15)E*√R δ^(5/2), F = (4/3)E*√R δ^(3/2) → drop heights 0.8, 2.6, 8.1, 25.8, 81.9 mm for 0.5/1/2/4/8 kN. Shown at SLOW-MO ×4 (labelled); rebound e 0.35, winch-up between hits.
- Crack: geodesic distance (Dijkstra, 3 px grid) from the cut (u 520 px) through the glass; front at 1,800 m/s × ×100,000 = 360 px/s; crack branches = random walks up the distance gradient with 3.5%/step bifurcation (~430 branches). Path length 32.6 mm → **18.4 µs**.
- Shards: Voronoi cells of a jittered 5.5 px grid (1,781 shards), coloured by the fringe colour under them, released when the front passes; outward from the local axis 0.06-0.42 m/s (head; ×0.6 tail) + 0.02-0.14 m/s up (model). Clock ramps ×100,000 → ×10 over 0.55 s after the burst; gravity in real time; shards land on a heightfield pile (3 px bins, repose step), 1,394 land on the anvil. The cut tail end falls intact.

## Timeline (80 bpm)
- Hits 0.10 / 0.85 / 1.60 / 2.35 / 3.85 s; NOT A SCRATCH 3.97-5.1; cutters in 4.45-4.95; **snip 5.35**; head reached ~6.5; **shattered 7.19 (18 µs)**; glitter lands 7.4-9; final chord 9.10; "the TAIL was its weak spot" 7.64→; dissolve 10.9-11.5. **11.5 s, 690 frames.**
- Frame 0: the intact drop, hammer 0.8 mm above the head, meter + ✂ end rung, "0.5 kN" counter.

## Screen
- Counter y 1500: HIT FORCE "n kN" + ×2 pill + HIT n/5 pill → after the snip a µs clock "SINCE THE SNIP" → gold "18 µs TO SHATTER". Meter y 1300: 0.5 · 1 · 2 · 4 · 8 kN · ✂ (gold at the snip). Readouts: DROP n mm / HAMMER 0.5 kg (hammer phase), CRACK FRONT 1,800 m/s (crack phase), SLOW-MO ×n (top right, live). Watermark 35%.
- Side safe zone: drop x 210-720, anvil 150-880, text ≤ 884. Cutters slide off to the right at the end (decoration).

## Sound
- F. Chopin, Prelude Op. 28 No. 20 in C minor (1839, PD), Mutopia (typesetter PD), `<SOUNDFONTS_DIR>\scores\chopin_prelude_op28_20\SOURCE.txt`, read at runtime. Bars 1-2 at 80 bpm (the ff chords: piano + brass + strings + contrabass; timpani on every hit, a roll into hit 5), the snip on beat 7, then bar 12 (pp) under the crack and glitter, the final C-minor chord at 9.10 (+ strings + harp roll). Replaces the brief's Grieg concerto (no PD score data reachable: not on Mutopia, IMSLP has no MIDI/MusicXML).
- SFX: glass-on-steel TINK per hit (C-minor tones, +12 ms), a dry "tik" snip, a falling line of small glass tinkles as the front passes (≥14 ms apart), tiny tinkles for glitter landing.

## Checks (encoded mp4, output/ol_rupert_drop_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 690 frames, 11.50 s; **-14.01 LUFS**, peak -6.34 dBFS, last 0.5 s digital silence; flash_check PASS (0 flashes, mean lum 0.016); seam mean |Δ| 0.271.
- Stills read at 0.12, 1.62, 3.88, 4.6, 5.15, 5.9, 6.75, 7.25, 7.7, 8.6, 9.6, 11.3 s; 1:1 crops of the drop at 4.6 s and the SKIN chip at 2.0 s.

## Flags
`--label`, `--cap`, `--still --frame a,b`, `--dry`, `--audio`, `--resim`, `--sfx`, `--sound 0`.

## Upload draft
- `Every hit 2x harder… can anything break this glass? 🔨 #satisfying #physics #shorts`
- `A hammer can't break it. A tiny snip makes it explode 🔨 #satisfying #physics #shorts`
- `The glass drop that survives a hammer but not a snip 🔨 #satisfying #physics #shorts`
- Pinned: `the tail is its only weak spot. did you know these exist?`

## v2 (2026-11-01, owner review: "better visible force… at the end say weak spot")
- `--v2`, same sim. Per hammer hit: a FORCE bar right of the drop (x 852, 0-16 kN linear, dashed gold "LAB 15 kN" line = Aben et al.'s squeeze), jumps to the hit's model force in 0.04 s and decays (0.30 s), ghost tick per past hit, value ("0.5 kN"…"8 kN", rung colour) pops above the bar; a rainbow ring bursts from the contact point (radius by force); the Flamant fringe term is drawn ×2.2 stronger with τ 0.28 s (v1 0.16; a visual afterglow of a µs event, exaggerated on purpose); world shake 1.5 px (0.5 kN) -> 14 px (8 kN), decay 0.09 s. Bar fades before the snip.
- End card "WEAK SPOT:" / "THE TAIL" (v1 "the TAIL was / its weak spot").
- Deliverable `<VIDEOS_DIR>\DopamineExe\review\fixes_1101\ol_rupert_drop_v2.mp4`. 11.50 s, -14.01 LUFS, peak -6.34, silent tail, flash 0 (with the shake), seam 0.28. v1 -> archive/ol_rupert_drop_v1.mp4.

- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-13\1_ol_rupert_drop.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 690 frames, -14.01 LUFS, peak -6.34, flash 0, seam 0.17. Full HD -> archive/ol_rupert_drop_v2.mp4.
