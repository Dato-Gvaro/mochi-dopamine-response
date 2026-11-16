# box_tower — Mochi stacks 1, Bolt tosses 2: first tower to the CEILING wins (batch50, 2026-10-25)

- Brief: docs/BRIEF_batch50.md ("box_tower") + docs/BRIEF_batch51.md lessons (the win looks like winning; the music fits the mood). New scene file; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch50\box_tower.mp4` (**v1**, Full HD 9:16, 14.65 s, 879 frames; output label v3).
- Caption (baked; `--nocap` gives the base): "Mochi stacks ~1~, Bolt tosses ~2~:" / "first tower to the ~CEILING~ wins".
- **Twist:** the fast method loses. Bolt leads from frame 0 to 22 vs 17. His sloppy stack leans more with every toss, tips three boxes short of the ceiling and buries him. Mochi's straight column touches the ceiling on the cadence.

## Layout
- Warehouse interior with a steel ceiling girder (hazard-striped underside and a "CEILING" plate) at y 420, visible from frame 0. Floor y 1320. A steel pillar at x 1040 is the right wall.
- Boxes are 104 × 36 kraft cardboard boxes: Mochi's have coral tape, Bolt's mint tape. The kraft tone darkens slightly with height (ordered, not rainbow).
  - 25 boxes reach the ceiling exactly.
- Towers: Mochi at x 300, Bolt at x 560. Characters (r 42) stand on the floor: Mochi at x 168, Bolt at x 845. All key content is inside x 0.10–0.84w; only the debris pile against the pillar goes wider.
- A dashed plumb line runs straight up from each base. Mochi's column sits on hers; Bolt's drifts off it, and a second dashed line from his base to his top box (green → amber → red) shows the lean.
- A tag rides at the top of each tower: the box count + "/ 25", plus a LEAN pill under it. Mochi's reads "LEAN 0.0°"; Bolt's climbs 2.7° → 10.6°, then reads "CRASHED!".
- HUD panel (y 1362–1544):
  - "FIRST TO THE CEILING WINS";
  - each side's name, count / 25 BOXES and rule ("STACKS 1 PER BEAT" / "TOSSES 2 AT A TIME");
  - a LEADING / TIED / CRASHED / WINNER pill.
- Calm camera (static), no white flash. The win is a gold glow + sparkles where Mochi's box meets the ceiling.

## The rule and the physics (honest)
- **Mochi:** one box a beat, dead centre and flat. From beat 15 (right after the crash) one box per eighth note. Her boxes are lobbed in a neat arc from above her head. The top boxes arc in flatter so nothing passes through the ceiling; the 25th slides in at its apex.
- **Bolt:** a pair every dotted quarter (two boxes thrown together, landing a 16th apart). The pair spins in flight, and each box lands off-centre: a small drift toward him (9·(k/21)^0.6 px) plus a ±0.3 zig-zag. His 22nd toss is the sloppiest, 30 px off.
  - The boxes lie flat, so the stack is a leaning staircase.
  - A cosmetic ±1.4° skew per box (drawn only) blends out in the first 0.15 s of the crash.
- **Static check (`margins`):** for the floor and every box, the vertical through the centre of mass of everything above must lie over the support face.
  - The minimum margin falls 47.8 → 1.8 px through box 21, then goes to **−3.0 px at box 22** (the top 21 boxes tip about box 1's edge). The scene asserts that box 22 is the first unstable count.
- **The crash = a rigid-box simulation** (scene-local; deterministic; dt 1/480; 20 sequential-impulse iterations):
  - gravity 2200 px/s², box friction 0.30, floor friction 0.6, restitution 0.3;
  - SAT pair normals, so a loaded stack does not squeeze boxes out sideways;
  - colliders: Bolt's head (a circle), Mochi and her tower (fixed), the floor and the pillar.
  - It starts the moment box 22 lands, with that box's landing velocity. The upper 17 boxes swing over as one bending column and fold down onto Bolt and against the pillar. A 5-box stub stays.
  - Box count (clip s): 22 at 8.44 → 17 → 13 → 5.
- **The hat:** the first box to touch Bolt's head from above (box 14) snaps onto his head at clip 9.88 s (a cartoon cheat). Dazed stars circle it.
- Growth: Mochi +1 a beat (3 → 25, quarters then eighths). Bolt +2 a toss (4 → 22) and is ahead 22 vs 17 at the topple.

## Timeline (clip s; clip = sim + 0.15)
- **0.0 s:** Mochi 3, Bolt 4 (LEADING, lean 2.7°). Mochi's box 4 lands at 0.15 and Bolt's pair is mid-air. The pair lands at 0.48 / 0.64.
- **0.5 / 1 / 2 s:** 4 v 5 (lean 3.9°) → 5 v 6 (3.8°) → 6 v 8 (4.6°). A box is in the air on both sides in every frame.
- **6.3 s:** "IT'S LEANING..." (Bolt 17, lean ~8°). Mochi laughs.
- **7.46 s:** "ALMOST THERE!" (Bolt 20 vs 15). Bolt cheers; Mochi is worried.
- **8.44 s:** box 22 lands ("LEAN 10.6°"). A long tonal creak, then "UH-OH...", and the tower begins to fold.
- **8.89 s:** CRASHED (the count drops). **Lead change ≈ 8.97 s:** Mochi leads as Bolt's count falls past hers.
- **9.88 s:** the column slams down on Bolt. "CRASH!", hat box on his head, wince, then a dazed/annoyed face with stars.
- **9.9–11.53 s:** Mochi's sprint: one box per eighth note, each with a rising chime.
- **11.85 s (cadence, bar 20 A-flat):** box 25 touches the ceiling. Gold glow, "MOCHI WINS!", HUD WINNER 25 vs CRASHED 5. Mochi cheers, then laughs.
- **12.7 s:** "again?" next to Bolt (buried, box on head, deadpan).
- **14.05–14.65 s:** dissolve into the pre-roll (sim −0.75 → −0.15). The HUD switches at the midpoint.

## Sound (music first)
- **Piece:** Scott Joplin, *The Easy Winners*, A Rag Time Two Step (c. 1901; Joplin d. 1917, PD). It is a playful, bouncy rag, chosen for a cartoon stacking stunt per the batch51 mood lesson.
  - Not on any used or banned list, and no other scene uses it (other Joplin used: Entertainer, Maple Leaf, Elite Syncopations, Pineapple Rag). Not kid-coded.
- Source: Mutopia-2013/01/08-352 (engraving and MIDI placed in the **public domain**), at `<SOUNDFONTS_DIR>\scores\joplin_easy_winners\winners.mid` (+ `.ly`, `-let.pdf`, `SOURCE_mutopia_352.txt`). Downloaded 2026-10-25.
- **Excerpt:** A strain, bars 11–20, from the bar-11 downbeat (sim 0) to the **bar-20 A-flat downbeat = the ceiling touch, 11.85 s clip**. One steady tempo, quarter = 0.65 s (92 bpm, "Not fast").
- **Arrangement** (lib/orchestra, MuseScore_General):
  - honky-tonk piano on both hands (runtime alias, as in bowling_hook) + a soft grand piano on the top voice;
  - tuba + pizzicato on the bass;
  - clarinet doubling the tune from bar 13, soft strings on the chords from bar 15;
  - a light kick on beat 1 and rim on beat 2;
  - **cadence:** A-flat tutti (strings_slow, brass, honky chord, tuba, timpani) + a celesta arpeggio.
- **SFX** (all tonal; energy above 4 kHz 0.14%):
  - cardboard "thock" per landing (round body dropping onto the note in 10 ms + 2.3× and 5× partials), pitched to the chord sounding and climbing with height;
  - a soft "hup" tick per throw;
  - a **tonal creak** per Bolt pair once the lean is over 1.5° (a bowed-wood groan: harmonics 1–3, slow bend, 13 Hz stick-slip flutter, louder with lean);
  - a long bending creak at the topple;
  - **crash clatter** = every simulated impact over 140 px/s, gathered on a 32nd grid and pitched to the harmony (lower for harder hits, doubled a fifth up for clusters);
  - a "bonk" when boxes hit Bolt and when the hat lands;
  - Mochi's sprint chimes climb the A-flat scale; a three-note ding chord at the ceiling.
- Mastering: `level_bed` (+2.5 dB crescendo, `--findb 2.0`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS), with the last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 879 frames = 14.65 s.
- −14.00 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −18.0 −17.8 −17.9 −17.6 −17.3 −17.3 −16.8 −17.2 −15.8 −15.8 −14.8 −16.1 −13.8 (cadence) −16.4 (hold), then the silent tail.
- SFX events/s: 8 6 8 7 7 7 7 8 6 16 24 8 4 0.
- Box landings/s: 4 3 4 3 4 3 4 4 3 2 3 3.
- flash_check PASS (0 flashes, mean luminance 0.031).
- Seam (check_clip): 0.575 mean delta encoded (within 0.12–0.72); the dissolve goes into the pre-roll.
- Frames read from the mp4 at 0, 0.5, 1, 2, 6.4, 7.4, 8.4–9.0 (topple onset), 9.55–10.6 (the fold and crash), 11.72 / 11.87 (ceiling touch), 13.0 and the last frame.
- 1:1 crops: the ceiling contact at 11.72 s and Bolt buried with the hat at 13.0 s.

## Doubts
- The lean reads modest (max 10.6°). That is honest for a 22-box staircase of 104-px boxes (it tips once the centre of mass passes a support edge). An earlier "curved, crushed cardboard" model reached 26°, but rigid boxes cannot hold that shape, and the sim threw boxes out, so it was dropped.
- Several fallen boxes come to rest standing on their ends against each other and the pillar. This is the physics, but it looks a little tidy.
- The event rate sags after the crash (second 11: 8/s) before the cadence. Mochi's eighth-note sprint + chimes carry it.
- Cartoon cheats:
  - boxes appear above the characters' heads before each throw;
  - the hat box snaps onto Bolt's head;
  - the 25th box slides in level under the girder.
- The Easy Winners was newly downloaded; the parallel batch50 builders were not checked for the same pick.

## Args and cost
- Args: `--sfx 0.34`, `--findb 2.0`, `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- `--report` prints the per-box lean and stability margins, the crash timings and the counts.
- Cost: the crash sim is ~3.5 s; the Full HD render is ~30 s at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)
