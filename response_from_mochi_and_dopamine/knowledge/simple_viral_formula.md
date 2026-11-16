# The "simple viral sim" formula: measured (2026-10-16)

Trigger: owner pointed at CodeCraftedPhysics "What was that ending?!" (FOxbcTk7_nI, 1.20M views, 59 s, uploaded 2026-09-08). Hypothesis: "maybe the formula is simple videos like this, not our creative things".

Tags: **FACT** = a published primary or secondary source (URL). **MEASURED** = our own measurement (method given). **INFERENCE** = my reading of the evidence, not proven.

## Dataset (MEASURED)
- yt-dlp `--flat-playlist` over the Shorts tabs of 20 channels gives 2,608 genre Shorts with view counts (rounded). Per-video metadata (exact views, duration, upload date, likes, comments) for 1,189: every CodeCraftedPhysics (CCP) Short plus top-20 + 70 random per other channel. Pulled 2026-10-15/16.
- Visual features come from YouTube storyboards (1 frame/s, 101x180): **151 videos**. That is the top-6 and bottom-6 settled videos of 8 channels, 63 CCP Shorts from Jul 2025 on, and our 29. Measures: frame-0 filled area, colourfulness (Hasler-Susstrunk), hue count, motion.
- **12 audio tracks** were analysed for onset rate, pitched onsets, pitch classes and spectral flatness. 20+ storyboard sheets were read by eye.
- "Within-channel z" means a video's log-views z-scored inside its own channel. It removes channel size, the main confound. "Settled" means uploaded ≥21 days ago.
- Scratch data and scripts: `<local path removed>` (meta_all.json, sbfeat.txt, scripts/).
- Limits:
  - Channels were found through YouTube search, so they are biased toward ones that succeeded.
  - Views ≠ stayed-to-watch, and no retention data is public.
  - n is small wherever stated.

| Channel (Shorts) | n | median views | p90/p10 | ≥1M share | typical length | active |
|---|---|---|---|---|---|---|
| visualizing-magic | 359 | 675K | 36x | 35% | 24-38 s | 2024-08 → now |
| CodeCraftedPhysics | 258 | 206K | 24x | 23% | 48-59 s (2026: 55-84) | 2023-11 → now |
| satisfying.ba11s | 417 | 86K | 46x | 14% | 41-54 s | stopped 2025-03 |
| MusicBouncingBall | 265 | 73K | 156x | 8% | 43-59 s | **started 2026-01** |
| SoftbodySimulationDude (IP characters) | 322 | 67K | 18x | 8% | n/a | |
| Satisfying_Shape5 | 202 | 65K | 119x | 19% | 44-56 s | stopped 2025-04 |
| CountryEggs (countryballs) | 123 | 62K | 30x | 3% | n/a | |
| bouncing_ba11s | 209 | 55K | 6x | 2% | 41-58 s | |
| Satisfying2DSims (parent) | 310 | 34K | 17x | 1% | 26-42 s | 2026-07 → now |
| zenmathart | 302 | 17.5K | 41x | 4% | 22-28 s | |
| vibegeometry | 73 | 14K | 21x | 0% | 31-58 s | fell to ~1-2K in 2026 |
| gravitylab (new) | 41 | 1.3K | 9x | 0% | 34-49 s | 2026-08 → now |
| **Mochi & Bolt (ours)** | 29 | **1.2K** | **3x** | 0% | 18-38 s | 2026-09 → now |

## Findings

### 1. The reference video (MEASURED: 360p frames + 1 fps storyboard)
- **Frame 0** is a full-width (~0.95 w) dense rainbow-gradient spiral of thin bricks on black. Contender 1 (a line) is already on screen at the spiral's mouth. The first debris burst comes at ~1 s.
- **HUD:** a small top roster shows all 6 contenders (LINE, TRIANGLE, SQUARE, HEXAGON, OCTAGON, BALL). The current one is highlighted and failed ones are crossed out. The structure and the end state are readable at frame 0.
- **Goal:** a small skull emblem sits at the centre.
- **Attempts** last ~7-10 s each. Each one eats part of the spiral, stalls and is crossed out. The spiral's hue rotates through the rainbow as it is consumed (orange → green → cyan → blue → magenta → red).
- **Finale:** at ~52 s the ball reaches the centre, the spiral clears to glowing rings, and the camera zooms into a glowing core for ~6 s.
- **Audio:** continuous (1% of frames below -40 dB) and noisy/crunchy (spectral flatness 0.46, debris SFX), with pitched content across 8 pitch classes.
- **CCP's 2026 hits use the same skeleton:** a big rainbow spiral or rings of bricks that is visibly consumed, a parameter that escalates per attempt (ball speed, number of balls), a tiny HUD, often a viewer-comment card at the top for the first ~10 s, and an explosion or flood finale. Examples: 26.8M "When it finally reached the center", 17.9M, 11.1M, 6.7M.

### 2. Characters vs pure mechanic (Q1)
- **MEASURED:** every genre channel above 14K median is characterless shapes on a plain stage.
- **MEASURED:** the character physics channels that reach scale use famous IP or meme characters. SoftbodySimulationDude uses Minecraft Steve, Among Us and Alphabet Lore (160M top). IdanDavid uses Yoshi and SpongeBob. CountryEggs uses countryballs. We can't use any of them (IP rule; Alphabet Lore is also MFK-coded).
- **MEASURED:** I found no physics-sim channel with ORIGINAL characters that broke out. ShapeArenaTV (original blobs, text-heavy HUD, our look) has a 1.1K median, but it is only 1 week old. This is absence of evidence from a limited search, not proof.
- **MEASURED (ours):** our 4 characterless clips (pendulums 1.3K, galaxies 1.2K, zoom 1.1K, sand 1.0K) sit in the same 1.0-1.5K band as the character clips. Removing characters alone did not change anything on our channel (n=4).
- **MEASURED (parent):** the same engine, characterless, had a first-30-upload median of 5.3K, about 4x our first 29.
- **INFERENCE:** the owner is half right. "Simple" wins, but the active ingredient is not the absence of characters. It is the structure (see 4), and characters add cost with no measured benefit. Test it head-to-head (recipe A/B below) instead of assuming.

### 3. Length (Q2)
- **MEASURED:** pooled within-channel Spearman for duration vs views is **-0.05** (n=947 settled, 10 channels). Mean z by bucket ranges from -0.07 to +0.12 for 15-61 s. **Length does not predict views in this genre.**
- **MEASURED:** each channel has a house length, and the direction differs:
  - visualizing-magic: duration vs views ρ=-0.44 (shorter wins; top-10 median 26 s).
  - CCP since Jul 2025: **ρ=+0.33** (n=63; longer wins; top-10 median 61 s).
- **FACT:** YouTube's Shorts lead said there is no length that benefits creators; use the length the story needs (Todd Sherman, TechCrunch 2023-08-25). Shorts may run up to 3 min since 2024-10-15 (PetaPixel 2024-10-04).
- **Reconcile with ours (r=-0.45, n=20):**
  - Our longer clips lost people midway: 52-63% average viewed at 32-38 s.
  - The genre's 55-65 s hits hold because a progress meter visibly advances toward an end promised at frame 0.
  - **INFERENCE:** length is a symptom. Our long clips are long without a visible meter. Rule: length = the number of honest attempts or rungs. An attempts format needs ~50-65 s; a single-build format needs 25-40 s.

### 4. Structures that recur in hits (Q3) (MEASURED: storyboards of 12 hits, 11-41M + 0.8M, vs 9 low performers)
- **A visible progress meter with a terminal state promised at frame 0: 12/12 hits.** Examples: a spiral or rings to be eaten, a circle to be filled, a count to explode, a field of contenders to shrink to one.
- **Sequential attempts / elimination: 7/12.** Examples: each shape fails until the last; "each ball has only 4 seconds to escape" (36.7M); "Which ball will be the last one standing?" (18.8M); escalating ball speed per attempt (26.8M).
- **A distinct big finale: 10/12** (zoom, explosion, flood, shatter).
- **Black background: 11/12.** The exception is visualizing-magic's 40M on cream.
- **Many hues: 9/12.**
  - Within CCP (n=63): views vs hue count ρ=+0.34, colourfulness +0.35, frame-0 filled area +0.34.
  - Top-15 vs bottom-15: frame-0 fill 0.37 vs 0.09; colourfulness 50 vs 20; hues 6 vs 3.
  - Across 8 other channels: more hues in the top-6 in 6 of 8 channels. Other crude features (motion, fill) were coin-flips (3-5 of 8).
- **Debris particles on impact: 6/12** (all the brick-breaking ones). **A minimal HUD: 12/12.** No hit has more than 2 small text lines.
- **The low performers show the opposite:**
  - CCP 64K: monochrome grey rings with an empty black frame 0.
  - MusicBouncingBall 2.2K: one colour and no visible progress for 60 s.
  - CCP lowest: a single repeated tone.
  - gravitylab 11 views: a "3-2-1, pick your side" countdown opening.
  - vibegeometry 102 views and ShapeArena 154 views: 3+ text lines and counters in a brown or busy UI, close to our look.
- **MEASURED (the caveat that matters most):** near-identical siblings differ 90-1000x.
  - MusicBouncingBall's "Will the balls get to center?": 2.59M vs 28.6K, same look, 5 days apart.
  - Satisfying_Shape5: top-6 median 21.6M vs bottom-6 median 20.5K, with visually indistinguishable features.
  - **The format sets the odds. Each upload is a lottery ticket.**
- **MEASURED:** MusicBouncingBall (new in 2026-01) ran 13 uploads of one format at 3-8K. At upload 14 it switched mechanic to "Will the balls get to center?" (CCP's spiral) and got 72K. Upload 19 got 2.59M, and franchise episodes with identical titles followed at 1-8M. The breakout came from a mechanic switch plus repetition, not slow growth.
- **MEASURED (ours):** our p90/p10 is **3x** (every clip at 0.5-3.3K) against 17-156x for every genre channel. No clip has passed the seed test, so the problem is shared by all our formats.

### 5. Titles (Q4) (MEASURED: within-channel z, 2,608 Shorts, 15 channels)
- Every title feature is weak: question mark +0.02; "can/will/how" +0.16 (7 of 11 channels positive); melody/recognition words +0.09 (7 of 10); "end/ending/finally" +0.06 (4 of 7); a number -0.17; "!" -0.23.
- In CCP, "ending" titles look strong overall (329K vs 192K median). In 2025-26 alone the gap vanishes (150K vs 163K), so it is an era confound.
- The top channel (visualizing-magic, median 675K) uses **hashtag-only titles**. MusicBouncingBall reuses one title verbatim per franchise.
- **INFERENCE:** titles are not a measurable lever in this feed. Keep them short and honest, and don't spend iteration on them.

### 6. Audio (Q5)
- **FACT:** the genre went viral on YouTube Shorts in Nov 2023 when each bounce started playing the next note of a famous melody. The first was Crystal Castles "Kerosene" (satisfying.ba11s, 38M in 5 months). Before that, the same visuals got ~191K. (knowyourmeme.com/memes/will-the-ball-escape-ball-bouncing-brainrot)
- **MEASURED:** 10 of the top 25 genre Shorts have titles about recognising a tune ("Reminds me of something", "Sounds familiar", "My pc crashed #pedro", "What sound was that?"). MusicBouncingBall's hits carry "Did you recognise the sounds?" on screen.
- **MEASURED (12 tracks):**
  - Hits: pitched onset sequences with 5-8 pitch classes (melodies), or a continuous bed plus crunchy debris SFX (CCP).
  - CCP's lowest Short: one pitch class repeated (103 of 103 onsets on the same note).
- **FACT:** familiar music activates reward and limbic circuitry more than unfamiliar music, independent of liking (Pereira et al. 2011, PLoS ONE, pubmed.ncbi.nlm.nih.gov/22110619).
- **Constraint:** the viral melodies are copyrighted pop songs, which CLAUDE.md rule 4 forbids for us. Our version is a famous **public-domain** melody (adult-coded classical; check `kit.KID_CODED_MELODIES`) or an owner-provided track.

### 7. Loops / replays (Q6)
- **FACT:** since 2025-03-31 a Shorts view is counted at every start or replay, with no minimum watch time. The old metric is now "engaged views" (TeamYouTube post, 2025-03-26: support.google.com/youtube/thread/333869549; coverage ppc.land/youtube-changes-how-shorts-views-are-counted-from-march-31/).
- **FACT:** YPP eligibility and Shorts revenue use **engaged** views (support.google.com/youtube/answer/12504220).
- **Implications:**
  - Public view counts on 2025-26 Shorts (including the 1.2M reference) include loops.
  - Loops inflate the number we compare, not the money.
  - No primary source says replays raise ranking; vendor claims are unverified.
- **MEASURED (ours):** ring_escape2 had 132% average viewed but 26% stayed and 1.2K views. Rewatching by the few who stayed did not trigger a push.

### 8. Other facts
- **FACT:** Shorts distribution tests a "seed audience" and then expands or tapers (Sherman, TechCrunch 2023-08-25: techcrunch.com/2023/08/25/youtube-demystifies-the-shorts-algorithm-views-and-answers-other-creator-questions/).
- **FACT:** recommendations use viewing behaviour, likes, dislikes and satisfaction surveys (youtube.com/howyoutubeworks/recommendations/).
- **FACT:** high-arousal positive emotion (awe) predicts sharing (Berger & Milkman 2012, JMR: faculty.wharton.upenn.edu/wp-content/uploads/2011/11/Virality.pdf). That fits a "what was that ending?!" finale (INFERENCE).
- **FACT (weak transfer):** near-misses recruit win-related reward circuitry and raise motivation to continue (Clark et al. 2009, Neuron, PMC2658737). The effect held only under personal control, so applying it to "each one almost made it" viewing is INFERENCE.
- **FACT:** I found no peer-reviewed study of "oddly satisfying" videos; there are only press explanations (Live Science, Discover).
- **Weak (vendor) sources:**
  - An Inflow study (n=5,400) says 50-60 s Shorts got 22x the views of under-10 s Shorts. These are bucket totals, not per video.
  - Metricool (~800K videos) reports average Shorts watch ~16 s.
  - Treat both as weak.
- **MEASURED (cadence):** CCP uploads ~1-2 per week in 2026 (2026 Q3: 15 uploads, median 350K). The parent uploads 3-5 per day (34K median).

## Rules that follow (INFERENCE from the above)
1. **One mechanic + a visible progress meter + a terminal state readable at frame 0.** A spiral to eat, a container to fill, a roster to cross out, or a count to explode. The viewer must see "where this ends" before the first swipe.
2. **Sequential attempts / elimination** is the strongest recurring skeleton: a roster HUD, each contender fails visibly, and the last succeeds into a big finale.
3. **Frame 0 is full-width, colour-dense and multi-hue on black**, with the first contender already moving and the first impact by ~1 s. Never an empty, monochrome or countdown frame.
4. **Minimal HUD:** at most 2 short text lines plus a small icon roster or parameter readout. No panels or title cards.
5. **Audio:** a continuous bed plus crisp impact or debris SFX, or note-per-hit through a famous PD melody. Never a single repeated tone.
6. **Length follows the attempts:** ~50-65 s for 5-6 attempts, 25-40 s for one build. The meter must keep advancing to the end.
7. **Volume on ONE proven skeleton, with franchise episodes,** because per-video outcomes vary 100x even within a format. Judge a format on ≥10 uploads, not 1.
8. Titles: short and honest; stop iterating on them.

## Video recipes
**A. "Who breaks through?": attempts until one succeeds (CCP skeleton, our engine)**
- **Frame 0:** a rainbow-gradient spiral or concentric rings of ~400 thin bricks filling 0.9 w on black, a goal emblem at the centre, and contender 1 already at the mouth.
- **HUD:** a top roster of 5-6 contenders as icons, highlighted when active and crossed out when failed. Contenders: shapes (line → triangle → … → ball) or tools (hammer, drill, saw, laser…).
- **Each attempt (~8-10 s):** eats bricks with debris particles and crunch SFX, then stalls. The spiral hue shifts per attempt.
- **The last contender** reaches the centre, followed by a zoom-into-core finale (~5 s).
- **Audio:** an owner track or PD bed plus brick SFX (+12 ms off notes).
- **Length:** 55-62 s. **Nameable change per episode:** the structure (spiral → maze → tower), the contender set, or the rule ("each attempt is 2x faster").

**B. "Recognise it?": a melody ball with a fill payoff**
- One ball in a circle. Every collision plays the next note of a famous adult-coded PD melody (e.g. In the Hall of the Mountain King, Can-can, Toccata in D minor, Eine kleine Nachtmusik).
- The ball grows or speeds up per hit, leaving a rainbow trail, until it fills the circle and the melody's climax lands.
- Length 30-45 s. On-screen line: "Do you recognise it?"
- **Nameable change:** the melody and the growth rule.

**C. "Every exit spawns 2": exponential count to overflow**
- One ball in a rotating box with a gap. Every escape spawns 2 inside. A big count HUD.
- It builds to a container overflow or burst finale. Length 45-60 s.
- This is the parent's best skeleton ("Every ball crushed splits into 3", 1.8M; "15,939 pieces", 2.4M).

**Head-to-head test of the owner's hypothesis**
- Ship recipe A twice per day for ~10 days: half pure shapes, half the same video with Mochi and Bolt as the two last contenders (faces small, no extra HUD).
- Compare stayed-to-watch % and views. This settles "characters vs simple" on OUR channel instead of by assumption.
