# Early breakouts: how genre channels got their first hits (2026-10-20)

Owner question: on which Shorts did @Satisfying2DSims get good views WHEN IT STARTED, what kind, so we can follow the example.

Tags: **MEASURED** = our own count from yt-dlp data or storyboard frames (method given). **INFERENCE** = my reading, not proven. No FACT-level sources were needed.

## Method and limits
- yt-dlp only. Flat Shorts lists plus per-video metadata (upload date, duration, exact views, likes):
  - Satisfying2DSims: all 332 Shorts (pulled 2026-10-19/20).
  - MusicBouncingBall (MBB), Satisfying_Shape5, visualizing-magic, satisfying.ba11s: oldest 75 each. CodeCraftedPhysics (CCP): all 258 (cached 2026-10-15).
  - Flat lists only: vibegeometry, gravitylab, BounceLab, SpinfallSim, ShapeArenaTV, ours.
- Frames: 1 fps storyboards (101x180) of 14 parent Shorts (7 early hits, 7 early flops, including a matched pair) and 2 MBB Shorts.
- "Ratio" = views / median of the 10 previous uploads on the same channel.
- **Limit 1:** today's view counts on old videos include views that accrued later, after the channel grew. The parent's newest uploads show 145-1.9K at under 1 day, the same as ours. So "early floor" numbers overstate what those videos got in week 1.
- **Limit 2:** the channels were found because they succeeded (survivor bias).
- Scratch: `<local path removed>` (parent_table.txt, mbb_table.txt, chron_*.json, frames/).

## 1. Satisfying2DSims (parent), first upload 2026-07-06 (MEASURED)

| Phase | Uploads | Days | Uploads/day | Median length | Median views | Min | Notes |
|---|---|---|---|---|---|---|---|
| A: stall | #1-31 | 0-23 | 1.3 | **58 s** | **5.2K** | 2.7K | 0 of 31 ≥ 20K. Best: #12 "The Triangle Plays WHAT?" 12.6K |
| B: step | #32-60 | 23-31 | **3.2** | **31 s** | **24K** | 5.6K | 66% ≥ 20K. First breakouts #39-40 |
| C | #61-100 | 31-44 | 2.9 | 32 s | 34K | 9K | first ≥ 100K at #79 |
| D | #101-144 | 45-62 | 2.4 | 44 s | 45K | 19K | |
| E: 1M era | #145-200 | 62-77 | 3.5 | 29 s | 55K | 22K | 4 Shorts ≥ 1M |
| F | #201-332 | 77-105 | 4.6 | 30 s | ~30K | | now fading (#251-332 median 28K) |

- **Thresholds:**
  - First ≥ 10K: #12 (day 9).
  - First ≥ 20K: #32 "The Square plays WHAT?" 26.5K (day 23).
  - First ≥ 100K: **#79** "It had to shatter every single one" 260K (day 37).
  - First ≥ 1M: **#145** "Every ball crushed splits into 3" 1.85M (day 62).
- **What changed at the step (#32, day 23):** all of it at once, so the cause can't be separated.
  - Cadence went from 1.3/day to 3.2/day.
  - Length went from 58 s to 31 s.
  - Titles went from describing the rule ("The ball grows every bounce inside a SPINNING hexagon") to stating the result ("i watched a triangle become a circle", "it hit 100% and just kept going").
  - Within phase B-C, length vs views is Spearman **+0.24**, so once the step happened, shorter did not keep winning. The -0.49 across #1-100 is the step itself.
- **Title type in phase A:** rule, statement and question titles all had 4.9-5.9K medians. Titles were not the lever.

### Early hits vs early flops (storyboards, MEASURED)

| Views | # | Title | What is on screen |
|---|---|---|---|
| **67K** | 40 | Each escaped ball spawns 3 more | 1 ball in a gap ring that cycles hue. Line 2: "**until the ring OVERFLOWS**". "Balls: N" counter. First spawn ~2 s; 139 balls by ~18 s; 7,254 spill out of the ring. 30 s |
| **7.8K** | 6 | Every escaped ball spawns 3 MORE | **Same engine and look.** No line 2, no promised end. "Balls: 1" for the first ~9 s; ~900 at the end, no overflow. 50 s |
| 9K | 98 | How many escapes before the ring can't hold it? | Same look. Spawns are additive (+3, +4, +5), so "Balls: 1" for ~18 s |
| **260K** | 79 | It had to shatter every single one | Full rainbow brick spiral at frame 0 (CCP skeleton). "It gets FASTER until it hits the CENTER". km/h readout + progress bar; core burst |
| **154K** | 92 | When the square fills, it gets bigger | A multi-hue sweep fills 44% of the frame by 2 s. "Filled: %" meter; every 100% leads to a bigger square |
| 75K | 86 | How long before the triangle overflows? | The spawn-3 rule on a triangle, "until the arena OVERFLOWS" |
| **1.85M** | 145 | Every ball crushed splits into 3 | 4 presses already closing at frame 0. "How many can it HANDLE?" with red highlights. 1 → 6,239 balls, then overflow burst. 48 s |
| 10K | 82 | Every bounce DOUBLES it | One tiny shape in an empty pentagon for ~18 s; the number is unreadable inside the shape |
| 10.6K | 48 | Every bounce inflates it until it pops | Busy from frame 0 but no focal threat; the count rises and then falls |
| 13.8K | 76 | Blade VS Balls | Pastel dots, an 8-team legend HUD, "Last colour alive wins". **Closest to our look** |

**Reading (INFERENCE from the matched pairs):** with the same engine and colours, the hit differs from the flop by:
1. a promised terminal state in caption line 2 ("until it OVERFLOWS", "until it hits the CENTER", "How many can it HANDLE?");
2. the first rule event within ~2 s, and multiplicative growth (×3), not additive;
3. a full, multi-hue frame by the climax plus a burst or overflow finale;
4. one focal threat with one counter.

The flops show dead starts (9-18 s), empty frames, busy multi-team HUDs or no end state.

### How the parent followed up hits (MEASURED, mechanic families by title keyword)

| Family | Hit | Sequels within 14 days | Sequels after 14 days |
|---|---|---|---|
| press / crush | #145 1.85M (d62) | **6, median 186K, 3/6 ≥ 250K**: hydraulic press "handle" 735K (+2 d), **"crushed one ball into 15,939 pieces" 2.74M (+5 d, the channel's biggest ever)**, drop hammer 318K (+10 d), plus 52K, 54K, 50K | 8, median 31K, 2/8 ≥ 250K ("Every crushed ball becomes 3" 396K at +19 d; "How many balls does it take to break a hydraulic press?" 331K at +27 d) |
| Pac-Man (IP) | #138 676K (d59) | 1: "ate the ENTIRE ghost swarm" **803K** (+4 d) | 4, median 22K |
| fire vs water | #183 1.13M (d71) | 0 (first sequel at +15 d) | 9, median 45K, none ≥ 250K |
| huge number | #188 486K (d73) | 3, median 46K; xylophone quintillion 918K (+9 d) | 4, median 21K |
| shape morph | #39 84K (d25) | 3, 20-34K (≈ channel median) | |
| spawn 3 | 2 flops (#6, #26) **before** the 67K hit (#40) | | |

- **Base rate** for ≥ 250K: 1% (#1-80), 6% (#81-160), 9% (#161-250), 4% (#251-332).
- **A sequel inside the 14-day window was 5-8x more likely to break out than a random upload. After the window it fell back to the base rate.**
- **What changed per sequel:** ONE nameable thing (press → drop hammer → 7 presses → lift; "splits into 3" → "into 15,939 pieces"; the count framing). The skeleton stayed the same: 1 ball, a machine already moving, an exponential count, overflow.
- The winning mechanic was often a retry. Spawn-3 flopped twice (7.8K, 7.3K) before 67K. The melody family took 16 tries before 918K. The huge-number family took 5 tries before 486K.

## 2. Other channels: early phase (MEASURED)

| Channel (start) | Era floor (first 20, median) | First ≥ 100K | First ≥ 1M | What changed right before | Follow-up |
|---|---|---|---|---|---|
| **MusicBouncingBall (2026-01)** | 5.4K | #76 (day 91) | #76 2.59M | #1-57: ONE format, "The ball has to escape in under 1 minute", ~60 s, 1/day, median **4.6K**. #58-64: rotated 4 new mechanics and cut length to 30-47 s, median **16K**. #65: "Will the balls get to center?" (CCP rainbow spiral + "Did you recognise the sounds?") 71K | Repeated that exact title 10x at 10-37K (median 18K) until #77 2.5M. Then 6 identical-title franchises in rotation. Floor #78-96: 38K; #97-140: **240K**. "Will the Ball Multiply?" went 73K → 330K, 3.1M, 4.3M, 1.3M in 5 consecutive episodes. The old flop format ("escape in under 1 minute", 57 uploads at ~4K) hit **1.0M** at #117 |
| vibegeometry (2025) | 15K | #11 | none | Switched from "bounce shrinks border" rules to "Every Exit Spawns Two Balls" | Same title: 747K (#11), 801K (#17). Then "Part 2" 34K, triangle 110K, and later reruns 12-14K. **No floor lift** (#12-30 median 20K vs 15K before). Faded to ~1-2K in 2026 |
| CodeCraftedPhysics (2023-11) | 36K | #4 | #13 (day 9) | Nov-2023 genre gold rush ("every bounce it gets bigger" rule titles, 59 s) | Clusters: #24-29 had 4 videos ≥ 1.6M in 7 days |
| Satisfying_Shape5 (2024-03) | 66K | #1 | #15 (day 20) 34M | Copyrighted-melody recognition ("What sound was that?") | 2024 era; we can't copy (music rule) |
| satisfying.ba11s (2023-11) | 118K | #1 | #7 (day 4) | Same melody wave; "Reminds me of something" 38M at #34 | Same title reused 5+ times at 5-13M |
| visualizing-magic (2024-08) | 78K | #1 | #24 (day 69) | Went from sporadic (11 uploads in 64 days) to 7-14/week; 1M+ at #24, #27, #30 within 5 days | 2024 era |

**Negative controls, autumn 2026 starters (flat lists, MEASURED):**
- gravitylab: since 2026-08-24, 50 Shorts, median **1.4K**, max 13K. "Which side fills first?" races, monochrome.
- BounceLab: since 10-09, 34 Shorts, median 1.2K.
- SpinfallSim: 12 Shorts, median 1.1K.
- ShapeArenaTV: 28 Shorts, ~1.2K, rules written as long sentences.
- **Ours: 40 public Shorts, median 1.3K, p90 2.2K, one 83K (press_split2, #32).** We are the only autumn-2026 starter found with a breakout.
- **INFERENCE:** ~1.2-1.4K is the 2026 seed-test floor for new genre channels, not a defect of our channel. The earlier-era 5K-100K floors are not achievable benchmarks.

## 3. What the early winners did (cross-channel, INFERENCE from the above)
1. **The first hit came from a mechanic switch, and the next ones came from repeating it.**
   - Parent: spawn ×3 + overflow, then the CCP spiral, then the press.
   - MBB: the CCP spiral after 57 uploads of one format.
   - vibegeometry: "Every Exit Spawns Two Balls".
   - The breakout skeletons recur: **exponential multiplication to an overflow** (parent 67K / 1.85M / 2.74M, vibegeometry 747K / 801K, MBB "Will the Ball Multiply?" 14M) and **a rainbow brick spiral eaten to the centre** (parent 260K, MBB 2.5M, CCP 26.8M).
2. **Sequels of a hit right away.** Parent: 14-day window, 50% of sequels ≥ 250K vs 6-9% base. MBB: consecutive episodes 3.1M / 4.3M / 1.3M. Each sequel changed one nameable thing; MBB even kept the title identical.
3. **One hit lifts the floor for everything.** Parent 5.2K → 24K. MBB 18K → 38K → 240K, and its old flop format later hit 1.0M. vibegeometry is the exception (no lift, faded): it reran one title without adding new formats.
4. **Cadence 3+/day during the climb** (parent). MBB broke out at ~4/week, so cadence is not required. It raises the number of lottery tickets inside the sequel window.
5. **Looks of the winners:** abstract shapes on black, one focal threat, one counter, a caption whose line 2 is the stake or terminal state, the first event ≤ 2 s, full multi-hue frame at the climax, an overflow or burst finale, a rewind loop to frame 0. Flops: dead starts, empty frames, multi-team legends, pastel colours.

## 4. Playbook for us (INFERENCE; the owner decides)
**Situation:** press_split2 (83K, 77.6% stayed) went live on Oct 16, so today (Oct 20) is day 4 of the ~14-day sequel window. press_split3 (splits into 4) and press_split4 (heavier hammer) are built. The owner rated press_split episodes as duplicates and set "at most ONE story episode, a week or more apart".

**Conflict, flagged in one line:** the parent's best evidence says the window is days 0-14 and the 2nd-3rd sequels were its biggest videos (2.74M at +5 d). The owner's one-episode-after-a-week rule spends most of that window unused.

Next week (Oct 21-27), if the owner agrees:
1. **Ship 2-3 press sequels by ~Oct 30, each with ONE nameable change:**
   - press_split4 (the rematch with a heavier hammer) first;
   - then one that changes the machine or material, like the parent's "drop hammer" (318K) and "15,939 pieces" (2.74M): e.g. a saw vs a laser, glass vs steel balls, or a "how many can it HANDLE" count framing.
   - Keep the skeleton: one ball, both machines moving at frame 0, ×3 per crush, two rival counters, overflow finale, Für Elise note per crush.
   - This is not a re-skin as long as the change is nameable (CLAUDE.md rule 2). Skip press_split3 (×4) if it reads as a duplicate: "×4 instead of ×3" is the weakest nameable change.
2. **Fill the other slots with transfers of the same skeleton to new mechanics**, the owner's "unique" preference:
   - "every escape spawns 3 until the ring OVERFLOWS" (parent 67K / 75K, vibegeometry 747K);
   - a rainbow brick spiral eaten to the centre, "it gets FASTER until it hits the CENTER" (parent 260K, MBB 2.5M);
   - a fill → grows % meter (parent 154K).
   - Each needs: a stake line 2 with the end state, the first event ≤ 2 s, ×N growth (never +N), one focal threat.
3. **Cadence: keep 3/day** (the parent's climb rate) for the next 14 days, so the window holds ~40 tickets.
4. **Expect most of them at 1-3K.** The parent's family sequels outside a hit's window ran 20-55K on a 5x bigger floor, so 1-3K is normal for us. Judge on the 14-day block, not per clip.
5. **Don't change titles as a lever.** Title type was flat in every early phase measured. Keep "<rule> + <A> or <B>?".
6. **Retry near-misses.** The parent's spawn-3 needed 3 tries and melody needed 16. A format that got 1-3K once is not dead (beam_clash2 and collapse_floors are candidates for one nameable-change retry).
7. **Re-measure ~Oct 31.** Check whether the floor lifted (parent ×4.7, MBB ×2). If our post-hit median is still ~1.3K, the hit was one ticket, not a channel lift, and the volume-on-skeleton plan continues.

## Rules (keep)
- After a breakout, ship 2-3 one-change sequels inside 14 days; after 14 days, sequels revert to the base rate.
- Caption line 2 states the terminal state ("until it OVERFLOWS" / "How many can it HANDLE?").
- First rule event ≤ 2 s; multiplicative growth; no dead starts (matched pairs: 7.8K vs 67K, 9K vs 75K).
- One focal threat and one counter; no multi-team legends.
- Judge a format on ≥ 10 uploads. Winners were often the 3rd-16th attempt of the same mechanic.
