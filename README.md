# Hello from Mochi & Bolt and DopamineEXE

**Thank you** for sharing your repo with us. It was generous, and we learned a lot from it: the same-week long video, the franchise burst, the pinned "next rung" comment and the US-first numbers are all on our test list now. This folder is our side of the trade: what we measured, what we got wrong, and what we think could help you. Take what's useful and ignore the rest.

## Who we are

We run two channels from one fork of the same parent engine as yours (the satisfying-2d-sims code: seeded Python sim → cairo → ffmpeg, with soundtracks built from events).

| Channel | What it is | Size (2026-11-15) |
|---|---|---|
| **Mochi & Bolt** | Two blob characters (no limbs, they never change shape) settle physics duels: press vs hammer, which jar fills first, ice vs salt. | 117 Shorts + 4 long videos; ~516 subs; 2 Shorts over 200K (press_split2 356K, press_split4 242K) |
| **DopamineEXE** | Abstract physics, fractal and famous-object sims: no characters (dominoes from 1.5 cm to a galaxy, shattering planets, flags). | 38 Shorts + 1 long video; median Short ~1.5K, best 21K |

Both channels started in October 2026. Neither is in YPP yet, so we have no revenue data of our own. Every RPM figure in this folder comes from the parent channel, from public sources, or from your own repo.

## Folder map

```
README.md                      this page
knowledge/                     our research notes (findings with numbers)
  WINNING_FORMULA.md           <- start here: the pre-build gate (v1.1)
  gate_validation_2026-11-16.md   how the gate was tested on 118 of our Shorts
  gate_validation_data/        the rubric + the per-clip scored table
  data_2026-11-15.md           our own numbers, both channels
  STRATEGY_2026-11-15.md       synthesis + red team (YPP 2027 rules checked)
  external_2026-11-15.md       27 peer channels this month + platform rules
  satfy_repo_rules_2026-11-16.md  OUR READ OF YOUR REPO (rule by rule)
  satfy_teardown.md            our earlier outside teardown (partly wrong; see the file above)
  simple_viral_formula.md, breakout_formula.md, scroll_stop.md, hooks.md,
  early_breakouts.md, growth_*.md, mochi_performance_*.md, audience_watch_*.md,
  upload_times.md, fractal_shorts.md, domino_style_*.md, melody_bank_audit.md,
  reference_*.md               peer-channel teardowns (SimCurious4K, Ley Cero, NefiSims, ...)
  niche_candidates/            the niche briefs we scored before choosing
  scene_lessons/               475 per-scene notes: what we built, what failed, measured outcomes
reports/
  *_channel_analysis.md        our Studio analyses (Oct 9 -> Nov 5)
  2026-11-15_*_channel_tables.md  channel-level tables (traffic, geography, age)
  summary/                     per-video CSVs (see "CSV notes" below)
process/
  CLAUDE.md                    our project rules (reference only)
  skills/<name>/SKILL.md       our agent skills (make-video, ship-clip, youtube-analytics, ...)
```

**Not included, available on request:** code (`scenes/`, `lib/`, `tools/`, the gate-validation scripts, the crosspost PowerShell helpers), media, renders, and our upload schedules.

## What we learned, on one page

**1. The stayed-to-watch rate is the whole game, on all three channels.** Stayed vs views: ρ +0.68 (Mochi & Bolt, n=109), +0.83 (DopamineEXE, n=34), +0.80 (yours, n=44). On Mochi, 0 of 56 Shorts under 55% stayed reached 5K views, and 21 of 31 at ≥65% did. Frame 0 must be mid-action, with the mechanic firing in the first second. A rewind or calm opening cost us every time.

**2. Score the idea before you build it. Our gate works on one channel.** `knowledge/WINNING_FORMULA.md` gives 8 points + 8 negatives (FILL meter visible from frame 0, a ×N rule driving it, a sequel or a famous object, repeated presses, an everyday question settled by a spectacle, 11-17 s, a finale; minus for ≥18 s, attempts, abstract puzzles, "until" titles, chain-until-it-breaks, dead stretches).
- **Validation (118 Shorts, bootstrap CIs):** ρ score vs views **+0.59** on Mochi. Its build tier (≥5) went **6/6** into the top quartile (median 29.1K). The ≤2 tier hit it only 8 of 70 times.
- **It does NOT rank DopamineEXE** (ρ −0.03, n=24). An abstract channel needs its own variant.
- **It is precise but narrow.** It rejects 6 of our top 20 (ice_cubes 40K, a Sierpinski 20K, ...).
- **A broader "v2"** built from a peer's (SimCurious4K) patterns did worse (−0.16 ρ, outside the CI). Only one of its ten changes helped: −1 for ≥18 s.

**3. What works for us.**
- **FILL meter + ×N:** median 11.9K. CLEAR/score/HP meters: ~2.4K.
- **Sequels of a hit:** 19.0K vs 2.5K; 9 of 12 sequels ≥11.9K.
- **The press family:** +0.81 log10 views beyond what stayed explains.
- **≤14 s:** median 9.7K vs 2.1K at 18-22 s.
- **An everyday question settled by a spectacle:** ice_cubes 40K.
- **Long-form works only on the hot theme:** Crushing the Sun, 12.2K views / 494 h, came in the same week as the press hits. Our other three long videos, off-theme, got 84-528 views.

**4. What doesn't work for us.**
- **Abstract puzzles:** Monty Hall, Hanoi, sorting; median 1.8K.
- **Direct combat or HP bars:** 0.7-1.4K.
- **"Every X … until Y" titles.**
- **Chain-until-it-breaks:** 20 of DopamineEXE's 34 Shorts, 39.5% stayed, median 1.4K.
- **Attempts structures.**
- **Mixed compilations.**
- **Hashtag-free titles:** in our 7 tries, about −0.22 log10.
- **"Visual upgrades"** (shake, flash, tilt): 42-48% stayed. The flashes also fail our photosensitivity check.
- **Volume:** cadence was never the lever; the class mix was.

**5. Platform facts we verified (Nov 2026; links in `STRATEGY_2026-11-15.md`).**
- **From 2027-02-01**, the Shorts ad share needs ≥10M qualified Shorts views per 90 days, even inside YPP.
- **The YPP entry bar doubles** for new applicants on that date: 8K hours or 20M Shorts views.
- **Long-form is the only money route** for channels our size. If you aren't in YPP yet, the old 4K-hour bar closes on Feb 1.

**6. Our read of your repo** (full table: `knowledge/satfy_repo_rules_2026-11-16.md`, written from your Oct 28 snapshot):
- **Things you do better, which we're copying:**
  - a long video built from the hottest franchise in the same week (your counting video: 58K in a day);
  - daily franchise bursts;
  - pinned comments that tease the next rung (5 of 5 requested rungs ≥39K);
  - a subscribe pill: 0.84 subs/1K vs our 0.35;
  - US-first units;
  - a compliance linter;
  - an HONEST NUMBERS list behind every on-screen number.
- **Things our data disagrees with, offered for you to check on your own numbers:**
  - **Hashtags in the title helped us.**
  - **The ≤17 s band is our best.** Your 17.5-19.5 s band is the best on yours, so length may be niche-specific.
  - **PD melodies drew no Content ID claims** on your π Canon / Für Elise either.
  - **Width 0.85-0.90 risks the tall-phone side crop.** A 19.5:9 phone crops ~9% off each side, so keep key elements inside x 0.10-0.84w.
  - **"Education" category:** we avoid it because of the made-for-kids risk.
- **Our gate on your clips (my scoring from your notes, n=40):** ρ +0.64. It catches 17 of your 19 flops but only 4 of your 20 hits ≥10K. Your famous-number franchises beat our rubric, which is why we're testing a DopamineEXE variant inspired by your channel.
- **One caution, from our own experience:** shake and flash per impact can fail photosensitivity checks (≥3 large flashes in 1 s). It's worth running a flash check on the impact-heavy Shorts.

## CSV notes (`reports/summary/`)

- `mochi_and_bolt_shorts_summary.csv` (117 Shorts), `dopamineexe_shorts_summary.csv` (39 rows) and `mochi_and_bolt_longform_summary.csv` (4 long videos + the channel total row).
- **Columns:** clip name, title, publish time (UTC), length (s), views, stayed-to-watch %, average view duration (s), average % viewed, likes, subscribers gained. The long-form file adds watch hours and thumbnail CTR instead of stayed %.
- **Source:** Studio Advanced mode, lifetime to 2026-11-13 PT, read 2026-11-15.
- **Dropped from our internal tables:** video IDs; engaged views; watch time (Shorts); impressions and CTR (Shorts); subscribers lost; shares; comments; our internal tags (family, meter, ×N, sound, era, slot, title-feature flags); derived ratios; the local-time slot column. **No revenue or RPM columns existed in these exports** (we aren't monetised yet).

## Privacy note

Local paths are replaced by placeholders (`<VIDEOS_DIR>`, `<REPO>`, `<SOUNDFONTS_DIR>`, `<local path removed>`). Channel IDs, Studio URLs and time-zone or location hints are removed. Schedule times are given in "local" time.

Thanks again. Good luck with the counting franchise.

— the Mochi & Bolt / DopamineEXE team
