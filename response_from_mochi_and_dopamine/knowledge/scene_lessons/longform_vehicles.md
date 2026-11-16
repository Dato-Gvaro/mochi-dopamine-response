# longform_vehicles: "Every crushed vehicle splits into 3... from a SUPERTANKER to a SKATEBOARD"

- Brief: docs/BRIEF_longform3.md (owner 2026-11-10, 18-vehicle list confirmed "ok build").
- Fork of `scenes/longform_atom.py` (the "Crushing the Sun" video, `--crushers` path); longform_atom.py untouched. Drawings: `lib/vehicles.py` (18 generic side-view illustrations, 3 detail tiers by on-screen length; `BODY` = each vehicle's 5-disc physics template).
- Status (2026-11-10, v5 step 4): weapons + per-chapter gravity (G_S 3.5, restitution 0; the table below was written at S=2.5), ships rocking, size-pitched thuds IN the sim. R0_1 490 (jar 1 top 378, MAX 340), jar 2 Z 1.49 (top 350). 84 s FHD test longform_vehicles_test_v5.mp4 (jet forced to n=9 with LFV_TEST_JET=9): -14.01 LUFS, flash PASS. First-hit SFX weak for rifle n2 / charge / jet. Full build + render not started.
- v5 fixes (render-time, no rebuild needed):
  - whole-jar glass cracks/shards are edge-only (`soft`/`edge_only`), no web over the pile;
  - water only in jar 1 ship chapters (`water_level`, drains 2 s from the first moon-rocket pop);
  - drawn MAX line = `jar_lines()` (median of 12 column tops at payoff);
  - audio: weapon hits louder + thunk, bed -23 LUFS pre-master (was -20), 7 dB duck at each first hit.
eview\longform3\`, waiting on the coordinator's review of the drawings. No test clip yet, no full render, no 4K.
- Build: `python scenes/longform_vehicles.py --report` (~35 min: jar 2 ~8 min, the column ~20 min; output/longform_vehicles_build_cr_j3_s1.pkl). Stills: `NF_FAST=1 python scenes/longform_vehicles.py --cache --label rev --still --frame 0.7s,...`. Sheet: `--sheet <png>`.
- Column check: side margin 41 px, fewest vehicles in view 132 (the bicycle chapter: big, open shapes); the floor margin is negative only in the ram chapters (the plate is drawn), as in the Sun video.
- Crusher looks drawn (themed, over the families): anchor, shipping container, sling load, junkyard magnet, scrapyard baler, hangar doors, railway buffers, launch pad, car lift, dry-dock pile driver, road compactor, car crusher, artillery shell, bike pump; press + wrecking ball as in the Sun video. Each look has its own extra SFX on top of the family's.

## v5 (owner 2026-11-10): WEAPONS replace the crushers + real WEIGHT (plan + FAST stills; not built yet)
- Spec: docs/BRIEF_longform3.md, the two "DECISION 2026-11-10" sections.
- The crushers are gone. **Mochi sits bottom-left (x 120), Bolt bottom-right (x 1800)**, in their exact rest shape. Their weapons float beside them (Mochi's at x 250, Bolt's red button at x 1670). The HUD stays in the two top corners, clear of both. The vehicles span the whole frame.
- A hit vehicle breaks into 2 smaller ones (the counter stays exactly 2^n). They take turns, no score: Mochi on even n, Bolt on odd n. From n 80 both fire every round; at the finale (n 109) both fire together. A "NEW WEAPON" pill marks each weapon's first use.
- **n 3 = the giant airship** (245 m vs a rule size of 229 m): generic, no name or markings (lib/vehicles `_zeppelin`; `ORDER[3]`).

### Weapon plan (single target early, multi-target late)
- Rounds n 0-3 have 1, 2, 4 and 8 vehicles: one shot per vehicle, ~0.4 s apart.
- From n 4, one area hit breaks the whole set as a wave. The wave = the old crusher families' pop orders, with no plate or lid drawn:
  - ring from a point = radial;
  - chain through the contacts = hop order;
  - across the frame = x-order;
  - from the top = top hop order.

| n | Who | Weapon (first use) | Hits |
|---|---|---|---|
| 0 | Mochi | ALIEN LASER RIFLE | 1 shot; frame 0 = the supertanker hit mid-fall (the hook) |
| 1 | Bolt | RED BUTTON ROCKET | 2 rockets drop and explode |
| 2 | Mochi | (laser rifle) | 4 quick shots |
| 3 | Bolt | PIRATE CANNON | a broadside of 8 cannonballs |
| 4 | Mochi | SOUND CANNON | rings: radial |
| 5 | Bolt | TNT PLUNGER | a buried charge: radial from inside |
| 6 | Mochi | FREEZE RAY | a cone freezes the pile; it shatters in hop order |
| 7 | Bolt | ANVIL | drops: top wave |
| 8 | Mochi | TRACTOR-BEAM UFO | lifts the pile and drops it: top wave |
| 9 | Bolt | TESLA BUTTON | chain lightning: hop order |
| 10 | Mochi | PLASMA ORB | radial |
| 11 | Bolt | BOWLING-BALL LAUNCHER | rolls through: x-order |
| 12 | Mochi | MAGNET GUN | pulls the pile together: squeeze order |
| 13 | Bolt | CATAPULT | a boulder: radial |
| 14 | Mochi | GRAVITY FLIP | the pile flips up and slams down: top wave |
| 15 | Bolt | CLUSTER-ROCKET AIRSTRIKE | several rings at once |
| 16 | Mochi | SWEEPING LASER | a sweep across |
| 17-59 | alternating | the unlocked weapons, cycled (never the same weapon twice in a row) | |
| 60 | Bolt | TANK-BUSTER JET | strafe run: a stylised generic twin-engine jet crosses the frame; a bullet line rakes the rows; rockets drop; our own synthesized "brrrt" |
| 61 | Mochi | UFO MOTHERSHIP | a wide-beam sweep |
| 80-108 | both every round | pairs of weapons | the rate climbs |
| 109 | both | the jet + the mothership together | the nanocars, on the last chord |

- Explosions are fire + smoke + debris in warm mid-luminance colours, never white (lib/arsenal `explosion`). flash_check must pass over the whole 10 min. Empty vehicles only; no realistic real-world guns.

### Weight (owner: "bouncing like rubber ducks")
- Cause: one fixed G = 3000 px/s² at every scale, plus springy ball-jar contacts.
- Fix: per-chapter gravity from the real metres per pixel, g_screen = clamp(9.81 m/s² / mpp × S², 150, 3000) with S = 2.5 (the giants run at 2.5× real time: still slow, still heavy).
  - From the motorbike down it is clamped at 3000 px/s². At the micro scale real objects are drag-dominated, so this is honest enough; it is flagged here.

| n | Vehicle | Rule size | mpp | g real (px/s²) | g on screen (px/s²) |
|---|---|---|---|---|---|
| 0 | supertanker | 458 m | 0.403 m/px | 24.3 | 152 |
| 1 | cruise ship | 364 m | 0.403 m/px | 24.3 | 152 |
| 2 | ocean liner | 289 m | 0.403 m/px | 24.3 | 152 |
| 3 | giant airship | 229 m | 0.403 m/px | 24.3 | 152 |
| 5 | destroyer | 144 m | 0.403 m/px | 24.3 | 152 |
| 8 | jumbo jet | 72.1 m | 0.548 m/px | 17.9 | 150 |
| 10 | airliner | 45.4 m | 0.402 m/px | 24.4 | 152 |
| 13 | freight locomotive | 22.7 m | 0.201 m/px | 48.8 | 305 |
| 17 | battle tank | 9.02 m | 0.0798 m/px | 123 | 768 |
| 20 | family car | 4.51 m | 0.0399 m/px | 246 | 1537 |
| 23 | motorbike | 2.25 m | 0.0199 m/px | 492 | 3000 |
| 27 | skateboard | 89.5 cm | 0.00792 m/px | 1.24e+03 | 3000 |
| 35 | skateboard | 14.1 cm | 0.00125 m/px | 7.87e+03 | 3000 |
| 49 | skateboard | 5.55 mm | 4.91e-05 m/px | 2e+05 | 3000 |
| 68 | skateboard | 68.8 µm | 6.09e-07 m/px | 1.61e+07 | 3000 |
| 96 | skateboard | 107 nm | 9.44e-10 m/px | 1.04e+10 | 3000 |
| 109 | skateboard | 5.29 nm | 4.68e-11 m/px | 2.1e+11 | 3000 |

- Restitution 0: a landing kills the approach speed. Measured in the landing test: the supertanker falls 260 px (105 m) in 1.97 s, touches down at 185 px/s, and rises 0.0 px afterwards (no bounce); the 0.04 rad tilt settles flat. Stills: review\longform3\heavy_landing_and_airship.png.
- Dust: puffs scaled by the vehicle's size. Sound: a thud pitched by size (lower = bigger). Camera shake for the giants only (n ≤ 6: ~10 px, 0.12 s decay).
- Ships rock in the water in the ship chapters (n 0-5 and the hovercraft): a water band in the tank, buoyancy plus a slow roll. Planned, not built.
- Hits scale with real mass (∝ length³): the same weapon impulse gives Δv_screen = J / m / mpp. A laser barely nudges a supertanker (~2 px) and flings a scooter (~300 px).

### Duration estimate (v5)
- Same 110 splits.
- The single-shot series at n 0-3 add ~4 s.
- The slower giant falls in jar 1 add ~2-3 s per chapter; the micro rounds stay on the music.
- **Estimate ~10:15** (v3: 9:58.7). The planner gives the exact figure once the weapon timings are coded.

## v3 (coordinator 2026-11-10): past the skateboard into the micro world, to the 4 nm NANOCAR
- Rule unchanged: every crush makes 2 at 0.794x; counter exact 2^n. 110 crushes: 1 supertanker -> 2^110 = 1,298,074,214,633,706,907,132,624,082,305,024 nanocars.
- n 0-27: the 28 vehicles (as v2). n 28-109: no vehicle is this small, so the SKATEBOARDS keep shrinking (said on screen: "NO VEHICLE IS THIS SMALL... SO THE SKATEBOARDS KEEP SHRINKING"); each micro chapter = one deep jar of the column ending on a scale marker ("EACH SKATEBOARD IS NOW THE SIZE OF ..."), JAR FULL -> the floor gives -> the drop, as the Sun video's chapters. Real tiny machines (delivery drone 60 cm, pocket drone 10 cm, insect-sized flying robot 3 cm, millimetre microrobot 1 mm) are markers too, drawn in the card, at the n where their real size matches the rule (within ~10 %).
- Finale n 110: the real smallest car ever built, a single-molecule nanocar (~4 nm; the rule gives 4.2 nm), drawn as a molecule (carbon chassis, H/O atoms, buckyball wheels). The hydraulic press makes it (it opens the video too); the last chord on the payoff.
- Micro tools (one per jar, cycled): side vise, sound waves, bottom ram, laser pulse, drop weight, pile driver (Sun-video looks).
- Drawings: review\longform3\vehicles_micro_sheet.png (5 machines + the nanocar, 15 marker icons, the fixed small sprites).
- Weak-spot fixes: the excavator draws a solid, simple silhouette below 70 px (no lattice tangle); the jets/airliners draw a dark window band below 70 px; the pour gap: plan = a tighter pour camera (TODO in the build step).
- Pacing: strokes 8.0 s apart at the start, falling steadily to 3.7 s at the nanocar (the rate climbs to the end); 20 jars.

### v4 micro retention fixes (coordinator 2026-11-10; render-only, the v3 build stays valid)
- Problem: the micro section (~6 of 10 min) was one orange stick-and-dot mesh; the markers were only text.
- Fixes:
  - one hue per micro chapter (`MICRO_HUES`, changes at each marker);
  - solid silhouettes for the thin shapes in piles (`VH.draw_solid`: skateboard pill + 2 wheel dots, e-scooter, nanocar);
  - a "SAME SIZE" inset at each marker (1 skateboard and the marker object at the same real scale, held ~2 s, then shrunk into the strip cell);
  - no "10 TONS" on the micro drop weight.
- Stills: review\longform3\test_v4_micro_stills.png.
- Not done (optional): micro-themed crushers (pipette tip, AFM tip) would change the sim's tool physics, so they need a re-build; deferred.

### v3 build + tests (2026-11-10)
- Build: `python scenes/longform_vehicles.py --report` (~1 h on this laptop; T 598.75 s; jar 1 top 343, jar 2 326 at MAX 340; column check side margin 46 px, fewest vehicles in view 196).
- Tests: `NF_SCALE=1.0 python scenes/longform_vehicles.py --cache --label t3a --window 185,252` (5.5-6.4 fps) and `... --label t3b --window 558.75,598.75`.
- Encoded checks for both:
  - h264 yuv420p 1080p60;
  - -14.01 LUFS;
  - flash_check PASS (0, and 4 with worst 1 s = 2);
  - no black.
- Sound rise at each wave's first pop: +3.6 to +8.4 dB, except the sound-waves chapter (+0.4 to +3.3).
- New code:
  - the micro top-right card (skateboard size, the next marker's icon, "= THE SIZE OF ..." at a marker);
  - the micro progress strip (28 vehicles done, 19 markers, nanocar GOAL);
  - banners only at markers in the micro world;
  - the nanocar finale card (all 34 digits);
  - the pour camera framed from the MAX line down (was from the press head: an empty frame).
- Weak spots:
  - thin shapes (scooters, skateboards, nanocars) read as a mesh in big piles;
  - the micro drop weight still says "10 TONS";
  - the sound-waves pops are soft.

### v3 plan (planner; `python scenes/longform_vehicles.py --plan`)
| Ch | n | Vehicle (crushed) | Real length | Rule length | Crusher look (family) | Jar | Stroke |
|---|---|---|---|---|---|---|---|
| 1 | 0 | supertanker | 458 m | 458 m | HYDRAULIC PRESS (press) | 1 | 0:01.2 |
| 2 | 1 | cruise ship | 365 m | 364 m | SHIP'S ANCHOR (anvil) | 1 | 0:09.1 |
| 3 | 2 | ocean liner | 269 m | 289 m | DRY-DOCK PILE DRIVER (piledriver) | 1 | 0:17.0 |
| 4 | 3 | bucket-wheel excavator | 225 m | 229 m | SCRAPYARD BALER (vise) | 1 | 0:24.7 |
| 5 | 4 | submarine | 173 m | 182 m | SHIP'S ANCHOR (anvil) | 1 | 0:32.4 |
| 6 | 5 | destroyer | 155 m | 144 m | DRY-DOCK PILE DRIVER (piledriver) | 1 | 0:39.9 |
| 7 | 6 | moon rocket | 111 m | 115 m | LAUNCH PAD (ram) | 1 | 0:47.4 |
| 8 | 7 | giant cargo plane | 84 m | 90.9 m | HANGAR DOORS (vise) | 2 | 0:53.8 |
| 9 | 8 | jumbo jet | 73 m | 72.1 m | SHIPPING CONTAINER (anvil) | 2 | 1:01.1 |
| 10 | 9 | hovercraft ferry | 56 m | 57.3 m | SLING LOAD (anvil) | 2 | 1:08.3 |
| 11 | 10 | airliner | 44 m | 45.4 m | HANGAR DOORS (vise) | 3 | 1:17.3 |
| 12 | 11 | space shuttle orbiter | 37 m | 36.1 m | LAUNCH PAD (ram) | 3 | 1:24.8 |
| 13 | 12 | heavy-lift helicopter | 30 m | 28.6 m | SLING LOAD (anvil) | 3 | 1:32.2 |
| 14 | 13 | freight locomotive | 23 m | 22.7 m | RAILWAY BUFFERS (vise) | 3 | 1:39.5 |
| 15 | 14 | articulated bus | 18 m | 18 m | CAR CRUSHER (press) | 3 | 1:46.7 |
| 16 | 15 | mining dump truck | 15 m | 14.3 m | WRECKING BALL (wrecking) | 3 | 1:53.9 |
| 17 | 16 | fire truck | 11.5 m | 11.4 m | JUNKYARD MAGNET (anvil) | 3 | 2:01.0 |
| 18 | 17 | battle tank | 9.8 m | 9.02 m | SCRAPYARD BALER (vise) | 3 | 2:08.0 |
| 19 | 18 | camper van | 7 m | 7.16 m | CAR CRUSHER (press) | 3 | 2:14.9 |
| 20 | 19 | pickup truck | 5.9 m | 5.68 m | JUNKYARD MAGNET (anvil) | 3 | 2:21.8 |
| 21 | 20 | family car | 4.5 m | 4.51 m | CAR LIFT (ram) | 3 | 2:28.6 |
| 22 | 21 | small car | 3.7 m | 3.58 m | CAR CRUSHER (press) | 3 | 2:35.3 |
| 23 | 22 | tuk-tuk | 2.8 m | 2.84 m | CAR LIFT (ram) | 3 | 2:42.0 |
| 24 | 23 | motorbike | 2.2 m | 2.25 m | ROAD COMPACTOR (piledriver) | 3 | 2:48.6 |
| 25 | 24 | bicycle | 1.8 m | 1.79 m | BIKE PUMP (ultrasonic) | 3 | 2:55.2 |
| 26 | 25 | wheelbarrow | 1.45 m | 1.42 m | ROAD COMPACTOR (piledriver) | 3 | 3:01.7 |
| 27 | 26 | e-scooter | 1.2 m | 1.13 m | HYDRAULIC PRESS (press) | 3 | 3:08.1 |

| Jar | n | Scale markers reached (real size, rule size) | Crusher | First stroke | Jar full |
|---|---|---|---|---|---|
| 4 | 27-31 | n 29: a delivery drone (60 cm, rule 56.4 cm); n 31: a laptop (33 cm, rule 35.5 cm) | SIDE VISE | 3:14.1 | 3:34.5 |
| 5 | 31-35 | n 35: a phone (15 cm, rule 14.1 cm) | SOUND WAVES | 3:39.2 | 3:59.0 |
| 6 | 35-39 | n 36: a pocket drone (10 cm, rule 11.2 cm); n 39: a matchbox (5 cm, rule 5.59 cm) | BOTTOM RAM | 4:03.8 | 4:22.6 |
| 7 | 39-42 | n 42: an insect-sized flying robot (3 cm, rule 2.8 cm) | LASER PULSE | 4:27.4 | 4:40.3 |
| 8 | 42-49 | n 49: an ant (5 mm, rule 5.55 mm) | DROP WEIGHT | 4:44.9 | 5:18.4 |
| 9 | 49-53 | n 53: a flea (2 mm, rule 2.2 mm) | PILE DRIVER | 5:22.8 | 5:39.6 |
| 10 | 53-56 | n 56: a millimetre microrobot (1 mm, rule 1.1 mm) | SIDE VISE | 5:44.3 | 5:55.5 |
| 11 | 56-59 | n 59: a grain of sand (500 µm, rule 550 µm) | SOUND WAVES | 6:00.1 | 6:11.1 |
| 12 | 59-62 | n 62: a dust mite (300 µm, rule 275 µm) | BOTTOM RAM | 6:15.6 | 6:26.1 |
| 13 | 62-68 | n 68: a human hair's width (70 µm, rule 68.8 µm) | LASER PULSE | 6:30.5 | 6:53.3 |
| 14 | 68-72 | n 72: a pollen grain (30 µm, rule 27.3 µm) | DROP WEIGHT | 6:57.9 | 7:11.9 |
| 15 | 72-78 | n 78: a red blood cell (7 µm, rule 6.82 µm) | PILE DRIVER | 7:16.5 | 7:38.5 |
| 16 | 78-83 | n 83: a bacterium (2 µm, rule 2.15 µm) | SIDE VISE | 7:42.9 | 8:00.3 |
| 17 | 83-88 | n 88: a giant virus (750 nm, rule 677 nm) | SOUND WAVES | 8:04.7 | 8:22.0 |
| 18 | 88-96 | n 96: a virus (a bacteriophage, ~100 nm class, rule 107 nm; icon = the "lunar lander" phage, not a spiky ball) | BOTTOM RAM | 8:26.5 | 8:55.1 |
| 19 | 96-102 | n 102: a ribosome (25 nm, rule 26.7 nm) | LASER PULSE | 8:59.5 | 9:19.5 |
| 20 | 102-110 | n 110: the smallest car ever built: one molecule (4 nm, rule 4.2 nm) | DROP WEIGHT (the last crush: HYDRAULIC PRESS) | 9:24.1 | 9:51.7 |

- **Total: 9:58.7** (the nanocar payoff 9:51.7 = the last chord, + 7 s finale). Honest: 110 real splits, no padding.

## v2 (coordinator 2026-11-10, option C): 2-way splits, 28 vehicles, whole-frame layout
- Rule: every crush makes 2 smaller ones, each 2^(-1/3) = 0.794x as long (equal total volume). Split n's vehicles = the real vehicle closest to 458 m x 0.794^n (all within ~10 %; the skateboard 0.8 m vs 0.9 m). Counter exact (2^n); finale 2^27 = 134,217,728 skateboards.
- Layout (owner 16:9 rule): the jars are wide glass tanks across the whole frame (inner walls x 70-1850, floor 1000, MAX line 340); the column uses the whole frame. HUD = two corner overlays (top-left: rule + exact counter; top-right: chapter, vehicle, real vs rule length, a status line) + a progress strip of all 28 vehicles along the bottom edge (current in gold, done ticked, skateboard = GOAL). Mochi & Bolt stand in the scene, front left.
- Small sprites: under 70 px the bicycle draws solid tyres + a fat frame (no spokes), the skateboard a fat deck + big wheels, motorbike/wheelbarrow wheels without spokes.
- Crushers: by vehicle family, reused (a "NEW CRUSHER" pill at each look's first stroke); the press opens and closes; no weapon look (the artillery shell is gone).
- Jars: jar 1 n 0-7 (R0_1 568 = the supertanker's half-length; calib 560 -> top 359, 620 -> 243 at MAX 340), jar 2 n 7-10 (Z 1.36; 1.2 -> 241, 1.4 -> 367), jar 3 n 10-27 = the column (HL_TGT 50: a new vehicle is ~100 px long on screen).

### Plan (planner times; ~8 s per chapter, falling to ~7 s)

| Ch | n | Vehicle (crushed) | Real length | Rule length | Crusher look (family) | Jar | Its stroke (pop) |
|---|---|---|---|---|---|---|---|
| 1 | 0 | supertanker | 458 m | 458 m | HYDRAULIC PRESS (press) | 1 | 0:01.2 |
| 2 | 1 | cruise ship | 365 m | 364 m | SHIP'S ANCHOR (anvil) | 1 | 0:09.7 |
| 3 | 2 | ocean liner | 269 m | 289 m | DRY-DOCK PILE DRIVER (piledriver) | 1 | 0:18.0 |
| 4 | 3 | bucket-wheel excavator | 225 m | 229 m | SCRAPYARD BALER (vise) | 1 | 0:26.3 |
| 5 | 4 | submarine | 173 m | 182 m | SHIP'S ANCHOR (anvil) | 1 | 0:34.4 |
| 6 | 5 | destroyer | 155 m | 144 m | DRY-DOCK PILE DRIVER (piledriver) | 1 | 0:42.4 |
| 7 | 6 | moon rocket | 111 m | 115 m | LAUNCH PAD (ram) | 1 | 0:50.3 |
| 8 | 7 | giant cargo plane | 84 m | 90.9 m | HANGAR DOORS (vise) | 2 | 0:57.2 |
| 9 | 8 | jumbo jet | 73 m | 72.1 m | SHIPPING CONTAINER (anvil) | 2 | 1:04.9 |
| 10 | 9 | hovercraft ferry | 56 m | 57.3 m | SLING LOAD (anvil) | 2 | 1:12.6 |
| 11 | 10 | airliner | 44 m | 45.4 m | HANGAR DOORS (vise) | 3 | 1:21.5 |
| 12 | 11 | space shuttle orbiter | 37 m | 36.1 m | LAUNCH PAD (ram) | 3 | 1:29.9 |
| 13 | 12 | heavy-lift helicopter | 30 m | 28.6 m | SLING LOAD (anvil) | 3 | 1:38.1 |
| 14 | 13 | freight locomotive | 23 m | 22.7 m | RAILWAY BUFFERS (vise) | 3 | 1:46.3 |
| 15 | 14 | articulated bus | 18 m | 18 m | CAR CRUSHER (press) | 3 | 1:54.3 |
| 16 | 15 | mining dump truck | 15 m | 14.3 m | WRECKING BALL (wrecking) | 3 | 2:02.3 |
| 17 | 16 | fire truck | 11.5 m | 11.4 m | JUNKYARD MAGNET (anvil) | 3 | 2:10.2 |
| 18 | 17 | battle tank | 9.8 m | 9.02 m | SCRAPYARD BALER (vise) | 3 | 2:17.9 |
| 19 | 18 | camper van | 7 m | 7.16 m | CAR CRUSHER (press) | 3 | 2:25.6 |
| 20 | 19 | pickup truck | 5.9 m | 5.68 m | JUNKYARD MAGNET (anvil) | 3 | 2:33.2 |
| 21 | 20 | family car | 4.5 m | 4.51 m | CAR LIFT (ram) | 3 | 2:40.8 |
| 22 | 21 | small car | 3.7 m | 3.58 m | CAR CRUSHER (press) | 3 | 2:48.2 |
| 23 | 22 | tuk-tuk | 2.8 m | 2.84 m | CAR LIFT (ram) | 3 | 2:55.6 |
| 24 | 23 | motorbike | 2.2 m | 2.25 m | ROAD COMPACTOR (piledriver) | 3 | 3:02.9 |
| 25 | 24 | bicycle | 1.8 m | 1.79 m | BIKE PUMP (ultrasonic) | 3 | 3:10.1 |
| 26 | 25 | wheelbarrow | 1.45 m | 1.42 m | ROAD COMPACTOR (piledriver) | 3 | 3:17.3 |
| 27 | 26 | e-scooter | 1.2 m | 1.13 m | HYDRAULIC PRESS (press) | 3 | 3:24.4 |
| 28 | 27 | skateboard (finale) | 80 cm | 89.5 cm | - | 3 | last chord 3:26.4, end 3:33.4 |

- **Total: 3:33** (27 strokes; jar 1 FULL 0:52, jar 2 FULL 1:14). That is the honest length: one crush per vehicle, each chapter = the crusher coming in, the squeeze, the wave of pops on the music, the new vehicles settling, at ~7-8.5 s (falling: the rate climbs). Stretching to 8:00 would mean ~17 s per chapter of the same single crush (padding). Ways to a real 8:00 if wanted: a longer ladder (more vehicle sizes between and below), or 2 crushes per vehicle size with a finer rule.

### v2 test (2026-11-10)
- Commands:
  - build: `python scenes/longform_vehicles.py --crushers --tend 82 --report` (sims to 82 s: jar 1 ~5 min, jar 2 ~6 min, the jar-3 pour);
  - render + audio: `NF_SCALE=1.0 python scenes/longform_vehicles.py --crushers --tend 82 --cache --label test --window 0,80` (8.6 fps; 9.3 min).
- Encoded checks:
  - h264 yuv420p 1920x1080 60 fps, 4,800 frames, 80.000 s; aac 80.000 s;
  - -14.01 LUFS, peak -5.9 dBFS;
  - flash_check PASS (10, worst 1 s = 2);
  - blackdetect: none.
- Strokes on the beat (0.00-0.01 s), hangar doors +0.49 s.
- Pop sync: 53 groups, rise median +3.6 dB, min +1.2. The pop squash/plink gains were raised (0.30 -> 0.45, 0.20 -> 0.34): at the old gains the median was +2.9 dB.
- Encoded frames read at every contact + first pop and at both breaks/pours.
- Fixed on the way:
  - The pressure gauge moved to the middle of the press head (the corner HUD hid its label).
  - The HUD rewrite had deleted fmt_big/visible_balls (restored).
  - A `--check` without `--report` falls through into the full render: always use `--report` for checks. Hit once; stopped at once.

## v1 (superseded): 3-way splits, 18 vehicles, 2:07, centre jar + side panels (review\longform3\stills_fast_*.png)

### v1 rule
A crushed vehicle splits into 3 vehicles 0.693x as long (3^(-1/3): equal total volume). Split n's vehicles = the real vehicle closest to 458 m x 0.693^n. Counter exact (3^n); finale 3^17 = 129,140,163 skateboards. Goal ladder (all 18 vehicles, skateboard marked GOAL) visible from frame 0 in the right panel.

### v1 chapter plan (one split = one chapter = one crusher; times from `--plan`)

| Ch | n | Vehicle (crushed) | Real length | Rule length | Crusher look (physics family) | Jar | Its stroke (pop) |
|---|---|---|---|---|---|---|---|
| 1 | 0 | supertanker | 458 m | 458 m | HYDRAULIC PRESS (opens) (top) | 1 | 0:01.2 |
| 2 | 1 | aircraft carrier | 333 m | 317 m | SHIP'S ANCHOR (drop weight) | 1 | 0:08.6 |
| 3 | 2 | bucket-wheel excavator | 225 m | 220 m | SCRAPYARD BALER (boxed side vise) | 1 | 0:16.0 |
| 4 | 3 | destroyer | 155 m | 153 m | DRY-DOCK PILE DRIVER (pile driver) | 1 | 0:23.2 |
| 5 | 4 | Moon rocket | 111 m | 106 m | LAUNCH PAD (bottom ram) | 1 | 0:30.4, jar 1 FULL, breaks, pour |
| 6 | 5 | jumbo jet | 73 m | 73 m | HANGAR DOORS (boxed side vise) | 2 | 0:37.9 |
| 7 | 6 | hovercraft ferry | 56 m | 51 m | SHIPPING CONTAINER (drop weight) | 2 | 0:44.4, jar 2 FULL, pour, zoom in |
| 8 | 7 | heavy-lift helicopter | 40 m | 35 m | SLING LOAD (drop weight) | 3 (column) | 0:54.8 |
| 9 | 8 | freight locomotive | 23 m | 24 m | RAILWAY BUFFERS (boxed side vise) | 3 | 1:02.0 |
| 10 | 9 | semi-truck | 16.5 m | 17 m | WRECKING BALL (swing) | 3 | 1:09.2 |
| 11 | 10 | city bus | 12 m | 11.7 m | CAR CRUSHER (press) | 3 | 1:16.3 |
| 12 | 11 | battle tank | 7.9 m | 8.1 m | ARTILLERY SHELL (blast: dives in, booms) | 3 | 1:23.4 |
| 13 | 12 | pickup truck | 5.9 m | 5.6 m | JUNKYARD MAGNET (drop weight) | 3 | 1:30.3 |
| 14 | 13 | small car | 4.0 m | 3.9 m | CAR LIFT (bottom ram) | 3 | 1:37.2 |
| 15 | 14 | microcar | 2.7 m | 2.7 m | ROAD COMPACTOR (pile driver) | 3 | 1:44.0 |
| 16 | 15 | bicycle | 1.8 m | 1.9 m | BIKE PUMP (sound-wave rings) | 3 | 1:50.8 |
| 17 | 16 | e-scooter | 1.2 m | 1.3 m | HYDRAULIC PRESS returns (closes) | 3 | 1:57.4 |
| 18 | 17 | skateboard (finale) | 0.8 m | 0.9 m | - | 3 | the last chord ~2:00, end 2:07.1 |

- **Total: 2:07 at ~7 s per chapter.** One split per vehicle gives 17 strokes, so the honest length is ~2-3.5 min, not the Sun video's 9 min (no mid-rolls under 8:00). Options:
  - (a) Keep 2:07.
  - (b) ~10-12 s per chapter (a slower stroke, a longer look at each new vehicle and crusher): ~3:30, no padding.
  - (c) Extend the ladder (more vehicle sizes between the listed ones, or below the skateboard) for more honest rungs.
  - Owner decision.
- No tool repeats back to back. Families used: press x3, drop weight x4, boxed vise x3, pile driver x2, bottom ram x2, wrecking ball, blast, sound waves. Themed looks are drawn for the test after the drawings OK (until then the stills show the family's drawing and name).
- Music: Brahms, Hungarian Dance No. 5 (PD). The melody comes from the flutetunes MIDI with our own oom-pah harmony; the four statements are looped, fuller each pass; the F#-minor cadence is the 3^17 payoff. 112 bpm +0.20 bpm/s.

## Physics: rigid vehicles (new in this fork)
- Each vehicle = 5 discs (one radius) on its template (`lib/vehicles.BODY`), kept rigid by shape matching inside every PBD iteration (stiffness `SM_K` 0.7). Contacts inside one vehicle are skipped; the hop graph runs through each vehicle.
- A split puts the 3 children stacked across the parent. Each child grows from 70 % to full size over 0.3 s (`GROW0`, `GROW_F`), and the children pop apart gently (`SPLIT_SP` 0.35).
- Measured, not guessed:
  - Rigid elongated bodies pack far looser than balls. Popped at full size, they crossed through each other; contact pushes vs rigidity then drove the pile up into the jar's ceiling (overlap sum 47k px; the pile rose ~1,500 px in 1 s when freed).
  - The fixes:
    - growth ramp + soft shape matching;
    - symmetric contact weights (`LOW_W` 1.0; balls used 0.3);
    - a vehicle may rise at most `V_UP` 420 px/s (falls are free);
    - a crusher stays as the lid until `EXIT_LEAD` 2.2 s before the next stroke, then leaves upward and the next one comes in.
  - Result in jar 1: no spring-ups.
- Jars: jar 1 n 0-5 (whole), jar 2 n 5-7 (whole, Z 1.18: rigid vehicles grow the pile less than balls; 1.45 -> top 588, 1.12 -> 267, 1.22 -> 373; a 3-split jar 2 = 33k discs was too slow to simulate), jar 3 n 7-17 = the column.
- Fill: `R0_1` 345 (the supertanker's half-length, 690 px of the 700 px jar): jar 1's pile tops at 336 at its payoff (MAX 330; 325 -> 406, 340 -> 351, 349 -> 343).
- Frames store one record per VEHICLE (centre, angle, gen, load, birth); the renderer blits cached illustration sprites (5 % length buckets) rotated to the body's angle, flattened and glowing hot under load.

## v6 (owner feedback on v5, 2026-11-10)
- Pace:
  - first hit at 0.85 s (T_FIRST);
  - a turn every ~3.7 s in jar 1 (bps 7), ~3.1 s in jar 2 (bps 6), then gap_min 2.9 s falling to 2.0 s (GAP0/GAP1/T_GAP0/T_GAP1 = 2.9/2.0/40/300);
  - sqb 1.2, GAP_FIX 0.15, WIN_GAP 0.35, CULL_LEAD 0.30 (weapons mode).
  - Full video now plans at ~6:00 (v5 ~10:15). It is honest: same rungs, less waiting.
- Gravity G_S 6.5 (was 3.5), G_MIN 300: falls ~1.9x faster; still no bounce.
- Water (jar 1, ship chapters only):
  - WATER_H 150; buoyancy WB 3.1 (a lone hull floats ~32 % under = the red band) + water drag WDRAG 3/s;
  - stacked hulls get pushed under;
  - the drain starts at the dry stroke's first hit (N_DRY = 6, moon rockets).
  - Splashes (`find_splashes`): a body's bottom crosses the surface > 70 px/s -> soft jets + mist + droplets + ripples, a splash sound, and no dust or thud.
- Weapons:
  - each slides out from behind its owner 0.3 s before contact and back after the last hit (`_w_out`); hands are empty between turns;
  - Bolt's remote only for REMOTE_LOOKS (rocket, charge, jet, cluster, anvil); devices (cannon, tesla, ball, catapult) show alone.
- Anvil = family "run": 5 anvils left -> right, 0.17 s apart, each breaks its own column and gets its own slam.
- Tractor / gravity: THREE flyers over the jar; the hit vehicles inside the 3 beams are LIFTED in the sim (LIFT_V 300 px/s up to 240 px over the pile), then dropped.
- Freeze: each target ices over in the 0.55 s before its hit (frost crust, ice shell, highlights, icicles, crystals, mist), then shatters into ice shards; its halves keep a thin frost that thaws.
- The test jet moves to n=17 (LFV_TEST_JET=17), so the tesla mast (n9) shows.
- v6 follow-ups found in the test:
  - higher gravity made pours spray the pile -> POUR_KEEP 0.25 (a pour lands with a quarter of its fall speed);
  - flash_check tripped in the column at the faster pace -> constant-rate zoom over the whole turn (deep_ramps from the real re-base), smoothed camera height (cam_cy), flyers routed over the pile, PILE_FILL 0.65 (a dark fill of the vehicles' own colour behind the column pile);
  - jar-2 landing thuds at 0.45 (hundreds land after a lift), a louder first tesla strike;
  - drop0 = WATER_H + 110 (the tanker splashes in at ~-0.15 s and floats by the first hit).
- v6 test results: -14.0 LUFS, flash PASS (worst 2), hits +6.3 to +10.4 dB. Full video plans at ~6:00.

## v2 (brief longform3b, 2026-11-11): fix the 8-minute skateboard padding
- `LFV_VER=1` (+ `LFV_FLASHFIX=0`) keeps full v1 bit-reproducible (cache `_j20_s1.pkl`); v2 caches and frame stores carry `_v2`.
- Pace: the v6 hook through n 7 (T_HOOK 29.0); vehicles 9-28 at GAPV0 7.3 -> GAPV1 6.0 by T_V1 176 s (beat-snapped: 7.6 -> 6.2 s per turn, n 27's micro hand-over at ~2:55); micro GAPM0 4.2 -> GAPM1 3.0 by 520 s (placeholder: retune with the roster).
- VOLLEYS (`volley_plan`, `Jar.weapon_fire_v2`): after the hook a turn fires V volleys, V = min(4, fit, round(gap x rate)), rate 0.45 -> 0.95/s by 9:00. Each volley takes one sector of the pile (equal counts, from the shooter's side), has its own target, fire frame, kick and sounds; the weapon stays out for the whole turn and re-aims. Windows fill VOL_FRAC 0.80 of the turn, end >= VOL_END 1.05 s before the next first hit, VOL_GAP 0.25, VOL_MIN 0.45. Lifts (tractor, gravity) stay one long wave. The bed ducks only on a turn's first volley.
- MICRO_ROSTER rows (n0, n1, obj, hue, (anchor id, n)) -> VEH, micro_hue, MICRO_MARKERS/MARKER_ICON. New objects: `VH.register(key, name, length_m, aspect, draw_fn, color, body, solid_fn)`; unregistered ids draw as the skateboard (warned). True-scale anchor drawings: `ANCHOR_DRAW[id] = fn(ctx, cx, cy, px_per_m, u)`. HUD/banner/inset text reads the pile object's name (no hard-coded SKATEBOARD in the micro HUD).
- Flash fix (render-side, FLASH_FIX): see the v1 diagnosis below.
- v1 flash diagnosis (per-frame cell events on the v1 file + FAST pieces): every flagged window is a WHOLE-WIDTH change of a frame-filling pile, not one blast.
  - Rocket shots (1:38, 4:04, 6:23): one rocket per hit vehicle = a dark swarm of hundreds over the bright pile, then a fireball each.
  - Freeze (4:24, 5:14, 6:54, 7:02, 8:32): the ice shells + shard mists of hundreds of targets iced and shattered a third of the frame white within a second.
  - Tractor (1:07): a pile of WHITE camper vans (cell luminance 0.40) + beams; any surface motion stepped 0.1.
  - Jet (4:37), mothership (8:11): passed once the above were capped.
- Fix (FLASH_FIX, render only, the sim and the hits are unchanged): blasts queued per frame under FX_COV 6 % of the screen (radius caps 105 per shot / 150 single); <= SHOT_DRAW 3 projectiles/beams per note; ice mists ICE_COV 5 %, <= ICE_MAX 36 shattering vehicles drawn per frame, ice shells on pile-sized sprites at ICE_PILE_K 0.35, freeze cone 0.5; pile-sized sprites toned to <= PILE_LUM_CAP 0.30 mean linear luminance; tractor/gravity beams at half opacity with 0.43 s fades; pile fill sized by the count-weighted gen (the argmax flip stepped the whole fill).
- Proof (FAST pieces of the v1 build, `output/tmp/flash_driver.py`): fix off FAIL at 1:06-1:09.5 (3) and 1:37-1:40.5 (4); fix on: all 11 flagged windows PASS (worst 1 s <= 1).
- v2 STOP 2 (2026-11-11): PLAN_v2 roster live (lib/micro.py: 26 objects + 19 icons + ANCHOR_DRAW giants ant/salt/wbc/E. coli, hair strand, flea-jump event; `LFV_ROSTER=placeholder` = skateboards). Micro drops ~2.5 s (RAMP_MIN 0.35, DROP_LEAD 0.40, DROP_D 600, DROP_CAM 0.25, half-beat snap); hits per volley >= VOL_K0 6 -> VOL_K1 9 in the micro world; lifts cut to LIFT_FRAC 0.55 of the windows (a 6 s lift emptied the next view: 79 vehicles at 1:32.9). Giants (> 3x) and events: 4.2 s, no card, "TO SCALE: ..." pill, drawn under the HUD. Banners only for SAME SIZE anchors. 8:45.4.
