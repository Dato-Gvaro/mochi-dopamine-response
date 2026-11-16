# press_drill — THE MINE: Mochi's DRILL vs Bolt's shredding SAW; every gem hit splits into 3

- Brief: coordinator task 2026-10-23 (batch49, docs/BRIEF_overnight_1023.md): drill vs saw, from press_tools' "deep vs wide" suggestion.
- **v1 (superseded):** press_tools' jar look with Mozart's Queen of the Night aria.
  - Owner: "it's like the third with the same visuals — maybe not jars, a different situation?" press_split3/4/5 in the jar look got ~1.5K views each.
- **v2 (superseded):** the mine re-skin (carts, gems, Grieg). The saw could only dig 85 px under the pile top.
  - Owner: "the saw not going to the bottom makes it unpleasant to watch."
- **v3:** the mine, carts, gems and Grieg are kept. **The saw now reaches the full depth; it loses because it SHREDS.**
  - Coordinator: the saw side froze and went silent for ~7 s, and the clink rate fell (no dead middle).
- **v3.1 (this):**
  - **The saw side stays alive.** The blade churns the gravel it runs through: each grain it touches is kicked up and along the cut at 300 px/s, and one in 8 sprays off at twice that. The grains fall and resettle.
  - Each 16th the blade churns gravel plays a soft tonal **gravel crunch** (8–9 per second, all clip).
  - The saw's counter creeps honestly (+0–5/s) from the odd gem the churn knocks into the blade.
  - **Bolt gets frustrated** after the lead change (annoyed / worried squints at 1.6, 3.3 and 4.8 s after it) while Mochi cheers.
  - **The drill's clinks thicken with its count:** on every 16th of a beat in which it split gems, it plays an up-strum of chord tones, 1.25 + gems / 400 notes (dithered, max 9, 16 ms apart, kept in C5–B6, gain / √notes). So the **audible event rate climbs every second to the end.**
  - Fix: when the drill sits high over a full cart, its bit now slides up into the chuck. Before, the motor was drawn over the beam.
  - Sim: the churn changes the saw cart slightly. Same timeline: lead change 8.05 s, snap 14.93 s.
- Caption: "Every gem ~HIT~ splits into 3" / "~Drill~ or ~Saw~:" / "first cart to ~4,000~ gems?".

## Look (from v2)

- A lantern-lit mine tunnel: a rock wall, a timber frame (posts + a lintel beam with the tools' steel rail), and rails with sleepers.
- **Two riveted ore carts on wheels**, cut-away, coral for Mochi and mint for Bolt.
  - The walls end at the brim. A pile above the brim spills over the side and drops past the rails (no lid, no invisible walls).
- **Faceted hexagon gems**, coloured by generation: deep amber → ruby → violet. The last generation is **grey gravel, too small to split**.
- **Tools** in solid steel.
  - Drill: a coral carriage, motor and chuck, and a fluted spinning bit.
  - Saw: a mint carriage, an arm, and a 14-tooth spinning blade.
- **HUD:** a goal meter per cart from frame 0 (gems / 4,000; reads "FULL!" at the end), labels, counters "Gems: N" (gold = the leader), and the faces.
- Side safe zone: caption, meters, carts and HUD sit within 0.10–0.84w. The posts and the finale spill are decoration only.

## The rule and the race (v3)

- **Both carts start with the same load:** a jittered hex pack of amber gems (r 16) up to 0.6 × 710 px.
- **The music clock:** 128.6 bpm, so a beat is 28 frames and a 16th is 7 frames. Every gem a tool touches splits into 3 on the next 16th. A gem split by a stroke is immune to the rest of that stroke.
- **DRILL (clean splits):** one plunge per beat to the cart floor (touch half-width 4 px) across 9 stops; the first wave pops on the beat.
  - Each split makes 3 pieces at **0.66× size**.
  - Gems split this way stay splittable for 4 generations, up to 81 pieces per load gem.
- **SAW (shreds):** one full-width sweep every 2 beats. **Each sweep runs 50 px deeper, from the pile top down to the cart floor, then starts again at the top.** It reaches every gem in its cart.
  - Each saw split makes 3 pieces **3 sizes smaller (~0.29×)**.
  - After 2 saw generations everything is grey gravel: at most 9 pieces per load gem.
  - Gravel packs small, so the saw's pile sinks.
- **Why the race turns:**
  - The saw's wide, full-depth sweeps win early.
  - Its cart then turns grey from top to bottom and stalls at ~1,750, with nothing left that can split.
  - The drill's clean ×3 splits keep making splittable gems. It overtakes and reaches 4,000; its cart heaps over the brim and spills.
- `--target 4000` ends the race. The snap lands on the next beat, which is the music's cadence.

## Timeline (seed 0, clip time)

- **0 s** (sim 0.93 s, score beat 6): both carts are full of amber gems.
  - The drill is mid-plunge: 283 gems, 7%.
  - The saw is at the cart floor with violet shreds and the first grey: 381 gems, 9%.
- **0.5 s:** 323 vs 433. **2 s:** 501 vs 551 (saw leading). **6 s:** 1,141 vs 1,551 (the saw's biggest lead; its cart is mostly grey).
- **LEAD CHANGE at 8.05 s** (1,713 vs 1,665). By then the saw's cart is all grey and sinking.
- **14.47 s:** the drill reaches 4,000. The banner reads "4,000 GEMS!" and its cart is heaped over the brim.
- **14.93 s = the D-major cadence = the snap:** the drill's bit and motor fly off, the cart erupts, and the banner reads "DRILL WINS!" (4,047 vs 1,749).
  - Mochi cheers and laughs. Bolt goes wow, then annoyed, with a big mint "again?!" over his near-empty cart of grey gravel.
- Clip **16.68 s** (1001 frames). The last 0.6 s dissolves into the pre-roll.
- **Splits per second:**

  | Second | Drill | Saw |
  |---|---|---|
  | 0 | 52 | 79 |
  | 1 | 64 | 52 |
  | 2 | 53 | 98 |
  | 3 | 79 | 142 |
  | 4 | 88 | 89 |
  | 5 | 100 | 171 |
  | 6 | 97 | 44 |
  | 7 | 147 | 13 |
  | 8 | 177 | 12 |
  | 9 | 151 | 19 |
  | 10 | 177 | 2 |
  | 11 | 188 | 1 |
  | 12 | 180 | 8 |
  | 13 | 190 | 0 |
  | 14 | 146 | 0 |

## Sound (from v2)

- **Grieg, "Wedding Day at Troldhaugen", Op. 65 No. 6** (1896; Grieg d. 1907, PD).
  - Source: Mutopia-2006/06/17-781 (Schirmer 1903, engraving PD), `<SOUNDFONTS_DIR>\scores\grieg_troldhaugen\troldhaugen.mid`.
  - Score beats 6 → 38 (the D-major cadence = the snap), at one steady 128.6 bpm.
- **Arrangement** (lib/orchestra), all notes read from the score:
  - Piano on both staves. The melody on strings + violin, with clarinet and, from 45%, horns an octave down.
  - Inner tones on strings; pizz + contrabass bass; timpani every second bar and a roll into the cadence.
  - Cadence: a D-major tutti, a rolled piano chord, a harp run, timpani and a soft boom.
- **SFX (v3.1)**, all on the 16th grid and pitched to the chord the score is sounding:
  - Drill: a gem-clink up-strum that thickens with its count (see v3.1).
  - Saw: a clink (octave 6) per 16th it split something, plus a soft gravel crunch per 16th it churns gravel. The crunch is 4 tiny pitched ticks (root, fifth, octaves) 6–9 ms apart over a short low body.
  - No noise.
- Mastering: `level_bed` ride (finale target +5.5 dB on the bed), SFX 0.20, `master(peak_db=None, reverb=0.5)`, and the last 0.6 s zeroed.

## Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\press_drill.mp4, v3.1)

- Video: h264 yuv420p 1080x1920, 60 fps, 1001 frames = 16.68 s.
- Loudness: −14.00 LUFS, peak −6.3 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second:** −17.5, −17.2, −16.8, −16.9, −17.4, −16.7, −16.8, −16.6, −16.6, −16.6, −16.7, −16.7, −16.4, −16.4, −17.2, −16.1.
- **Finale:** +2.7 dB over the body median.
- **Audible events per second** (clinks + crunches): 26, 31, 39, 43, 43, 52, 53, 60, 65, 71, 73, 80, 85, 87, then 81 in the last 0.93 s before the cadence (= 87/s). It never falls.
- **Saw side moving** (mean frame diff over 3 frames in the saw cart): 8.3 at 9 s, 8.0 at 11 s, 12.5 at 13 s.
- **Saw counter (gems):** 1,697 at 9 s, 1,729 at 10 s, 1,737 at 11 s, 1,741 at 12–13 s, 1,751 at the snap.
- flash_check: 0 flashes = PASS.
- **Loop seam:** 3.43. It is the genuine step: frame 0 is 0.93 s into the sim, with the load still settling.
- Frames read from the encoded file at 0, 0.5, 2, 8.05, 9, 11, 13, 14.93 and 16.66 s.

## Nits / doubts

- **The drill's strum is dense at the end** (up to ~9 notes per 16th, a fast shimmer). It is quiet per note (gain / √notes), but it is measured, not heard.
- **The saw's lead is small early** (547 vs 501 at 2 s). It peaks at 6 s (1,389 vs 1,141).
- **The seam (3.43) is high** because the clip starts early in the sim, to fit the lead change at ~8 s.

## Args and cost

- Defaults are the shipped values:
  - Load and race: `--seed 0 --r0 16 --ngen 5 --rdust 3.1 --fill0 0.60 --ymax 500` (the brim), `--target 4000`.
  - Drill: `--drillw 4 --dlead 5`.
  - Saw: `--sawjump 3 --sawr 34 --sawd 14 --sawbeats 2 --leveldy 50 --slead 4 --kick 300`.
  - Drill strum: `--nstgems 400 --nstmax 9`.
  - Music and mix: `--beatf 28` (128.6 bpm), `--b0 6`, `--tend 1.75`, `--fin 2.0 --findb 5.5 --sfx 0.20`.
- Other args: `--label`, `--cap`, `--still --frame a,b`, `--report`, `--verbose`, `--audition`, `--cache`. `kit.arg` takes the FIRST occurrence of a flag.
- Cost: sim ~1 min; Full HD render ~9 min at 2 encoder threads.
- Delivered <VIDEOS_DIR>\MochiAndBolt\review\batch49\press_drill.mp4 (v3.1 overwrote v3). Owner review: pending.
- **Shelved 2026-10-24** to MochiAndBolt/reserve after 3 rounds: the owner could not read why the saw's pile shrinks (saw pieces 0.29× vs the drill's 0.66×). The rule does not read in 1 second.
