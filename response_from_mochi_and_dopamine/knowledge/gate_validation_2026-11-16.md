# Gate validation: v1 vs the SimCurious-derived v2, on our own Shorts (2026-11-16)

**Verdict: keep v1, and add one of v2's ten changes: −1 for 18 s or longer.** v2 ranks our Shorts worse than v1 on Mochi (ρ +0.43 vs +0.59) and pooled (+0.31 vs +0.46). The gap is outside the bootstrap CI. Of v2's ten changes, only "−1 for ≥18 s" helps on our data. The other nine are neutral or hurt. Neither gate ranks DopamineEXE (n=24).

## Numbers first
**Spearman ρ of score vs outcome.** CIs are 95% bootstrap (2,000 resamples, stratified by channel). "Pooled" uses within-channel percentile ranks, because the channels have different baselines. On raw pooled views: v1 +0.36, v2 +0.20.

| Set | n | Outcome | v1 | v2 | v2 − v1 |
|---|---|---|---|---|---|
| Mochi & Bolt | 94 | views | **+0.59** [+0.42, +0.72] | +0.43 [+0.23, +0.60] | **−0.16** [−0.30, −0.04] |
| Mochi & Bolt | 94 | stayed | +0.54 [+0.38, +0.68] | +0.35 [+0.16, +0.52] | −0.20 [−0.31, −0.08] |
| Mochi, research era (E2+E3) | 64 | views | +0.60 [+0.38, +0.76] | +0.40 [+0.15, +0.60] | −0.20 [−0.40, −0.02] |
| DopamineEXE | 24 | views | −0.03 [−0.48, +0.43] | −0.19 [−0.56, +0.25] | −0.16 [−0.50, +0.18] |
| DopamineEXE | 24 | stayed | −0.12 [−0.56, +0.37] | −0.08 [−0.46, +0.33] | +0.04 [−0.32, +0.45] |
| Pooled | 118 | views | +0.46 [+0.31, +0.61] | +0.31 [+0.13, +0.46] | −0.16 [−0.27, −0.04] |
| Pooled | 118 | stayed | +0.42 [+0.26, +0.55] | +0.26 [+0.09, +0.42] | −0.15 [−0.26, −0.05] |

**Tiers.** The share of each tier that reached its own channel's 75th-percentile views (Mochi 3,841; DopamineEXE 2,407). The base rate is 25% by construction. Wilson 95% CIs.

| Gate | Channel | Build (≥5) | 3-4 | ≤2 |
|---|---|---|---|---|
| v1 | Mochi | **6/6** (61-100%), median 29.1K | 10/18 (56%) | 8/70 (11%) |
| v1 | Dopa | 0/0 | 4/14 (29%) | 2/10 (20%) |
| v2 | Mochi | 1/2 | 11/17 (65%) | 12/75 (16%) |
| v2 | Dopa | 1/2 | 2/12 (17%) | 3/10 (30%) |
| v2 | pooled | 2/4 (15-85%) | 13/29 (45%) | 15/85 (18%) |
| **v1.1** (v1 + "−1 for ≥18 s") | Mochi | **5/5** (57-100%) | **10/12 (83%)** | 9/77 (12%) |
| v1.1 | Dopa | 0/0 | 3/11 | 3/13 |

**False negatives: the pooled top 20 by views** (18 Mochi + ol_domino_giant + ol_sierpinski).

| Gate | Rejected (≤2) | Below build (<5) | Which top-20 Shorts it rejects |
|---|---|---|---|
| v1 | **6** | 14 | ice_cubes 40K, ol_sierpinski 20K, jenga_pull, paper_fold, rocket_stage, rain_run |
| v1.1 | 7 | 15 | the same six + comment_overflow 11.9K (20 s) |
| v2 | **9** | 19 | v1's six + sand_rise4 15K, sand_rise3 13K, comment_overflow |

- **v1:** precise but narrow. Its build tier is 6/6 hits, but it reaches only 6 of Mochi's 24 top-quartile Shorts.
- **v2:** builds only 1 of the top 20. It demotes the press hits (press_split2 356K, press_split4 242K, press_tools 31K, press_bomb 19K) from 5-6 to 4, through the ≥18 s and flat-rate −1s, and its broader points give them nothing new.

## Ablation: each v2 change alone
**Δρ vs views:**
- **fw** = v1 plus this one change, compared with v1.
- **bw** = v2 compared with v2 minus this change.
- Positive = the change helps.
- The pooled CI is for fw.

| Change | Mochi fw / bw | Dopa fw / bw | Pooled fw / bw | Pooled fw CI | Mochi stayed fw | Verdict |
|---|---|---|---|---|---|---|
| p2 meter toward a named end state (not only FILL) | −0.03 / −0.03 | −0.14 / −0.07 | −0.04 / −0.03 | [−0.09, +0.01] | −0.05 | **hurts** |
| p3 escalation = ×N, a ladder or speeding hits | −0.05 / −0.03 | 0.00 / −0.01 | −0.03 / −0.03 | [−0.08, +0.02] | −0.04 | **hurts** |
| p4 + iconic one-word end state | −0.01 / −0.01 | +0.07 / +0.04 | −0.01 / −0.01 | [−0.03, +0.01] | −0.01 | neutral (n=8) |
| p5 discrete countable actions (replaces press) | −0.05 / −0.04 | −0.12 / −0.04 | −0.05 / −0.05 | [−0.11, +0.00] | **−0.09** | **hurts most** |
| p7 9-14 s (15-17 s only with honest rungs) | −0.03 / −0.03 | +0.02 / +0.01 | −0.02 / −0.02 | [−0.05, −0.00] | −0.03 | **hurts** |
| −1 attempts only without a parameter climb | 0.00 / 0.00 | 0 / 0 | 0.00 / 0.00 | [−0.01, +0.01] | +0.01 | untestable (n=5) |
| −1 "until" only for the "Every … until" template | 0.00 / −0.01 | +0.01 / −0.01 | −0.01 / −0.01 | [−0.02, +0.01] | −0.01 | neutral |
| −1 continuous process (new) | −0.05 / −0.05 | +0.01 / +0.03 | −0.04 / −0.04 | [−0.08, +0.01] | −0.04 | **hurts** (Mochi) |
| **−1 for ≥18 s (new)** | **+0.05 / +0.08** | −0.07 / −0.06 | **+0.03 / +0.06** | [−0.01, +0.07]; bw [+0.01, +0.10] | +0.04 | **helps** (Mochi) |
| −1 flat/falling event rate or a ≥9/s wash (new) | −0.03 / −0.03 | −0.02 / −0.01 | −0.02 / −0.02 | [−0.07, +0.02] | −0.03 | **hurts** |

**v1 → v1.1 (adds "−1 for ≥18 s"):** 4,000 bootstrap resamples.

| Set | v1 → v1.1 | Δ [95% CI] | P(Δ > 0) |
|---|---|---|---|
| Mochi views | +0.59 → **+0.64** | +0.05 [+0.01, +0.10] | 0.99 |
| Mochi research era | +0.60 → +0.66 | +0.06 [−0.01, +0.13] | 0.95 |
| Mochi stayed | +0.54 → +0.59 | +0.04 [−0.01, +0.09] | 0.94 |
| Dopa views | −0.03 → −0.10 | −0.07 [−0.24, +0.12] | 0.23 |
| Pooled | +0.46 → +0.50 | +0.03 [−0.02, +0.08] | 0.91 |

## Why v2 fails here: its broadened points are table stakes on our channel
Each component alone. ρ vs views; for a −1 point, a positive ρ means it penalises the right Shorts.

| Point | v1 version: share of Shorts, ρ pooled / Mochi / Dopa | v2 version: share, ρ pooled / Mochi / Dopa |
|---|---|---|
| 2 meter | FILL 19%: **+0.33** / +0.35 / +0.28 | named end state 47%: +0.15 / +0.15 / +0.17 |
| 3 escalation | ×N 42%: **+0.32** / +0.43 / −0.07 | any escalation 74%: +0.12 / +0.15 / −0.14 |
| 4 sequel/famous | 13%: +0.27 / +0.30 / +0.16 | + iconic end 18%: +0.18 / +0.16 / +0.26 |
| 5 action | press 18%: **+0.28** / +0.33 / +0.08 | discrete 71%: **0.00** / −0.01 / +0.06 |
| 7 length | 11-17 s 35%: +0.27 / +0.43 / −0.26 | 9-14 s (+rungs) 29%: +0.21 / +0.37 / −0.24 |
| −1 ≥18 s | — | 64%: **+0.29** / +0.43 / −0.19 |
| −1 continuous | — | 19%: −0.01 / −0.04 / +0.12 |
| −1 rate | — | 75%: **−0.09** / −0.10 / −0.07 (wrong sign) |

- **Discrete hits.** 71% of our Shorts already have them, flops included. SimCurious's D-vs-C split doesn't separate our clips.
- **Continuous processes are some of our best everyday spectacles:**
  - ice_cubes 40K (a melt); sand_rise4 15K and sand_rise3 13K; rocket_stage 7.5K; rain_run 7.4K;
  - Mochi median: continuous 2.3K vs discrete 2.0K.
- **Named-end meters other than FILL don't behave like FILL** (Mochi medians):

  | Meter | Median views | n |
  |---|---|---|
  | FILL | 4.9K | 16 |
  | CLEAR | 2.5K | 15 |
  | RACE | 2.1K | 27 |
  | PCT100 | 1.9K | 6 |
  | COUNT_TARGET | 1.8K | 19 |

- **Event rate.**
  - Climbing Shorts: median 1.8K, vs 2.2K for flat or falling (Mochi).
  - Our onsets include the PD-melody note per hit and the cadence, so this measures the audio, not the visual hits. It still gives no support for the rule.
- **Iconic end.** n=8, all ≤2.9K. But they are maths visuals (Mandelbrot, galaxy, sorting wheel, golden spiral), not "hits reshape one object into a named shape". **That format is untested on our channels, not refuted.**
- **Length.** Mochi medians fall with length:

  | Length | Median views | n |
  |---|---|---|
  | ≤14 s | 9.7K | 3 |
  | 15-17 s | 3.8K | 23 |
  | 18-22 s | 2.1K | 35 |
  | 23 s+ | 1.6K | 33 |

  - "9-14 s" removes the point from our proven 15-17 s band, so it hurts.
  - "−1 for ≥18 s" adds weight to the 18 s+ bands that flop, so it helps.
  - It also holds in the research era (Δ +0.06), so it is not just the E1 era effect.

## Sensitivity: v1 > v2 on Mochi in every variant
| Variant | Mochi v1 / v2 | Dopa v1 / v2 | Pooled v1 / v2 | Top-20 rejected v1 / v2 |
|---|---|---|---|---|
| Main | 0.59 / 0.43 | −0.03 / −0.19 | 0.46 / 0.31 | 6 / 9 |
| Narrow −1s: "abstract" = the Nov 15 puzzle tags; "chain" = Dopa's "chain until it breaks" family | 0.60 / 0.43 | **+0.34 / +0.13** | 0.55 / 0.38 | 5 / 5 |
| Rate threshold "climbing" ≥1.0× or ≥1.2×; wash ≥10/s; full-length thirds | 0.59 / 0.43-0.45 | −0.03 / −0.17 to −0.19 | 0.46 / 0.30-0.32 | 6 / 8-9 |
| v2 point 7 strictly 9-14 s | 0.59 / 0.39 | −0.03 / −0.10 | 0.46 / 0.29 | 6 / 11 |
| Low-confidence codings dropped (n=97) | 0.65 / 0.45 | −0.03 / −0.19 | 0.47 / 0.27 | 7 / 9 |
| v1 ×N only with FILL | 0.54 / 0.43 | +0.13 / −0.19 | 0.44 / 0.31 | 8 / 9 |
| v1 vs v1.1, narrow −1s | 0.60 → 0.65 | 0.34 → 0.23 | 0.55 → 0.58 | 5 → 6 |

**DopamineEXE.**
- 22 of its 24 Shorts sit at 0.9-4.8K, so any ranking hinges on 2 hits: ol_domino_giant (18 s) and ol_sierpinski (16 s).
- With blind, literal reading, the coders marked 24 Shorts "abstract" and 29 "chain until it breaks" (the Nov 15 tags had 5 abstract on Mochi). That puts sierpinski (fractal, "turns to DUST") at v1 = 0.
- Read narrowly, as v1's own evidence defined them, v1 ranks Dopa at +0.34. **v1's −1 wording is too loose; that is a v1 fix, not a v2 change.**
- Dopa has no length signal (median 1.6K at 14-17 s vs 1.8K at 18-22 s). The ≥18 s −1 lowers its ρ by 0.07 (CI −0.24 to +0.12). This is untested rather than contradicted.

## Overfitting and limits
- **v1 is in-sample on Mochi.** Its points were fit on the Nov 15 tags of these same Shorts (79 of the 94), so v1's +0.59 is optimistic, and any change to v1 starts at a disadvantage. That cannot explain the component table, though: v2's new features (discrete, continuous, rate, named meter) score 0 or the wrong sign on their own.
- **v2 is out-of-sample here, as intended.** It lost. Its SimCurious in-sample gain (10/12 hits ≥5) did not transfer.
- **Small n.** Mochi has 24 top-quartile Shorts; Dopa has 6. Δρ CIs are about ±0.13 on Mochi and ±0.35 on Dopa. Every Dopa number is noise-level.
- **Our catalogue barely samples v2's target formats.** Iconic named-shape construction, the finite-count scramble and the softness ladder have n = 0-8 here. For those points, "no support" means don't pay points yet, not "it fails".
- **Blind coding by 6 coders:**
  - Agreement with the Nov 15 hand tags: ×N 96%, spectacle 94%, famous 94%, attempts 93%, press 88% (coders read "press family" literally: 16 vs 5), abstract 84%.
  - 21 of 118 codings are low-confidence (remake docs that only describe the change). Dropping them widens the v1 lead.
- **Measurement.**
  - Views are Studio lifetime at the Nov 14 08:00 UTC cutoff, at ≥7 days old.
  - Day effects (e.g. Nov 11) and slot effects are ignored.
  - Event rate is spectral-flux onsets on the mixed audio, the same method as the SimCurious teardown.

## Recommendation
1. **Keep v1.** Do not adopt v2.
2. **Adopt one v2 change: "−1 for ≥18 s".**
   - Mochi Δρ +0.05 [+0.01, +0.10]; its build tier stays 5/5 and its 3-4 tier rises to 10/12.
   - **Cost:** press_split2 and press_split4 (26 s) would have scored 4-5, and comment_overflow (20 s) 2. Under v1.1, a long press episode needs its rungs cut to ≤17 s; press_tools3 did that at 14 s.
3. **Tighten two v1 negatives to the evidence they came from:**
   - "abstract puzzle" = puzzles and algorithm demos only (Monty Hall, Hanoi, sorting/maze algorithms, penny doubling), not fractal or maths visuals built by splits;
   - "chain until it breaks" = load added step by step until a structure breaks (Dopa's family), not an everyday "which one survives" spectacle.
   - This restores Dopa ρ to +0.34 and is not a re-fit: it is the original tags' definition.
4. **Reject the other nine v2 changes for scoring.** Run SimCurious's formats (D1 snowflake press, D3 scrambled flag, M1 sword forge) as **labelled tests**, scored on v1.1 and v2.
   - All four proposed ideas are ≤13 s, so their v1 scores ("Now" 7 / 7 / 5 / 3) stand under v1.1.
5. **The real test for both gates is the next 20 Shorts,** scored on v1.1 and v2 BEFORE their 7-day read, with the rubric and scripts in `research/gate_validation_2026-11-16/`.
6. **Seen in passing, for the next re-fit (not changed now):**
   - On blind coding, v1's "method duel with no fill" (ρ −0.07), "chain" (−0.08) and "no lead change" (−0.06) −1s show no signal on Mochi.
   - v1 score 4 was 6/6 hits on Mochi (in-sample).

## Proposed replacement block for WINNING_FORMULA.md (v1.1, NOT applied)
```
## The gate (v1.1, 2026-11-16: v1 + "≥18 s" −1 + two clarified negatives; validated in research/gate_validation_2026-11-16.md)

| # | Point | Evidence |
|---|---|---|
| 1 | Frame 0 is mid-action and the mechanic fires in the first second (aim for ≥65% stayed) | stayed ρ +0.68 / +0.83 |
| 2 | A FILL meter to MAX/FULL/OVERFLOW, visible from frame 0 (NOT %, count or race readouts: they score like SCORE/CLEAR on Mochi, 1.8-2.1K vs FILL 4.9K) | FILL ρ +0.33 alone; named-end meters +0.15 |
| 3 | A ×N rule that drives the fill (each hit = ×2 / into 3 / grows 1.5×) | ×N ρ +0.32; "any escalation" +0.12 |
| 4 | A sequel of a proven hit, OR a famous object or extreme (Sun, Moon, black hole, Earth, a flag) | sequel 19.0K vs 2.5K |
| 5 | Repeated pushes or impacts, the press family (the same action again and again, each one bigger) | press ρ +0.28; "any discrete hits" 0.00 |
| 6 | An everyday question settled by a SPECTACLE (melt, flood, smash, wave), not a queue/score/path sim | 7.4K vs 2.2K. Continuous melts/floods count (ice_cubes 40K) |
| 7 | 11-17 s (≤14 s best) | Mochi medians 9.7K / 3.8K / 2.1K / 1.6K for ≤14 / 15-17 / 18-22 / 23+ s |
| 8 | A big finale or reveal you wait for | |

**Negative points (−1 each):**
- 18 s or longer (NEW; Mochi Δρ +0.05 [+0.01, +0.10]; DopamineEXE untested);
- an attempts structure;
- an abstract PUZZLE: Monty Hall, Hanoi, sorting/maze algorithms, probability or doubling maths (NOT fractals or maths visuals built by splits);
- a method duel with no fill;
- "Every X … until Y" / "until" titles;
- the chain-until-it-breaks family: load added step by step until a structure breaks (NOT an everyday "which one survives" spectacle);
- no lead change in a race that should have one;
- dead stretches over 3 s.

**Tiers:** unchanged (≥6 build first · 5 build · 3-4 filler/test, labelled · ≤2 don't build).
**Tested and NOT adopted (2026-11-16):** v2's named-end meter, broad escalation, iconic end state, discrete hits, 9-14 s, the attempts and "until" exemptions, and the continuous-process and event-rate −1s. Each was 0 or negative on our 118 Shorts. Re-test on the next 20 Shorts scored both ways.
```

## Method
- **Sample:** every Short ≥7 days old at the Studio cutoff, which is 118: Mochi & Bolt 94, DopamineEXE 24.
  - Data: `reports/exports/2026-11-15/mb_full.csv` and `dx_full.csv`. 4 rows with no clip name were matched by title to bolt_sort2, hourglass_race, paint_battle and halloween_switch2.
- **Blind features:**
  - Each Short's UPLOAD.md section and `docs/scenes/<scene>.md` were stripped of outcome/analytics/lessons sections, every line naming views/stayed/likes/subs, and every "NK" number.
  - They were shuffled into 6 bundles. Six coders who had no access to any data file coded 25 features per Short against `RUBRIC.md`.
- **Mechanical features:**
  - length = Studio seconds;
  - sequel-of-hit = a coder-named or earlier same-name sibling with ≥10K views, published before the Short;
  - "until" / "Every … until" = title regex;
  - event rate = spectral-flux onsets per third of the clip up to its last onset;
  - climbing = last third ≥1.10× the middle third; wash = ≥9 onsets/s.
- **Scoring:** both gates are summed by `score.py` from these features alone, and outcomes are joined after (`stats.py`, `sens.py`).
- **v2 as implemented:**
  - p2 = FILL/PCT100/COUNT_TARGET with the end state visible at frame 0;
  - p3 = ×N or a ladder or speed-up;
  - p4 = + iconic end;
  - p5 = discrete;
  - p7 = 9-14 s, or 15-17 s with an escalation and no dead stretch;
  - −1s per the proposal table, with the shared v1 −1s kept.
- **Files** (`research/gate_validation_2026-11-16/`): `RUBRIC.md`, `features.csv`, `onsets.csv`, `scored.csv`, `sel.csv`, and the scripts `bundle.py`, `onsets.py`, `score.py`, `stats.py` and `sens.py`.

## Per-Short table
Sorted by channel, then views. The features and scores were computed before views were joined.

**Feature codes:**
- **Meter:** the meter type; ✓ = end state visible at frame 0.
- **Flags:**
  - F0 = mid-action frame 0;
  - lad = parameter ladder;
  - spd = hits speed up;
  - seq = sequel of a ≥10K hit;
  - fam = famous object;
  - disc / cont = discrete / continuous;
  - spect = everyday spectacle;
  - fin = finale;
  - race+LC / race−LC = race with / without a lead change.
- **on/s:** onsets per second by third of the clip.

**Point lists:** the gate points earned, then the −1s.

| Short | Ch | s | Coded features (blind) | v1 points | v1 | v1.1 | v2 points | v2 | Views | Stayed |
|---|---|---|---|---|---|---|---|---|---|---|
| press_split2 | M&B | 26 | FILL✓ F0 ×N spd press disc fin duel race+LC on/s 3.2/3.8/5.8 | 1,2,3,5,8 | 5 | 4 | 1,2,3,5,8 −18s | 4 | 356,187 | 75.9 |
| press_split4 | M&B | 26 | FILL✓ F0 ×N seq press disc fin duel race+LC on/s 3.3/5.0/5.5 | 1,2,3,4,5,8 | 6 | 5 | 1,2,3,4,5,8 −18s −rate | 4 | 241,525 | 76.5 |
| ice_cubes | M&B | 14 | SCORE F0 cont spect duel race+LC on/s 6.1/5.4/6.6 | 1,6,7 −duel | 2 | 2 | 1,6,7 −duel −cont | 1 | 40,380 | 70.7 |
| sandcastle_wave | M&B | 15 | CLEAR F0 ×N lad press disc spect fin duel chain on/s 7.1/7.1/9.2 | 1,3,5,6,7,8 −duel −chain | 4 | 4 | 1,3,5,6,7,8 −duel −chain | 4 | 36,702 | 67.9 |
| press_tools | M&B | 19 | FILL✓ F0 ×N seq press disc fin duel race+LC on/s 9.8/8.8/9.6 | 1,2,3,4,5,8 | 6 | 5 | 1,2,3,4,5,8 −18s −rate | 4 | 30,583 | 79.0 |
| press_squeeze | M&B | 17 | PCT100✓ F0 ×N seq press disc fin chain on/s 9.4/10.8/11.7 | 1,3,4,5,7,8 −chain | 5 | 5 | 1,2,3,4,5,7,8 −chain −rate | 5 | 27,518 | 74.0 |
| press_bomb | M&B | 21 | FILL✓ F0 ×N spd seq press disc fin duel race+LC on/s 8.3/9.2/8.7 | 1,2,3,4,5,8 | 6 | 5 | 1,2,3,4,5,8 −18s −rate | 4 | 18,755 | 67.5 |
| sand_rise4 | M&B | 15 | FILL✓ F0 seq cont fin duel race+LC on/s 12.3/8.5/4.7 | 1,2,4,7,8 | 5 | 5 | 1,2,4,8 −cont −rate | 2 | 15,070 | 67.2 |
| sand_rise3 | M&B | 17 | FILL✓ F0 spd cont duel on/s 6.6/6.8/4.6 | 1,2,7 | 3 | 3 | 1,2,3,7 −cont −rate | 2 | 13,081 | 58.9 |
| tug_war | M&B | 15 | RACE✓ F0 ×N disc fin duel race+LC on/s 6.1/6.3/7.1 | 1,3,7,8 −duel | 3 | 3 | 1,3,5,7,8 −duel | 4 | 12,134 | 60.2 |
| comment_overflow | M&B | 20 | COUNT_TARGET✓ F0 ×N lad spd seq press disc fin abs chain on/s 7.4/8.0/8.0 | 1,3,4,5,8 −abs −chain | 3 | 2 | 1,2,3,4,5,8 −abs −chain −18s −rate | 2 | 11,897 | 77.3 |
| jenga_pull | M&B | 14 | RACE F0 disc spect fin duel chain race−LC on/s 6.4/5.0/8.7 | 1,6,7,8 −duel −chain −lead | 1 | 1 | 1,5,6,7,8 −duel −chain −lead | 2 | 9,707 | 71.4 |
| paper_fold | M&B | 25 | RACE✓ F0 ×N fam disc fin abs duel race+LC on/s 2.7/3.5/5.4 | 1,3,4,8 −abs −duel | 2 | 1 | 1,3,4,5,8 −abs −duel −18s | 2 | 9,311 | 68.5 |
| galton_split | M&B | 17 | FILL✓ F0 ×N fin abs duel race+LC on/s 10.2/9.8/8.6 | 1,2,3,7,8 −abs | 4 | 4 | 1,2,3,7,8 −abs −rate | 3 | 9,051 | 66.9 |
| snowball_fort | M&B | 15 | CLEAR✓ F0 lad spd press disc spect fin duel race+LC on/s 6.4/7.5/8.1 | 1,5,6,7,8 −duel | 4 | 4 | 1,3,5,6,7,8 −duel −rate | 4 | 8,735 | 67.8 |
| rocket_stage | M&B | 16 | RACE✓ lad cont fin duel dead race+LC on/s 7.4/8.4/8.2 | 7,8 −duel −dead | 0 | 0 | 3,8 −duel −dead −cont −rate | -2 | 7,473 | 57.8 |
| rain_run | M&B | 15 | SCORE F0 cont fin duel on/s 8.9/8.5/7.6 | 1,7,8 −duel | 2 | 2 | 1,8 −duel −cont −rate | -1 | 7,402 | 66.1 |
| cradle_showdown | M&B | 16 | RACE✓ F0 lad press disc fin duel race+LC on/s 5.0/5.8/5.2 | 1,5,7,8 −duel | 3 | 3 | 1,3,5,7,8 −duel −rate | 3 | 5,751 | 69.7 |
| glass_tower3 | M&B | 21 | FILL✓ F0 spd cont race+LC on/s 12.1/11.3/11.6 | 1,2 | 2 | 1 | 1,2,3 −cont −18s −rate | 0 | 5,078 | 65.8 |
| box_tower | M&B | 15 | FILL✓ F0 disc spect fin duel chain race+LC on/s 5.0/5.8/6.6 | 1,2,6,7,8 −chain | 4 | 4 | 1,2,5,6,8 −chain | 4 | 4,674 | 59.9 |
| foam_overflow | M&B | 18 | FILL✓ F0 ×N spd cont fin duel race+LC on/s 8.0/7.8/5.9 | 1,2,3,8 | 4 | 3 | 1,2,3,8 −cont −18s −rate | 1 | 4,424 | 54.3 |
| gossip_spread | M&B | 22 | COUNT_TARGET✓ F0 ×N fam cont fin abs duel race+LC on/s 7.3/7.2/7.2 | 1,3,4,8 −abs −duel | 2 | 1 | 1,2,3,4,8 −abs −duel −cont −18s −rate | 0 | 4,292 | 50.0 |
| cell_split | M&B | 20 | FILL✓ F0 ×N spd disc fin duel race+LC on/s 10.2/9.7/7.7 | 1,2,3,8 | 4 | 3 | 1,2,3,5,8 −18s −rate | 3 | 4,262 | 56.9 |
| halloween_switch2 | M&B | 22 | NONE F0 spd disc fin dead on/s 4.8/6.6/5.6 | 1,8 −dead | 1 | 0 | 1,3,5,8 −dead −18s −rate | 1 | 3,861 | 49.7 |
| log_gauntlet | M&B | 16 | RACE F0 lad spd fin duel race+LC on/s 10.4/10.0/8.7 | 1,7,8 −duel | 2 | 2 | 1,3,7,8 −duel −rate | 2 | 3,782 | 73.3 |
| ice_crack_race | M&B | 19 | RACE✓ F0 ×N disc spect fin duel chain race+LC on/s 9.4/9.6/7.2 | 1,3,6,8 −duel −chain | 2 | 1 | 1,3,5,6,8 −duel −chain −18s −rate | 1 | 3,749 | 71.5 |
| collapse_floors | M&B | 18 | CLEAR✓ F0 spd disc fin race+LC on/s 6.2/8.5/8.5 | 1,8 | 2 | 1 | 1,3,5,8 −18s −rate | 2 | 3,638 | 48.1 |
| toast_drop | M&B | 17 | SCORE F0 spd disc duel on/s 6.8/6.8/6.8 | 1,7 −duel | 1 | 1 | 1,3,5,7 −duel −rate | 2 | 3,490 | 68.8 |
| double_bounce3 | M&B | 24 | FILL✓ F0 ×N spd disc fin duel chain race+LC on/s 8.5/9.7/10.8 | 1,2,3,8 −chain | 3 | 2 | 1,2,3,5,8 −chain −18s −rate | 2 | 3,481 | 66.6 |
| brick_tunnel | M&B | 18 | CLEAR F0 ×N spd disc fin duel race+LC on/s 8.9/11.3/8.1 | 1,3,8 −duel | 2 | 1 | 1,3,5,8 −duel −18s −rate | 1 | 2,972 | 55.1 |
| spiral_roll2 | M&B | 22 | CLEAR F0 ×N lad press disc fin att on/s 9.3/10.5/7.9 | 1,3,5,8 −att | 3 | 2 | 1,3,5,8 −18s −rate | 2 | 2,910 | 71.3 |
| egg_drop | M&B | 15 | RACE✓ F0 ×N lad press disc fin duel chain race+LC on/s 6.6/7.3/7.6 | 1,3,5,7,8 −duel −chain | 3 | 3 | 1,3,5,7,8 −duel −chain −rate | 2 | 2,861 | 54.1 |
| card_cascade | M&B | 17 | PCT100 F0 lad spd fin duel race+LC on/s 9.3/10.2/8.3 | 1,7,8 −duel | 2 | 2 | 1,3,7,8 −duel −rate | 2 | 2,842 | 57.7 |
| hot_dog_contest | M&B | 21 | FILL✓ F0 spd disc duel race+LC on/s 6.9/7.5/6.4 | 1,2 | 2 | 1 | 1,2,3,5 −18s −rate | 2 | 2,707 | 54.6 |
| beam_clash2 | M&B | 27 | RACE✓ ×N cont fin abs duel race+LC on/s 4.4/5.4/6.3 | 3,8 −abs −duel | 0 | -1 | 3,8 −abs −duel −cont −18s | -2 | 2,703 | 38.7 |
| last_brick2 | M&B | 30 | CLEAR✓ F0 ×N disc fin on/s 9.1/10.8/9.1 | 1,3,8 | 3 | 2 | 1,3,5,8 −18s −rate | 2 | 2,528 | 55.9 |
| freefall_cargo3 | M&B | 23 | RACE✓ F0 disc fin duel race+LC on/s 3.2/2.8/3.4 | 1,8 −duel | 1 | 0 | 1,5,8 −duel −18s | 1 | 2,521 | 45.0 |
| demolition_duel | M&B | 27 | CLEAR F0 disc fin duel chain race+LC on/s 9.1/8.2/8.2 | 1,8 −duel −chain | 0 | -1 | 1,5,8 −duel −chain −18s −rate | -1 | 2,491 | 63.6 |
| grand_prix4 | M&B | 18 | CLEAR F0 disc duel race+LC on/s 7.3/6.6/5.2 | 1 −duel | 0 | -1 | 1,5 −duel −18s −rate | -1 | 2,455 | 46.0 |
| rock_avalanche | M&B | 18 | COUNT_TARGET✓ F0 ×N spd disc fin duel chain race+LC on/s 3.9/3.7/4.2 | 1,3,8 −duel −chain | 1 | 0 | 1,2,3,5,8 −duel −chain −18s | 2 | 2,433 | 55.7 |
| grand_prix | M&B | 20 | SCORE cont race+LC on/s 9.0/10.5/10.5 | - | 0 | -1 | - −cont −18s −rate | -3 | 2,412 | 48.3 |
| glass_smash3 | M&B | 17 | RACE F0 disc fin duel race+LC on/s 11.0/10.8/11.5 | 1,7,8 −duel | 2 | 2 | 1,5,8 −duel −rate | 1 | 2,388 | 51.2 |
| cannon_split | M&B | 17 | CLEAR✓ F0 ×N spd disc fin duel race+LC "until" on/s 4.6/6.2/6.0 | 1,3,7,8 −duel −until | 2 | 2 | 1,3,5,7,8 −duel −rate | 3 | 2,277 | 46.2 |
| vacuum_drop | M&B | 22 | RACE✓ F0 lad spd fin att duel dead race−LC on/s 6.5/6.6/6.8 | 1,8 −att −duel −lead −dead | -2 | -3 | 1,3,8 −duel −lead −dead −18s −rate | -2 | 2,182 | 61.4 |
| edge_slide | M&B | 17 | RACE✓ F0 lad disc fin duel race+LC on/s 6.5/7.5/7.7 | 1,7,8 −duel | 2 | 2 | 1,3,5,7,8 −duel −rate | 3 | 2,159 | 51.3 |
| coin_bridge2 | M&B | 16 | SCORE F0 disc fin duel chain on/s 10.5/10.9/10.2 | 1,7,8 −duel −chain | 1 | 1 | 1,5,8 −duel −chain −rate | 0 | 2,143 | 61.5 |
| lava_ice2 | M&B | 21 | RACE✓ F0 cont fin duel race+LC on/s 11.2/11.6/11.6 | 1,8 −duel | 1 | 0 | 1,8 −duel −cont −18s −rate | -2 | 2,142 | 59.8 |
| hanoi_64 | M&B | 23 | COUNT_TARGET✓ F0 ×N lad spd fam disc fin abs duel on/s 8.0/8.3/5.2 | 1,3,4,8 −abs −duel | 2 | 1 | 1,2,3,4,5,8 −abs −duel −18s −rate | 2 | 2,020 | 56.0 |
| checkout_queue | M&B | 17 | CLEAR F0 disc duel race+LC on/s 8.7/5.8/5.6 | 1,7 −duel | 1 | 1 | 1,5 −duel −rate | 0 | 1,967 | 53.7 |
| bowling_hook | M&B | 20 | COUNT_TARGET✓ F0 disc fin duel race+LC on/s 7.9/7.8/6.1 | 1,8 −duel | 1 | 0 | 1,2,5,8 −duel −18s −rate | 1 | 1,954 | 51.1 |
| geode_crack | M&B | 25 | PCT100 F0 lad spd press disc fin chain on/s 8.1/10.6/6.5 | 1,5,8 −chain | 2 | 1 | 1,3,5,8 −chain −18s −rate | 1 | 1,947 | 60.4 |
| mousetrap_chain | M&B | 19 | COUNT_TARGET✓ F0 ×N spd disc fin duel race+LC on/s 8.2/10.9/3.6 | 1,3,8 −duel | 2 | 1 | 1,2,3,5,8 −duel −18s −rate | 2 | 1,921 | 42.0 |
| pinball_split | M&B | 16 | COUNT_TARGET✓ F0 ×N lad spd disc duel race+LC on/s 7.6/9.7/12.6 | 1,3,7 −duel | 2 | 2 | 1,2,3,5,7 −duel −rate | 3 | 1,901 | 41.0 |
| balloon_chain | M&B | 18 | COUNT_TARGET✓ F0 ×N spd disc fin duel race+LC on/s 6.5/8.5/7.0 | 1,3,8 −duel | 2 | 1 | 1,2,3,5,8 −duel −18s −rate | 2 | 1,884 | 44.6 |
| demolition_duel2 | M&B | 14 | RACE✓ F0 disc fin duel chain race+LC on/s 6.2/5.8/7.4 | 1,7,8 −duel −chain | 1 | 1 | 1,5,7,8 −duel −chain | 2 | 1,866 | 53.4 |
| monty_hall2 | M&B | 22 | COUNT_TARGET✓ spd disc abs duel race+LC on/s 5.7/10.4/10.3 | - −abs −duel | -2 | -3 | 2,3,5 −abs −duel −18s −rate | -1 | 1,864 | 52.7 |
| coin_pusher | M&B | 19 | RACE✓ F0 disc spect fin duel race+LC on/s 9.8/9.6/9.8 | 1,6,8 −duel | 2 | 1 | 1,5,6,8 −duel −18s −rate | 1 | 1,843 | 41.6 |
| pilot_ketchup | M&B | 18 | PCT100 F0 press spect fin att on/s 5.8/5.6/6.7 | 1,5,6,8 −att | 3 | 2 | 1,6,8 −att −18s | 1 | 1,836 | 61.2 |
| block_overhang | M&B | 22 | RACE✓ F0 lad spd disc fin att abs duel race−LC on/s 5.2/7.7/8.5 | 1,8 −att −abs −duel −lead | -2 | -3 | 1,3,5,8 −att −abs −duel −lead −18s | -1 | 1,804 | 44.9 |
| snake_duel4 | M&B | 22 | COUNT_TARGET✓ spd disc abs duel race+LC "until" on/s 7.0/6.8/7.1 | - −abs −duel −until | -3 | -4 | 2,3,5 −abs −duel −18s −rate | -1 | 1,804 | 53.8 |
| neon_trails4 | M&B | 17 | RACE✓ cont abs duel race+LC on/s 6.6/6.6/5.1 | 7 −abs −duel | -1 | -1 | - −abs −duel −cont −rate | -4 | 1,799 | 66.6 |
| sort_wheel | M&B | 25 | COUNT_TARGET✓ spd cont fin abs duel icon:wheel race+LC on/s 10.0/10.7/8.3 | 8 −abs −duel | -1 | -2 | 2,3,4,8 −abs −duel −cont −18s −rate | -1 | 1,794 | 52.9 |
| core_drop | M&B | 26 | CLEAR✓ F0 lad press disc fin att chain on/s 1.7/2.3/3.1 | 1,5,8 −att −chain | 1 | 0 | 1,3,5,8 −chain −18s | 2 | 1,716 | 59.9 |
| laser_mirrors3 | M&B | 21 | COUNT_TARGET lad disc abs duel race+LC on/s 4.7/5.0/4.8 | - −abs −duel | -2 | -3 | 3,5 −abs −duel −18s −rate | -2 | 1,716 | 35.3 |
| seesaw_lava2 | M&B | 29 | RACE✓ spd disc fin race+LC on/s 9.2/10.1/8.5 | 8 | 1 | 0 | 3,5,8 −18s −rate | 1 | 1,709 | 36.3 |
| treasure_capsize | M&B | 22 | FILL✓ lad press fin duel chain on/s 2.7/2.9/6.5 | 2,5,8 −chain | 2 | 1 | 2,3,8 −chain −18s | 1 | 1,700 | 46.3 |
| birthday_room | M&B | 21 | PCT100✓ F0 spd disc fin abs "until" on/s 6.4/8.1/8.4 | 1,8 −abs −until | 0 | -1 | 1,2,3,5,8 −abs −18s −rate | 2 | 1,689 | 46.8 |
| domino_path | M&B | 18 | RACE✓ F0 disc duel race+LC on/s 11.5/11.9/10.2 | 1 −duel | 0 | -1 | 1,5 −duel −18s −rate | -1 | 1,672 | 49.7 |
| fastest_slide2 | M&B | 24 | RACE✓ cont fin duel race+LC on/s 4.6/4.2/3.6 | 8 −duel | 0 | -1 | 8 −duel −cont −18s −rate | -3 | 1,670 | 56.3 |
| pilot_one_trip | M&B | 19 | COUNT_TARGET✓ F0 disc spect fin chain on/s 8.2/8.3/8.2 | 1,6,8 −chain | 2 | 1 | 1,2,5,6,8 −chain −18s −rate | 2 | 1,666 | 58.7 |
| tesla_duel4 | M&B | 22 | RACE disc fin duel race+LC on/s 5.6/6.9/7.9 | 8 −duel | 0 | -1 | 5,8 −duel −18s | 0 | 1,648 | 46.3 |
| bridge_test3 | M&B | 28 | SCORE lad press disc fin duel chain on/s 1.7/3.1/5.7 | 5,8 −duel −chain | 0 | -1 | 3,5,8 −duel −chain −18s | 0 | 1,620 | 37.4 |
| butterfly_effect4 | M&B | 26 | NONE lad cont abs icon:arm on/s 2.4/2.5/2.5 | - −abs | -1 | -2 | 3,4 −abs −cont −18s −rate | -2 | 1,598 | 44.6 |
| mandelbrot_dive3 | M&B | 30 | COUNT_TARGET✓ cont fin abs icon:mandelbrot on/s 0.9/2.2/6.3 | 8 −abs | 0 | -1 | 2,4,8 −abs −cont −18s | 0 | 1,579 | 43.6 |
| galaxy_collision4 | M&B | 32 | NONE F0 fam cont fin icon:galaxy on/s 4.9/6.9/7.3 | 1,4,8 | 3 | 2 | 1,4,8 −cont −18s −rate | 0 | 1,574 | 51.2 |
| bolt_sort2 | M&B | 38 | FILL✓ disc fin on/s 3.3/4.5/6.3 | 2,8 | 2 | 1 | 2,5,8 −18s | 2 | 1,574 | 52.4 |
| territory_hockey2 | M&B | 22 | COUNT_TARGET✓ F0 spd disc race+LC on/s 2.9/3.7/4.5 | 1 | 1 | 0 | 1,2,3,5 −18s | 3 | 1,567 | 44.9 |
| ring_burst | M&B | 25 | CLEAR F0 lad spd disc fin dead icon:rainbow on/s 4.7/3.8/5.7 | 1,8 −dead | 1 | 0 | 1,3,4,5,8 −dead −18s | 3 | 1,545 | 45.5 |
| tube_sort3a | M&B | 26 | COUNT_TARGET✓ disc abs on/s 4.9/5.2/5.7 | - −abs | -1 | -2 | 2,5 −abs −18s | 0 | 1,541 | 37.4 |
| mirror_duel3 | M&B | 31 | COUNT_TARGET fam fin duel race+LC on/s 7.1/6.9/7.2 | 4,8 −duel | 1 | 0 | 4,8 −duel −18s −rate | -1 | 1,536 | 47.3 |
| maze_pirate | M&B | 28 | RACE✓ F0 spd disc fin race+LC on/s 3.9/5.3/6.8 | 1,8 | 2 | 1 | 1,3,5,8 −18s | 3 | 1,523 | 33.5 |
| forge_thread | M&B | 17 | COUNT_TARGET✓ F0 spd disc fin on/s 4.5/5.4/5.8 | 1,7,8 | 3 | 3 | 1,2,3,5,7,8 −rate | 5 | 1,500 | 51.1 |
| maze_algo3 | M&B | 22 | RACE✓ spd cont fin abs duel race+LC on/s 11.3/12.9/10.4 | 8 −abs −duel | -1 | -2 | 3,8 −abs −duel −cont −18s −rate | -3 | 1,485 | 52.7 |
| hourglass_race | M&B | 32 | CLEAR F0 spd cont race+LC on/s 5.1/6.4/7.8 | 1 | 1 | 0 | 1,3 −cont −18s | 0 | 1,446 | 49.6 |
| siege_duel3 | M&B | 23 | RACE F0 disc fin duel chain race+LC on/s 12.0/11.7/8.7 | 1,8 −duel −chain | 0 | -1 | 1,5,8 −duel −chain −18s −rate | -1 | 1,429 | 47.3 |
| orb_eaters2 | M&B | 20 | COUNT_TARGET F0 spd disc duel race+LC on/s 6.1/7.1/7.0 | 1 −duel | 0 | -1 | 1,3,5 −duel −18s −rate | 0 | 1,422 | 45.0 |
| ring_escape2 | M&B | 23 | CLEAR F0 disc race+LC on/s 5.3/7.4/7.3 | 1 | 1 | 0 | 1,5 −18s −rate | 0 | 1,357 | 27.8 |
| paint_battle | M&B | 32 | RACE F0 spd race+LC on/s 9.7/10.0/8.5 | 1 | 1 | 0 | 1,3 −18s −rate | 0 | 1,348 | 50.9 |
| chladni_plate4 | M&B | 25 | NONE cont fin abs on/s 1.4/3.4/4.6 | 8 −abs | 0 | -1 | 8 −abs −cont −18s | -2 | 1,342 | 48.7 |
| cannon_duel | M&B | 23 | PCT100✓ spd disc fin duel chain race+LC on/s 8.1/4.5/5.4 | 8 −duel −chain | -1 | -2 | 2,3,5,8 −duel −chain −18s | 1 | 1,301 | 40.1 |
| clones_battle3 | M&B | 38 | RACE✓ ×N spd disc race+LC on/s 7.7/8.4/7.5 | 3 | 1 | 0 | 3,5 −18s −rate | 0 | 1,262 | 46.5 |
| bolt_bubbles3 | M&B | 35 | SCORE spd disc fin on/s 6.4/8.2/8.2 | 8 | 1 | 0 | 3,5,8 −18s −rate | 1 | 1,005 | 44.0 |
| boss_fight2 | M&B | 27 | CLEAR lad spd disc fin duel race+LC on/s 4.7/5.3/4.0 | 8 −duel | 0 | -1 | 3,5,8 −duel −18s −rate | 0 | 699 | 41.9 |
| penny_double | M&B | 23 | FILL✓ F0 ×N lad disc fin abs duel race+LC on/s 7.9/10.2/4.8 | 1,2,3,8 −abs | 3 | 2 | 1,2,3,5,8 −abs −18s −rate | 2 | 537 | 79.6 |
| ol_domino_giant | Dopa | 18 | COUNT_TARGET✓ F0 ×N lad spd fam disc fin on/s 3.6/7.0/7.5 | 1,3,4,8 | 4 | 3 | 1,2,3,4,5,8 −18s −rate | 4 | 21,108 | 74.7 |
| ol_sierpinski | Dopa | 16 | COUNT_TARGET✓ ×N lad spd disc fin abs chain "until" on/s 11.4/9.2/6.8 | 3,7,8 −abs −until −chain | 0 | 0 | 2,3,5,7,8 −abs −until −chain −rate | 1 | 20,341 | 72.0 |
| ol_sierpinski_carpet | Dopa | 18 | COUNT_TARGET✓ ×N lad spd seq disc fin abs chain "until" on/s 10.0/13.4/4.3 | 3,4,8 −abs −until −chain | 0 | -1 | 2,3,4,5,8 −abs −until −chain −18s −rate | 0 | 4,773 | 63.2 |
| ol_golden_spiral | Dopa | 17 | FILL✓ F0 ×N lad disc fin abs icon:spiral "until" on/s 4.4/5.2/5.0 | 1,2,3,7,8 −abs −until | 3 | 3 | 1,2,3,4,5,7,8 −abs −rate | 5 | 2,927 | 57.7 |
| ol_rice_board | Dopa | 15 | FILL✓ F0 ×N lad spd fin abs "until" on/s 9.4/7.0/5.3 | 1,2,3,7,8 −abs −until | 3 | 3 | 1,2,3,7,8 −abs −until −rate | 2 | 2,662 | 57.7 |
| ol_wall_collapse | Dopa | 18 | PCT100✓ F0 ×N spd press disc fin chain on/s 5.6/6.1/6.9 | 1,3,5,8 −chain | 3 | 2 | 1,2,3,5,8 −chain −18s | 3 | 2,627 | 59.2 |
| ol_split_tree | Dopa | 9 | FILL✓ ×N spd disc fin "until" on/s 7.7/11.7/8.6 | 2,3,8 −until | 2 | 2 | 2,3,5,7,8 −until −rate | 3 | 2,334 | 62.1 |
| ol_marble_escape | Dopa | 15 | PCT100✓ F0 cont fin on/s 12.7/11.9/10.0 | 1,7,8 | 3 | 3 | 1,2,8 −cont −rate | 1 | 1,845 | 34.2 |
| ol_hydraulic_press | Dopa | 15 | FILL✓ F0 ×N lad spd press disc fin chain "until" on/s 4.6/6.6/7.0 | 1,2,3,5,7,8 −until −chain | 4 | 4 | 1,2,3,5,7,8 −until −chain −rate | 3 | 1,819 | 58.5 |
| ol_meteor_split | Dopa | 17 | CLEAR✓ F0 ×N spd disc fin "until" on/s 6.0/6.6/6.0 | 1,3,7,8 −until | 3 | 3 | 1,3,5,7,8 −rate | 4 | 1,780 | 49.7 |
| ol_glass_floors | Dopa | 21 | COUNT_TARGET✓ F0 ×N lad spd press disc fin chain on/s 8.6/8.4/9.0 | 1,3,5,8 −chain | 3 | 2 | 1,2,3,5,8 −chain −18s −rate | 2 | 1,769 | 54.0 |
| ol_magnet_sphere | Dopa | 10 | COUNT_TARGET✓ F0 ×N spd disc fin icon:sphere "until" on/s 3.6/5.3/6.1 | 1,3,8 −until | 2 | 2 | 1,2,3,4,5,7,8 −until | 6 | 1,639 | 49.5 |
| ol_hourglass_split | Dopa | 17 | FILL✓ F0 ×N spd press fin chain "until" on/s 12.4/11.4/7.1 | 1,2,3,5,7,8 −until −chain | 4 | 4 | 1,2,3,7,8 −until −chain −rate | 2 | 1,592 | 34.7 |
| ol_earth_drill | Dopa | 18 | RACE✓ F0 spd fam cont fin duel race+LC on/s 6.7/7.6/5.9 | 1,4,8 −duel | 2 | 1 | 1,3,4,8 −duel −cont −18s −rate | 0 | 1,501 | 54.3 |
| ol_apollonian | Dopa | 14 | PCT100✓ ×N lad spd disc fin abs on/s 8.2/6.2/8.0 | 3,7,8 −abs | 2 | 2 | 2,3,5,7,8 −abs | 4 | 1,483 | 55.0 |
| ol_crack_ice | Dopa | 11 | PCT100✓ ×N spd disc fin chain "until" on/s 10.5/9.8/9.1 | 3,7,8 −until −chain | 1 | 1 | 2,3,5,7,8 −until −chain −rate | 2 | 1,468 | 39.0 |
| ol_marble_funnel | Dopa | 18 | FILL✓ F0 ×N spd fin chain "until" on/s 11.3/11.8/11.8 | 1,2,3,8 −until −chain | 2 | 1 | 1,2,3,8 −chain −18s −rate | 1 | 1,445 | 42.1 |
| ol_spiral_center | Dopa | 17 | PCT100✓ F0 ×N spd press disc fin "until" on/s 9.5/9.5/9.9 | 1,3,5,7,8 −until | 4 | 4 | 1,2,3,5,7,8 −until −rate | 4 | 1,372 | 39.6 |
| ol_spiral_maze | Dopa | 16 | PCT100✓ F0 ×N disc fin "until" on/s 11.4/8.7/5.2 | 1,3,7,8 −until | 3 | 3 | 1,2,3,5,7,8 −until −rate | 4 | 1,364 | 36.4 |
| ol_bubble_wrap | Dopa | 16 | PCT100✓ F0 ×N spd disc fin "until" on/s 7.3/7.8/7.8 | 1,3,7,8 −until | 3 | 3 | 1,2,3,5,7,8 −until −rate | 4 | 1,320 | 39.4 |
| ol_gear_train | Dopa | 18 | COUNT_TARGET✓ F0 ×N lad spd disc fin on/s 8.5/7.4/8.2 | 1,3,8 | 3 | 2 | 1,2,3,5,8 −18s | 4 | 1,285 | 33.8 |
| ol_merge_sun | Dopa | 17 | COUNT_TARGET✓ F0 ×N lad spd fam cont fin icon:star "until" on/s 6.0/7.7/7.0 | 1,3,4,7,8 −until | 4 | 4 | 1,2,3,4,7,8 −cont −rate | 4 | 1,278 | 35.6 |
| ol_brick_breakout | Dopa | 16 | CLEAR✓ F0 ×N spd disc fin chain "until" on/s 9.1/9.5/8.4 | 1,3,7,8 −until −chain | 2 | 2 | 1,3,5,7,8 −until −chain −rate | 2 | 1,229 | 30.3 |
| ol_ring_multiply | Dopa | 15 | COUNT_TARGET✓ F0 ×N spd disc fin chain "until" on/s 8.4/7.1/7.3 | 1,3,7,8 −until −chain | 2 | 2 | 1,2,3,5,7,8 −until −chain −rate | 3 | 935 | 31.0 |
