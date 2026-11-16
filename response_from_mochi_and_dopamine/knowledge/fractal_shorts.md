# Fractal / Koch Shorts: what works (research 2026-10-23)

Why: the owner rejected `ol_koch_snowflake` v2 and v3 ("not engaging at start", then "search successful versions"). Scene notes are in `docs/scenes/ol_koch_snowflake.md`.

Method:
- YouTube search pages (hl=en, gl=US) were parsed for Shorts shelves.
- `yt-dlp -j --skip-download` gave views, likes, date, length and channel.
- Frames were read from YouTube storyboard sprites (about 1 frame/s, 101x180). No videos were downloaded.
- Views are as of 2026-10-23.
- **Audio was not checked on any video (unverified).** Sprites cannot show sub-second timing; "first 2 s" means storyboard frames 0-2.

## Headline finding
The Koch snowflake as a TOPIC is weak on Shorts.
- "Infinite perimeter, finite area" Shorts mostly sit at 0.1-5K views. Exceptions: MrGee (a talking head, 261K), MathVisualProofs (85K) and MathCa (60K).
- The fractal Shorts that reach millions:
  1. Show a striking, complete shape (or one already moving) at frame 0.
  2. Make the silhouette change BIG every second, not get finer.
  3. Carry a challenge or question caption.
  4. End on a nameable payoff.
- Getting finer is exactly where our v1-v3 died: from about gen 5 the new detail is sub-pixel.

## Examples (views | length | date | channel)

| # | Short | Views | Len | Date | Channel (subs) |
|---|---|---|---|---|---|
| 1 | [Binary Fractal Tree Creates MAGICAL Patterns](https://www.youtube.com/shorts/nFyA7qElVIo) | 7.96M | 18 s | 2024-01-07 | Visual Alchemy (182K) |
| 2 | [How The Sierpiński Triangle Repeats Itself](https://www.youtube.com/shorts/MIKUO5wpFV8) | 9.02M | 39 s | 2026-09-08 | Zack D. Films (29.3M) |
| 3 | [Can you Guess the Fractal?](https://www.youtube.com/shorts/e9CCJ0OV-UM) | 2.78M | 42 s | 2024-03-07 | Visual Alchemy |
| 4 | [Fold a strip in half 12 times, open to 90°: a dragon](https://www.youtube.com/shorts/CbTu5Ye77s4) | 1.22M | 30 s | 2026-10-17 | Rollody (1.4K!) |
| 5 | [Snowflake Fractals](https://www.youtube.com/shorts/Oog_thZrExE) (Koch) | 1.12M | 60 s | 2024-05-09 | Chirag Dudhat (344K) |
| 6 | [Infinite Sierpiński Zoom](https://www.youtube.com/shorts/3EtaP1HnBm4) | 652K | 5 s | 2023-10-25 | Mathematical Visual Proofs (260K) |
| 7 | [VFigures KOCH SNOWFLAKE](https://www.youtube.com/shorts/201odsb3Bb4) | 491K | 23 s | 2026-10-12 | 27Balls (77K) |
| 8 | [6,560 Steps, One Line, Every Cell of a Square](https://www.youtube.com/shorts/ehnQNKt7U6o) (Peano) | 284K | 49 s | 2026-10-20 | Rollody |
| 9 | [This shape has an infinitely long perimeter!](https://www.youtube.com/shorts/CVf48N_BAcY) | 262K | 59 s | 2025-06-07 | MrGee Math (178K) |
| 10 | [The Koch Star Fractal Pattern](https://www.youtube.com/shorts/IS1oB9cR7Zk) | 92K | 40 s | 2024-03-26 | webduncetv (12K) |
| 11 | [Koch Snowflake: Infinite Perimeter but finite area](https://www.youtube.com/shorts/yuCKYvh3bUw) | 86K | 60 s | 2025-01-21 | Mathematical Visual Proofs |
| 12 | [Can a shape with finite area have an infinite edge?](https://www.youtube.com/shorts/fIoOtZUVeqA) | 60K (in 3 days) | 24 s | 2026-10-20 | MathCa (19K) |
| 13 | [The Koch Snowflake but every iteration is audible](https://www.youtube.com/shorts/V6FOsh7tTsU) | 36K | 20 s | 2025-08-13 | Infinity SI (149K) |

Also seen:
- Imagine falling into the Mandelbrot Fractals (HcyGjt3pC1w): 6.6M.
- DIY Fractal in PAINT (0TqGhHmoj7o): 3.9M.
- Zoomquilt (jlgTPCHsOpc): 19M.
- Mandelbrot "Outbound… horrific" (PzvfVl8ichs): 1.86M, 12 s.
- PENTADENDRITE (GX9WW15gJpA): 1.24M.
- L-System Fractal Unfolds (7pIje5mbH74): 1.14M.
- Dragon Fractal Curve (bkO5pwClw9U): 397K.
- Quintuple Fractal Tree (5BjuKaaleLk): 381K.
- Lingualin ternary tree / dragon (N8Srozf63ig, ePFP3YL1xO4): 361K / 329K.

## What is on screen (storyboards)

**1. Binary tree (7.96M).**
- Frame 0 is already a full fractal: a magenta-to-orange canopy on near-black.
- Caption: "CAN YOU PAUSE IT PERFECTLY?"
- The branch angle sweeps continuously, so the silhouette morphs every second: mushroom → hexagon → Sierpiński triangle → pentagon → bat.
- The video ends back on the opening shape, so it loops. The quintuple tree (#381K) is the same template.

**2. Zack D (9M).**
- A 3D-rendered hand and pen draw on a whiteboard. Subtitles: "Place a point anywhere inside the triangle".
- This is the chaos game, explained step by step. The Sierpiński triangle then appears with green "1 2 3" highlights.
- It ends on a zoom and a red ∞ drawn on the triangle.
- Voice narration (Zack D's normal format; the audio itself was not checked).
- Its reach comes from the channel's 29M subscribers. It is not a template for us.

**3. Guess the fractal (2.78M).**
- Frame 0 is one white line on charcoal. Caption: "CREATE A FRACTAL WITH ME" / "CAN YOU GUESS…".
- Copy, rotate 90° and attach, every ~1 s. The shape lurches into a new silhouette each step, and the Lévy C curve emerges.
- No camera moves: the shape is rescaled to fit.

**4. Rollody dragon (1.22M in 6 days, from a 1.4K-subscriber channel; closest to our style).**
- Dark navy background, glowing strips coloured by generation (teal / orange / blue).
- Question caption at the top: "Fold a strip in half 12 times, open every crease to 90°. What shape?"
- Big counters FOLDS / SEGMENTS (1/2 → 12/4,096). Frame 0 is a strip already mid-unfold.
- Each fold doubles the silhouette and it re-fits to the frame.
- Payoff: "the Heighway dragon" is named, then 4 dragons in 4 colours tile around one point with "SHARED EDGES 0".
- The same channel's Peano Short (284K) uses the same grammar. It has a counter with the target visible from frame 0 ("4 / 6,560"), a caption that is a spec ("One line, never crossing, must visit all 6,561 cells"), a pink fill sweeping the grid, and a rewind to loop.

**5. Chirag Dudhat Koch (1.12M).**
- A thin white pen line draws the triangle stroke by stroke from frame 0.
- Each iteration is drawn as a moving pen trace. Mid-video the camera zooms along one edge to show self-similarity, then pulls back.
- It ends on a "Koch Snowflake Fractal" title card.
- Plain and slow, 60 s. Its reach probably comes from his Mandelbrot hits (6.6M) (unverified).

**6. Sierpiński zoom (652K).**
- A 5 s perfect loop: an infinite zoom where the end frame equals frame 0. Replays inflate views.

**7. 27Balls VFigures (491K).**
- Not a growth demo. Koch-edged polygons named "triangle / hexagon / …" fall into a V on a cyan background.
- It is a physics series that borrows the name.

**9. MrGee (262K).**
- A talking head with big punch-word captions ("FINITE AREA", "INFINITELY LONG PERIMETER") and paper cut-in diagrams.
- Personality-driven; not applicable to us.

**10. webduncetv (92K).**
- Opens on the FINISHED snowflake with the title "KOCH STAR", which is the end state at frame 0.
- Then it resets to the triangle, and each generation's new bumps flash green before turning red.

**11. MathVisualProofs (86K).**
- Thin blue Manim lines on black. Formulas stack under the shape.
- It ends with a red circle around the flake (finite area).

**12. MathCa (60K in 3 days).**
- The same look as ours: navy background, circle arena, a question caption plus a big "edge = 3.00" counter.
- A comet-ball runs along the edge, and the edges it leaves sprout spikes.
- The colour shifts by generation: teal → violet → pink → orange → gold. The end reads "edge → ∞".
- The same channel has 17M and 2M Shorts with "Will they…?" question captions.

**13. Infinity SI (36K).**
- A Koch-antisnowflake variant in coloured nodes on black. Caption: "does this sound satire?". Each iteration is sonified.

## Patterns that worked
1. **Frame 0 is already interesting**: a complete fractal (VA tree, webduncetv), or something visibly in motion (Rollody mid-fold, Chirag's pen, MathCa's ball). Never a static plain triangle.
2. **Big silhouette changes, not finer detail.** The winners change the WHOLE outline every ~1 s: angle sweeps, folds, copy-and-rotate. When detail would go sub-pixel they re-fit, morph, or switch mechanic. Camera dives into detail appear only in pure-zoom loops (Mandelbrot, Sierpiński), which are a different genre.
3. **A challenge or question caption**: "Can you pause it perfectly?", "Can you guess the fractal?", "What shape?", "Don't blink!". Our caption rule bans viewer-prediction questions. "What shape?" and "Can you guess" are prediction-type, so this conflicts with our rule.
4. **Counters with an exponent and a target**: Rollody's FOLDS 12 / SEGMENTS 4,096 and "/ 6,560"; MathCa's edge 3.00 → ∞.
5. **A nameable payoff** beyond "it got detailed": the dragon is named, then 4 dragons tile with 0 shared edges; a famous shape emerges from an unrelated rule.
6. **Length**: 12-24 s for morph and zoom Shorts; 30-49 s only with a reveal structure.
7. **Colour**: on black or navy, either a single warm gradient (VA) or colour per generation (Rollody, MathCa). Both fit our calm rainbow.

## Recommendations for a redone Koch Short
1. **First 2 s.**
   - Open on the full, glowing, multi-colour snowflake, centred and filling ~0.7w. A tracer or comet is already racing along its edge, and a big counter is ticking ("EDGE 3.00 → ∞" with ∞ shown as the goal).
   - The caption is a spec, e.g. "Every edge grows a spike — the edge never stops".
   - Then snap back to the triangle and rebuild fast: gens 1-4 in about 2 s, each gen in its own hue.
   - No camera dive and no slow zoom.
2. **Make the silhouette change, not shrink.**
   - After gen 4-5, keep the whole flake in frame and sweep the spike angle (Koch → Cesàro family, 60° → 85°+). The outline then morphs every second, and the edge visibly packs toward filling the triangle. This is VA's 8M mechanic applied to Koch.
   - Alternative: copy and tile. Koch snowflakes of two sizes tile the plane. Grow one, then clone it outward in rainbow rings until the frame is tiled.
3. **End state and payoff.**
   - A named, finite answer the video certainly delivers, e.g. "EDGE → ∞, AREA = 1.6×", with a gold ring locking around the flake (MathVisualProofs' red circle, done our way). Or the finished tiling: "0 gaps".
   - Then loop back to frame 0.
   - Total 12-18 s. One note per generation or tile ring (unverified for the references; their audio was not checked).
