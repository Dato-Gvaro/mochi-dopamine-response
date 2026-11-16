# Growth deep dive: views, subs, long-form (2026-11-12)

**Method.**
- yt-dlp pulls on 2026-11-12: the Shorts and Videos tabs of 36 channels (flat lists; views and subs are rounded to 2-3 significant figures), RSS feeds for upload cadence, and per-video metadata for 97 oldest/top/newest videos plus every ScaleShock upload.
- Web: official YouTube/Google pages, one Google research paper, and analyst studies.
- No Chrome.
- Data and scripts: `output/tmp/research_1112/` (`summary.json`, `flat/`, `meta/`, `meta_ss/`, `rss/`, `thumbs_grid.png`, `scripts/`).

**Grades:**
- **A** = YouTube/Google official.
- **P** = a primary research paper by Google engineers.
- **M** = measured by us here.
- **B** = an analyst or study with data.
- **C** = a vendor blog.
- **D** = an anecdote or creator practice.
- **I** = inference.

**Limits:**
- Public views include replays (since 2025-03-31) and count from the first frame (since 2026-08-24), so view-based ratios for channels from before 2025 are not comparable.
- Survivor bias: channels were found by search and through our audience report.
- The subs per 1K views ratio uses lifetime subs from all sources.

## (a) What prior research already concluded (do not redo)
1. **Hook:** stayed-to-watch is the gate (ρ=+0.63; 0 of 49 Shorts under 55% stayed reached 5K). What works: a FILL meter + ×N, 15-17 s, one decisive end. What fails: everyday SCORE/RACE duels, attempts clips, abstract puzzles.
2. **Hits:** they come from a mechanic switch, then one-change sequels inside 14 days. The press family is the engine. Famous physical scale and growth races fit our audience.
3. **Subs:** they come from volume at ~0.4 per 1K. Long-form converts ~9x better (Crushing the Sun: 3.4/1K, 87% Browse). A themed journey beats a mixed compilation.
4. **Money:** under the YPP 2027 rules (20M Shorts views per 90 d or 8K long-form hours), long-form hours are the only realistic route. Point the related-video link at the matching long-form. Make the channel page a subscribe page.
5. **Myths already listed:** posting time, a volume threshold, deleting and reposting, hashtags, comment bait for reach, "Shorts must be 50-60 s", titles as a lever.

**What the prior files got wrong or left open:**
- **"One hit lifts the floor"** (early_breakouts) only holds for a few weeks; see B5.
- **"~1.3K is the seed floor"** is right, but our problem is graduation, not the floor; see B2.
- **"Characters add cost with no benefit"** needs splitting: characters don't help in the Shorts feed, but in long-form thumbnails a protagonist-vs-boss image is what wins in our cluster; see B9.
- **"Compilations flop"** is n=1. Peers' compilations do 64-208K, so packaging is untested; see B8.

## (b) New findings

### Views: how the Shorts feed distributes
**B1. Every new Short gets a bootstrap slot. The 100x happens only after it "graduates" to the main recommender (P + B).**
- **The Google paper** (KDD 2023, "Fresh Content Needs More Attention"; co-author Cristos Goodrow, YouTube VP Engineering; the platform is unnamed):
  - Fresh and tail content gets **one dedicated floating slot per session**, ranked by a Thompson-sampling bandit.
  - The real-time model trains on the last 15 min of feedback, with ~2 h latency. The main stack's latency is 18-24 h.
  - An item leaves the slot after **n consumptions** and is then "readily picked up by the main recommendation system" if it earned positive interactions.
  - The success metric is measured at **7 days, because it converges by then**.
- **What this explains (I):**
  - The fixed ~1-3K floor.
  - "Took off on day 2": the main stack retrains daily (Crushing the Sun; press_split2's repeat pushes).
  - Why a Short is decided in its first week.
- **Beaupré, Sep 2026 (A, via PPC Land):**
  - Ranking is per viewer, and the system learns **separately per audience**.
  - Viewers with history on a channel and topic rank its videos higher.
  - **New channels are matched on topical preferences.**
  - Some videos gain most of their audience a month or more later. Most likely this means evergreen long-form (I).

**B2. Our weak spot is graduation, not the floor (M + B).**
- **vidIQ** (367K Shorts channels created H1 2025; B):
  - The median Short has 1,362 views at 30 days. Upload #1, #5 and #10 are all the same (~1.3K), so there is no learning curve. Long-form rises 51% from upload #1 to #10.
  - Per Short: P(≥1K) = 56.6%, P(≥10K) = 20.9%.
- **Ours** (Shorts tab without the 6 newest):

| Channel | ≥1K | ≥10K |
|---|---|---|
| Mochi & Bolt | **98%** | **14%** |
| DopamineEXE | 97% | 7% |
| SatFy (started Oct 4) | 100% | 57% |
| OrbitMathLab (Oct 18) | 100% | 51% |
| AlgorithmBattles (Oct 17) | 100% | 50% |
| PinkSimulations | 100% | 76% |

- Our seed always pays out. It rarely graduates.
- **Those same-month peers sit in the cluster our audience watches** (maths and science "brain-satisfying"; `audience_watch_2026-11-03.md`). Our everyday duels sit outside it.
- Recent examples: coffee 608 views, microwave 675.

**B3. Posting volume is not what separates channels (M + B + A).**
- **Peer cadence** (last 15 uploads per RSS) against the newest-30 median:

| Channel | Uploads/day | Newest-30 median |
|---|---|---|
| CodeCraftedPhysics | 0.17 | 364K |
| MathMango | 1.1 | 221K |
| MusicBouncingBall | 1.0 | 213K |
| VectorFox | 2.3 | 401K |
| PinkSimulations | 6.0 | 32K |
| WatchTheMath | 5.4 | 2.5K |
| Mochi & Bolt | 3.1 | 2.8K |

- **OverseerOS** (16.8K videos; C): days with two Shorts got lower per-Short medians in aggregate, but 62% of channels did better per video on two-Short days.
- **YouTube** pays for volume only through the YPP-only Shorts consistency bonus pilot (Oct 2026; A).
- **Verdict:** keep 3/day. Don't add more. The lever is which class fills the slots.

**B4. Revival is rare; plan on the first 10 days (B).**
- **Mario Joos** (Dec 2025, 7 channels at 100M-1B monthly views; analyst theory that YouTube has not confirmed):
  - Since mid-Sep 2025, Shorts older than ~28-30 days lose impressions sharply.
  - Tim Chesney saw the same on 2B views.
- **Metricool** (799,718 videos, Feb 2025 vs Feb 2026): **83% of interactions arrive within 10 days.**
- **Our data agrees:**
  - press_split2 is at 355K, still adding ~4K/day at 4 weeks. Its rate is decaying.
  - press_tools and sandcastle got one spike each, then fell 95% the next day.
- **Deleting or privating flops:**
  - No source shows it helps.
  - Sherman (A, 2023): delete-and-repost "gets seen as spam".
  - Ritchie (A, weekly column): don't delete, private or unlist only to change channel performance.

**B5. A breakout's floor lift decays within 2-4 weeks unless the "show" keeps evolving (M).**
Median Shorts views per upload block, oldest to newest (newest block left out because those clips are young):

| Channel | Block medians | Pattern |
|---|---|---|
| Ballculus | 170K → 140K → 10K → 23K → 11K → 9.9K → 7.8K | decays in ~3 weeks |
| MathMango | 682K → 226K → 1.3M → 187K → 167K | falling |
| NefiSims | 220K → 115K → 133K → 59K → 38K → 50K | falling |
| Satisfying2DSims (parent) | 52K → 46K → 37K → 25K → 17.5K | falling |
| WatchTheMath | 17.5K → 6.8K → 3.2K | falling |
| VectorFox | 14K → 212K → 567K → 730K | rising |
| MusicBouncingBall | 5K → 246K → 311K | rising |
| PinkSimulations | 4.6K → 33K | rising |

- **The channels that keep rising share three things:**
  - A fixed wrapper the viewer recognises:
    - VectorFox: flags, "find your country".
    - MusicBouncingBall: "Will the Ball…", one title reused ×25.
    - PinkSimulations: 🩷 on every title, micro-story titles.
  - A new mechanic or topic inside the wrapper every upload.
  - 1-6 uploads a day.
- **Mechanism (I, from B1):** viewers with channel history get our next upload ranked higher. A recognisable wrapper builds that history.
- **Our returning viewers: 0.9% (99.1% new, Nov 3).** No affinity is accumulating.

**B6. Titles: still weak, but famous objects are consistently positive (M).**
- **Data:** within-channel z of log views, 20 channels from 2026, 3,170 Shorts.

| Title feature | z | Channels positive |
|---|---|---|
| Famous object (Moon, Sun, atom, googol…) | **+0.30** | 10/12 |
| "Every/Each…" rule | +0.24 | 7/10 |
| "How many/long/far / What if" | +0.13 | 8/12 |
| "?" | +0.12 | 13/17 |
| Viewer-participation words | +0.02 | 4/10 |
| **Big number in the title** | **−0.33** | 4/11 |

- **Comments don't spread Shorts.** Viral Shorts in every peer channel have **0.01-0.2 comments per 1K**. The comment rate falls with reach, as likes do.

### Subs: why Shorts convert poorly and what changes it
**B7. Our conversion is the genre norm. Long-form is the only big multiplier (M).**
- **Shorts-only channels that started in 2026, subs per 1K public views:**
  - NefiSims 0.45, VectorFox 0.49, WatchTheMath 0.50, PinkSimulations 0.52, MathMango 0.61, MusicBouncingBall 0.62, Ballculus 0.65, AlgorithmBattles 0.69, OrbitMathLab 0.71, gravitylab 0.75.
  - **Ours 0.44, DopamineEXE 0.37:** the bottom of the band, not an outlier.
  - Per engaged view we are at 0.71 (370 subs on 520K engaged).
- **Long-form share predicts conversion:**
  - Spearman long-form share vs subs per 1K = **+0.59** (n=31 channels with ≥1M views).
  - Median **0.64** with <5% long-form views (n=14) vs **2.87** with ≥50% (n=12).
- **Named characters don't fix conversion in the feed.** NefiSims: 3 named characters, 0.45/1K.
- **Converting channels have story or fandom with ongoing stakes**, and their views are mostly long-form:
  - Jelle's Marble Runs: league teams, 7.14/1K.
  - Haminations 3.83, Alan Becker 3.45.
- **Cause (I + A):**
  - In the feed, more of the same arrives without subscribing, so a sub has to buy something the feed won't deliver: the next episode of a story.
  - Beaupré (A): people subscribe to what they expect next, and series hold TV viewers.
  - The subscribe action is weak anyway (~90% of subscribers skip an upload).
  - The Subs tab moved into the Home top bar on Oct 22, 2026 (9to5Google via secondary reports). Subscription-feed value falls further.

**B8. The case that matters: ScaleShock, in our exact cluster, got 10.1K subs in 15 days (M).**
- **Uploads:** first upload Oct 28, 2026. 22 Shorts (481K views) and 12 long videos of 6-15 min (1.41M views) in 15 days. **75% of its views are long-form; 5.35 subs per 1K.**
- **The format:**
  - **"×2" is a glowing orb with a face**: a protagonist fighting famous-object "bosses" with HP bars: sand → whale → pyramid → Earth → Sun → universe → googol → googolplex.
  - **One long video a day for 9 days.** Parts 1-3 on Oct 29/30/31 (338K / 183K / 297K). Median long video ~69K.
  - **2-3 same-day Shorts on the same boss** ("Can DOUBLING destroy the SUN in 30 seconds?" 27K, posted the same day as Part 1).
- **The participation layer:**
  - The description says: "Guess the number of hits before every fight… Comment your result (__/12)".
  - Each part has a "Challenger from your comments" round and a "You asked" opener.
  - Each part ends on an A/B/C question answered in the next part.
  - Every long video description carries a `?sub_confirmation=1` link ("JOIN TEAM ×2").
- **Long-form comments run 4-8 per 1K** vs 1-2 for peers.
- **Contrast in the same cluster and month:** Ballculus had a Shorts hit (n² vs 2ⁿ, 1.6M) and 4.9M Shorts views, and has **3.3K subs**. ScaleShock got 3x the subs on 40% of the views.
- **Thumbnails** (`thumbs_grid.png`):
  - The top long videos in our cluster (ScaleShock, SatFy 291K, Ballculus 77K) all show **a character or protagonist vs a giant boss/goal, with an HP or goal bar and a ≤5-word challenge.**
  - Ours have no protagonist, except the island video, whose conflict reads weakly.

### Monetisation: Shorts and long-form
**B9. Long-form gets Home traffic on topic demand, not from Shorts (M + A + B).**
- **Our videos:**

| Long video | Views | Days live |
|---|---|---|
| Crushing the Sun | 11.5K | 10 |
| Island duels | 197 | 5 |
| Compilation 1 | 436 | 13 |
| DopamineEXE domino journey | **17** | 6 |

- **ScaleShock got 338K on day-2 of a brand-new channel.** So Browse is open to new channels; packaging and topic decide.
- **Compilations can work** for channels with 25-98M Shorts views and search-phrase titles:
  - PinkSimulations: "18 Most Satisfying Physics Simulations (Every Sound Is A Real Collision)" 208K; others 64-135K.
  - NefiSims: 74-90K.
- **Joos (B, Dec 2025):** organic long-form choices on Home were cut by up to 80% (Shorts shelves took the slots). There are fewer slots, so CTR decides more.
- **AIR** (18K channels; B, correlational):
  - In entertainment and science, long-only channels have equal or higher median subs than mixed channels.
  - Above 55% Shorts uploads, long-form performance drops.
- **Verdict:** Shorts neither feed nor kill long-form. Related Shorts brought 0.3% of Crushing the Sun's traffic. The two formats share a topic and a brand.
- **Hours (I):**
  - Crushing the Sun ≈ 11.5K views × ~2.6 min ≈ 500 h.
  - **Eight episodes at ~20K views ≈ 4,000 h** = the old YPP bar, before the Feb 2027 doubling.
  - Shorts give us 1.1M per 90 d against a 10M bar. Long-form is the only route.

**B10. Tools.**
- **Test & Compare (A/B titles and thumbnails):**
  - Long-form only, on desktop Studio, with advanced features.
  - **Shorts are excluded** (Help 16391400; A).
- **Shorts hook test ("upload up to three video cuts"):**
  - Announced on Sep 23, 2026 as "coming soon" (YouTube blog / Creator Insider; A).
  - Eligibility not stated.
  - It is ideal for code-generated variants.
- **Shorts Series:** YPP-only (TechCrunch, Sep 23, 2026; A).
- **Custom feeds** (prompt-built; US, English, signed-in, Oct 2026; A):
  - The matching method is undisclosed.
  - "Ask YouTube" uses titles, descriptions and chapters (prior research), so give long videos dense chapters.

### Brainrot audience (US/English)
- **What holds (M, peers):**
  - A question the viewer already has, about a famous object: MathMango's "How Many Folds To Reach The Moon?" got 27.7M with 1.1 uploads a day.
  - Self-reference: VectorFox's "find your country", median 400-700K.
  - Pick-a-side races: Jelle's "Pick your color!" Shorts are its top Shorts at 334K vs a 47K median.
  - A recurring fighter: ScaleShock's ×2.
- **Our comments already read our duels as game archetypes** ("skill vs spam", "early vs late game").
  - **The converting peers use game structures:** bosses, HP bars, brackets, "final boss", tournaments (ScaleShock, Ballculus).
  - This is adult-coded framing, which suits the made-for-kids rules.
- **Comment prompts that aren't cheap (M):**
  - A score to report ("__/12").
  - A challenger chosen from the comments.
  - An open question answered in the next part.
  - All live in long-form. In Shorts, participation words are neutral for views (B6). Keep CLAUDE.md's "no viewer-prediction question" for Shorts captions.

## (c) Competitor table (2026-11-12, yt-dlp)
**Columns:**
- "Med" = median views of all Shorts (rounded).
- "≥10K" = share of Shorts with ≥10K views, newest 6 excluded.
- "LF%" = share of the channel's views that come from long-form.
- "S/1K" = subs per 1K total views.

| Channel | Started | Subs | Shorts | Med | Top | ≥10K | Long | LF% | S/1K | Structure / conversion clue |
|---|---|---|---|---|---|---|---|---|---|---|
| **Mochi & Bolt** | Oct 3 (this era) | 497 | 110 | 2.1K | 355K | 14% | 3 | 1% | 0.44 | Mixed classes; no fixed wrapper; 0.9% returning |
| **DopamineEXE** | — | 35 | 35 | 1.4K | 21K | 7% | 1 | 0% | 0.37 | Domino long video: 17 views |
| **ScaleShock** | **Oct 28** | **10.1K** | 22 | 17K | 56K | 75% | 12 | **75%** | **5.35** | ×2 protagonist vs bosses; daily Parts; Shorts as same-day trailers; score-in-comments |
| MathMango | Oct 12 | 32.9K | 29 | 221K | 27.7M | ~100% | 4 | 0% | 0.61 | "How Many X To Y?" famous questions; long-form from Nov 4 (31K) |
| Ballculus | Oct 8 | 3.3K | 38 | 11K | 1.6M | 69% | 20 | 4% | 0.65 | "A vs B: leads… until it doesn't"; long "Math Heroes vs a Boss" 77K; median decayed 170K → 8K |
| SatFy | Oct 4 | 2.8K (1.82K on Nov 1) | 114 | 12K | 317K | 57% | 10 | 12% | 0.89 | Counting/π franchises; long "Count to a Million… Infinity" 291K |
| OrbitMathLab | Oct 18 | 1.8K | 73 | 9.1K | 801K | 51% | 2 | 0% | 0.71 | Pivoted from "X ball 🎵" to famous questions |
| AlgorithmBattles | Oct 17 | 1.1K | 64 | 8.6K | 321K | 50% | 0 | 0% | 0.69 | Fixed title suffix "\| Algorithm Battles"; rotating fighters |
| NefiSims | Sep 28 | 44.5K (22.8K on Oct 27) | 171 | 75K | 20.7M | ~100% | 10 | 0% | 0.45 | Named characters; 5/day; compilations 74-90K; median decaying |
| PinkSimulations | Aug 13 | 13.6K | 330 | 21.5K | 7.9M | 76% | 22 | 3% | 0.52 | 🩷 on every title; micro-story titles; 6/day; compilations 64-208K |
| VectorFox | Jun 6 | 67K | 181 | 237K | 23.8M | ~100% | 7 | 0% | 0.49 | Flags/countries self-reference; median still rising |
| MusicBouncingBall | Jan 7 | 115K | 293 | 84K | 30.6M | 82% | 2 | 0% | 0.62 | One title ×25 per franchise ("Will the Ball Merge Into Final Form?") |
| WatchTheMath | Aug 14 | 8.8K | 306 | 3.7K | 4.1M | 28% | 0 | 0% | 0.50 | 5/day; median decayed 17.5K → 3K |
| Satisfying2DSims (parent) | Jul 6 | 30.7K | 448 | 30K | 3.7M | 86% | 30 | 12% | 0.74 | Median decaying 52K → 17.5K |
| CodeCraftedPhysics | 2023 | 478K | 263 | 206K | 29M | ~100% | 38 | 10% | 1.48 | 0.17 uploads/day; pre-2025 views not comparable |
| visualizing-magic | 2024 | 550K | 401 | 630K | 41M | ~100% | 36 | 2% | 0.70 | Hashtag-only titles |
| Jelle's Marble Runs | — | 1.52M | 40 | 47K | 543K | 97% | 777 | 99% | **7.14** | League teams, seasons; "Pick your color!" Shorts |
| Riley Marbles / Crazy Marble Race / Marble Factory | — | 313K / 256K / 146K | ~0 | — | — | — | 101-325 | 100% | 3.18 / 2.31 / 2.00 | Country/team elimination races, long-form only |
| Haminations / Alan Becker | — | 9.1M / 34.4M | 55 / 105 | 13M / 18M | 99M / 94M | — | 62 / 156 | 51% / 75% | 3.83 / 3.45 | Character story arcs |
| gravitylab (control) | Aug 24 | 98 | 64 | 1.4K | 13K | 3% | 32 | 4% | 0.75 | Monochrome "which side fills"; never graduated |

## (d) Ranked actions (both channels)

### 1. M&B: launch a long-form saga, "Mochi vs Everything", in the ScaleShock frame
- **What:**
  - Mochi (×2) and Bolt (×3, or a rival rule) are the fighters.
  - Famous-object bosses with HP bars, rising: sand → whale → pyramid → Earth → Sun → galaxy → googol.
  - 6-10 min, with 10-15 round chapters of ≤25-40 s each (L2).
  - Parts 1-3 on consecutive days, then 2/week.
  - Honest maths; on-screen text only, no voice.
- **Thumbnail:** blob face vs giant boss + HP bar + "CAN MOCHI BEAT THIS?".
- **Rules check:**
  - Mochi and Bolt stay in exact rest shape: no limbs, no stretch. Impact comes from floating props.
  - **Conflicts (one line each):** this replaces the "compilations 1-2/week" cadence, and the 1-episode-per-week rule for this saga only. The owner decides.
- **Expected:** 5-70K views per part at 3-7 subs/1K = **+20-400 subs and ~200-3,000 h per part**. Evidence: B8, B9.
- **Cost:** high. ~1 agent-day per part plus 15 min of owner review.
- **Measure (72 h / 7 d):** impressions and CTR, retention at the 10% mark, subs/1K per part, Browse share.
- **Kill rule:** if Parts 1-2 each get <3K impressions in 72 h, repackage with Test & Compare before Part 3.

### 2. M&B: one daily Shorts slot = a same-day trailer of the current part
- **What:** the same boss, the same day ("Can Mochi crush the SUN in 15 seconds?"). Its related video = that part.
- **Expected:** these sit in our best class (growth/scale; tug_war 11.9K, galton 8.9K) and tie Shorts viewers to an episode they can follow.
- **Cost:** low (a cut of the long-form sim).
- **Measure:** trailer stayed% and views vs the channel median; the part's Shorts-feed traffic share.

### 3. M&B: stop the out-of-cluster class now
- **What:** no more everyday SCORE/RACE duels, pilots, attempts clips or abstract puzzles. All 3 slots come from FILL+×N, famous physical scale, growth/boss battles and press episodes.
- **Expected:** ≥10K rate from 14% to ≥25%; median from 2.1K to 3-4K. Evidence: B2, B6, prior S5.
- **Cost:** none. Built clips move to reserve.
- **Measure:** ≥10K share and median of the next 30 Shorts at 72 h; stayed% ≥60% on ≥2/3 of them.

### 4. M&B: one "show" wrapper for returning viewers
- **What:**
  - A fixed series tag in every title before the hashtags (e.g. "| Mochi vs Bolt").
  - A fixed frame-0 signature: both blobs + the meter in the same place.
  - One-line channel promise: "two blobs, one rule each, physics decides".
- **Expected:** returning viewers from 0.9% to ≥3%; slows the post-hit decay (B5).
- **Cost:** low.
- **Measure:** Studio Audience, returning viewers per week; Shorts block median.

### 5. Package every long video with Test & Compare (3 titles × 3 thumbnails)
- **Retest now:**
  - Compilation 1, with a search-phrase title like PinkSimulations' "N Most Satisfying Physics Simulations (hook)".
  - The island video.
  - DopamineEXE's domino video ("Can 1 Domino Knock Down the Universe? (0.6 in → Everest → Earth → Universe)").
- **Expected:** a CTR lift where impressions exist. It shows whether packaging, not the format, sank the compilation (B9).
- **Cost:** low; agents render the thumbnails.
- **Measure:** the winner by watch-time share in 3-14 d; impressions before vs after.

### 6. Long-form participation layer, not in Shorts
- **What:**
  - Description and pinned comment: "guess the hits before each round, comment your score __/12".
  - A "challenger from the comments" round (a real suggestion, credited).
  - Each part ends on an A/B/C question answered in the next part.
- **Expected:** comments from ~1/1K to 4-8/1K (ScaleShock), a pipeline of episode ideas, return visits.
- **Cost:** low.
- **Measure:** comments/1K and returning viewers on parts 2+.

### 7. Subscribe path on long-form
- **What:**
  - First description line: "JOIN TEAM MOCHI → youtube.com/@<handle>?sub_confirmation=1" (D, ScaleShock).
  - Channel trailer = saga Part 1. Featured video = the newest part.
- **Expected:** small; a no-regret change.
- **Cost:** 10 min of owner time once.
- **Measure:** Subscription source report, 28 d before vs after.

### 8. DopamineEXE: 14-day decision test
- **What:**
  - Cut to 1 Short/day from its two proven families only: "SPLITS… until DUST" (20K) and the scale journey (21K).
  - Repackage the domino video (#5).
- **Fold rule:** if by Nov 26 DopamineEXE's long video still gets <1K impressions in 72 h and its Shorts ≥10K rate stays <10%, fold its formats into M&B (prior option a). Beaupré (A): one channel per audience, and both channels draw the same cluster.
- **Expected:** frees 1-2 builds/day for #1.
- **Cost:** saves time.
- **Measure:** impressions, subs/day, ≥10K rate.

### 9. Franchise to the decay curve, not to a count
- **What:**
  - After a hit, ship 2-3 one-change sequels within 14 days (prior rule).
  - Then require each further episode to hold ≥0.3x the parent's views. Below that, move the wrapper to a new mechanic.
  - Peers' post-hit medians halve in ~2-4 weeks (B5).
- **Expected:** fewer dead sequels; satisfies the owner's "no duplicates" with data.
- **Cost:** none.
- **Measure:** sequel/parent view ratio at 72 h.

### 10. Check Studio weekly for the Shorts "video cuts" hook test
- **What:** when it appears, ship every franchise Short with 3 frame-0 variants. The code makes them almost free. Stayed% is our #1 predictor (ρ=+0.63).
- **Expected:** +3-8 stayed points on the winners (I).
- **Cost:** low.
- **Measure:** the winning cut's stayed% vs the channel median.

## (e) Myths to ignore (new, beyond the 2026-10-31 list)

| Claim | Verdict | Evidence |
|---|---|---|
| "Our sub conversion is uniquely terrible" | It is the 2026 Shorts-only norm (0.45-0.75 per 1K); we are 0.44. Long-form is the only big multiplier. | M (n=10) |
| "Characters make Shorts viewers subscribe" | NefiSims (3 named characters) converts 0.45, the same as us. Story and episodes convert, mostly through long-form. | M |
| Old channels' ratios (satisfying.ba11s 2.6, Shape5 1.3 per 1K) as benchmarks | Views from before 2025 excluded replays, so they are not comparable. | A (counting changes) |
| "Post more Shorts to raise the median" | Short #10 performs like Short #1 (367K channels). Cadence of 0.17-6/day doesn't separate peers. | B, M |
| "A breakout permanently lifts the floor" | The lift decays within 2-4 weeks unless the wrapper evolves. | M (5 channels) |
| "Old Shorts will revive" | Since Sep 2025 there is a reported <30-day recency tilt; 83% of interactions arrive within 10 days. Don't plan on it. | B (analyst; YouTube unconfirmed) |
| "Private or delete flops to clean the channel" | No evidence it helps. YouTube says don't do it to change performance; repost = spam risk. | A |
| "Big numbers in the title boost a Short" | z = −0.33 within channel (4/11 channels positive). Use a famous object instead (+0.30, 10/12). | M |
| "Comment bait spreads Shorts" | Viral Shorts get 0.01-0.2 comments per 1K. Comments matter for long-form community, not feed reach. | M |
| "A/B test Shorts titles or covers" | Test & Compare excludes Shorts. The video-cut test is not live yet. | A |
| "Subscribers will see our uploads in the Subs tab" | Subs moved into a Home top tab (Oct 22, 2026). ~90% of subscribers skip an upload, and suggested videos are where subscribers watch most. | A / secondary |
| "Shorts traffic will grow the long video" | Related Shorts = 0.3% of Crushing the Sun's traffic. Browse decides; Shorts share the topic, not the viewers. | M, A |
| Vendor claims: "satisfaction surveys now rank Shorts", "test window under an hour", "16.9 subs per 10K Shorts views" | No primary source. | C |

## Sources
**Official (A):**
- Sherman, Creator Insider 2023: https://www.youtube.com/watch?v=n3jsYK_-aRU (quotes via https://outlierkit.com/resources/youtube-shorts-algorithm/)
- Beaupré, Creator Insider Sep 2026: https://www.youtube.com/watch?v=rHLjxrbXmmY (claims via https://ppc.land/subscribers-skip-90-of-uploads-in-their-feed-youtube-director-says/)
- A/B test titles & thumbnails (Shorts excluded): https://support.google.com/youtube/answer/16391400
- Video-cut A/B announcement: https://ppc.land/youtube-to-test-up-to-3-versions-of-one-video-on-real-viewers-shorts-too/ · https://80.lv/articles/youtube-adds-a-b-testing-for-video-cuts-expanding-studio-s-toolkit/
- Shorts Series (YPP): https://techcrunch.com/2026/09/23/youtubes-new-short-series-feature-brings-episodic-viewing-to-shorts/
- Custom feeds: https://ppc.land/youtube-lets-viewers-build-their-own-feed-with-a-text-prompt/
- Confirmed-changes log: https://outlierkit.com/resources/youtube-algorithm-updates/
- Ritchie, don't delete/private to change performance: https://blog.youtube/culture-and-trends/renes-top-five-on-youtube-march-28-2024-edition/

**Research (P):**
- Wang et al., KDD 2023, "Fresh Content Needs More Attention": https://arxiv.org/abs/2306.01720 (read via https://ar5iv.labs.arxiv.org/html/2306.01720)

**Analyst / data (B):**
- vidIQ first-10-videos study, Jul 2026: https://vidiq.com/research/youtube-first-10-videos-study/
- AIR Media-Tech, 18K channels: https://air.io/en/audience-growth/do-youtube-shorts-help-your-long-form-videos-grow-data-from-18000-channels
- Metricool 2026: https://www.socialmediatoday.com/press-release/20260727-metricools-2026-youtube-study-reveals-a-slow-burn-effect-more-views-less/
- Joos, Shorts recency: https://www.searchenginejournal.com/youtube-shorts-algorithm-may-now-favor-fresh-over-evergreen/562661/
- Joos, Home feed: https://ppc.land/youtubes-home-feed-quietly-kills-long-form-video-discovery/
- Subs tab move: https://outlierkit.com/resources/youtube-subscriptions-tab-moved-2026/ · https://www.analyticsinsight.net/news/youtube-moves-subscriptions-tab-to-the-top-of-the-home-screen

**Vendor (C):**
- OverseerOS, Shorts per day: https://www.overseeros.com/blog/how-many-youtube-shorts-per-day

**Measured (M):**
- `output/tmp/research_1112/`: `summary.json` (36 channels), `meta_ss/` (all ScaleShock uploads), `thumbs_grid.png`, `scripts/analyze.py`, `scripts/titletypes.py`, `scripts/rss.py`.

## Correction 2026-11-13 (owner pushback on action 3)
"Everyday duel" is the wrong class line. Own data (flat/MochiBolt_shorts.json):
- Everyday subjects that people argue about, settled by a physical SPECTACLE (melt, flood, fill, smash), do well: big vs crushed ice 39K, sea wall 36K, higher ground 28K, sloppy strings 16K, shredder 15K, rain walk/run 7.3K, shaken soda 4.6K.
- Queue/traffic/abstract-manoeuvre sims fail: lane switch 2.5K, checkout line 1.9K, 2 trips 1.5K, Monty Hall doors 1.8K, $1M vs penny 530.
- The coffee 608 / microwave 675 examples were <24 h old when scraped, so they are invalid evidence.

New test, per clip: (1) a real argued-about question, AND (2) the answer is shown as a physical spectacle, not a queue or path sim.

## Owner decisions 2026-11-14 (the "reorganization" talk)
- Long-form cadence, compilations, Shorts slot mix: DEFERRED. First the owner reviews Iceberg, then we ship one Iceberg long video and decide from its numbers.
- Action 8 (DopamineEXE fold rule) REJECTED: DopamineEXE stays and experiments freely with its OWN videos. When it catches what its audience likes, DopamineEXE itself grows on that format. It is NOT a lab for Mochi; never move its formats there. No Nov 26 fold.
