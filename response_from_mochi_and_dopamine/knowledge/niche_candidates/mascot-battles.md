# Niche: mascot-battles

**Status:** candidate
**One-line pitch:** two faced rival blobs, Pip (red) vs Bloo (blue), slam around a code-physics arena under a new rule each episode; a versus bar says who's winning.

Owner fit (satisfying + 1-2 recurring characters): **medium-high.** The physics is satisfying. The rivalry pulls the format toward "who wins" tension rather than calm satisfaction.

## Hard filters
- [x] Code-renderable at quality. The references are flat 2D: a white square, circles, HP numbers (`ref_mascot-battles_1/2`).
- [x] Episodes differ by a nameable change: the arena or rule ("this time every hit makes the loser SMALLER").
- [x] No borrowed IP, as long as we avoid what Awesome_Ball_Battle does (Invincible, Pepsi, celebrities).
- [x] Short loop/payoff (KO, then the loser reforms at frame 0) AND 8+ min compilation (a tournament bracket of episodes).
- [x] Advertiser-friendly if the "weapons" stay cartoon (no blood). Weapon-ball comps carry no gore.

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 3 | Small channels do break out, but rarely. @weaponballfight (12.8k subs, started 2025-07-28) "the infinity slayer" got 1.33M (2026-03-28); its next best is 88k and the shorts median is 30k. @Eeize (5.7k subs) magenta-vs-blue ball sim got 511k in 1 day (2026-10-02), plus 319k and 174k (median 48k). Copycats stall: @Loggernamy (2.56k subs, 251 shorts since 2026-01-24) tops out at 20k, @weaponballfight-game (45 subs) at 3k, @Ballbrawls (9 subs) at 1.4k. |
| Supply gap | 2 | Weapon balls are saturated, and the originator is decaying. @Earclacks (209k) has a shorts median of 38k, recent shorts at 8k-29k and the best at 110k (2026-09-06). A this-month search returns Earclacks, Loggernamy, VXRITY, Ace Waters, Solistt, BallsBrawl and Micro_Studio, all in the same white-square look. The gap is FACES and a recurring rivalry: none of the weapon-ball channels have characters with personalities. |
| Our edge | 4 | Our engine already does the arena, collisions, `versus_bar`, per-event audio, 4K60 and deterministic seed search for close finishes. The references run at 30fps or lower with flat SFX. |
| Episode depth | 5 | Arena × rule × win condition: grow-on-hit, shrink-on-hit, gravity flips, spinning gaps, tug-of-war, races, king-of-the-hill, duplicate-on-hit (Earclacks' "Duplicator" got 110k). 50+ is obvious. |
| Long-form RPM | 2 | Long-form underperforms in this lane. @Earclacks /videos median is 17k (best 47k, 1-6 min). The audience skews young and gaming (comments, emoji titles). Battles watch well in sequence but less well as background. |
| Build cost | 5 | `_template.py` already does a ball bouncing in a circle with accelerating events. Adding two balls with faces (`lib/character.py`) and a versus bar (`Canvas.versus_bar` exists) is under a day. |
| Policy safety | 4 | The characters are original and each episode has a nameable rule change. The risk is that the weapon-ball LOOK reads as a template copy, so the look must be ours, not a white square with emoji weapons. |
| **Total** | **25/35** | Passes the 22 bar, narrowly. |

**Cannibalisation vs parent:** HIGH. This is the closest lane to the parent (2D physics sims, accelerating bounces). We separate it in two ways. (1) The characters: faces, eyebrows and a running Pip-vs-Bloo rivalry with a season score. (2) A bright-daylight look (cream background, thick dark outlines) instead of neon on black. Even so, expect audience overlap. Never cross-promote the two channels on the same day.

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @Earclacks | 209k | 2025 (trend originator) | 110k, 106k, 87k, 83k, 79k (recent 40) | weapon vs weapon, 30-70 s, emoji titles; long-form median 17k |
| @weaponballfight | 12.8k | 2025-07-28 | 1.33M, 88k, 63k, 61k, 54k | meme captions ("who made this demon bro???"), 5-7 s micro-clips |
| @Eeize | 5.7k | 2026 | 511k, 319k, 174k, 122k, 109k | 3D procedural magenta-vs-blue ball falls, 8 s; no faces |
| @Loggernamy | 2.56k | 2026-01-24 | 20k, 10k, 9k, 7.1k, 6.8k | Earclacks copy, 251 shorts: proof that a pure copy stalls |
| @lostmarbles2d | 154k | older | 20k, 19k, 16k | weapon balls with named OC characters; low |

## Reference videos decoded
- `ref_mascot-battles_1` (weaponballfight, 1.33M, 6.8 s). Infinity ball vs Super Lucky Scythe in a white square. Meme caption at the top. HP numbers sit inside the balls, with a stat panel under the arena (Roulette DMG/Jackpot Chance ticking up 6 → 25 each hit). It ends on a grey flash, then a zoom onto the winner's scythe. Audio is hit SFX at -12.7 LUFS. The escalation is the visible stat creep.
- `ref_mascot-battles_2` (Earclacks, 110k, 32 s). Club vs Duplicator. The Duplicator splits on each hit, going 1 → 15 balls. Damage/Stun counters climb (1.5 → 23.5). Cream background, "earclacks.fun" watermark, -22 LUFS. The event rate climbs as the balls multiply, which matches our rule.
- `ref_mascot-battles_3` (Eeize, 511k, 8 s). A 3D magenta block and a blue block fall onto a lime grid and drain through it. No characters, pure team-colour satisfaction, -14.5 LUFS.

## Characters
- **Pip** (red, hot-headed): a circle. Two eyebrows angled down (cairo lines, rotation = anger level), oval eyes with pupils tracking Bloo, mouth arc (grin or grimace by HP).
- **Bloo** (blue, calm): a rounded square, `poly` with bezier corners. Heavy-lidded eyes (a clipped circle), a flat mouth. It smirks when ahead.
- **Emoting:** squash and stretch on impact (scale by velocity along the normal), eye squeeze `> <` on hit, a sweat drop below 25% HP, a 3-hop victory bounce, and the loser flattens into a puddle. At the loop the puddle re-inflates to the frame-0 pose.
- **Sound:** each character gets a pitched "boop" chirp (sine blip plus formant sweep, not a voice). Pip is high, Bloo is low.

## 10 episode ideas (each with its nameable change)
1. Every hit makes the hitter BIGGER.
2. Every hit makes the victim SMALLER (shrink to zero = KO).
3. The arena spins and has a gap; first to fall out loses.
4. Tug-of-war: a rope between them, every wall bounce pulls 1 notch.
5. Each wall bounce spawns a minion of that colour (Duplicator-style).
6. Gravity flips every 5 s.
7. Paint war: each bounce paints the floor its colour; most area at the end wins.
8. Race along a spiral track with bumpers.
9. King of the hill: whoever sits in the centre ring scores per second.
10. Speed-up rule: both get 5% faster per collision, and the last 10 s is chaos.

## Engine changes needed
- look (palette, background, fonts): a daylight palette (cream `#F6EFE2`, ink outline `#1E1B24`, Pip red, Bloo blue). Re-skin `studio.PALETTE` once.
- layouts: a square arena option next to the circle. Versus bar at ~0.78h.
- audio voice: per-character chirp voices in `audio.py`. Reuse `synth_pok` and `synth_squash` for hits.
- new lib module: `lib/character.py` (face rig: eyes, brows, mouth, blink, squash and stretch, emote states), shared with any later character niche.

## Risks
- Saturation and decay: the trend leader's recent shorts are at 8k-29k.
- One-hit-wonder distribution: @weaponballfight has one 1.33M short and a 30k median.
- Weak long-form (Earclacks' long-form median is 17k).
- A young audience can trigger a made-for-kids classification.
- High cannibalisation with the parent.
- A "who will win?" title is a viewer-prediction question and breaks the caption rule. Use a finite stake instead ("First to 0 HP loses").

## Cheapest proving test clip
"Pip vs Bloo: every hit makes the hitter BIGGER." Circle arena from `_template`, two faced balls, versus bar, about 30 s. The hit rate climbs because the balls grow and fill the arena. It ends when one ball fills the arena, then the loser re-inflates and both reset to frame 0. Under 1 day.
