# Channel analysis 2026-11-05: Mochi & Bolt (Studio export, data to Nov 3 PT)

**Sources:**
- `reports/exports/2026-11-05/`: `content/Table data.csv` (lifetime per video), the traffic, geo and age text files, `retention_notes.md` (6 curves read by eye).
- Joined per-video data: `joined.csv`. Scripts: `build_joined.py`, `analyze.py`. Full output: `analysis_out.txt`.

**Scope:**
- 85 Mochi-era Shorts have data. 79 are **settled** (≥48 h old at the cutoff, Nov 4 08:00 UTC): 30 from E1 (Oct 3-15, before the research rules) and 49 from E2 (Oct 16 onward).
- The 38 Battlefield videos are excluded, including the Aug 2026 one.
- Too young to judge: rock_avalanche (44 h), sand_rise4 (36 h), monty_hall2 (28 h), pinball_split (20 h), egg_drop (12 h), jenga_pull (4 h).
- No data yet: snowball_fort, ice_crack_race, and everything published from Nov 5.

**Two products, analysed separately (owner, 2026-11-05):**
- **Shorts:** the gate is stayed-to-watch (stay vs swipe), then the loop (avg % viewed).
- **Long videos:** the gates are thumbnail CTR × impressions, then early retention, average view duration (AVD) in minutes, and subs per 1k views.
- No conclusion from one product is applied to the other.

**Evidence rules:**
- Spearman ρ with bootstrap 95% intervals.
- Mann-Whitney p-values are a guide only.
- "n is small" means n < 6.
- Tags are hand-made and correlated: press clips are also FILL, ×N and shorter, so the key tests are repeated without the press clips.

---

## 0. Headline: are we on a good path?

**Partly.**
- **The base grew.**
  - Daily channel views by week (Oct 3 → Nov 3): 2.2K → 4.3K → 37.6K → 42.1K → 50.0K.
  - Without the 4 biggest hits: 2.2K → 3.8K → 7.9K → 11.1K → **17.6K/day**.
  - The typical E2 Short gets 2,324 views (non-press median, n=44) vs 1,526 in E1 (n=30), p<0.001.
- **Reach still comes from a few hits.**
  - The 5 press-family videos hold 71% of all Shorts views.
  - The top 2 hold 62%.
  - The 8 videos with ≥10K views brought 73% of new subscribers (219 of 302).
- **One number decides a Short: stayed-to-watch** (ρ = +0.63 with views, n=79).
  - No Short with stayed under 55% has reached 5K views: **0 of 49**.
  - Above 55%, 12 of 30 did (Fisher p ≈ 2e-6).
- **The pipeline points the wrong way.** 13 of the 22 Shorts going live Nov 5-12 are everyday duels or pilots with a points, temperature, distance or attempts meter.
  - The 7 settled everyday SCORE/RACE examples: stayed median 49.8%; only 1 of 7 reached 55% (vacuum_drop, 59.9%).
  - Their views: median 2.0K, max 2.5K.

| Mochi era (Oct 3 → Nov 3) | Value |
|---|---|
| Views (all content) | 803.7K, 94.4% from the Shorts feed |
| Shorts with data / settled | 85 / 79 |
| Subscribers from Shorts | +302 gained, −9 lost (0.38 per 1k views) |
| Stayed to watch, median | E1 45.6% → E2 57.1% |
| Avg % viewed, median | E1 82.6% → E2 103.4% |
| Length, median | E1 25.5 s → E2 20 s |
| Shorts ≥5K views | E1 0/30, E2 12/49 |
| Long videos | 2. Crushing the Sun took off on day 2: 4,667 views, CTR 5.3%, +16 subs live (§4) |

## 1. What changed since the last analyses

**vs last night's public-view research** (`research/mochi_performance_2026-11-05.md`). Studio shows **why** most of its findings hold:

| Research claim | Studio verdict |
|---|---|
| FILL meter beats CLEAR/SCORE | **Holds, and it works through the hook.** Non-press E2: FILL stayed 59.4% vs 51.0% (p=0.014); views 4.2K vs 2.0K (p=0.005). |
| ≤17 s is better | **Holds, and it works through the loop.** % viewed 119 vs 92 (p<0.001); stayed +5.5 points. Once stayed and % viewed are known, length adds nothing (§3.2). |
| ×N rule helps | **Only with FILL.** Non-press E2 ×N clips: FILL + ×N stayed 66.4%, 4.2K views (n=7) vs CLEAR/SCORE + ×N stayed 43.0%, 1.7K views (n=7); p=0.004 (stayed), p=0.026 (views). ×N alone does nothing: stayed 56.5 vs 54.6 (p=0.47). |
| PD melody vs ASMR: no effect | **Holds.** Stayed 57.0 vs 57.1 (E2). |
| Late lead change: weak | **No hook effect.** Stayed 57.1 vs 57.5. |
| Everyday duels ~2K | **Holds, and the cause is the hook.** Everyday SCORE/RACE clips: stayed median 49.8% (n=7); 1 of 7 reached 55%; views max 2.5K. |
| Abstract puzzles fail | Views 1.6K vs 2.4K (p=0.012). Stayed is 50.8 vs 56.4: lower, but not significant (n=4, n is small). |
| penny_double flopped on its title | **Overturned as a content failure.** Stayed 78.9% and 98% viewed, with a good curve until a cliff at 0:19. The feed simply never scaled it: 454 views. This is a distribution problem (n=1). |
| E2 weekly medians are flat | **Holds within E2** (non-press views vs publish order ρ = +0.16, p=0.30). The real step is E1 → E2 (§3.4). |
| Long video gets ~35x the views per hour of the compilation | **Confirmed, and bigger.** Live Nov 5: 4,667 views and 44K impressions in ~2.3 days, vs the compilation's 736 impressions in 5 days. The Nov 3 table (101 views) predates the Home-feed pickup (§4). |

**vs the Oct 16 report** (n=24, almost all E1):
- **Overturned:** "high stayed alone doesn't push" (then stayed ρ = +0.17, % viewed +0.29).
  - Inside E1 it is still +0.17 (n=30), because E1 never reached the gate: only 2 of 30 E1 Shorts had stayed ≥55%.
  - Across the channel, stayed is now the best predictor: **+0.63**.
- **Held:**
  - Length correlates negatively with views (−0.38 then, −0.50 now).
  - "A visible meter toward a promised end": E2 beats E1.
- **Did not pan out:** beam_clash2 as "the new signal". It ended at 2,644 views with 38.0% stayed, below the gate.

## 2. The batch under judgement (published Oct 28 → Nov 3)

The comparison point is the E2 non-press median: **2,324 views, 55.8% stayed**.

| Clip | Age h | Len s | Views | Stayed % | Viewed % | Tested | Verdict |
|---|---|---|---|---|---|---|---|
| press_tools | 125 | 19 | 30,307 | **79.0** | 112 | press episode | hit (13x) |
| sandcastle_wave | 60 | 15 | 29,603 | **68.0** | **143** | everyday + ×N waves, CLEAR | hit; best loop on the channel |
| tug_war | 101 | 15 | 11,871 | 59.6 | 133 | ×2 race | hit through the loop |
| comment_overflow | 117 | 20 | 11,594 | **77.3** | 104 | comment reply on press_split2 | hit |
| sand_rise4 (young) | 36 | 15 | 10,034 | 68.0 | 125 | sequel of sand_rise3 | hit (36 h) |
| galton_split | 133 | 17 | 8,852 | 67.0 | 111 | FILL + ×2, famous object | good |
| rocket_stage | 93 | 16 | 7,107 | 57.4 | 127 | famous "why" | good, through the loop |
| glass_tower3 | 141 | 21 | 4,883 | 65.6 | 89 | method duel, FILL | above median |
| box_tower | 85 | 15 | 4,276 | 59.1 | 132 | everyday, FILL to the ceiling | above median |
| halloween_switch2 | 77 | 22 | 3,584 | 49.0 | 104 | seasonal | median; best subs per 1k (1.4) |
| hot_dog_contest | 165 | 21 | 2,510 | 53.1 | 96 | everyday SCORE | median |
| freefall_cargo3 | 109 | 23 | 2,293 | 42.5 | 91 | everyday RACE | below |
| cannon_split | 68 | 17 | 1,957 | 45.7 | 91 | ×2 CLEAR | below |
| bowling_hook | 157 | 20 | 1,789 | 49.9 | 82 | everyday SCORE | below |
| coin_pusher | 149 | 19 | 1,668 | 38.7 | 97 | everyday SCORE | below |
| rock_avalanche (young) | 44 | 18 | 1,668 | 53.0 | 94 | ×N CLEAR | below |
| jenga_pull (4 h) | 4 | 14 | 1,582 | 59.4 | 130 | everyday SCORE, 14 s | too young; stayed is promising |
| treasure_capsize | 173 | 22 | 1,519 | 45.5 | 89 | everyday SCORE | below |
| balloon_chain | 52 | 18 | 1,419 | 39.5 | 88 | ×2 CLEAR, no hashtags | below |
| monty_hall2 (young) | 28 | 22 | 1,039 | 43.8 | 105 | abstract puzzle | below |
| egg_drop (young) | 12 | 15 | 1,015 | 43.0 | 149 | ×2 SCORE | below |
| pinball_split (young) | 20 | 16 | 903 | 34.4 | 117 | ×N SCORE, no hashtags | below |

**What the batch says:**
1. Every clip with stayed ≥65% beat the median. Every clip under 50% fell below it, except halloween_switch2 (49.0%, 3.6K; a seasonal one-off).
2. Sequels and episodes of hits keep working: press_tools, comment_overflow and sand_rise4 all ≥10K.
3. The four "doubling with a CLEAR or SCORE meter" clips (cannon, balloon, rock, pinball) hooked only 34-53%. tug_war and galton used the same doubling idea with a RACE line or a FILL container and did 9-12K.
4. The hashtag A/B (balloon, pinball) can't be read: both sit in the weak ×N CLEAR/SCORE class.

## 3. SHORTS (product 1)

### 3.1 Which Studio metric predicts views (settled Shorts)
Spearman ρ against log views. Rates are per 1,000 views.

| Metric | All (n=79) | 95% CI | E2 (n=49) | Without press-like (n=74) | E2 without press-like (n=44) |
|---|---|---|---|---|---|
| **Stayed to watch** | **+0.63** | +0.45 to +0.77 | +0.63 | +0.56 | +0.53 |
| Avg % viewed | +0.53 | +0.34 to +0.67 | +0.44 | +0.50 | +0.44 |
| Avg view duration (s) | +0.09 | −0.15 to +0.31 | +0.28 | +0.01 | +0.16 |
| Length (s) | −0.50 | −0.66 to −0.29 | −0.22 | −0.55 | −0.36 |
| Likes per 1k | −0.20 | −0.41 to +0.01 | **−0.54** | −0.16 | −0.50 |
| Subs gained per 1k | +0.22 | −0.02 to +0.44 | 0.00 | +0.23 | +0.03 |
| Shares per 1k | +0.21 | ns | +0.47 | +0.05 | +0.33 |
| Comments per 1k | −0.73 | artifact | | | |

**Notes on the weaker metrics:**
- **Likes per view fall as a video spreads.** Hits get 6.9 likes per 1k vs 10.8 for clips under 2.5K (p=0.02). Wider feed audiences like less. Likes follow reach; never target them (same as the parent channel).
- **Comments per 1k are an artifact.** 49 of 79 Shorts have exactly 1 comment: our own pinned comment.
- **Shares are too sparse to use:** 25 shares across all 79 settled Shorts.
- **Average view duration in seconds tells you nothing.** It is roughly the clip's length times % viewed.

**Controlled checks** (partial Spearman on ranks):
- Stayed vs views, controlling for length and era: **+0.47** (p<0.0001).
- Stayed vs views, also controlling for % viewed: **+0.44** (p=0.0001).
- % viewed vs views, controlling for stayed, length and era: +0.14 (p=0.23).
- **So the hook is the first gate; the loop adds a little on top.** The two retention numbers alone explain 46% of the variation in log views (R²; 37% without press).

**Is there a cliff?** Yes: a two-step one. The parent channel's single cliff was near 65%.

| Stayed to watch | n | Median views | ≥5K | ≥10K |
|---|---|---|---|---|
| ≤45% | 19 | 1,536 | 0 | 0 |
| 45-50% | 19 | 1,605 | 0 | 0 |
| 50-55% | 11 | 1,718 | 0 | 0 |
| 55-60% | 11 | 2,688 | 3 | 2 |
| 60-65% | 4 | 1,945 | 0 | 0 |
| 65-70% | 7 | 5,578 | 4 | 1 |
| >70% | 8 | 19,451 | 5 | 5 |

- **Under 55%:** nothing reached 5K (0 of 49).
- **55-65%:** a hit is possible (3 of 15). All three were 15-17 s with ≥99% viewed: sand_rise3, tug_war, rocket_stage. A strong loop rescued a medium hook.
- **65% and up:** a hit is likely (9 of 15 reached 5K).
- The best single split is at 67%: average 13.2K views above it vs 2.0K below. A bootstrap puts the split between 56.5% and 74% (80% interval).
- **Not sufficient on its own:** 6 of the 15 Shorts with ≥65% stayed stalled under 5K.
  - penny_double: 454 views.
  - neon_trails4: 1.7K.
  - spiral_roll2: 2.75K.
  - double_bounce3: 3.1K.
  - log_gauntlet: 3.6K.
  - glass_tower3: 4.9K.
  - Three were 21-24 s and looped under 92%: spiral_roll2, double_bounce3, glass_tower3.

**Retention curves** (coordinator's readings, n=6):
- Winners hold a plateau to the end: press_split2 ~90% from 0:17; sandcastle_wave sliding slowly from ~140%. (`retention_notes.md` labels this row sandcastle_wave2. The id 5NNOM7s8LEs is episode 1, sandcastle_wave.)
- Flops slide to ~35% and lose most viewers at **0:04-0:07** (bowling, traps). This matches the parent channel's 4-10 s dip.

### 3.2 Tags: does the effect run through the hook or the loop?
E2, without press-like clips (n=44). Medians for yes vs no.

| Tag | n yes | Stayed % | Viewed % | Views | Runs through |
|---|---|---|---|---|---|
| FILL meter | 12 | **59.4 vs 51.0** (p=0.014) | 98 vs 101 | **4.2K vs 2.0K** (p=0.005) | hook |
| ≤17 s | 14 | 58.9 vs 53.4 (p=0.07) | **119 vs 92** (p<0.001) | **3.9K vs 2.0K** (p=0.006) | loop, plus some hook |
| ×N rule | 13 | 56.5 vs 54.6 (p=0.47) | 98 vs 99 | 4.2K vs 2.3K (p=0.16) | nothing on its own; only with FILL (§1) |
| SCORE meter | 10 | 49.8 vs 57.3 (p=0.12) | 101 vs 98 | 1.9K vs 2.6K (p=0.055) | hurts the hook |
| CLEAR meter | 15 | 52.1 vs 57.1 (p=0.35) | 91 vs 104 (p=0.12) | 2.0K vs 2.7K (p=0.09) | weaker on both |
| RACE meter | 6 | 58.5 vs 54.9 | 113 vs 97 (p=0.08) | 2.9K vs 2.3K | loop |
| Everyday duel | 9 | 49.9 vs 56.5 (p=0.22) | 98 vs 99 | 2.0K vs 2.4K | hurts the hook |
| Abstract puzzle | 4 | 50.8 vs 56.4 | 101 vs 98 | **1.6K vs 2.4K** (p=0.012) | n is small |
| Famous physical scale | 4 | 62.2 vs 54.9 | 104 vs 98 | **7.3K vs 2.2K** (p=0.005) | hook; n is small |
| Attempts until it breaks | 5 | 60.1 vs 54.6 | **77 vs 104** (p<0.001) | 1.8K vs 2.4K | hooks, then **kills the loop** |
| Method duel | 9 | 57.1 vs 55.2 | 119 vs 98 (p=0.06) | 2.4K vs 2.3K | neutral |
| ASMR vs PD melody | 17 / 27 | 57.1 vs 53.8 (p=0.34) | 108 vs 98 | 2.4K vs 2.0K | no effect |
| Late lead change | 18 | 55.1 vs 55.8 | 100 vs 96 | 2.9K vs 2.1K (p=0.15) | no hook effect |
| Comment reply | 2 | 77.3 / 52.1 | | 11.6K / 1.7K | follows the parent video; n is small |
| Press (all E2) | 4 | **77.4 vs 56.3** | 111 vs 99 | 104K vs 2.4K | hook, plus repeated pushes |

**Length bands** (all settled):

| Length | n | Views | Stayed % | Viewed % |
|---|---|---|---|---|
| ≤14 s | 1 | 1.7K | 52.1 | 120 |
| 15-17 s | 16 | **3.9K** | **59.4** | **117** |
| 18-22 s | 29 | 2.0K | 49.0 | 97 |
| 23 s+ | 33 | 1.5K | 48.3 | 81 |

The ≤14 s band is **untested**: 1 settled clip, plus jenga_pull at 4 h.

**What drives stayed, using only what we decide when we build** (OLS, n=79, R² = 0.56):

| Build choice | Stayed points | Standard error |
|---|---|---|
| FILL meter | **+8.6** | 2.8 |
| Length ≤17 s | **+5.9** | 2.3 |
| Press family | +16.3 | 4.5 |
| E2 research rules | +6.9 | 2.1 |
| ×N rule | −0.5 | 2.6 |

**Mediation** (OLS on log views, with and without stayed + % viewed in the model):
- **≤17 s:** +0.17 → −0.07 (non-press +0.27 → +0.16). The length effect is fully carried by retention.
- **FILL:** +0.49 → +0.30 (non-press +0.17 → +0.13). Partly carried by the hook.
- **×N:** non-press +0.16 → +0.15. Not carried by retention.
- **Press:** +1.30 → +1.10. Most of the press effect sits outside the two retention numbers: press_split2 and press_split4 were pushed again and again for 2-3 weeks (daily peaks of 48K, 38K and 49K for press_split2, which still did 8.9K on Nov 3).
- press_tools and sandcastle_wave each got **one** spike (21.4K and 23.9K) and then dropped ~95% the next day. One test wave per Short is normal; a re-push is the exception.

### 3.3 Loops (avg % viewed >100%)
- 32 of 79 settled Shorts loop on average.
- % viewed is mostly length: −3.1 points per second (ρ = −0.74).
- **Best loopers after adjusting for length** (points above the length trend):

| Clip | Adjusted | Length |
|---|---|---|
| press_split4 | +26 | 26 s |
| brick_tunnel | +26 | 18 s |
| sandcastle_wave | +25 | 15 s |
| vacuum_drop | +21 | 22 s |
| tug_war | +15 | 15 s |
| box_tower | +14 | 15 s |
| rocket_stage | +12 | 16 s |

- **What they share:** one decisive final event that is readable in a glance (the wave hits, the flag crosses the line, the tower touches the ceiling), with the result shown instantly.
- **Worst loopers:**
  - Attempts clips: median −10.5 points (p=0.03).
  - ×N CLEAR clips: cannon_split, mousetrap_chain and balloon_chain at −20 to −21.
  - E1 visual pieces: chladni −29, butterfly −20.
  - The penny_double curve cliffs at 0:19, once the answer is shown.
- **Loop strength helps views a little** (ρ = +0.24, p=0.03), less than the hook.

### 3.4 Floor vs hits
Lifetime views of settled Shorts, by upload week. Weeks start on Saturday Oct 3.

| Week | n | 25th percentile | Median | 75th percentile | ≥5K | Median stayed |
|---|---|---|---|---|---|---|
| Oct 3 | 12 | 1,327 | 1,438 | 1,569 | 0 | 46.9 |
| Oct 10 | 19 | 1,491 | 1,549 | 1,673 | 0 | 45.3 |
| Oct 17 | 22 | 1,955 | 2,417 | 4,174 | 4 | 57.6 |
| Oct 24 | 19 | 1,754 | 2,293 | 5,231 | 5 | 54.6 |
| Oct 31 | 7 | 2,771 | 4,276 | 9,489 | 3 | 57.4 |

- **The floor stepped up once, at E2:** median ~1.5K → ~2.3K, 25th percentile ~1.4K → ~1.8K. It has not moved since.
  - Within E2, non-press views vs publish order: ρ = +0.16 (p=0.30).
  - Stayed drifts slightly down over E2: ρ = −0.25 (p=0.11), as more everyday clips went out.
- **The Oct 31 week looks better, but n is small** (7). It also leaves out 5 weaker young clips (0.9-1.7K) that will land in it.
- **What separates a 10K+ Short from a sub-2.5K Short** (n=8 vs 53):

| Metric | 10K+ | Under 2.5K | p |
|---|---|---|---|
| Stayed | **75.4%** | 46.7% | <0.0001 |
| Avg % viewed | 111% | 89% | 0.001 |
| Length | 18 s | 23 s | 0.03 |
| Likes per 1k | 6.9 | 10.8 | (a consequence of reach) |
| Subs per 1k | 0.40 | 0.00 | 0.33 (ns) |

  - In E2, 75% of 10K+ Shorts are FILL and 88% are ×N, vs 8% and 20% of the sub-2.5K ones.

### 3.5 Subscribers
- **Totals from Shorts:** +302 gained, −9 lost. That is 0.38 per 1k views pooled; the per-video median is 0.41. (The 0.6 in `longform_notes.md` divides the whole channel's 491 subs, including Battlefield and unattributed, by Mochi-era views.)
- **17 settled Shorts with ≥1.5K views gained no subscriber at all.**
- **Nothing measurable predicts subs per 1k:**
  - vs stayed ρ = +0.09; vs % viewed +0.16; vs length −0.01; vs likes per 1k +0.03 (all ns).
  - vs views: 0.00 in E2.
- **Subscribers come from volume.** The 8 videos with ≥10K views brought 73% of them. The 4 press videos brought 174 (0.31 per 1k).
- **A hint about which hits convert** (n is small, 3-5 per group):
  - Rivalry/story hits converted **0.46-0.77 per 1k**: sandcastle 0.74, press_squeeze 0.77, comment_overflow 0.52, sand_rise3 0.46. paper_fold reached 1.05.
  - Pure-number races converted **0.11-0.17 per 1k**: tug_war 0.17, rocket_stage 0.14, galton_split 0.11. cradle_showdown got 0 on 5.6K views.
  - halloween_switch2 had the best rate of any clip over 2K views (1.4 per 1k) with only 49% stayed.
- **Lost subscribers are negligible:** 9 in total, 6 of them on press_split2.

### 3.6 Shorts: what works / what doesn't
- **Works:**
  - Press franchise episodes: 5 of 5 ≥11.6K including comment_overflow; stayed 74-79%.
  - Sequels of hits: 5 of 5 ≥10K, including sand_rise4 at 36 h.
  - FILL + ×N with a visible FULL line: galton, paper_fold, foam, cell, gossip; median stayed 66%, 4.2K views.
  - 15-17 s clips that end on one decisive event: sandcastle, tug_war, rocket, box_tower.
  - Famous physical scale: 7.3K median (n=4).
- **Doesn't work:**
  - Everyday SCORE/RACE duels: stayed 49.8%, max 2.5K views, n=7.
  - ×N with a CLEAR or SCORE meter: stayed 43%, 1.7K, n=7.
  - Attempts until it breaks: loop −10.5 points, 1.8K, n=5.
  - Abstract puzzles: 1.6K, n=4.
  - Anything 23 s or longer: 1.5K, n=33 (mostly E1).
  - Music type, hashtags and slot: no detectable effect, or confounded.

## 4. LONG-FORM (product 2)
**n=2. These are anecdotes plus the parent channel's priors** (labelled). Sources:
- The Studio table, to Nov 3 PT.
- The coordinator's live read (`reports/exports/2026-11-05/longform_notes.md`, Nov 5 ~10:00 local): Studio overview, Reach tab and the retention curve.

| | compilation 1 ("…Get Out of Hand") | Crushing the Sun (Sun → atom, press theme) |
|---|---|---|
| Length / published | 9:33 / Oct 30 | 9:08 / Nov 2 22:00 UTC |
| Studio table (to Nov 3 PT) | 75 views, 736 impressions, CTR 6.0%, AVD 1:51 (19.5%), +1 sub | 101 views (34 h old), 2,993 impressions, CTR 2.0%, AVD 2:59 (32.8%), 0 subs |
| **Live (~2.3 days old)** | ~101 public views by Nov 4 | **4,667 views, 44K impressions, CTR 5.3%, 200.8 watch hours (~2.6 min average), +16 subs** |
| Traffic | never got Home-feed distribution | **Browse/Home 87%**, Suggested 9.6%, channel pages 0.3%, related Shorts 0.3% |
| Early retention | | 73% at 0:30; **64% at the 10% mark (0:55)**; 50% at 2:00; 31% at 5:00; 17% at the end (curve from the first ~95 viewers only; noisy) |
| Subs per 1k views | (1 sub; meaningless) | **3.4** vs Shorts **0.38** (302 subs / 803K views): ~9x, n=1 |

**What works (anecdote, n=1 each):**
- **A themed journey with a goal (Sun → atom) took off on day 2 in the Home feed.** It got 60x the impressions of the mixed best-of in half the time.
- **It beats similar-length videos early.** At 0:55 (the 10% mark) 64% of viewers remain; the parent prior is ~35% gone by then. Studio: +54 to +64 points vs typical for the first 1:15.
- **Viewers come for the transitions.** 10 of the 14 rises in the curve sit 0-6 s before a chapter start: viewers skip to the next "SMALLER THAN …!" drop. The space → lab switch at 4:25 lost nobody.
- **It converts subscribers about 9x better per view than Shorts** (3.4 vs 0.38 per 1k; n=1).
- **The thumbnail recovered.** CTR rose from 2.0% (first 3K impressions) to 5.3% on 44K impressions, so the early CTR was not representative.

**What doesn't work:**
- **Long chapters.** Mimas (39 s) lost 9 points and Marble/Pea (41 s) lost 7.5 points: the biggest mid-video losses.
  - Bennu lost 7 points in 15 s.
  - The middle (3:28-4:25) sits 8-19 points below typical.
- **A compilation of unrelated Shorts.** 736 impressions in 5 days and 19.5% viewed.
- **Our own Shorts fans.** Returning viewers fall to ~48% by 0:11, vs 91% for new viewers (n≈21, very noisy).

**Parent priors** (re-validate here):
- Long-form earned 90% of revenue on 26% of views (RPM $1.79 vs $0.067 for a Short).
- The 1-hour cut earned 3.1x the RPM of an 8-10 min compilation, but had the lowest CTR.

## 4b. How Shorts and long-form should feed each other
- **The two audiences barely overlap so far.**
  - Crushing the Sun gets 87% of its traffic from Browse/Home and only 0.3% from related Shorts and 0.3% from channel pages.
  - Its returning (channel) viewers leave fastest.
  - So **long-form does not need Shorts traffic.** It needs a theme the Home feed will test, and a CTR that holds.
- **Shorts supply the theme, not the viewers.** Theme long videos on Short families that pass the Shorts hook gate, since those mechanics have proven they stop a scroll:
  - Press: 5 Shorts, ~570K views, stayed 74-79%. Crushing the Sun is this family.
  - Room fill (sand_rise): stayed 59-68%.
  - FILL/×N growth (galton, paper_fold, tug_war).
  - Sandcastle.
  - The same "smaller/bigger than X" scale journey that makes paper_fold and rocket_stage work as famous physical scale.
  - Never theme on everyday SCORE duels, attempts clips or abstract puzzles: they hook only 45-50%.
- **The structure that holds long viewers is a chain of Short-length beats.** Each chapter is roughly a 15-25 s Short with its own payoff ("SMALLER THAN …!"). This is the long-form version of Shorts rule S4.
- **Long-form → subscribers.** At 3.4 subs per 1k, one 4.7K-view long video brought 16 subs. That equals the subs from ~42K Shorts views at 0.38 per 1k. Subscribers are the Partner Program bottleneck (§6).
- **Shorts → long-form links.** Keep the related-video link from top press Shorts to Crushing the Sun, but expect little: related Shorts = 0.3% of its traffic.

## 5. Audience and traffic (Oct 3 → Nov 3)
**Traffic:**

| Source | Share of views |
|---|---|
| Shorts feed | 94.4% |
| Channel pages | 3.3% |
| YouTube search | 1.2% |
| Other YouTube features | 0.8% |
| Browse | 0.1% |

Search viewers watch 109%. Channel-page viewers watch 96%.

**Geography:**

| Country | Share of views |
|---|---|
| US | **16.1%** (was 7.2% in the Oct 17 read) |
| Indonesia | 10.9% |
| India | 6.8% |
| Philippines | 5.9% |
| Vietnam | 5.6% |
| Brazil | 5.1% |
| Russia | 4.0% |
| Thailand | 3.2% |
| UK | 2.2% |
| Germany | 2.1% |
| Malaysia | 2.1% |
| Canada | 1.8% |
| Japan | 1.7% |
| France | 1.6% |

- Tier-1 countries (US, UK, Germany, Canada, Japan, France) make up **25.5%**.
- South-East Asia (Indonesia, Philippines, Vietnam, Thailand, Malaysia) makes up 27.7%.
- South-East Asia loops the most: Malaysia 114%, Indonesia 114%, Philippines 110%, US 109%, India 97%.

**Age** (signed-in viewers only):

| Age | Share of views |
|---|---|
| 25-34 | 29.3% |
| 35-44 | 21.8% |
| **13-17** | **19.2%** (was 10.3% in the Oct 17 read) |
| 18-24 | 14.0% |
| 45-54 | 11.4% |
| 55+ | 4.3% |

**Made-for-kids risk:**
- The teen share nearly doubled during the ball-splitting hits.
- Viewers already call the characters "cute" (sandcastle, Halloween).
- Under-13 viewers are not reported at all.
- Keep the owner's made-for-kids rules strict: adult framing, no kid words or tunes, no candy emoji.

## 6. Monetisation
- **Not monetised yet.** The Shorts views come mostly from low-RPM countries (about 25% tier-1). Expect a Shorts RPM in the parent's range (~$0.07).
- The money case is long-form plus US reach. Crushing the Sun logged 200.8 watch hours in ~2.3 days; long-form watch hours are the other Partner Program path.
- Subscribers are the YouTube Partner Program bottleneck: +293 net in the Mochi month. Check the Earn tab for the current thresholds.

## 7. Risks and hygiene
- **Scheduled pipeline (Nov 5-12): see the table below.**
- **penny_double:** 79% stayed, 350 thumbnail impressions, 454 views. Check Studio for a restriction or a "limited" flag on that video before reusing money/finance framing.
- **Near-duplicate titles:** sand_rise3 ("…MORE sand 😱") and sand_rise4 ("…MORE balls 😱") differ by one word. That is fine for a series, but give sand_rise5 a new hook word.
- **Repetitive-content risk:** 13 everyday duels share one HUD/banner template. Each has a nameable change, so the policy is OK, but the series is the weak class anyway.
- **Data limits:**
  - The tags are hand-made. The E1 tags are mine and rough.
  - Studio days are Pacific time; the cutoff is Nov 4 08:00 UTC.
  - `Chart data.csv` has daily views for the top 5 videos only, so there are no fixed-age views. Lifetime views are used, and young clips are listed separately.

**Scheduled clips, classified (the owner can reorder or swap):**

| Live (local) | Clip | Len s | Class | Meter / ×N | Expectation (evidence) |
|---|---|---|---|---|---|
| Nov 5 | rain_run | 14.6 | everyday | SCORE (drops) | **weak**: everyday SCORE stayed 49.8%, max 2.5K |
| Nov 5 | pilot_ketchup | 18.0 | everyday pilot | attempts + % meter | **weak**: attempts loop −10.5; everyday |
| Nov 5 | toast_drop | 16.7 | everyday myth | SCORE | **weak** |
| Nov 6 | checkout_queue | 16.5 | everyday | RACE (items ahead) | **weak** |
| Nov 6 | pilot_one_trip | 18.0 | everyday pilot | SCORE (bags n/20) | **weak** |
| Nov 6 | **press_bomb** | 20.2 | press | FILL ×3 | **strong**: press 5/5 ≥11.6K |
| Nov 7 | ice_cubes | 13.7 | everyday | SCORE (°C) | **weak** |
| Nov 7 | lane_switch | 15.6 | everyday | RACE | **weak** |
| Nov 7 | microwave_spot | 16.1 | everyday | SCORE (cold %) | **weak** |
| Nov 8 | soda_tap | 14.0 | everyday myth | SCORE | **weak** |
| Nov 8 | stone_skip | 14.8 | everyday | SCORE (skips) | **weak** |
| Nov 8 | coffee_milk | 13.4 | everyday | SCORE (°C) | **weak** |
| Nov 9 | **blender_pulse** | 13.7 | split | ×2 + SNOW goal meter (FILL-like) | **good**: FILL + ×N, short |
| Nov 9 | quake_damper | 15.0 | physics duel | ×2 escalation, survive | uncertain (attempts-like) |
| Nov 9 | phantom_jam | 15.8 | everyday traffic | RACE (laps to 70) | **weak** to medium |
| Nov 10 | string_fan | 15.0 | physics | ×2, strings snap (CLEAR) | **weak**: ×N + CLEAR stayed 43% |
| Nov 10 | **shred_race** | 14.3 | split | FILL bin + ×2 | **good**: FILL + ×N, short |
| Nov 10 | stack_bounce | 14.0 | physics | race to a ceiling MAX line | medium (box_tower 4.3K, 59%) |
| Nov 11 | pilot_parking | 16.9 | everyday pilot | attempts | **weak** |
| Nov 11 | dune_deflate | 13.7 | race | RACE to the top | medium-weak (race median 2.4K) |
| Nov 12 | **growth_race3** | 15.3 | growth | FILL tank + ×2 vs x³ | **good**: tug_war 11.9K, galton 8.9K |
| Nov 12 | **sandcastle_wave2** | 14.4 | sequel of a 29.6K hit | CLEAR + ×N waves | **strong**: sequels 5/5 ≥10K |

**13 of 22 are the weak class. Four days have no good or strong clip:** Nov 5, Nov 7, Nov 8 and Nov 11. A sketch:
- Swap sandcastle_wave2 into Nov 7 (it replaces microwave_spot). That brings the sequel 5 days closer to its 4-day-old parent.
- Swap growth_race3 into Nov 8 (it replaces coffee_milk).
- Fill the two TBD slots (Nov 11, Nov 12) with FILL + ×N or sequel builds, e.g. last night's list: press_tools2, sand_rise5, tug_war2, galton_split2.
- The result: one good-or-strong clip every day from Nov 6. Nov 5 is already live.
- Caveat: the new everyday clips are 13-18 s, while the old everyday SCORE clips were 17-23 s. jenga_pull (14 s) showed 59.4% stayed at 4 h. If jenga_pull, rain_run and toast_drop pass 55% stayed at 48 h, the class deserves a second look. If they fail, stop building it.

## 8. Recommendations
1. **Judge every new Short by stayed-to-watch at ~48 h.**
   - Franchise it at ≥65%: 9 of 15 reached 5K, and sequels went 5 of 5 ≥10K.
   - Drop the format under 55%: 0 of 49 reached 5K.
2. **Build every new format around a container that FILLS to a visible FULL/MAX line** (+8.6 stayed points with everything else held fixed; non-press 4.2K vs 2.0K views).
3. **Use ×N only with FILL** (stayed 66% vs 43% with CLEAR/SCORE; n 7 vs 7, p=0.004).
4. **Make it 15-17 s and end on one decisive event** (% viewed 117 vs 97 for 18-22 s; views 3.9K vs 2.0K). Treat ≤14 s as a test: there is 1 settled clip.
5. **Pause new everyday SCORE/RACE duels, attempts clips and abstract puzzles** until the 13-18 s everyday clips report (n=7 settled, max 2.5K). Reorder the schedule as in §7.
6. **Keep the press franchise weekly, and sequel sandcastle, sand_rise, tug_war and galton within 14 days.** These are the only formats with stayed ≥59% and ≥8.8K views.
7. **Keep Mochi & Bolt's rivalry visible on number races.** It may lift subscribers (0.46-0.77 vs 0.11-0.17 per 1k; low confidence, n=3-5).
8. **Long-form: make the next long video a themed journey from a proven Short family, with chapters ≤ ~25 s.** Crushing the Sun: 44K impressions, CTR 5.3%, 64% at the 10% mark, 3.4 subs per 1k; its 39-41 s chapters lost the most. Judge it on CTR × impressions, the 10% mark, AVD in minutes and subs per 1k.
9. **Check penny_double for a restriction** (79% stayed, 454 views).
10. **Next export ~Nov 9,** with per-video traffic sources and retention for the Nov 5-8 everyday clips and press_bomb.

## 9. Not on disk / missing
- Per-video traffic source, geography and age.
- Per-video retention curves, except the 6 read by eye.
- Feed impressions for Shorts (Studio exports only thumbnail impressions).
- Daily views for every video beyond the top 5.
- The long-form retention curve covers only the first ~95 viewers. Re-pull ~Nov 7, when it covers the 4.6K.
- Revenue: not monetised.

---

## Rules for the next videos

### Shorts
| # | Rule | Evidence | Confidence |
|---|---|---|---|
| S1 | **Target stayed ≥65%. A format under 55% at 48 h is dead: no sequel, no rebuild.** | 0/49 under 55% reached 5K; 9/15 at ≥65% did; ρ = +0.63, n=79 | **High** |
| S2 | **The core meter is a container filling to a FULL/MAX line visible at frame 0.** | +8.6 stayed points (se 2.8) with other choices held fixed; non-press FILL 4.2K vs 2.0K, p=0.005 | Medium-high |
| S3 | **×N only together with FILL. Never ×N with a CLEAR, points or distance meter.** | ×N + FILL 66% stayed, 4.2K; ×N + CLEAR/SCORE 43%, 1.7K; n 7 vs 7, p=0.004 | Medium |
| S4 | **15-17 s, ending on one decisive event.** | 15-17 s: 117% viewed, 3.9K vs 18-22 s: 97%, 2.0K; the length effect runs entirely through retention | Medium-high (≤14 s untested) |
| S5 | **Stop making everyday SCORE/RACE duels, attempts-until-it-breaks clips and abstract puzzles.** | Stayed 49.8%, max 2.5K views (n=7) / loop −10.5 points, max 2.75K (n=5) / 1.6K median, max 1.9K (n=4); 0 of 16 reached 5K | Medium (n is small per class) |
| S6 | **Sequel any Short at ≥65% stayed within 14 days, with one nameable change.** | Sequels of hits 5/5 ≥10K | Medium (n=5; mostly press) |
| S7 | **Don't optimise music type, hashtags or slot.** | PD vs ASMR stayed 57.0 vs 57.1; hashtag A/B n=2; slot confounded | Medium (as a null) |

### Long-form
| # | Rule | Evidence | Confidence |
|---|---|---|---|
| L1 | **One themed journey with a goal per long video, built from a family that passes the Shorts gate (press first). Prefer this over mixed best-of compilations.** This conflicts with the project's "compilations 1-2/week" cadence. At n=1 vs 1, test one more of each before rewriting that rule. | Crushing the Sun: 44K impressions and 87% from Home in 2.3 days; compilation: 736 impressions in 5 days | Low-medium (n=1 vs 1) |
| L2 | **Chapters ≤ ~25 s, or a new event every ~15 s inside longer ones. The transition ("SMALLER THAN …!") is the payoff.** | 39-41 s chapters lost 7.5-9 points each; 10 of 14 skip-rises land just before a chapter start | Low-medium (curve from ~95 viewers) |
| L3 | **Open with the strongest, fastest beat.** | 64% remain at the 10% mark (parent prior: ~35% gone); +54 to +64 vs typical for the first 1:15 | Low (n=1) + parent prior |
| L4 | **Judge long-form on CTR × impressions, the 10% mark, AVD in minutes and subs per 1k. Wait ~3 days before judging CTR.** | CTR went from 2.0% on 3K impressions to 5.3% on 44K; it took off on day 2 | Rule (owner, 2026-11-05) + n=1 |
