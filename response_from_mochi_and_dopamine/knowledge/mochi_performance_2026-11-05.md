> Superseded in part by reports/2026-11-05_channel_analysis.md (Studio data).

# Mochi & Bolt: what is working (data to 2026-11-04 ~17:00 UTC)

## Data and limits
- **Views:** exact public counts per video (`yt-dlp` per-video metadata), pulled 2026-11-04. 86 Shorts + 2 long videos. Slots and scene names come from `<VIDEOS_DIR>\MochiAndBolt\uploaded\<date>\UPLOAD.md`; every title matched one entry (2 fixed by hand).
- **Not read: Studio** (stayed-to-watch, % viewed, subs per video). The owner's Chrome is signed into an account that gets "Oops, you don't have permission to view this page" for this channel. I did not switch accounts. The latest Studio export is 2026-10-16.
- **Tags are mine,** read from `docs/scenes/<scene>.md`. Meter = what the on-screen progress measures:
  - **FILL:** a container fills toward a MAX/FULL line.
  - **CLEAR:** something is destroyed down to 0.
  - **SCORE:** points, a distance or a count with no container.
  - **RACE:** position toward a line.
- **Eras:**
  - E1 = Oct 3-15 (pre-research, `#usa`): n=30, median **1,528**, nothing broke out.
  - **E2 = Oct 16 → Nov 4** (research rules): n=56. **Settled** (≥40 h): n=51, median **2,445**.
- **Small samples:** p-values are Mann-Whitney on views, as a guide only. Groups of 5-15 clips; one upload can be a 100x lottery ticket.

## Top 20% vs the rest (E2 settled, n=51; top 10 ≥ 8,834 views)
| | Top 10 | Rest (41) |
|---|---|---|
| Median views | **20,120** | 2,071 |
| FILL meter (container to a MAX line) | **8/10** | 10/41 (Fisher p≈0.002) |
| ×N rule (×3 split, ×2, ×1.5 waves) | **8/10** | 11/41 |
| FILL **or** ×N | **10/10** | 15/41 (Fisher p≈0.0003) |
| Late single lead change | 7/10 | 16/41 |
| ≤17 s | 6/10 (median 17 s) | 14/41 (median 20 s) |
| PD melody / ASMR | 9 / 1 | 25 / 16 |
| Everyday situation | 1/10 (sandcastle) | 8/41 |
| SCORE meter | **0/10** | 10/41 |
| CLEAR meter | 1/10 (sandcastle) | 15/41 |

Top 10:
1. press_split2 322.6K
2. press_split4 180.9K
3. sandcastle_wave 31.7K
4. press_tools 30.2K
5. press_squeeze 27.3K
6. sand_rise3 12.9K
7. sand_rise4 12.3K (47 h)
8. tug_war 11.8K
9. comment_overflow 11.6K
10. galton_split 8.8K

## Group medians (non-press settled, n=47 unless stated)
| Split | Yes | No | p | Read |
|---|---|---|---|---|
| Press family (n=51) | **4/4 ≥27K, median 106K** | 2.4K | <0.001 | our engine; never failed |
| FILL meter | **4.35K** (n=14) | 2.0K | 0.001 | strongest non-press signal |
| CLEAR meter | 1.9K (n=16) | 3.2K | 0.045 | 1 breakout (sandcastle) |
| SCORE meter | 1.9K (n=10) | 2.7K | 0.036 | 0 breakouts |
| ×N rule | 4.2K (n=15) | 2.3K | 0.18 | only with FILL: ×N + FILL 4.2K vs ×N + CLEAR/SCORE 1.0-2.0K |
| ≤17 s | **3.6K** (n=19) | 2.0K | 0.006 | holds inside each meter group (FILL 6.6K vs 4.2K; CLEAR 2.3 vs 1.8); ρ(len, views) = −0.37 |
| PD melody vs ASMR | 2.0K | 2.4K | 0.75 | no detectable effect |
| Famous fact/puzzle | 3.1K (n=10) | 2.4K | 0.79 | split: physical scale works, abstract doesn't (below) |
| Everyday situation | 2.0K (n=9) | 2.4K | 0.58 | 1 breakout in 9 |
| Late lead change | 2.9K (n=20) | 2.1K | 0.19 | weak |
| Attempts-until-it-breaks | 1.8K (n=5) | 2.4K | 0.22 | 0/5 top |

- **Sequels of winners hold:**
  - sand_rise4 = 0.95x sand_rise3.
  - press_split4 / press_tools / press_squeeze all ≥27K.
  - comment_overflow (a press spin-off) 11.6K.
  - Sequels of non-winners stay low: demolition_duel 2.4K → demolition_duel2 1.7K.
- **Famous facts split cleanly:**
  - **Physical scale works:** paper_fold 7.6K, rocket_stage 7.1K, galton 8.8K, gossip 4.2K.
  - **Abstract probability/algorithm puzzles don't:** birthday 1.6K, Monty Hall 1.1K, Hanoi 1.9K, block overhang 1.6K, penny_double 0.46K (FILL + ×2 + famous and still the lowest E2 clip; maybe the "$1,000,000" title, n=1).
- **Weekly E2 medians are flat** (2.56K / 2.00K / 2.73K). Growth comes only from hits; the floor has not moved.
- **Hashtag A/B:** 2 pairs, inconclusive. balloon (none) 1,468 vs rock (tags) 1,855; pinball (none) 1,017 vs monty 1,093 / egg 1,149. Judge at ≥6 pairs (ice_crack, rain_run, one_trip, microwave and soda_tap are queued).
- **Slots since Oct 27:**
  - 14:45-15:00 ET: median 6.6K (n=6; holds sandcastle, sand_rise4, galton).
  - 07:00 ET: 3.7K.
  - 23:00 ET: 1.7K.
  - This is confounded by which clip went where. No evidence against the afternoon slot.
- **Long videos:** "Crushing the Sun" (press theme extended) has 1,315 views in 45 h. The 26-clip compilation has 101 views in 123 h. The themed long video gets ~35x the views per hour.

## What clearly does NOT work (our channel)
1. **SCORE meters** (points eaten, bowling score, overhang cm, coins won): 0/10 top, median 1.9K.
2. **CLEAR meters** (break the castle / ceiling / mountain to 0): median 1.9K. The recent "doubling beats linear" clips that CLEAR all flopped: cannon_split 2.0K, balloon 1.5K, rock 1.9K. The ones that FILL worked: cell 4.2K, foam 4.3K, galton 8.8K.
3. **Abstract famous puzzles:** median 1.6K (n=5).
4. **Attempts-until-it-breaks** (CCP recipe A: core_drop, ring_burst, last_brick2, geode, spiral_roll2): median 1.8K, 0/5. It did not transfer.
5. **Everyday duels** (hot dog, bowling, coin pusher, treasure, vacuum, edge, freefall): median 2.0K. **14 of the 19 clips scheduled Nov 5-12 are this class with SCORE/RACE meters** (checkout, one-trip, ice cubes, lane switch, microwave, soda, stone skip, coffee, quake, phantom jam, string fan, stack bounce, parking, dune). Expect ~2K each. jenga_pull (2.7K at 15 h) is the one early sign against this; re-check it Nov 6.

## What viewers say (top comments, 16 best videos)
- **"skill vs spam" is the most-liked comment on the channel** (76 likes, press_split4; also on press_split2 ×2 and galton). Viewers read our duels as gaming archetypes: "early game vs late game", "quality vs quantity", "high damage slow cooldown vs low damage fast cooldown", "rabbit vs turtle". Title test: "Skill vs SPAM".
- **Open request on the #4 video** (press_tools 30K): "Trident would have been the winner if he went deeper", @Haroldedits123-3D1T, 8 likes.
- Recognition: "Fur Elise" ×4, Radetzky and Vltava named. One "stop this ai slop" (press_split4).
- **MFK watch:** "cute characters" (sandcastle) and "so cute glad i found this channel" (Halloween). Keep framing adult.

## Confidence
- **High:** the press franchise is the engine (4/4 ≥27K); every top-10 clip has a FILL meter or a ×N rule (10/10 vs 15/41, p≈0.0003).
- **Medium:**
  - FILL beats CLEAR/SCORE (p=0.001, but the tags are mine and overlap with "lots of balls");
  - SCORE meters don't break out (0/10 top, median p=0.036; the Fisher test on top-10 share alone is p=0.18);
  - shorter (≤17 s) is better (p=0.006, but newer clips are shorter);
  - abstract puzzles and everyday duels stay near 2K.
- **Low / none:** music type, hashtags, slot, lead-change type. Retention is unknown without Studio.

## Rules for the next batch (from this data)
1. A container that FILLS to a visible MAX line, driven by a ×N or accelerating rule, with lots of balls or grains. Never a points/distance meter.
2. 13-17 s.
3. **Franchise the top-10 formats** with ONE nameable change. A new format starts from FILL + ×N.
4. A famous fact only when it has physical scale (Moon, orbit, a bell curve of 9K balls), never abstract probability.

## BUILD TONIGHT (ranked)
Side safe zone x 0.10-0.84w. No kid words or tunes, no candy emoji, no trademarks. Each melody is unused on Mochi & Bolt.

### 1. press_tools2: "You said the Trident wins if it goes DEEPER" (comment reply)
- **Concept:** press_tools exactly (every ball hit splits into 3, Trident vs Spike, MAX line, overflow). ONE change: Mochi's trident now drives to the floor like the spike.
- **Hook:** frame 0 shows the real comment card (@Haroldedits123-3D1T: "Trident would have been the winner if he went deeper") over both tools mid-strike, first split ≤0.1 s.
- **Why the data says it works:**
  - The press family is 4/4 ≥27K.
  - The comment-reply format did 11.6K (comment_overflow).
  - This is the one open request on our #4 video.
- **Honest physics:** same jackhammer power for both tools (P = F·v). A deep trident pushes 3 prongs through the pile, so its stroke drag is ~3x and it moves ~1/3 as fast inside the pile. Deeper but slower. The sim decides, either "you were right" or "deeper still loses". If the honest result is a blowout, change the setup (pile height, MAX line), never the result.
- **Length:** ~19 s.
- **Melody:** Suppé, *Light Cavalry* Overture, galop (1866, PD; parent Für Elise).

### 2. sand_rise5: "Every second the room fills with MORE balls… and there's ONE way out"
- **Concept:** sand_rise4's flood, ladders and the balls-to-the-eyes ending. ONE change: Mochi and Bolt share ONE room with ONE hatch. First out is free; the other gets buried (rope gag optional).
- **Hook:** frame 0 is mid-action: the room 45% full, both scrambling under the same lit EXIT, "ONE WAY OUT" in the HUD.
- **Why:**
  - The room-fill format is 2/2 ≥12K (12.9K, 12.3K in 47 h), and the sequel held 95% of the parent.
  - It is a FILL meter with a rising flood.
  - Comments frame it as "gambling vs consistency".
- **Honest physics:** sand_rise4's granular model and calibrated `SCHED_N` pour, Mochi's 70% jump, Bolt's one rung per beat. The two bodies collide and block as rigid discs, with no new rules. Who reaches the hatch first is what the sim gives.
- **Length:** ~14 s.
- **Melody:** Dvořák, Slavonic Dance Op. 46 No. 8 (furiant, 1878, PD; parent Brahms Hungarian Dance 5).

### 3. tug_war2: "Doubling vs FACTORIAL: who wins the tug of war?"
- **Concept:** tug_war's field, flag and LINE. ONE change: the rules.
  - Bolt starts with 100 and doubles every second.
  - Mochi starts ALONE and multiplies by 1, 2, 3, 4… (n!).
  - Doubling LOSES this time: the template reverses.
- **Hook:** frame 0 shows Bolt's 100 dragging the flag toward Mochi's line, her alone digging in, the ×2 and ×n badges popping.
- **Why:**
  - tug_war got 11.8K.
  - Our audience watches growth races ("n² vs 2ⁿ" 1.3M).
  - It is the next rung after growth_race3 (x³ vs 2ˣ, Nov 12).
  - It breaks the predictable "doubling wins late" ending: the 5 such clips since Nov 1 sit at 1.0-2.0K (2 are still young).
- **Honest maths:** exact counts. Bolt 100·2ᵗ vs Mochi t!:
  - t7: 12,800 vs 5,040;
  - **t8: 25,600 vs 40,320 (LEAD CHANGE)**;
  - t9: 51,200 vs 362,880.
  - Force ∝ head-count difference (the tug_war model).
  - Crowds over ~5K are drawn as a labelled density ("1 figure = 100").
- **Note:** ×2 vs n! was built once as growth_race2 (pallets, batch67). It was rejected for the look, not the maths. This puts it in the look that worked.
- **Length:** ~15 s.
- **Melody:** Elgar, *Pomp and Circumstance* March No. 1 (1901, PD; parent Radetzky March).

### 4. galton_split2: "1 ball became 1,048,576 on a Galton board"
- **Concept:** galton_split's two boards. ONE change: Bolt's board has 20 rows, so ONE dropped ball splits at every peg into 2²⁰ = 1,048,576. Mochi blasts a firehose of single balls. First board to FULL wins.
- **Hook:** frame 0 shows both bell outlines and FULL lines, Mochi's firehose already piling, and Bolt's single ball splitting at row 1. The "BALLS ON BOARD" counter doubles every row.
- **Why:**
  - galton got 8.8K (FILL + ×2 + a famous object).
  - It is SatFy's bigger-number franchise move (9,216 → 1,048,576).
  - The bell-curve punchline repeats ("both make the SAME bell").
- **Honest maths:**
  - Bolt's bins get exactly C(20, j).
  - Mochi's pile is a binomial(20, ½) sample.
  - Set her firehose rate so she leads until about row 18.
  - The counter counts balls on the board (in flight included), honestly labelled.
  - Render in-flight balls as a point-density field.
  - Rows slow to about 0.5 s near the bottom so the doubling reads.
- **Length:** ~16 s.
- **Melody:** Liszt, *La Campanella* (1851, PD; bell-like notes on each row split; parent Chopin Fantaisie-Impromptu).

## TEXT-ONLY concepts (for the owner, not built)
### A. paper_fold2: "Fold paper 103 times = bigger than the UNIVERSE? Paper vs LIGHT"
- **Concept:** paper_fold's stack and zoom (parent 7.6K). The rival is a beam of light (one fold a minute vs c).
- **Honest maths:** 0.1 mm·2ⁿ.
  - Light leads until **fold 54** (1.80×10¹² m vs 9.7×10¹¹ m): the paper "outruns" light.
  - Landmarks: Moon 42, Sun 51, Proxima Centauri 69, Milky Way 84, Andromeda 88, observable universe 103 (1.0×10²⁷ m > 8.8×10²⁶ m).
  - It is a thought experiment, labelled as one.
- **Why:** a scale journey (DopamineEXE 77 dominoes 12.6K, MotionRelax atom 143K) and a famous fact with a bigger number.
- **Length and music:** ~25 s. R. Strauss, *Also sprach Zarathustra* sunrise (1896, PD).

### B. "More grains of sand on Earth, or stars in the universe?"
- **Concept:** Mochi counts sand: handful → bucket → beach → every beach (~7.5×10¹⁸). Bolt counts stars: naked eye ~5,000 → Milky Way ~10¹¹ → all galaxies ~10²²-10²⁴.
- **How it plays:** a log FILL meter for each. Sand leads (one handful beats every star you can see), and stars pass it once the count reaches other galaxies.
- **Why:** a famous question people already ask (Sagan), honest published estimates, real pouring sand, and a lead change.
- **Length and music:** ~16 s. Liszt, *Liebestraum* No. 3.

### C. "Why hourglasses use SAND, not water"
- **Concept:** same volume, same neck. Mochi's water bulb vs Bolt's sand bulb; the first bottom bulb FULL wins.
- **Honest physics:**
  - Water drains by Torricelli (flow ∝ √head): fast, then slowing.
  - Sand drains by Beverloo (flow independent of fill height): constant.
  - With sand's rate set to 0.7x water's starting rate, water leads until both have drained 84% (t = 1.2 V/Q₀). Sand finishes at 1.43 V/Q₀; water at 2.0.
  - A real reason hourglasses tick evenly.
- **Why:** a FILL meter, grains, a famous "why" (rocket_stage "Why rockets…" 7.1K) and a late lead change.
- **Length and music:** ~15 s. Haydn, Symphony No. 101 "The Clock", II (used once on DopamineEXE only).

## Appendix: every E2 Short (views 2026-11-04; "young" = under 40 h)
| # | Views | Age h | Len s | Clip | Family | Meter | ×N | Sound | Lead change | Tags |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 322,641 | 450 | 26 | press_split2 | press | FILL | yes | PD melody | late | yes |
| 2 | 180,896 | 308 | 25 | press_split4 | press | FILL | yes | PD melody | late | yes |
| 3 | 31,747 | 71 | 14 | sandcastle_wave | everyday | CLEAR | yes | PD melody | late | yes |
| 4 | 30,237 | 136 | 19 | press_tools | press | FILL | yes | PD melody | late | yes |
| 5 | 27,292 | 260 | 17 | press_squeeze | press | FILL | yes | PD melody | ? | yes |
| 6 | 12,948 | 337 | 17 | sand_rise3 | room fill | FILL | - | ASMR | many | yes |
| 7 | 12,253 | 47 | 14 | sand_rise4 | room fill | FILL | - | PD melody | late | yes |
| 8 | 11,820 | 112 | 15 | tug_war | growth/split | RACE | yes | PD melody | late | yes |
| 9 | 11,559 | 128 | 20 | comment_overflow | comment reply | FILL | yes | PD melody | none | yes |
| 10 | 8,834 | 144 | 16 | galton_split | growth/split | FILL | yes | PD melody | late | yes |
| 11 | 7,641 | 356 | 24 | paper_fold | growth/split | FILL | yes | PD melody | late | yes |
| 12 | 7,104 | 104 | 16 | rocket_stage | famous fact | RACE | - | PD melody | late | yes |
| 13 | 5,573 | 232 | 16 | cradle_showdown | method duel | SCORE | - | ASMR | many | yes |
| 14 | 4,887 | 152 | 20 | glass_tower3 | method duel | FILL | - | ASMR | many | yes |
| 15 | 4,404 | 96 | 15 | box_tower | everyday | FILL | - | PD melody | ? | yes |
| 16 | 4,302 | 313 | 17 | foam_overflow | growth/split | FILL | yes | PD melody | late | yes |
| 17 | 4,188 | 359 | 22 | gossip_spread | growth/split | FILL | yes | PD melody | late | yes |
| 18 | 4,157 | 354 | 20 | cell_split | growth/split | FILL | yes | PD melody | late | yes |
| 19 | 3,604 | 378 | 15 | log_gauntlet | race | RACE | - | ASMR | many | yes |
| 20 | 3,584 | 104 | 22 | halloween_switch2 | seasonal | OTHER | - | PD melody | none | yes |
| 21 | 3,152 | 428 | 24 | double_bounce3 | growth/split | FILL | yes | PD melody | late | yes |
| 22 | 2,837 | 258 | 17 | brick_tunnel | method duel | CLEAR | - | ASMR | ? | yes |
| 23 | 2,755 | 426 | 22 | spiral_roll2 | attempts | CLEAR | - | ASMR | none | yes |
| 24 | 2,732 | 15 (young) | 13 | jenga_pull | everyday | SCORE | - | PD melody | none | yes |
| 25 | 2,690 | 256 | 17 | card_cascade | method duel | FILL | - | ASMR | late | yes |
| 26 | 2,510 | 176 | 20 | hot_dog_contest | everyday | SCORE | - | PD melody | late | yes |
| 27 | 2,445 | 284 | 30 | last_brick2 | attempts | CLEAR | - | ASMR | none | yes |
| 28 | 2,391 | 289 | 26 | demolition_duel | method duel | CLEAR | - | ASMR | ? | yes |
| 29 | 2,361 | 384 | 17 | grand_prix4 | race | CLEAR | - | ASMR | many | yes |
| 30 | 2,299 | 448 | 16 | glass_smash3 | method duel | CLEAR | - | ASMR | late | yes |
| 31 | 2,263 | 120 | 22 | freefall_cargo3 | everyday | RACE | - | ASMR | ? | yes |
| 32 | 2,071 | 402 | 21 | lava_ice2 | territory | FILL | - | PD melody | many | yes |
| 33 | 2,052 | 424 | 15 | coin_bridge2 | method duel | SCORE | - | ASMR | ? | yes |
| 34 | 2,003 | 212 | 22 | vacuum_drop | everyday | RACE | - | PD melody | none | yes |
| 35 | 1,997 | 79 | 16 | cannon_split | growth/split | CLEAR | yes | PD melody | late | yes |
| 36 | 1,978 | 208 | 16 | edge_slide | everyday | SCORE | - | ASMR | ? | yes |
| 37 | 1,926 | 332 | 22 | hanoi_64 | growth/split | SCORE | yes | PD melody | none | yes |
| 38 | 1,855 | 55 | 18 | rock_avalanche | growth/split | CLEAR | yes | PD melody | late | yes |
| 39 | 1,845 | 282 | 25 | geode_crack | attempts | CLEAR | - | ASMR | none | yes |
| 40 | 1,836 | 306 | 18 | mousetrap_chain | growth/split | CLEAR | yes | PD melody | ? | yes |
| 41 | 1,786 | 168 | 20 | bowling_hook | everyday | SCORE | - | PD melody | late | yes |
| 42 | 1,717 | 236 | 13 | demolition_duel2 | method duel | CLEAR | - | PD melody | late | yes |
| 43 | 1,674 | 452 | 26 | core_drop | attempts | CLEAR | - | PD melody | none | yes |
| 44 | 1,665 | 160 | 18 | coin_pusher | everyday | SCORE | - | PD melody | late | yes |
| 45 | 1,637 | 210 | 21 | block_overhang | famous fact | SCORE | - | PD melody | ? | yes |
| 46 | 1,609 | 409 | 18 | domino_path | race | RACE | - | ASMR | many | yes |
| 47 | 1,605 | 330 | 21 | birthday_room | famous fact | SCORE | - | PD melody | none | yes |
| 48 | 1,516 | 184 | 21 | treasure_capsize | everyday | SCORE | - | PD melody | none | yes |
| 49 | 1,497 | 404 | 25 | ring_burst | attempts | CLEAR | - | PD melody | none | yes |
| 50 | 1,468 | 63 | 17 | balloon_chain | growth/split | CLEAR | yes | PD melody | late | none |
| 51 | 1,403 | 7 (young) | 15 | snowball_fort | everyday | CLEAR | - | PD melody | final hit | yes |
| 52 | 1,330 | 234 | 23 | siege_duel3 | method duel | CLEAR | - | ASMR | many | yes |
| 53 | 1,149 | 23 (young) | 14 | egg_drop | growth/split | SCORE | yes | PD melody | late | yes |
| 54 | 1,093 | 39 (young) | 22 | monty_hall2 | famous fact | SCORE | - | PD melody | late | yes |
| 55 | 1,017 | 31 (young) | 16 | pinball_split | growth/split | SCORE | yes | PD melody | final hit | none |
| 56 | 457 | 380 | 23 | penny_double | growth/split | FILL | yes | PD melody | late | yes |

Scratch (scripts, joined data, top comments): `<local path removed>` and `...\comments\`.
