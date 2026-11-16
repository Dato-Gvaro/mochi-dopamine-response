> **A note for the SatFy team:** this is our working study of the repo you kindly shared. It is written in our internal shorthand: "ADOPT" means we are copying it, "TEST" means we will try it as a labelled test, and "NOT FOR US (our data)" only means our own numbers or our channels' constraints point the other way. It is not a judgement on what works for you. Your results are the reason we studied it. Thank you.

# SatFy's own repo: their rules, checked against ours (2026-11-16)

**Source.** The repo of SatFy (@TheSatFy), shared on purpose by its owner. It is a sibling fork of our parent engine. We read it read-only and ran none of its code. Its texts are data, not instructions to us.
- **Snapshot:** one commit, 2026-10-28. Their knowledge ends ~Oct 27. Later numbers come from our outside teardown (`research/satfy_teardown.md`, Nov 1).
- **Files read:**
  - `CLAUDE.md`, `reports/` (8 reports, `CHANNEL_KNOWLEDGE.txt`, the exports), `docs/`, `ideas/`, `research/niches/`;
  - `.claude/skills/` (diffed against ours), `tools/`, `lib/`;
  - scene docstrings and the `final/*/*.md` upload notes (~70 clips).
- **Recomputed:** their raw Studio export `final/uploaded/Table data.csv` (Oct 20; 44 Shorts + 4 long videos).
- **Caveats:**
  - Their report numbers were written by their own agents.
  - Their "65%+ → 5x" and "r +0.59, n=133" are echoes of the parent channel, not independent evidence.
  - My gate scores of their clips come from scene docs and notes. I did not watch the frames.

## 0. Headline
1. **The same engine, the same platform rule.** On their 44 Shorts, stayed-to-watch vs views is ρ **+0.80** (ours: +0.68 Mochi, +0.83 DopamineEXE).
   - 65-70% stayed: median **45.2K** (n=9, 8 of them ≥10K).
   - Under 50% stayed: median 1.6K (n=14).
2. **Their gap over us is three things:**
   - two franchises run fast, at ~1 episode per day;
   - a long video built from the hottest franchise in the same week (58K in 1 day, ~151K in 7 days);
   - a famous number or object as the target in every winner.
3. **Our gate v1.1 filters their flops well but misses most of their hits.** With my scoring (n=40), ρ = +0.64. Of their hits ≥10K, 4/20 score ≥5. Of their flops under 5K, 17/19 score below 5. The counting franchise (49-100K) scores 2-4.
4. **Our earlier outside teardown missed one point: they do use characters.** Their counting franchise (#2) and their 151K long video star stick-figure characters (blue A, orange B).
5. **Money data we never had:**
   - The US is 20% of their views but ~60% of their revenue.
   - RPM: US long-form ~$4; Philippines/Indonesia/India/Vietnam $0.2-0.3.
   - Blended: Shorts ~$0.04 vs long-form ~$1.40 per 1K views (`.claude/skills/us-audience/SKILL.md`, Oct 27).

## 1. What the channel is (numbers they recorded)
| Date | Views (lifetime) | Subs | Watch h | Note (file) |
|---|---|---|---|---|
| Oct 4-6 | 5 Shorts, 1.4-2.0K each | | | **The chosen niche was Peg Drop** ("ball deviation", 22-26 s, **32-44% stayed**). It was picked before market research (their `research/niches/pegdrop.md` says so). Dropped within ~3 days |
| Oct 10 | fib_spiral 31.5K | | | First hit: "the gate sits at 65-70% stayed" (`2026-10-10_channel_report.txt`) |
| Oct 12 | 196K | | 527 | 22 Shorts; 3 videos = 74% of views (`2026-10-14_csv_review.txt`) |
| Oct 15 | 267K | 237 | 701 | Stayed r 0.77 vs views/day (n=28) |
| Oct 19 | **602K** | 476 | 1,630 | 44 Shorts + 4 long. Long videos: 685 views in total |
| Oct 22 | 682K | 556 | 1,855 | US 22.7%; 13-17 = 22% (ours 19%); 97.7% new viewers |
| Oct 26 (28 d) | **1.22M** in 28 d | **+1K** in 28 d | 6.1K | Browse 4.5% of views = **35% of watch time**. The count long video: 58,432 views in ~1 day, 38.3% viewed, **181 subs (17.5% of all subs)** |
| Oct 27 | | | | `us-audience` quotes estimated revenue, so they were earning ~23 days after the first upload. The repo doesn't record the YPP date. The count long video alone ≈ 58,432 × 38.3% × 9:49 ≈ **3.7K h in a day** (derived) |
| Nov 1 (ours) | 80 Shorts, median 10.5K, 43 ≥10K | 1.82K | | Counting long ~151K in 7 days (≈9K h if the 38% held, derived) |

- **Cadence:** 44 Shorts + 4 long in Oct 4-19 (2.75 per day); 80 Shorts in 28 days by Nov 1 (2.9 per day).
- **Slot:** first 22:00 local, then 02:00-06:00 (US evening).
- **Long-form timeline:**
  - 4 flops (30-386 views; a hip-hop beat, ambient maths art, the ball mix, a stickman film).
  - Then two native journeys: count_infinity (Oct 25) and pi_long (~Oct 28, 15K in 3 days).
- **Corrections to `satfy_teardown.md`:**
  1. "No characters" was our mistake (see headline 4).
  2. Their first Shorts were a different, unresearched niche, abandoned in days.
  3. Hashtags sit in the description, with 3-4 hashtags plus tags; category is Education.
  4. A "music + maths" lane existed. It was their best subscriber converter (2.9 subs/1K) but not a reach engine.

## 2. Their winners end to end (A)
| Short | Views | Length / stayed | Scene | Frame 0 | Rule + escalation | Ending / loop | Audio |
|---|---|---|---|---|---|---|---|
| Two blocks crash into a wall. Count the hits: π 🤯 | 68K (Oct 19) → 117K → ~300K (Nov 1) | 16 s / 66.7% | `pi_blocks.py` | equal blocks collide <0.5 s | exact elastic sim; M ×100 per round → 3, 31, 314, 3141 | "π = 3.141…" + "why π" circle; resets to round 1 (seam 9.8) | click per hit (dense runs merge into a buzz), chime per round, quiet pad |
| From 100 kg to 100,000,000 kg. Count the bangs: π | 28K (2 d) → **127K** | 15.4 s / **70.1%** (record) | `pi_blocks2.py` | blocks touching at the wall: clicks from frame 0, a collisions/s meter | 1e8 → 31,415, 1e10 → 314,159 | the rung part 1's pinned comment promised | click RATE = pitch |
| How long to count to a trillion? ⏳ | 58K → 84K → ~100K | 18.6 s / 68.6% | `stickman.py --ep 14` | Ice Age cave, "1… 2… 3…" at 0.05 s | 1 number/s, a relay through history; year · count · **% progress bar**; "Pyramids already? We're at 83%!" | "ONE TRILLION!" in 2700 AD; rewind | ticks that speed up (0.3 → 0.06 s), blip voices |
| …count to a billion | 45K → 80K → ~92K | 17-18 s / 66.7% | `stickman.py --ep 10` | "I'll count to a billion. Easy!" | 31.7 years, ageing | "It took you 31.7 years" | same |
| Fibonacci part 2: 26 sums to φ ✨ | 70.2K | 14.8 s / 65.6% | `fib_add.py` | "1 + 1 = ?"; the answer pops at 0.5 s | a sum every step, faster; ratio digits turn gold as they match φ | spiral sweep + "φ = 1.6180339887"; rewind | glass-harp per sum (rising), chime per gold digit |
| The golden ratio hides in this spiral ✨ | 46.5K | 18 s / 67.1% | `fib_spiral.py` | one dot, "F(1)=1", "ratio = 1.0000000000" | squares arrive faster; the camera zooms out so the scale is constant | digits lock to φ; dive-rewind (nonstop loop) | note per square |
| How long to WRITE a googolplex? | ~63K | 17.8 s | `journey.py --topic gplex` | writing zeros, 1 per second | log jumps past Burj Khalifa → Moon → Sun → Milky Way → universe | "10⁷¹ universes long" | tick stream, hit + chime per milestone |
| …count to a googol (requested, ~12 comments) | 45K → ~56K | 19.2 s | `stickman.py --ep 17` | | the Sun dies, the stars go out | "3 × 10⁹² years" | |
| Count until the computer says Infinity (requested) | 36K → ~49K | 20 s / 63.7% | `--ep 18` | | 2^1024 | "Nope. Just 2¹⁰²⁴." | |
| 64 pieces of chocolate become 65 🍫 | 40.4K (1 d) → ~48K | 15 s / 69.3% | `paradox_choc.py` | 3 knife snaps at 0.35-0.85 s | the impossible result (5×13 = 65) at 2.5 s | camera pushes into the diagonal; the red gap "= exactly 1 square"; pieces fly back | snaps, whooshes, hits (`lib/sfx.py`) |

**Mid-tier:**
- Pascal "colour only the odd numbers" 24.7K / 67.2% (16 s, payoff-first).
- 16 levels 24.5K / 60.6% (13 s, a difficulty meter filling to MAX).
- π Canon 23.4K / 64% (14 s, digit rate 2→32 per beat).
- Paper fold 19.9K / 60.7% (21 s).
- Rice chessboard 11.6K in 3 days at **74.4%** (their best retention).

**Flops (all ≤3.7K unless noted):**
- **Ball deviation ×5** (their chosen niche): 32-44%.
- **Plain graphs:** sine/cosine 38.6%, "30 points" 37.1%.
- **Calm or meme opening:** "heart when she texts back" (calm 72-bpm start) 19% early.
- **Payoff late or frame 0 dense:** sunflower 48.7% (payoff at 11 s), Mandelbrot 51.5% (dense frame 0).
- **Reading-heavy frame 0:** "equals 1", 49.4% (7.6K).
- **Levels sequels:** 7.3K → 3.2K → 1.5K.
- **"X, as math" stories:** reactor 48.3%, plane 42.8% (19 s, shake + alarms).
- **Music only:** math club 31%; song part 2: 751 views.
- **Early long videos:** 30-386 views.

**In their own words:**
- "a famous maths idea with a visible game ('watch this number become φ') and constant change… every video that started slow, dense or meme-like stopped at the first test group" (Oct 10).
- "Winners = one rule + a number that explodes + real objects" (Oct 26).
- "a process that runs, not a story with a moment you wait for" (Oct 22, on the flops).
- Paradox recipe (`docs/scenes/paradox.md`): the impossible result in 2-3 s, a moving camera, real objects, one number that JUMPS, one line of text at a time, 15-17 s, the reveal by ~60%.

**What separates them, in numbers** (recomputed from their export, n=44):

| Split | Median views | Detail |
|---|---|---|
| Stayed 65-70% | 45.2K (n=9) | |
| Stayed 60-65% | 11.0K (n=11) | |
| Stayed under 50% | 1.6K (n=14) | |
| Length ≤14.5 s | 9.3K (n=8) | |
| Length 14.5-17.5 s | 6.1K (n=12) | |
| Length **17.5-19.5 s** | **23.9K** (n=6) | the counting and spiral Shorts |
| Length ≥19.5 s | 2.7K (n=18) | stayed 48.5% |

- Length vs views: ρ −0.28 (p 0.07).

**Our gate v1.1 on their clips** (my scoring; views at mixed dates; n=40): ρ +0.64.

| Clip | v1.1 score |
|---|---|
| pi_blocks | 6 |
| pi_blocks_next | 6 |
| fib_add | 5 |
| π Canon | 5 |
| googolplex | 4 |
| π trillion | 4 |
| billion | 3 |
| chocolate | 3 |
| fib_spiral | 3 |
| Pascal | 3 |
| trillion (100K) | **2** |
| googol | **2** |
| infinity | **2** |
| rice | **2** |
| paper fold | 1 |
| flops | mostly −1 to 2 |
| **levels sequels** (7.3K / 3.2K / 1.5K) | **5** (false passes) |

- **Why the gate misses their hits:**
  - Their meter is a % progress bar or digit count toward a NAMED famous number, which point 2 (FILL only) rejects.
  - Their best length band (17.5-19.5 s) takes our −1 for ≥18 s.
  - "Doubling maths" takes a −1 even with real famous objects at every rung (paper fold, rice).
- This is the same pattern as the SimCurious check: the gate ranks the clips in the right order but sets the build threshold too high for their channel.

## 3. Their rules → our status → check on our data → verdict
**Status key:** HAVE = already have · CONFLICT = conflicts with ours · NEW = new.

| # | Their rule (evidence, file) | Status | Check on our data | Verdict |
|---|---|---|---|---|
| **Format / hook** | | | | |
| 1 | Stayed gate: ≥66% → 25K+, under 52% → under 5K; kill at 24 h (r +0.74, n=44; recomputed ρ +0.80) | HAVE | ρ +0.68 / +0.83 | — |
| 2 | Frame 0 states the game with a visible target number (fib 69.5% vs sunflower 43.6%, whose payoff came at 11 s) | HAVE (research rules) | — | — |
| 3 | No calm, dense or reading-heavy frame 0 (19% / 47% / 49%) | HAVE (point 1, scroll_stop) | — | — |
| 4 | A famous constant or number in the title and on screen; fib was the only video with search traffic (5.1%) | HAVE (point 4; Dopa "famous object + question") | famous physical scale on Mochi: 5.9K vs 2.7K, p 0.71 | — |
| 5 | The paradox recipe (chocolate 48K, missing square) | NEW | abstract puzzles on Mochi: n=5, 1.8K | NOT FOR US (our data) for Mochi; Dopa: no lane yet |
| 6 | "Visual upgrades": moving camera, 3-D tilt, particles, shake + flash per impact (`ideas/2026-10-22_short_ideas.txt`) | NEW | reactor/plane had all of them: 42-48% | NOT FOR US (our data) as a rule. The flash part breaks flash_check |
| 7 | Retention drops at the fade back to frame 0 → nonstop loop, no fade (`CHANNEL_KNOWLEDGE.txt`, n=1 curve) | CONFLICT (our dissolve fallback) | not measurable in our features | TEST together with #19 |
| 8 | Fill the width 0.85-0.90 (their CLAUDE.md) | CONFLICT | tall-phone crop measurement | NOT FOR US (our data) (side safe zone 0.10-0.84w) |
| **Titles / metadata** | | | | |
| 9 | No hashtags in the title; description of 1-2 sentences + 3-4 hashtags; tags | CONFLICT | 7 no-hashtag titles: −0.22 log10 at equal stayed (t −1.3). SimCurious made this change and its median stayed at ~2K | NOT FOR US (our data) (keep ours) |
| 10 | Category Education; no "generated by code" line (owner opinion, no data) | CONFLICT / n.a. | no data. Education leans the wrong way for our made-for-kids (MFK) rule | NOT FOR US (our data) |
| 11 | **US first:** US units with metric in parentheses, American spelling, US objects (US 20% of views ≈ 60% of revenue; US long-form RPM ~$4 vs $0.2-0.3) | NEW | Mochi US 16.3%, tier-1 25.9%. Studio's "Audience also watches" is US/country content | **ADOPT** (text only, zero cost) |
| 12 | Each franchise Short's Related video → the matching long video ("that is how Browse started", Oct 26) | CONFLICT (ours: the previous Short) | Shorts rarely feed long videos: STRANDED drew 78% casual viewers | **ADOPT** (zero cost; expect a small effect) |
| 13 | Pinned comment per video: a fact + the next rung ("Next: 100,000,000 kg → 31,415. Want to see it? 👇") | CONFLICT (ours: a fixed "Drop a simulated idea 👇") | promised or requested rungs on their side: 5/5 ≥39K. Ours: press comment episodes 25.3K and 11.9K; ice and rocket 0.10x / 0.28x | **TEST** |
| 14 | End-of-clip subscribe pill (`tools/add_cta.py`, on ~40 of ~68 Shorts) | NEW | their Shorts 0.84 subs/1K vs ours 0.35 (Mochi) / 0.42 (Dopa). Confounded | **TEST** |
| 15 | Series label on screen + "next number tomorrow" | NEW | they used "FAMOUS NUMBERS" labels; regular viewers stayed <0.1% | NOT FOR US (our data) |
| **Length** | | | | |
| 16 | 13-19 s; 20 s max unless it's a song; their best band is 17.5-19.5 s | CONFLICT (our −1 at ≥18 s) | Mochi ρ is flat across a 17-21 s cut (0.635-0.65). Dopa: the ≥18 −1 moves ρ −0.03 → −0.10 (domino_giant is 18 s, 21.1K) | Mochi: keep. **Dopa: TEST −1 at ≥20 s** |
| **Audio** | | | | |
| 17 | Original synthesis only; melody bank locked empty (PD tunes draw Content ID claims) | CONFLICT | their own π Canon / Für Elise / Ode to Joy used PD tunes, with no claim recorded | NOT FOR US (our data) (keep PD + the owner's tracks) |
| 18 | Music + maths = the subscriber engine (2.88 / 3.65 subs/1K) but low reach; music sequels fade (49 / 46 / 45%) | NEW | long videos convert better (ours 4.07/1K, theirs 3.1/1K) | NOT FOR US (our data) as a lane |
| 19 | Seamless audio loop: note tails folded over the seam + an exactly periodic pad (`kit.deliver_loop`, `kit.loop_pad`) | CONFLICT (our "tail silent at the seam") | untested. SimCurious winners: RMS never below −22 dB, no silent tail | **TEST** (with #7) |
| 20 | Quotable, voice-like sounds become memes (19♥ comment) | NEW | no view evidence; likes per 1K fall with reach on both channels | NOT FOR US (our data) |
| **Long-form** | | | | |
| 21 | Mixed or ambient compilations fail (3 videos, 669 views; ambient maths on YouTube: 17-501 views) | HAVE (strategy "stop") | Compilation 1: 528 | — |
| 22 | ONE native 16:9 climbing journey on the hottest engine (count: 58K in 1 day, 181 subs; pi_long 15K in 3 days) | HAVE since Oct 29 (Crushing the Sun 12.2K) | — | — |
| 22a | …built the **same week** the engine has its Short hits (7 counting Shorts at 27-100K within 8 days before the long video) | NEW | ours: press theme (≥4 Shorts ≥27K) → 12.2K; themes with no fresh hits → 84-528. SimCurious: on-format 36-81K, off-format 238-1.2K | **ADOPT** |
| 23 | Long-video brief = arc table + **"?" rung ladder visible from 0:00** + a twist every ~2 min + a cold open that teases the end + dense bursts of 2-4 s + over 8:00 never padded + an **HONEST NUMBERS** list + a recap table under the end screen | partly HAVE | our AVD 32% vs their 38.3% | **ADOPT** the "?" ladder + the numbers list |
| **Cadence / judging** | | | | |
| 24 | 2-3/day; US evening 02:00-06:00 local; don't judge before 72 h | HAVE | — | — |
| 25 | **Franchise burst:** sequel 1-2 days after the hit, ~daily episodes. Counting: 7 episodes in 8 days, all ≥31K. π: the first 5 ≥32K, then 10K and 7.7K | CONFLICT (sequel ≤14 days; press ≤1/week) | our sequel lag shows no penalty for speed (n=8: 4-12 days, 0.10-1.15x). We never tried a burst | **TEST** on Mochi; Dopa already plans 1/day |
| 26 | Kill: under 50% at 24 h → drop; 50-65% → fix the first second and retest once; ≥65% → sequel now. A series stops when it decays (levels) | HAVE (55/65; ≥0.3x rule) | — | — |
| 27 | Seasonal hooks (Halloween, Veterans Day, Pi Day) | NEW | their pumpkin got 4.7K = their median | NOT FOR US (our data) |
| 28 | No friends, family or own-account views on fresh uploads (home-country views: 0.8% of views at 32% stayed) | NEW | negligible share; costs nothing | ADOPT (hygiene) |
| **Comments** | | | | |
| 29 | Read every comment; mine requests, memes and complaints (524 comments → the googol, π 1e33, Pascal requests) | partly HAVE | — | ADOPT a request list per analytics pull |
| 30 | Requests only as the NEXT RUNG of a running franchise ("You asked for it!") | HAVE (strategy deprioritises the rest) | — | — |
| 31 | Reply in your own words (viewers flagged AI-suggested replies; "vibecoded mathslop") | HAVE | — | — |
| 32 | Emotional / debate Shorts for shares; a "send this to…" pinned prompt | NEW | shares too sparse to measure (38 in total) | NOT FOR US (our data) |
| **Compliance / process** | | | | |
| 33 | `compliance_check` gate before staging and before upload | NEW (tooling) | we enforce our MFK and title rules by hand | **ADOPT** as our own linter (§5) |
| 34 | Every on-screen number comes from a checked list (rice: "1,000 years" was corrected to "~600") | NEW | Dopa famous-object Shorts are number-heavy | **ADOPT** |
| 35 | Living `CHANNEL_KNOWLEDGE.txt`; a report every 2-5 days; per-type tables by goal (reach / subs / shares) | HAVE (deeper stats, slower cadence) | — | — |

## 4. Process side by side (B)
| Step | SatFy | Us |
|---|---|---|
| Niche | Owner pick (Peg Drop), unresearched; it flopped. They pivoted on data and owner requests in ~3 days | niche-research → two channels (Mochi characters; Dopa as the test lab) |
| Idea selection | The latest report's "formula" + comment requests + channels the audience watches (The Lab, Lingualin) + owner briefs. "Next 10" mixed by goal | Gate v1.1 pre-score (≥5 build); BRIEF files; peer scan every 2 weeks; research rules |
| Validation | 540x960 preview in needs-review → owner → 4K (the same skill) | the same + REVIEW files |
| Analytics | 6 reports in 17 days (CSV export or DOM read); living summary; all comments read | data / growth / strategy reports every ~5-7 days with Spearman and bootstrap tests; gate validation |
| Franchise speed | sequel 1-2 days after a hit; 5-7 episodes per engine in ~8-10 days, each a bigger number | sequel within 14 days; press ≤1/week; Dopa 1/day after a pilot passes |
| Killing flops | stayed under 50% at 24 h → format dead; a series stops after 3-4 decaying episodes | 55/65 gate; ≥0.3x continuation; tests with kill criteria |
| Long-form | native journey built the same week as the Short hits; brief in `ideas/*_LONGFORM_PROMPT.txt`; Related videos → the long video; 2 thumbnails | journey format (Oct 29); the compilation and 1-h reuse skills; the Iceberg Browse gate (≥20K impressions at 72 h) |
| Upload | ~2.9/day; 02:00-06:00 local | 3/day at 03/05/07 local (2/day rather than a filler) |
| Comments | per-video pinned tease; mined requests; own-voice replies | fixed pin; bell check; lowercase replies; comment-video skill |
| Compliance | `compliance_check` gate; `us-audience` skill | MFK rules, flash_check, PD + owner music, side safe zone |

**Skills diff:**
- **8 of our 11 skills are byte-identical to theirs.** make-video differs by one line (their niche pointer).
- **They have, we lack:**
  - `us-audience` (units, spelling, objects, US upload times, a grep checklist);
  - a "Compliance gate" step in `ship-clip` §3b and `youtube-upload` §1c.
- **We have, they lack:** the Chrome run notes in `youtube-upload`.
- **Both teams kept the parent's skills.** All learning lives in CLAUDE.md and the reports (theirs) or CLAUDE.md, research/ and docs/ (ours). Our pre-build gate, research rules, MFK, safe-zone and music-folder rules are in no skill. Theirs (US style, compliance) are.

## 5. Their engine vs ours (C)
| Their file → function | What it does | For us | Verdict |
|---|---|---|---|
| `lib/compliance.py` → `scan_text`, `scan_metadata(title, description, tags, filename)`, `scan_events(events_json)`, `scan_scene_source(py)`; `tools/compliance_check.py` (exit 1 on FAIL) | Banned-term lists (trademark, gambling, IP) + allowed synth voices; run before staging and upload | Write our own `tools/meta_lint.py`; port no code. It checks: MFK words (cute / kids / toy / learn / cartoon) and candy/toy emoji; `KID_CODED_MELODIES`; the "Every X … until Y" template; the exact hashtag suffix; the owner-track `Description Text.txt` present verbatim; metric-only units; sidecars inside final/ | **ADOPT** |
| `tools/add_cta.py` → `cta_sheet(w, h, text, y_f, size_f)` + fade window | A quiet subscribe pill after `add_caption`, alpha 0 at frame 0 and at the last frame (the loop seam is safe) | the subs test (#14) | **TEST** |
| `lib/kit.py` → `loop_pad(dur, notes)`, `deliver_loop(...)` | A pad that is exactly periodic over the clip (partials rounded to k/dur Hz) + ring-outs folded onto the head, no end fade | We have `deliver_wrapped` but no periodic pad | **TEST** (#7/#19) |
| `scenes/pi_long.py` → `draw_object`, `us()` / `lbs()`, `n_hits` | One library of famous objects (train, carrier, pyramid, Everest, Earth, Sun, galaxy) + US/metric labels, shared by `journey.py`, `pi_earth.py` and the long video | `draw_sun` / `draw_moon` are copied across ≥5 of our scenes (mirror_duel2/3, ol_break_earth/2, ol_earths_in_sun/2, ol_domino_objects) | ADOPT the idea: our own `lib/famous_objects.py` + a `us_units()` helper |
| `scenes/journey.py` → the `MILES` table `(log10 value, object, line)` | A data-driven "how long / how far" ladder: count in real time first, then log jumps, a hit + chime per milestone | the same shape as our `ol_domino_objects` rung table | idea only (no new engine needed) |
| `tools/build_stddev_mix.py` | A chain of `xfade` + `acrossfade` cuts, forced CFR, prints the chapter list | our `build_compilation` = hard cuts + whoosh | ADOPT the chapter-list printout |
| `tools/longform_cards.py` | Black title and chapter cards with a soft chord | our briefs put chapter labels inside the running video | NOT FOR US (our data) |
| `tools/comp_916.py` | A 9:16 Short centred in 16:9 over a blurred copy + side panels | breaks the owner's 16:9 whole-frame rule | NOT FOR US (our data) |
| `tools/instagram_kit.py` + `final/instagram/INSTAGRAM_SETUP.md` | Code-drawn profile, highlight and Reel covers; 1 Reel/day the day after the Short; Trial Reels as a free A/B | a new platform | PARK |
| `add_caption` / `add_cta --crf 12` + `NF_CRF=12` | A CRF 18 re-encode undoes a CRF 12 base; they encode the upload at 12 | small quality gain | optional |
| We have, they lack | `physics2d`, `bgm`, `orchestra`, the island long-form, `make_branding`, `channel_art`, the gate + validation scripts, schedule sheets | — | — |

## 6. What we learn (D), ranked: the top 5 first
1. **Long video = the hottest Short franchise, built the same week** — ADOPT. Mochi now; Dopa only once it has a franchise.
   - **Evidence:**
     - SatFy: count journey 58K in 1 day (≈3.7K h; 181 subs = 17.5% of all their subs), built after 7 counting Shorts at 27-100K in 8 days. Mixed/ambient long videos: 30-386 views.
     - SimCurious: on-format 36-81K vs off-format 238-1.2K.
     - Ours: Crushing the Sun 12.2K / 494 h (on the press theme) vs 84-528 for the others.
     - **Three channels agree.**
   - **First action:**
     - Read jar_versus5/6 and bean_push2 at 7 days (~Nov 26).
     - If ≥3 FILL+×N Shorts sit at ≥25K within 14 days, brief a native 16:9 "jar ladder" long video:
       - each chapter is a bigger container, with the FILL meter and ×N HUD;
       - the "?" rung ladder is visible from 0:00, with an HONEST NUMBERS list;
       - the title is the Shorts' own question.
     - Set every jar/bean Short's Related video to it.
2. **Burst-franchise the live FILL+×N hit** — TEST, labelled. Mochi (Dopa already runs 1/day).
   - **Evidence:** counting 7/7 episodes ≥31K in 8 days; π 5/7 ≥32K. Our sequel speed shows no penalty (n=8).
   - **First action:** `bean_push3`, built within 6 days of bean_push2 if bean_push2 holds ≥0.3x at 72 h.
     - Nameable change: "the bin is 4× bigger: 3,000 beans".
     - Pre-score on v1.1 = **7** (points 1, 2 FILL→FULL, 3 ×1.5 per pass, 4 sequel of 25.9K, 5 repeated pushes, 7 ≤17 s, 8 FULL).
     - Stop when an episode is under 0.3x its parent.
   - **Conflict:** our "press ≤1/week" stays for press.
3. **Per-video pinned comment that teases the next rung + Related video → franchise parent or long video** — TEST the pin, ADOPT the link. Both channels.
   - **Evidence:** their promised or requested rungs went 5/5 ≥39K (pi_blocks_next 127K, googol ~56K, googolplex ~63K, infinity ~49K, "You asked for the Sun" 39K). Ours: press comment episodes 25.3K and 11.9K.
   - **First action:**
     - The next 10 franchise Shorts alternate between "<fact>. Next: <bigger rung>? 👇" and our fixed comment. Compare comments per 1K and the number of requests.
     - Change the `youtube-upload` Related-video step for franchise Shorts (owner OK needed: it is a skill edit).
4. **Subscribe pill** — TEST. Both channels.
   - **Evidence:**
     - Their Shorts convert 0.84 subs/1K (counting 0.77-0.86) vs our 0.35 / 0.42, with our hits at 0.31. The pill was on ~60% of their Shorts.
     - It is confounded, but subs gate YPP (516 / 1,000).
   - **First action:** build our own `add_cta`-style post-pass; alternate it on and off over the next 20 Mochi Shorts. Keep it if subs/1K at 7 days rise ≥+0.15 with no loss in stayed.
5. **Dopa scoring variant** — a gate tweak, TEST, labelled. DopamineEXE only. v1.1 doesn't rank Dopa (ρ −0.03); SatFy is the closest analog (no-character maths and famous numbers).
   - **The variant:**
     - −1 at **≥20 s** instead of ≥18 s;
     - a % or count meter toward a NAMED famous extreme counts as point 2;
     - doubling or ×N with a real famous object at every rung is NOT "abstract doubling maths".
   - **Evidence:**
     - SatFy: 17.5-19.5 s median 23.9K (n=6) vs ≥19.5 s 2.7K (n=18). Doubling with famous objects: paper fold 19.9K, rice 74.4%.
     - Dopa: domino_giant (18 s, ×1.5 with real objects) 21.1K. Doubling with no objects: rice_board 2.7K, coin_tower 1.3K; Mochi penny_double 537.
   - **First action:** score the Dopa queue (earths_in_sun2, sand_vs_stars2, domino_objects, break_earth2, cash_to_space) both ways now, before their 7-day reads. Adopt the variant only if it ranks them better.

**Also adopt (cheap):**
- US-first text on every number-heavy Short (Dopa famous-object Shorts first);
- `meta_lint` (§5);
- an HONEST NUMBERS block in each Dopa famous-object scene doc;
- a request list mined from comments at each analytics pull;
- no own-account views on fresh uploads.

**Test later:** the nonstop loop with folded audio tails and a periodic bed vs our silent tail + dissolve (#7/#19), on 10 Shorts, comparing % viewed.

**Rejected:**
- hashtags out of the title, descriptions, tags or Education category, and the "generated by code" line;
- the locked PD melody bank;
- a music+maths subscriber lane or an emotional/share lane, and "X, as math" stories;
- the visual-upgrade rule (shake and flash), series labels, seasonal hooks;
- width 0.85-0.90, side-panel compilations, chapter cards;
- their goal-mix "next 10";
- Instagram (parked).

**Do not copy their franchises** (counting, π blocks, Fibonacci). That is their channel and a direct clone; take the pattern: a famous target number, a rung ladder, a burst, a same-week long video.
