# pilot_one_trip — Bolt REFUSES to make 2 trips: can he carry ALL 20 bags in? (pilots, 2026-10-28)

- Brief: docs/BRIEF_pilots.md (pilot 1, "everyday situation" test). New scene file; lib/ and tools/ untouched. Characters (lib/toon), caption/HUD/banners and the sound/mastering chain copied from snowball_fort.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\pilots\pilot_one_trip.mp4` (**v1**, Full HD 9:16, 18.00 s, 1080 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Bolt ~REFUSES~ to make 2 trips:" / "can he carry ~ALL 20~ bags in?"

## v2 (batch55, 2026-10-28): a REAL physics stack
- Owner on v1: "interesting, but it lacks physics/simulation stuff. Maybe he stacks them in some way so they stack for real, and we show angles and movement in little details around it?" Brief: docs/BRIEF_batch55.md.
- Deliverable: `MochiAndBolt\review\pilots\pilot_one_trip.mp4` (v2, Full HD, 18.00 s, 1080 frames, label v2). v1 → `MochiAndBolt\archive\pilot_one_trip_v1.mp4`; v1 script kept at scratch `m55/pilot_one_trip_v1.py`.
- Same story, music, caption, camera, door/PULL gag, lintel twist, oranges, eggs. What changed:
  - **Real weights:** every bag has a kg (water 9, melon 4, detergent 3 … pizza 0.5), shown as a sticker; the physics uses them. HUD: BAGS n/20 + LOAD kg (42.9 kg at 20).
  - **The stacking rule:** Mochi tosses at the middle of the stack, off by N(0, 22 px). The bag rests where EVERY sub-stack's centre of mass stays on the top face of the bag below it (5 px margin) — the classic overhang condition; if her aim is outside that interval it slides (0.16 s) to the nearest balancing spot (2 visible slides: #16 at 5.5 s, #19 at 6.5 s).
  - **Squash:** each bag is compressed by the kg above it (paper 24 %, totes 20 %, boxes 4–10 % at ≥14 kg); the stack height uses the squashed heights.
  - **Balance (why it holds):** inverted pendulum on his head. His steady balance is only 0.25 × the full stack's tipping stiffness (M g hc), so past ~10 bags it drifts and he catches it with head jerks (intermittent control: he reacts 0.10 s after the plumb line passes 40 % of the way to his head's edge). Each jerk = a **BALANCE SAVE** (counter, 25 in the clip, 1 → 4 per second toward the door); his body leans with the jerk (gold angle mark at his feet, e.g. "4°").
  - **Overlays:** the stack's centre of mass (quartered dot), its dashed plumb line down to his head, his head's flat top as a support bracket (half-width 0.6 CR = 27.6 px), the tilt arc + "2.0°" next to the stack; colour mint → amber → red with the margin. "CENTRE OF MASS" tag for the first 3.6 s.
  - **TILT gauge (HUD, ±16°):** the needle = plumb-line angle; the red zone starts at the tipping angle atan(a / hc), which closes in as the stack grows (TIPS AT 38.9° → 15.4° → 7.2° → 6.4°).
  - **Details:** a loose orange rolls in each orange bag ((5/7)(g sinθ − a cosθ), knocks the bag wall = a soft marimba tick), tote handles swing (damped pendulums driven by the stack's motion), the two hand totes swing as in v1.
  - **Why it falls:** the lintel catches bags #6–#20; its knock spins the column back while it drops (0.64 rad/s, FITTED to just past the corner + 0.05 rad) so it lands on its back corner leaning 16.5°, past 13.6° where its COM is over the corner: the red plumb line lands BEHIND its base ("CENTRE OF MASS OFF ITS BASE", gauge "TIPPED!") and gravity tips it over, then the v1 tumble.
  - The v1 limbo lean was dropped (a −6° lean is past his tipping angle; it could not have held). He just walks in.
- Sim (seed 11, `--aim 22 --kratio 0.25 --cfrac 0.40 --react 0.10 --w0 0.03 --kick 0.5`): worst plumb-line excursion 0.95 of his head's half-width at 1.15 s (the 9 kg water lands off-centre: TILT 13.3° vs TIPS AT 15.4°), 0.7–0.83 at the door beats; it never tips (checked per second in `--report`). Seeds 4, 6, 8, 13–15 tip somewhere (>1.0) and were rejected; 12 holds but never gets close.
- Sound: v1's + a wooden tok + tick per save (pitched to the harmony, louder/brighter the closer to the edge) + orange knocks. SFX events/s: 8 11 14 8 14 13 21 8 10 12 14 16 10 9 7 30 32 (v1 dipped to 2–3 at 12–14 s).
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 1080 frames = 18.00 s; −14.01 LUFS, peak −2.00 dBFS, last 0.5 s −78 dBFS; flash PASS (0, mean lum 0.06); seam last→first 1.43 vs 1.10 for the frame 0→1 step (a bag lands on frame 0). Frames read: 0.5, 1.15, 1.55, 5.6, 13.4, 15.1; stills 0–1060 + 1:1 crops of the overlay at 5.6 / 11 s.
- **v2 doubts:** the camera is at 1.0 from 9 s, so the kg stickers (15 px) and the overlay are small on a phone; the head-jerk "saves" are a modelling choice (intermittent control) and the lintel spin is fitted; the in-door stack is still partly hidden by the tall tower.
- **Story:** Mochi tosses the shopping from the car boot onto Bolt (BAGS 4 → 20, one per melody note) while he walks to the house and hops up 3 steps. At the door: no hands free (two totes in his hands), he bumps it twice, it says PULL. Mochi strolls up empty-handed, pulls it open (he dodges back), he limbo-leans and walks in. The door is 2.15 m: the frame stops every bag above the lintel; that 15-bag column drops onto the porch on the cadence, tips over backwards and tumbles down the steps; oranges bounce down the steps; the egg carton (bag #20, on top) lands last: EGGS 12/12 OK. HUD: INSIDE 5/20. Bolt's stare from the doorway, Mochi's deadpan at the door.

## Car redraw + ship (batch56, 2026-10-28)
- Owner on v2: "good, but their car looks like an AI-generated deformed car". Only `draw_car` changed (new helpers `car_body_path`, `car_window_path`, `draw_wheel`, constants `CAR_*`); sim, sound, camera, story untouched. v2 script kept at scratch `m56/pilot_one_trip_v2.py`.
- **The car now:** a compact SUV in true side view at the scene's 100 px/m (door 2.15 m = 215 px), facing left, front off-screen: height 1.65 m with ONE straight roofline + roof rail, beltline 1.10 m, ground clearance 0.22 m, rear overhang 0.82 m, wheelbase 2.62 m; tyres r 34 px (0.68 m) centred at Y_G − 34 so they sit ON the path, concentric arches + dark liners, 5-spoke rims, a soft contact shadow. Rear door + quarter glass (tinted, one reflection streak), blacked-out B/C pillars, raked D-pillar, door seam, handle, fuel flap, shoulder crease, lower cladding, tail light on the body corner. **Open tailgate:** a slab hinged on the roof's rear edge, 1.12 m long, raised 22° above horizontal (tip 1.0 m above Mochi's head), its rear window edge-on, its light strip, a gas strut, a warm boot lamp.
- The remaining shopping shows through the side glass (bags stacked from a 0.80 m boot floor, 6 per row; a baguette / tote handles / bottle necks / greens stick up so even the floor row peeks over the beltline). The old 2.8 m-tall body and stick hatch are gone.
- Shipped 4K: `MochiAndBolt\schedule\2026-11-05\2_pilot_one_trip.mp4` (slot 2, 16:00 local Nov 6 = 07:00 US East Nov 6). FHD v2 review copy → `MochiAndBolt\archive\pilot_one_trip_fhd.mp4`.
- **Checks (encoded 4K):** h264 High yuv420p 2160x3840 @ 60, 1080 frames = 18.00 s; −14.01 LUFS, peak −2.00 dBFS, last 0.5 s −78.3 dBFS; flash PASS (0, mean lum 0.059); seam 1.26. Stills read: 0, 3, 5.5, 10, 16.7 s + 1:1 crops of the car at 0 / 3 / 5.5 / 10 s; encoded frames 0.5 s (1:1 crop of the car at 4K), 4 s, 12 s.
- Pinned comment staged as "saved it **24** times": the HUD counter tops out at ×24 (it freezes at the lintel hit; `--report`'s 25 includes one after it), the review README said 25.

## Layout (side view, dusk)
- Path y 1210; 3 steps (45 × 34 px) from x 500; porch y 1108 from x 590; door x 690–800, lintel y 893 ("DOOR 2.15 m" label from frame 0, a PULL plate on it).
- Car (batch56: compact SUV side view, tailgate up, remaining bags behind the side glass) at the left, rear bumper x 250, roof y 1045. Mochi x 330 → 852 (right of the door). Bolt x 450 → 745.
- Camera: ONE smooth zoom-out 1.35 → 1.0 between 2.4 and 9.0 s (frame 0 is close on the boot + both faces + the door; the full 20-bag stack fits by the time it is built). No other camera move.
- HUD (y 1366–1526): BAGS n/20 + bar, TRIPS: 1 → INSIDE 5/20, STILL OUTSIDE: 15. Key content inside x 0.10–0.84w (the car and the house's right side are decoration).

## The physics
- **Throws:** each bag flies a true parabola (0.55 s, g 1800 px/s²) aimed at the predicted stack top; the landing offset (aim noise σ 6 px + prediction error) is clipped to ±9 px from the bag below (it cannot hang off).
- **The stack:** a rigid inverted pendulum on his head (COM, inertia from the bags' masses: water 2.4, melon 2.2, detergent 1.8, eggs 0.6 …). Driven by the pivot's accelerations (his walk steps, hops, bumps, dodge) and the landing kicks. His balance is a restoring torque of FIXED strength = 1.30 × the full 20-bag tipping stiffness (M g h); every bag shrinks the margin, so the sway gets slower and bigger. Lean: ±3° while loading, −4° on the steps, +7° at the door bumps, −17…−27° in the limbo (a deliberate lean back, `--limbo`).
- **The lintel:** at t_hit 14.54 every bag whose top is above y 893 is caught (bags #6–#20); #3–#5 go in with him (+2 totes = 5 inside). The column falls 193 px (free fall) → porch impact **15.003 s = the cadence**; it tips backwards about its lowest bag's bottom-left corner (gravity torque, the impact's off-centre start) to 35°, then every bag flies on with its rigid-body velocity + spin, lands on the steps/path (under its middle) and settles upright/upside-down. Landings 15.5–16.0 s.
- **Oranges:** the two orange bags spill 6 each on landing → lib/physics2d circles (e 0.48) bouncing down the steps: 39 bounces, each a marimba note.

## Sound (music first)
- **Piece:** Luigi Denza, *Funiculì, Funiculà* (1880; Denza d. 1922, PD), the chorus. Not on any used list; Neapolitan, adult, famous worldwide, not kid-coded.
- **Source:** Wikimedia Commons MIDI "Funiculì funiculà.mid" (melody track, E-flat), cross-checked note for note against "Melody to Funiculi Funicula.mid"; saved with SOURCE.txt at `<SOUNDFONTS_DIR>\scores\denza_funiculi\`. Only the melody is taken; the harmony was re-derived as chord symbols (C7 … C#dim7, Dm7, E7b5, Am, F7/C, B♭, B♭m, Bdim7, F/C, C7, F) and voiced anew.
- **Excerpt:** F major, 6/8, dotted quarter = 120 (bar 1.0 s), chorus bars 1–15 + the F-major cadence (bar 16 = the crash).
- **Arrangement** (lib/orchestra): violins on the tune, clarinet 8vb, a pizz doubling (mandolin colour) from bar 5, flute 8va on the "funiculì" bars; 6/8 lilt: contrabass + tuba on 1 and 4, pizz chords on 2-3 / 5-6, an accordion (GM 21, added at runtime) holding the harmony; timpani roll into the cadence; the cadence = timpani + bass drum + F-major tutti + harp sweep.
- **SFX** (tonal): bag on the stack = soft thud + 2 crinkle ticks (ON the melody notes); Mochi's toss; footsteps/hops; 2 wooden knocks (door bumps); door click + a soft tonal glide; the lintel BONK; the column thump (cadence); bag landings descending the F chord; orange bounces = marimba notes down the F chord; eggs OK = 4-note chime.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 1080 frames = 18.00 s. −14.01 LUFS, peak −1.99 dBFS, last 0.5 s −84 dBFS.
- RMS/s: −18.6 −18.1 −17.9 −17.7 −17.4 −17.2 −17.0 −16.9 −17.0 −16.6 −16.6 −16.0 −15.9 −15.8 −16.7 −12.9 (cadence) −15.0 −24.8.
- SFX events/s: 8 9 14 6 10 11 15 6 8 10 12 6 2 3 2 31 35 2.
- flash_check PASS (0 flashes, mean lum 0.063). Seam mean |Δ| 1.05 (adjacent frames 0.4–0.9): frame 0 is bag #4 landing + the counter 3→4, i.e. the first event sits on the loop point.
- Frames read from the mp4: 0.5, 1, 2, 6.9, 11.2, 13.2, 14.3, 14.9, 15.3, 15.8, 16.5, 16.6, 17.3. Stills 0–1060 (≈25).

## Doubts
- The stack is small on a phone once the camera is wide (bags 70–104 px); the payoff (bags in a row on the path, oranges) is readable but not huge.
- The door opening (13.0 s) is mostly hidden behind the tower; the PULL joke is carried by the plate + "NO HANDS FREE!" more than by the swing.
- Cartoon cheats: a 6.5 m stack on his head; the collapse is a rigid tip-over then free flights (no bag-bag collisions: landed bags lie side by side/overlap in depth).
- Event rate dips at 12–14 s (door beat: 2–3 events/s) before the crash (31–35/s).

## Args and cost
- `--g --seed --kratio --damp --kick --aim --landmax --bumpdx --limbo --zoom --seed2 --sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~70 s at 2 encoder threads.
- Owner review (batch55): "add physics" → v2 to review.

## Outcome
- (fill after upload)
