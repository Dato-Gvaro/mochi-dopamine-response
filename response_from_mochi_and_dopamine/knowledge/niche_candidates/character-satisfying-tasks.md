# Niche: character-satisfying-tasks

**Status:** candidate (leader of the three)
**One-line pitch:** Tofu, a soft white blob with dot eyes, sorts, stacks, fills and cleans with crisp synthesized ASMR clicks, getting faster and happier until the task snaps complete.

Owner fit (satisfying + 1-2 recurring characters): **high.** This is literally the brief. The character is the brand and the task is the satisfaction.

## Hard filters
- [x] Code-renderable at quality. The best-performing competitor (@hayang04, 557k) uses simple line art: a white cat outline, flat fills, thick dark strokes (`ref_character-satisfying-tasks_2`). Cairo draws that natively.
- [x] Nameable change per episode: a new TASK ("this time Tofu sorts beads by SIZE").
- [x] No borrowed IP. Never do the PurrNest route (FNAF and Poppy Playtime restoration).
- [x] Loop: the finished task resets (the jar tips out, the stack topples) to frame 0. Compilations: hayang's long-form ASMR runs 2-8 min at a 961k median.
- [x] Advertiser-friendly. Avoid the gross-out sub-genre (ingrown toenails, ear wax).

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 4 | Small channels broke out in the last 90 days. @LittleJoy_World-z9c (18.3k subs) "This Cute Cat Makes a Tiny Pizza!" got 3.0M (2026-09-10, 40 s), with 5.4M (2026-09-13), 631k and 556k (cat café/tea ASMR). @uncoveredroom (2.87k subs) got 3.2M and 2.2M "Cute Cashews Make Kaju Katli" (2026-09-07, 18 s) with face-on-food characters. @PurrNest_ASMR (35.1k) has 2.1M and 359k. Caveat: LittleJoy and uncoveredroom are generative-AI 3D, so this proves the hunger for "cute character does a satisfying task", not our exact look. |
| Supply gap | 3 | The top is hand-drawn and slow. @hayang04 has 19 long videos; @cuppacatasmr (279k) posts about monthly. The small breakouts are AI 3D, the kind of mass-produced content the inauthentic policy targets. Code-drawn, crisp, original 2D with deterministic physics is unoccupied. |
| Our edge | 3 | Real physics for the satisfying part (granular fill, sorting, stacking, liquid levels), with each item's sound synthesized exactly on its event at 4K60. That cadence (5 Shorts/day) is impossible for hand animators. The weakness is character ACTING: hayang's expressive keyframed animation beats a procedural rig, so keep the character simple and let the task carry. |
| Episode depth | 5 | Tasks × materials × containers: sort by colour, size or shape; stack, fill, polish, untangle, fold, pack; ice cubes, beads, coins, marbles, sand, jelly. 50+ is obvious. A sidekick adds "Tofu vs Pebble race to finish" episodes. |
| Long-form RPM | 4 | Long-form demonstrably works. @hayang04 /videos median is 961k (6.3M "Cat's Lash Salon", 249 s; 4.1M, 384 s). @cuppacatasmr's "Mukbang Compilation ASMR" got 1.7M (503 s) and "Compilation 2" 1.5M (483 s), proving 8 min compilations. Calm ASMR works as background viewing. Made-for-kids risk docks a point. |
| Build cost | 3 | Needs `lib/character.py` (blob body, eyes, arms) and a task sim (sorting chute plus jars). The arena, collisions, plink voices and `MelodyWalker` exist. About 1-2 days to a first clip, slightly over the 1-day bar. |
| Policy safety | 4 | Original character, a new task each episode, code-authored with no AI. The made-for-kids classification (cute cartoon) must be answered honestly at upload: aim the look and titles at teen/adult ASMR-relax viewers, not toddlers. |
| **Total** | **26/35** | Best of the three. |

**Cannibalisation vs parent:** LOW-MEDIUM. Both are "satisfying". The parent is abstract neon-on-black physics; this is warm, light-background, character-led ASMR (task completion, cosiness). Tofu's face and reactions are what viewers subscribe to. Keep it distinct: no neon, no black arena, no "how many can it handle" escalation captions.

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @hayang04 | 557k | 2023 | shorts 414k, 252k; long 6.3M, 4.1M, 4.0M | line-art cat runs a salon or spa; ASMR at -29 LUFS (quiet foley) |
| @cuppacatasmr | 279k | about 2023-24 | long 2.3M, 1.7M (compilation), 1.5M | cat mukbang and spa, 3-8 min |
| @PurrNest_ASMR | 35.1k | 2024-11 | 2.1M, 359k, 155k, 59k, 54k | restoration ASMR but borrowed FNAF/Poppy IP (do NOT copy) |
| @LittleJoy_World-z9c | 18.3k | 2026 | 5.4M, 3.0M, 1.1M, 631k, 556k | AI 3D cat "Mochi" cooking/café, 40-66 s |
| @uncoveredroom | 2.87k | 2026 | 3.2M, 2.2M, 1.1M, 583k, 207k | AI food-with-faces cooking, 18 s; median only 4k |

## Reference videos decoded
- `ref_character-satisfying-tasks_1` (LittleJoy, 3.0M, 40 s). An orange kitten in an apron makes pizza: empty plate, knead, sauce spiral, oven, bites. Each step is one "satisfying" close-up. It ends where it began (eating at the plate). AI 3D, no text.
- `ref_character-satisfying-tasks_2` (hayang, 414k, 58 s). "cat's hair salon": a white outline cat grooms a woolly sheep-client. Close-ups of the fluff, a clipper, a shampoo pump, a water rinse, then a fluffy reveal. Letterboxed, title text top, handle bottom. Quiet foley ASMR (-29.4 LUFS, gaps). Very cairo-friendly line art.
- `ref_character-satisfying-tasks_3` (uncoveredroom, 2.2M, 18 s). Cashews with faces get ground, cooked and rolled, then cut into diamonds that cheer at the end. AI; human hands. The characters' REACTIONS to the task are the hook.

## Characters
- **Tofu** (lead): a soft white rounded-square blob. Body is a 4-point bezier path with squash and stretch (scale y/x by "effort"), a 5-6 px ink outline, two dot eyes, a small mouth arc, pink blush ovals, and stub arms (thick round-capped lines with an IK-lite 2-segment reach to the current item).
  - **Emoting:** blink every 2-4 s (seeded); `^ ^` arcs on each success; `> <` on effort; a sparkle burst when a container fills; a bigger, faster bounce as the streak grows; a happy wiggle at completion.
- **Pebble** (optional sidekick): a small grey round blob, a chaotic helper. Steals or helps items, and races Tofu in "who finishes first" episodes.
- **Sound:** soft synthesized clicks, pops and plinks per item (`synth_plink`, `synth_pok`, `synth_snap`, `synth_squash` exist). Tofu has a tiny pitched "mm!" chirp (sine blip, not voice) on success, and a PD melody walks across the sorted items.

## 10 episode ideas (each with its nameable change)
1. Tofu sorts falling candies into 4 colour jars.
2. Tofu sorts beads by SIZE through a sieve.
3. Tofu stacks blocks; the tower must reach the top line.
4. Tofu fills a jar with sand, layer by colour (rainbow jar).
5. Tofu scrubs a muddy floor tile by tile (clean reveal).
6. Tofu packs a box with odd shapes (Tetris-fit).
7. Tofu untangles a knot of yarn.
8. Tofu pops a sheet of bubble wrap, faster each row.
9. Tofu vs Pebble: who fills their jar first.
10. Tofu sorts coins into stacks by value; the stacks climb.

## Engine changes needed
- look (palette, background, fonts): warm light palette (cream/pastel background, ink outlines, pastel item colours), a rounded font. Re-skin `studio.PALETTE` once; add `Canvas.blob()` / outline helpers.
- layouts: a "workbench" layout. Character lower-left, task area centre, containers in a row at about 0.6-0.7h in 9:16; in 16:9, character left and task centre-right.
- audio voice: ASMR click/pop voice set at lower intensity (quiet, crisp), plus the success chirp. Master at -14 LUFS but keep sparse transients.
- new lib module: `lib/character.py` (rig, emote states, arm reach) and `lib/tasks.py` (sorting chute, container fill levels, stack physics).

## Risks
- Made-for-kids classification (cute cartoon). Must answer honestly; it kills comments and mid-rolls.
- The breakout evidence is AI 3D, so code-drawn 2D is unproven at Short scale. Hayang proves 2D line art works but took years.
- Character acting quality versus hand animators.
- Quiet ASMR versus the parent's loud event density, so retention behaviour is unknown.
- Escalation must be honest: speed up the task without making it frantic.

## Cheapest proving test clip
"Tofu sorts 200 falling candies into 4 colour jars." About 30 s in 9:16. Candies fall from a chute faster over time. Tofu flicks each one left or right into jars (plink per sort, the melody walks with it). The jars fill visibly, Tofu's eyes go `^ ^` per streak, and a sparkle fires on each full jar. At the end the jars tip back into the chute, giving the frame-0 loop. Reuses the circle and collision code and plink voices; the new code is the Tofu rig plus jars, about 1-2 days.
