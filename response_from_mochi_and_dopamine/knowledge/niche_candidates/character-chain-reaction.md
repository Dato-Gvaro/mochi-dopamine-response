# Niche: character-chain-reaction

**Status:** candidate
**One-line pitch:** BOLT taps one marble; it rolls into a domino line, which tips a
seesaw, which drops 10 marbles, which… — the cascade multiplies to hundreds of
events while Bolt (and Mochi at the finish) react to each stage.

Researched 2026-10-03.

## Hard filters
- [x] Code-renderable at quality — marble runs, ramps, seesaws, buckets, bells
      = circles + static/kinematic segments (`lib/physics2d.py` covers circles +
      static segments). True falling DOMINOES need rotating rigid boxes — not in
      physics2d; script them kinematically (deterministic topple timing) or add a
      box body.
- [x] Episodes differ by a nameable change — ONE new contraption per episode
      ("this time a spinning wheel"). Strongest axis of the three candidates.
- [x] No borrowed IP — comps that add characters use Peppa / Mario / Minecraft
      (Domino effect simulation Dude, InproViz 4D). We use our own cast only.
- [x] Short payoff (the last stage + character reaction) AND long-form (a
      cascade compilation is classic background viewing). Loop: the final stage
      resets the board (marbles drain to the start) — honest rewind or reset.
- [x] Advertiser-friendly.

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 4 | Several small channels with 100k+ Shorts in the last 90 days: **3Ds Marble Show** (6.02k subs, first Short **2026-08-26**) "green OR red?" **12.7M** (2026-08-29), median 43k; **3D Bili** (12.5k) "Ultimate Marble Collapse — 18,686 objects chain reaction" **5.68M** (Apr 2026), median 114k; **Dino_3DCG** (5.71k, started 2026-06-01) soft-body 7.4M / 3.6M / 869k (Sep 2026); **Adwait & Dominoes** (8.23k) "1→100 Dominoes" 2.55M (Mar 2026, real dominoes). -1: NONE of them has a recurring character — the character angle is unproven here. |
| Supply gap | 3 | The lane is crowded with 3D Blender sims (3D Bili, 3Ds Marble Show, Dino_3DCG, InproViz 4D 31.8k, CG BOX 3D 10k, RossRenders 78k median 274k). The gap is narrow: 2D + a named character + a cascade that GROWS by one contraption per episode. Nobody found doing that. |
| Our edge | 3 | Plus: exact event counting, one note per hit (marble-run music), deterministic multi-stage ladders, perfect resets, character reactions synced to stages. Minus: flat 2D cairo marbles look cheaper than glossy 3D renders that dominate the views (frames of ref_chain-reaction_1). |
| Episode depth | 5 | Every contraption is a nameable change: seesaw, funnel, spinning wheel, elevator bucket, bell row, trampoline, splitter (1→2), portal, magnet, pendulum, Plinko, spiral, staircase, conveyor… 50+ is easy, and the cascade can be cumulative ("the machine gets one part longer every episode"). |
| Long-form RPM | 3 | Chain-reaction compilations are watchable background; comps' long-form is thin though: 3D Bili 36-min 7.2k, 9-min 1.6k; RossRenders "Top Satisfying Domino Animations of 2025" (3 min) 69k. Parent prior: long-form RPM $1.79. |
| Build cost | 3 | Marble-run stages: ≤1 day with physics2d + toon. Dominoes, seesaws and wheels need rotating bodies or kinematic scripting (new code, ~1-2 days for a reusable `contraptions.py`). Camera must pan/scroll along a long machine in 9:16 — new. |
| Policy safety | 4 | Clearly original if each episode adds a contraption; human-reviewed. Minus: close to the parent channel's satisfying-sim format. |
| **Total** | **25/35** | Above the 22 bar. |

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| 3Ds Marble Show | 6.02k | 2026-08-26 (44 Shorts) | 12.7M, 505k, 211k, 129k, 126k | 3D marbles, "green OR red?" two-colour race framing, 17-21 s |
| 3D Bili | 12.5k | 2024-02 (124 Shorts) | 5.6M, 2.7M, 956k, 621k, 496k | Blender rigid-body collapses, weight labels (0.1 KG→100 KG) as escalation |
| Dino_3DCG | 5.71k | 2026-06-01 | 7.4M, 3.6M, 868k, 768k, 629k | "0% vs 100% softness" red vs green — two-colour rivalry |
| Adwait & Dominoes | 8.23k | (274 Shorts) | 3.7M, 2.55M, 415k, 412k | real dominoes, colour-gradient lines, 12 s |
| RossRenders | 78.1k | — | 161M, 851k, 713k, 640k | 3D domino art; one long-form "Top Satisfying Domino Animations of 2025" 69k |
| Ball Simulations Shorts | 1.88k | 2025-10-18 | 1.0M, 705k, 46k, 43k | 2D on black, emoji "characters" rolling down a spiral — closest to a character + sim |

## Reference videos decoded
- `ref_chain-reaction_1` (3D Bili, zlA3mAYUW_8, 27 s): a DNA-helix tower of rainbow marbles on a stand; a steel ball rolls in; label climbs 0.1 KG → 1 KG → 100 KG (the escalation is the WEIGHT LABEL); at 100 KG the stand fails and ~18k marbles pour into a pile; ending = giant mirror ball fills frame. No character, no caption beyond the weight text. Audio: marble clatter.
- `ref_chain-reaction_2` (Adwait & Dominoes, VlRaC8_hYs8, 12 s): real dominoes, colour-blocked lines; one line tips the next; camera pulls back to reveal the full nested pattern. Payoff = reveal of the whole layout.
- `ref_fill-up_1` (Ball Simulations Shorts, bkNfVXhCHiY, 24 s): emoji balls run a neon spiral on black; they queue near the centre; ending dissolves into particle burst. Shows faces on balls in a 2D sim get 705k from a 1.88k-sub channel — but it is the PARENT's look.

## The characters
- **BOLT** (mint rounded-square, sprout, calm) = the engineer: flips the start
  lever, watches the cascade, eyes TRACK the leading marble (`look` param),
  winces at near-misses, cheers on the final stage.
- **MOCHI** (coral round blob, greedy) = the payoff: the cascade ends in
  Mochi's mouth / Mochi's bell / Mochi's cake. Gives the finish an emotion.
- Both from `lib/toon.py` (cairo bezier bodies, param eyes/mouth/brows,
  squash-stretch). Small (≈0.12w) so the machine owns the frame.

## 10 episode ideas (each with its nameable change)
1. **The first machine**: lever → marble → 5 ramps → bell. "Bolt pulls one lever."
2. **Splitter**: every marble that hits the splitter becomes TWO. "Every splitter doubles them."
3. **Seesaw**: 10 marbles lift a seesaw that launches the next stage. "It takes 10 to tip it."
4. **Spinning wheel**: a water-wheel turns only when its buckets fill. "The wheel needs 20 marbles to turn."
5. **Domino wave**: 200 kinematic dominoes, each hit plays the next note of a PD melody. "Every domino is a note."
6. **Elevator bucket**: marbles ride a bucket up to restart the run — the machine loops itself. "The machine refills itself."
7. **Plinko finale**: 100 marbles through pegs into Mochi's bowl. "How many reach Mochi?"
8. **Cumulative build**: episode N = machine N-1 + one new part (series spine). "One part longer every episode."
9. **Bolt vs Mochi machines**: two mirrored machines race (versus bar). "Whose machine finishes first?"
10. **Gravity flip mid-run**: halfway through, gravity reverses and the machine runs upward. "Halfway, gravity flips."

## Engine changes needed
- look: `lib/toon.py` pastel toybox; contraption parts in wood/plastic tones with ink outline (same sticker style).
- layouts: tall machines need a vertical scrolling camera (9:16) or a fit-to-frame zoom-out reveal; 16:9 = whole machine visible.
- audio voice: marble-run knock per hit (synth_pok / plink), splitters raise pitch (ScaleWalker), PD melody on domino runs, bell at payoff; silence at loop seam.
- new lib module: `lib/contraptions.py` — seesaw, wheel, bucket elevator, splitter, funnel, kinematic domino line (topple timing from a closed-form chain speed, deterministic). Optional box-body support in physics2d.

## Risks
- **Cannibalisation vs parent (satisfying 2D physics, neon on black)**: high mechanical overlap (balls + collisions + escalation). Separation: pastel toybox look, named recurring cast with reactions, machine-building spine instead of arena rules. Never reuse the parent's arena/neon look here.
- **3D quality gap**: the views in this lane go to glossy 3D renders; flat 2D may underperform. Test it.
- **Character may be decoration**: if viewers come for the cascade, the character adds nothing and the channel is just "another sim channel". The test clip must check whether the reaction beats are what people comment on.
- Dominoes need rotating bodies — don't fake physics badly; script honestly or build it.

## Cheapest proving test clip
Idea 2 "Splitter": Bolt pulls a lever, 1 marble rolls through 6 splitters
(1→64 marbles), each split a higher note, all 64 pour into Mochi's bowl, Mochi
chomps, board resets (marbles drain back to the start = loop). 25-30 s,
circles + static segments only — buildable with existing `physics2d` +
`toon` in ≤1 day. Caption: "Every splitter DOUBLES them / How many reach Mochi?".
