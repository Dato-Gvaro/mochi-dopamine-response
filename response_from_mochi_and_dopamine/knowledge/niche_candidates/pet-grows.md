# Niche: pet-grows (satisfying eat / grow / evolve loop)

**Status:** candidate
**One-line pitch:** a cute blob (MOCHI) sits under a candy rain; every piece it
catches goes *chomp*, the counter ticks, and it visibly grows — the rain keeps
getting heavier until the frame can barely hold it.

Researched 2026-10-03. Framed as SATISFYING (owner scope change): crisp
eat -> grow -> evolve loop, one sound per eat event, visible counter. No sketch
comedy, no teaching.

## Hard filters
- [x] Code-renderable at quality — already proven: `scenes/mochi_feast.py` +
      `lib/toon.py` (uncommitted, 2026-10-03) render Mochi eating 320+ candies
      with a counter (output/mochi_feast_s1_f2100.png).
- [x] Episodes differ by a nameable change (food type / delivery machine /
      growth rule / evolution stage — see ideas)
- [x] No borrowed IP — the small breakouts in this lane lean on Minecraft
      (Cublium) and Pac-Man (Mantu AP, parent channel); we must NOT. Own cast only.
- [x] Short loop/payoff (burp back to frame-0 size = loop) AND 8+ min
      compilation (a "Mochi eats everything" marathon)
- [~] Advertiser-friendly — yes as designed, BUT the "eats and grows" search
      space is crowded with weight-gain / inflation / vore fetish uploads (see
      Risks). Growth must read as a game level-up, never a body.

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 4 | Small channels broke out in the last ~90 days on exactly "eat -> grow": **Cublium** (8.49k subs, first Short 2026-05-27) "Hungry Worm Steve Eats Too Much and Gets HUGE!" **5.5M** (Aug 2026), 2nd 4.6M, median 82k; **Mantu AP** (4.96k subs) Pac-Man grows/eats Shorts 4.1M / 3.2M / 3.2M. Original-character cute cast proven by **pio the platypus** (first Short 2026-01-14, now 191k subs, 213 Shorts, median 933k, "Protect Otti from the rain!" **15.9M** on 2026-09-19). Parent prior: "Pac-Man ate the ENTIRE ghost swarm" 754k, "Can Pac-Man reach the core?" 669k. -1 because the biggest small-channel hits borrow IP. |
| Supply gap | 4 | Search "pet grows / blob eats and grows / tamagotchi evolution" (Shorts filter, this year) returns Roblox gameplay ("Eat Blobs to Grow MASSIVE"), Minecraft, AI kids slop with 0-1k views, and fetish content — **no clean original-character eat/grow sim channel found**. Top comps are composites (real person + 3D Pac-Man) or 3D Minecraft. |
| Our edge | 4 | Deterministic physics: the counter is TRUE (every candy counted is a candy seen), one chomp note per event, 4K60, perfect loop via burp-reset. Cast already drawn in cairo with parameterised expressions (`toon.draw_char`). 3D comps (Cublium, Cuboidmonster) can't do 300+ exact events per clip cheaply. |
| Episode depth | 4 | Food x delivery machine x growth rule x evolution stage x arena = 50+ combos; each episode needs ONE that changes the outcome (not just candy colour). Risk of slide into re-skins if only food changes — guard at review. |
| Long-form RPM | 2 | Cute pastel cast + Minecraft/Roblox-adjacent comps = young audience, low RPM; Made-for-Kids misclassification possible (pastel animated characters is a YouTube MFK factor). Comps' long-form is weak: pio's 2 long-forms 9.5k / 11k views; Cublium none. Compilation is fine as background, but no comp proves it pays. |
| Build cost | 5 | `scenes/mochi_feast.py` already renders end to end (stills at f20/f60/f1000/f2100 + silent mp4 in output/). Audio voices exist: `synth_chomp`, `synth_gulp`, `synth_pok`, `synth_plink`. |
| Policy safety | 3 | Original cast, a nameable rule per episode. Minus: (a) template risk — "Mochi eats X" can decay into re-skins; (b) eat-and-grow is a fetish-genre trope (WolfyGoofyToons "Weight Limit Test" 702k, "Derg tube weight gain" 2.67M surfaced in the same searches) — keep growth abstract (stage-up, crown, sprout, shell), never belly/body-strain; (c) MFK-misclassification exposure. |
| **Total** | **26/35** | Above the 22 bar. |

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| Cublium (@Cublium) | 8.49k | 2026-05-27 (38 Shorts) | 5.5M, 4.6M, 2.3M, 1.6M, 735k | 3D Minecraft-look; worm eats food -> mound; ~18 s; titles "…Eats Too Much and Gets HUGE!" — borrowed look |
| Mantu AP (@Mantuapp) | 4.96k | 2026 | 4.1M, 3.2M, 3.2M, 1.2M, 1.0M | real person composited on 3D Pac-Men, 10-16 s, "ending will shock you" — borrowed IP, mixed content |
| Cuboidmonster 3d | 115k | 2025 | 17M, 16M, 1.4M, 1.2M, 716k | own googly-eyed capsule monsters, loops (#loops), 17 s; geometry simple enough for cairo |
| pio the platypus | 191k | 2026-01-14 | 15.9M, 4.9M, 4.3M, 4.1M, 3.6M | pastel flat vector duo (Pio + Otti), interactive/game Shorts ("Who climbs the fastest?" 3.1M, "Swimming race!" 2.8M) — proof a NEW original cast can break out in 2026 |
| Satisfying 2D Sims (parent) | ~10k | 2026 | 1.8M, 1.7M, 836k, 754k, 725k | prior only: Pac-Man eat episodes 754k / 669k |

## Reference videos decoded
- `ref_pet-grows_1` (Cublium, hZBbytdi-YM, 18 s): worm with Steve head eats cake/burger; body swells to a huge cone-mound; second character (Alex) reacts with open-mouth face. Escalation = size only, no counter. Ending: mound at max, no loop. Text: none on screen. Audio: comedic SFX + music.
- `ref_pet-grows_2` (Mantu AP, 3stwL4SjiVs, 16 s): man jumps onto coloured Pac-Men; each flattens; red one ends giant and swallows him. Payoff = final big chomp. Composite, borrowed IP.
- `ref_pet-grows_3` (Cuboidmonster, J3eG7VwgPRM, 17 s): row of capsule monsters with googly eyes + teeth; hearts/blocks pushed, door opens, new monster emerges, back to start pose = loop. Shows that big eyes + simple primitives carry a character.
- `ref_character_pio_1/2` (pio, 19 s / 27 s): flat pastel blobs, thick dark outline, dot eyes; text prompt top ("hover your finger to protect Otti!", "Choose your champion!" + countdown), clear WINNER/crown payoff. Exactly the line-weight style `lib/toon.py` already uses.

## The characters (already drawn in `lib/toon.py`)
- **MOCHI** — coral round blob with a hair curl. Greedy, bouncy; the eater.
  Body = closed bezier path scaled by `sx, sy` (squash on landing/chomp, stretch
  on hop), gradient fill + dark ink outline + shine highlight.
- **BOLT** — mint rounded-square with a two-leaf sprout. Calm, stubborn; the
  rival/feeder in duo episodes (feeds Mochi, or competes: who eats more).
- **Emoting** is all parameters: eye `look` (pupils track the nearest candy),
  `blink` (seeded schedule), mouth (smile / O / wide chomp / flat / wobble),
  brows (angry, worried), cheek blush, sweat drop, X-eyes. Growth stages add
  props (crown, bigger curl, sparkle aura), not body strain.

## 10 episode ideas (each with its nameable change)
1. **Candy rain** (built): every candy makes Mochi bigger; rain ramps 2/s -> 20/s. "Every candy makes it bigger."
2. **Doubling rain**: every candy eaten spawns TWO more at the top — exponential count. "Each bite brings two more."
3. **Peg-board Plinko feed**: candies fall through a Plinko board; only the slot Mochi sits in feeds it; Mochi slides to the busiest slot. "It has to find the jackpot slot."
4. **Evolution ladder**: every 50 bites Mochi EVOLVES (blob -> sprout -> crown -> star form); counter shows stage. "It evolves every 50 bites."
5. **Bolt vs Mochi eat-off**: two eaters under one rain, split screen bar (`versus_bar`). "Who eats more in 30 s?"
6. **Shrinking arena**: Mochi grows while the box walls close in — ends when it fills the box exactly. "It grows until it fills the room."
7. **Hard candy**: some candies are rocks — eating one shrinks Mochi; it learns to dodge (eyes track). "Rocks make it shrink."
8. **Conveyor feast**: a conveyor speeds up every 10 items. "The belt speeds up every 10 bites."
9. **Gravity flip**: every 25 bites gravity rotates 90°; Mochi rolls to the new floor. "Gravity turns every 25 bites."
10. **Comment-reply**: "make it eat 1,000" — counter target on screen, real count. "1,000 bites."

## Engine changes needed
- look: DONE in `lib/toon.py` (pastel sky/peach backgrounds, ink outline, sticker text). Lock it in CHOSEN.md; leave parent neon `studio.PALETTE` for any parent-style scene.
- layouts: mochi_feast hardcodes 1080x1920 (vertical-only, `FLOOR_Y=1360`). Needs a 16:9 layout (character centre stage, caption left, counter right) before compilations.
- audio voice: chomp/gulp per eat, pitched up the pentatonic scale per bite (ScaleWalker); evolution = short PD-melody phrase; burp at loop seam then silence.
- new lib module: `lib/physics2d.py` (circles + static segments) exists, uncommitted. Add: per-stage prop drawing, `evolve` animation helper.

## Risks
- **Fetish-adjacent neighbourhood**: "eat & grow" queries surface weight-gain/inflation/vore uploads. Keep growth abstract, never body distress; titles avoid "fat / stuffed / burst".
- **Made-for-Kids classification**: pastel cartoon characters are a listed MFK factor; mark "not made for kids" honestly only if the content/audience supports it — the satisfying-sim framing helps.
- **Re-skin decay**: "Mochi eats [new food]" is a re-skin. Each episode needs a rule change (list above).
- **Cannibalisation vs parent**: overlaps the parent's Pac-Man eat episodes (754k / 669k), but the look (pastel toybox vs neon-on-black) and the recurring named character make it a different channel with a different audience. Do not cross-post parent clips here.
- Long-form money unproven for character channels (pio long-forms ~10k views).

## Cheapest proving test clip
Already 90% built: finish `mochi_feast` (seed 1, 9:16, ~30 s, rain 2/s -> 20/s,
burp-reset loop), caption "Every candy makes Mochi BIGGER / How big can it
get?". Self-verify (onsets = eat events, -14 LUFS, rate still climbing at the
last frame), then owner review. Second clip to prove the franchise: idea 4
(evolution ladder) — it tests whether evolution stages carry episodes.
