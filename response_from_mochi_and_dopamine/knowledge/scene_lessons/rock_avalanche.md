# rock_avalanche — Mochi DIGS (1 rock a beat) vs Bolt KICKS an avalanche (every falling rock knocks loose 2): who clears the mountain FIRST?

- Brief: coordinator task 2026-10-24 (batch49, docs/BRIEF_overnight_1023.md). New mechanic, new file. It borrows cannon_split's lane style, HUD, banners, captions, dissolve loop and master.
- **Breaks the batch pattern:** the doubling side still wins, but the twist is the ending. The landslide that wins it for Bolt pours into the valley and **buries him up to his eyes**. Mochi looks down from her summit, deadpan: "worth it?".
- Caption: "Every falling rock knocks loose ~2~ more" / "~Dig~ or ~Avalanche~:" / "who clears the ~MOUNTAIN~ first?".
- Layout: two stacked lanes (violet neon panels, x 112-904 = 0.10-0.84w; Mochi y 400-860, Bolt y 880-1340 ≤ 0.70h).
  - Each lane holds an identical mountain: a running-bond staircase heap of **317 rocks** (22 rows of 18 × 13 px cells, irregular 6-8-sided rock shapes, face ~32°) that leans on a bedrock cliff. A far rock wall closes the valley.
  - **Mochi's lane is mirrored** (summit on the right), so her summit sits directly above Bolt's valley and she looks down at him at the end.
- Colour: one calm gradient by row, bottom → top: terracotta → ochre → sand → sage → slate blue (sat ~0.5-0.75), with 3 tone variants per row. No neon on the rocks, no white flash, no dust.
- HUD per lane (sky over the valley): the rule label ("DIG: 1 rock a beat" / "AVALANCHE ×2: N falling", live), "n / 317 rocks" (gold for the leader; Bolt's turns into "CLEARED!"), and a meter.

## The rule (each side readable at a glance)

- One gravity (1200 px/s²). Hops are true parabolas landing on the music's 8th grid (120 bpm: beat 30 frames, 8th 15).
- **DIG (Mochi):** on every beat she swings a pickaxe and pries the next rock of the top layer loose (right to left along each row, then the row below). She steps down as the summit sinks. Steady: 2 rocks/s. She stops on the cadence.
- **AVALANCHE (Bolt):** at frame 0 he kicks ONE mint rock from the valley up onto his summit (a 2-beat lob).
  - Every rock that lands on the heap knocks loose **2** rocks (the one it hits plus an exposed neighbour), with a gold "×2" pop.
  - Each loosened rock either **hops** onto an exposed rock lower on the heap (a hit, 2-5 8ths later; this is another ×2) or **misses** and tumbles down the face. The hitter itself bounces off and tumbles down.
  - The hit chance ramps 0.62 → 0.80 over 13 s, and the hops get quicker (3-5 → 2-3 8ths) over 12 s. A rock left with no rock under it falls too (the support rule).
  - It is a scripted branching process, like cannon_split: outcomes are chosen and arcs are solved to the chosen rocks. The seed was searched so that the collapse lands exactly on the cadence.
- **Collapse:** once ≤ 40% of his heap is left, the undermined remainder (a pillar against the cliff) comes down on the next beat, which is the cadence.
- **Loose rocks** move on the current terrain: the heap top (step corners filled into a ramp), the rubble pile and the floor. They bounce, slide and roll (sliding friction, spin from contact).
  - In the valley a rock runs free, then brakes to a chosen stop. The race's rubble stays short of Bolt (it is capped at x ≤ Bolt − 48).
  - **The landslide's toe** (the lowest 20% of the collapsing rocks) slides along the ground over the rubble and eases to a stop on a triangular mound centred on Bolt (half-width 64, 0.75-1.05 s run). That is the burial.
- Camera: static, plus **one smooth zoom (×2) inside Bolt's lane only** from 15.25 to 16.1 s, onto Bolt, so the punchline reads on a phone. Mochi's lane, the HUD and the caption never move.

## Timeline (seed 182; clip s)

- **0 s:** Mochi pries rock 21 on the downbeat (head start 20, 2 rocks rolling down her face). Bolt squashes and kicks the mint rock up the mountain.
- **0.5 s:** 22 / 0, with the kicked rock mid-air. **1 s:** the kicked rock lands on the summit: "×2", 23 / 2. **2 s:** 25 / 6 (two ×2 hits at the summit).
- **LEAD CHANGE at 8.25 s** (37 / 37 at 8.0 s, then 39 / 47 at 9 s).
- **CADENCE at 15.00 s:** the pillar collapses. Bolt's count goes 181 → 317, "CLEARED!", with the banner "AVALANCHE WINS!". Bolt cheers; Mochi goes "wow". Mochi ends at 50 / 317 (16%).
- **15.25-16.1 s:** the zoom. The landslide pours across the valley; Bolt sees it coming ("wow", looks left). By **16.0 s** the mound covers him up to his eyes (pile top ~31 px at his centre).
- From 16.1 s Bolt is annoyed (heavy lids, eyes only). Mochi is deadpan and looks down, with the "worth it?" sticker from 16.37 s.
- Clip **17.70 s** (1062 frames). The last 0.6 s dissolves into the pre-roll; the HUD switches at the midpoint.
- **Growth: Bolt 2 → 317 rocks (×158 from 1 s); "falling" 1 → 200.**
- Rocks loosened per second:

  | s | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Mochi | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 0 |
  | Bolt | 0 | 6 | 4 | 0 | 8 | 6 | 4 | 7 | 10 | 13 | 20 | 25 | 33 | 34 | 31 | 116 (collapse) |

## Sound (music first)

- **J. S. Bach, Concerto for Two Violins in D minor, BWV 1043, 1st movement (Vivace)** (c. 1730; Bach d. 1750, PD).
  - Source: Mutopia-2015/09/02-3 (Bach-Gesellschaft 1874, **Public Domain**), at `<SOUNDFONTS_DIR>\scores\bach_double_bwv1043\score.mid` (licence in `concerto-in-d-minor.rdf`).
  - No other scene uses it. It is not on the used or banned lists, not Chopin, not kid-coded and not circus.
- **Excerpt:** the opening ritornello, score beats 0-30 (bars 1-8): the fugal subject in violin II, the answer in violin I at bar 5 (8.0 s, right on the lead change), to the **A-minor cadence at bar 8 beat 3 = 15.00 s = the collapse**.
  - Frame 0 = the piece's first downbeat. One steady tempo, quarter = 120.
- **Arrangement** (lib/orchestra, MuseScore_General): every part is read from the score.
  - Tutti violins I/II on strings plus the two solo violins on violin, viola, the continuo on cello plus contrabass an octave down, and harp (a harpsichord stand-in). A CC11 crescendo through the clip.
  - **Cadence:** a held A-minor block (strings, soft horns, cello and bass A, a rolled harp, timpani A, a soft boom).
- **SFX** (all tonal, nothing above ~5 kHz, no noise beds):
  - **Mochi:** a big marimba-like stone clack per pry on the beat, pitched to the strings' chord near D5, plus a quiet pickaxe "tink" an octave up.
  - **Bolt:** a tonal thump for the kick. One crisp clack per 8th on which his rocks knock rocks loose, near G5, layering 1 + log2(rocks) voices (1 → 6).
  - **The valley:** a soft low knock per 8th on which rubble lands, pitched to the bass.
  - **The landslide:** a soft tonal rumble (A1 root, fifth and octave sines, slow swell) on the cadence, and a tonal thump when it buries Bolt (16.0 s).
- Mastering: cannon_split's `level_bed` (+2.5 dB crescendo, `--findb 1.5`) and `master_keep_lift()` (room reverb, -14 LUFS, a 5 ms lookahead limiter at -2 dBFS). The last 0.6 s is zeroed.

## Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\rock_avalanche.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 1062 frames = 17.70 s.
- Loudness: -14.01 LUFS, peak -2.00 dBFS. The last 0.5 s is silent (-240 dB).
- **RMS per second (muxed):** -18.0, -18.3, -17.6, -17.8, -17.1, -17.4, -17.2, -17.1, -16.1, -16.1, -16.2, -16.1, -15.6, -15.4, -16.1, -14.5, -17.5, (tail). No second below -18.3 before the finale.
- **Finale:** 0.4 s RMS +2.4 dB over the body. Energy above 4 kHz: 0.18%.
- SFX events per second: 3, 4, 4, 3, 6, 5, 4, 5, 7, 8, 6, 9, 8, 9, 10, 5, 3. Bolt's clack voices per second climb 5 → 16.
- flash_check: 0 flashes = PASS (mean luminance 0.015).
- **Loop seam:** check_clip mean delta 0.685 (good band 0.12-0.72). The last frame is the pre-roll frame start-1, fully dissolved.
- Side safe zone: lanes, HUDs, caption, characters, stickers and banners all sit inside 0.10-0.84w. Mochi's right edge is at ~0.80w; Bolt is at 0.77w (0.66w once zoomed).
- Frames read from the encoded file at 0, 0.5, 1, 2, 8.25, 13.0, 15.05, 15.6, 16.3 and 17.68 s, plus a 1:1 crop of Bolt's heap at 13.0 s (×2 pops, hopping rocks, the eaten face). Fast stills at 0, 0.5, 1, 2, 8, 15, 15.75, 16.25 and 16.7 s.

## Nits / doubts

- **Bolt's side is quiet from 2 to 4 s:** 0 rocks in second 3; the summit ×2s are small. Mochi carries the hook (a pry on every beat), and the kick plus the first ×2 land at 0 s and 1 s.
- **Scripted parts:** the branching (hit/miss outcomes, solved arcs), the collapse rule (≤ 40% left), the braking stop points in the valley, and the landslide toe's kinematic slide onto Bolt. Everything on screen moves consistently under one gravity, but the burial is aimed.
- The remaining heap at the cadence is a tall pillar against the cliff: the avalanche eats the face, not the core.
- Rocks are small at phone scale (18 px cells). The ending zoom makes the punchline readable, but the race itself is busy-small.
- The ending is 2.7 s after the cadence (clip 17.7 s, near the 18 s ceiling).
- Some race rubble rests in hollows of Bolt's heap until the collapse.

## Args and cost

- Defaults are the shipped values: `--seed 182 --p0 0.62 --p1 0.80 --pramp 13 --dramp 12 --reach 34 --uptol 14 --rfin 0.40 --tlead 8.0 --tend 2.70 --boltx 720 --ovl 0.72 --frrock 240 --frgnd 2200 --frslide 480 --pbury 0.20 --buryw 64 --buryt0 0.75 --buryt1 1.05 --brake 1800 --zoom 2.0 --fin 2.0 --findb 1.5 --sfx 0.24 --timp 0.36 --boom 0.18 --rumble 0.30`.
- Other args: `--search --seeds a,b` (prints seeds whose collapse lands on the cadence), `--report`, `--cache` (pickles the sim in output/), `--still --frame a,b`, `--audition`, `--reuse`, `--sound 0`, `--label`, `--cap`.
  - Any change to the branching parameters reshuffles the RNG, so re-search seeds after one.
- Cost: sim ~3 s; Full HD render ~70 s at 2 encoder threads.
- Owner review: pending.
