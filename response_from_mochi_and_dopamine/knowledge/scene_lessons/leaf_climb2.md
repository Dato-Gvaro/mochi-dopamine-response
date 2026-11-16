# leaf_climb2

- Redesign of leaf_climb after the owner's v1 review (2026-10-06): "leaves ugly, sounds not good; a sawn tree doesn't go down bit by bit — use the TRACTOR with the tree-destroying thing".
- New, self-contained file. leaf_climb.py is untouched.
- Rule: Bolt's tracked forestry MULCHER chews the trunk from the bottom up. Every bite drops the whole tree one step. Mochi must climb the leaves faster than the tree sinks to reach the golden fruit in the crown. Bolt wins if the drum reaches Mochi's leaf.
- Caption: "Climb to the TOP of the tree|~Bolt's mulcher EATS it~".

## Physics
- Leaves: v1's lever springboards (cantilever spring at the stem, plastic collision with the effective mass I/Lg^2, stomp on the down-stroke, leave at rest + leg pop).
  - Edge landing: launches 200-400 px.
  - Stem landing: a 50 px hop.
  - Leaves are springier up high (K_TIP 150 -> 55).
- Bites:
  - 27 px each (+-12%), 4.2 -> 8.2 per second, each drop eased over 85 ms.
  - Every bite kicks every leaf (qd -1.5): the leaves wobble with the chug.
  - Leaves are shredded as they reach the drum: they crumple to the stem plus a burst of leaf-coloured bits.
- The jam: at 50% eaten a knot jams the drum for 0.55 s (shake, clank, Bolt worried and sweating), then a steel latch.
- Mochi flies in world coords.
  - Launch and landing use the tree's AVERAGE sink rate.
  - Lesson: with the instantaneous rate, a launch mid-bite (the tree dropping at ~600 px/s) ate half his speed, and he fell into the drum within 2 s on most seeds.
  - He aims with the predicted sink at landing.
  - He only lands on leaves that are not yet eaten.
- Fixed camera: no split.
  - Balance: Mochi's screen height is the race. Too slow a mulcher and he leaves the top of the frame; too fast and he is caught early.
  - The search requires hmax <= 880 world (below the caption).

## Ending (s147)
1. 14.95 s: the drum eats leaf 13, the last leaf before the crown. "CHOMP!": Mochi is spat out with a double spin.
2. The finale: 10 bites/s x 44 px eats the rest of the tree.
3. The fruit pops out of the drum, BONKs the dizzy, chip-covered Mochi and lands on Bolt's cab roof (clank).
4. Bolt cheers in the cab ("BOLT WINS!") and laughs. Mochi gives an annoyed stare.

## Loop
- Over the 1.30 s reset, the tree rewinds up out of the drum and the leaves re-emerge.
- Mochi waits 0.48 s, then hops a Hermite path to the state one frame before frame 0.
- The drum spins a whole number of turns per clip, and fireflies and stars use whole cycles.

## Look
- Dusk sky, moon, fireflies, silhouette hills.
- Leaves:
  - Smooth Catmull-Rom outlines, ovate with a pointed tip, lit-to-deep gloss gradient.
  - Forward-swept vein pairs, a tapered midrib, a gloss streak and a rim light.
  - A three-layer glow hugging the blade and a sweet-spot glow at the tip that brightens with the bend.
  - Jewel colours run emerald -> teal -> sapphire up the tree; gold/teal crown with the golden fruit.
- Machine:
  - Graphite body, amber hazard stripe, teal glow line, tracks.
  - Glass cab with Bolt, two work lamps with light cones.
  - Exhaust puff per bite.
  - Steel toothed drum with speed streaks under an amber hood.
- Mochi R 56 (v1: 40).
- Bars: "MOCHI xx% CLIMBED" (stem height of his best leaf / crown) vs "BOLT xx% EATEN" (sink / crown). They meet at the catch.

## Sound (no noise beds)
- Bed (built in the scene, `render_soundtrack(bed=...)`):
  - per launch: a springy plucked-string note (eine_kleine +12, harmonics with a tiny upward-bent attack), brighter for bigger leaps;
  - a soft low pluck per landing;
  - per bite: one thump (52-112 Hz glide + wood knock) and 3-6 crisp wood-chip ticks;
  - per leaf shredded: a 9-tick crunch + a low pluck;
  - catch: a tick crunch + a rising 5-note pluck run while Mochi flies;
  - fruit pop: a high pluck.
- Mixer events: spit pop, landing bounce/squash, bonk, roof clank, cheer arpeggio + pop, jam clank/latch.
- Silent from ~18 s.
- `tools/regen_audio.py` cannot rebuild the bed. Rerun the scene.
- Balance (pre-master): pluck -20.6 dB RMS, thump -26.5, ticks ~-34.

## Numbers (s147)
- Catch 14.95 s, Mochi lands 16.25, fruit pops 15.64, bonk 16.70, roof 17.32, reset 19.30, clip 20.60 s (1236 frames).
- 15 jumps, 1 stem landing, 90 bites before the catch.
- Launches + bites per 5 s: 29, 31, 45.
- Progress (Mochi vs Bolt): 33/24 at 5 s, 51/50 at 9.5 s, 78/66 at 12 s, 92/91 just before the catch.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 20.60 s.
- -14.01 LUFS, peak -6.6 dBFS, last 0.5 s -240 dBFS.
- flash_check: PASS (0 flashes).
- Seam: check_clip reports 0.889, above the 0.72 band. That is the drum's spin plus the tree's first bite drop: mid-clip frame steps measure 0.56-3.0 (0->1 is 3.0, from the first bite), so the seam is one normal motion step.

## Args and search
- Args: --seed (147), --label, --cap, --melody, --search N, --still --frame.
- Search keeps catch >= 12.5 s, Mochi on leaf >= 12 and hmax <= 880.
  - 23 of 150 seeds fit, e.g. 19, 38, 62, 85, 93 (all caught on leaf 12).
  - 7/150 seeds are Mochi wins (no ending built for those).

## Delivery
- Delivered to <VIDEOS_DIR>\batch15\leaf_climb2.mp4. Owner review: pending.
- Owner review 2026-10-07: Doesn't work for now; moved to Reserve.
