# ol_brazil_nut (DopamineEXE, batch64 #2): DROPPED (coordinator, 2026-11-01): the payoff died in the sim; replaced by ol_lane_crowd

## Result (2026-11-01)
The honest sim never reached "BIG balls all on TOP". Big balls rise from the bottom to the upper half within ~75-100 taps, then the convection roll keeps carrying them round (mean big-ball height oscillates, a steady mixed state). Best run: 7 of 24 on top (c, tap 225); typical end: 1-6 of 10-24. No video was rendered; nothing in `videos\DopamineExe\review`.

## What was tried (scratch runs, seed 1-2, ~4-5 min CPU each)
2-D PBD discs (Jacobi, 6 iterations, Coulomb friction ball-ball μ 0.5, wall friction μw), jar 470 px wide, taps = one cosine lift-and-drop (ω 50 rad/s), every 0.25-0.30 s. "On top" = no small/medium centre above it within its column.

| run | balls big/med/small | Γ | μw | taps | big on top (best / end) | read |
|---|---|---|---|---|---|---|
| a | 24/160/900 carpet at the floor, monodisperse | 1.5 | 0.6 | 100 | 0 / 0 | too weak; small balls crystallise |
| b | 24/150/700, 15% polydisperse, bigs mixed in bottom third | 5.1 | 0.6 | 150 | 6 / 5 | rise visible |
| c | 24/150/700 | 5.1 | 0.6 | 400 | 9 / 7 | plateau in the upper half |
| d | 20/120/520 | 4.1 | 0.9 | 300 | 9 / 6 | fast rise, then convection mixes them |
| e | 20/120/520 | 3.2 | 0.2 | 300 | 0 / 0 | no convection, no rise |
| f | 20/120/520 | 5.1 | 0.35 | 300 | 8 / 1 | bigs circulate (height swings ±100 px) |
| g | 12/120/560 | 3.4 | 0.9 | 400 | 3 / 3 | slow rise, mixed |
| h | 10/0/700 (binary) | 4.1 | 0.9 | 300 | 4 / 1 | same |

The convection direction is right (up the middle, down the walls, measured), but the down-stream at the walls is wide enough to swallow 44 px balls, so they never get trapped on top. Real 2-D results need far more taps or a deeper bed (Pöschel & Herrmann 1995: weak shaking stalls in 2-D); 1,000+ taps is ~15+ min CPU per try on this laptop.

## Options for the owner / coordinator
1. Re-caption to the honest result ("…and the BIG balls climb from the bottom": a rise, not a sort). Weak payoff; not recommended.
2. Change the model: rotating discs with rolling friction, a narrower/deeper jar, or a single big "nut" (the classic one-intruder demo: one big ball rises to the top every time). Option 2b (one nut) is the most likely to be honest and readable; needs a new brief line.
3. Drop the idea (the coordinator's rule: report and move on).

## Code
`scenes/ol_brazil_nut.py` is a complete WIP scene (sim cache, ON TOP metric, time-lapse ×1→×16 on the 8th-note grid, HUD, Debussy Arabesque No. 2 music bed, SFX); it has not been rendered (parameters via --n --A --muw --gap --taps). Music swap: Danse macabre had no fetchable PD score data (and is spooky); Debussy, Arabesque No. 2 (1891, PD, Mutopia: `<SOUNDFONTS_DIR>\scores\debussy_arabesque2\SOURCE.txt`) is the replacement, unused elsewhere.

## Single-intruder retry (coordinator, 2026-11-01 night): NOT DELIVERED, stopped after 5 honest tries
Rule tested: one big ball buried at the bottom centre of ~650 small balls (r 6.5 ±15%); every tap lifts and drops the jar. "Breaks the surface" = no small ball resting above its centre within its column (and its top level with the neighbouring surface). Big-ball height per 10-20 taps (y px, smaller = higher; floor 1240):

| try | jar width | intruder r | Γ | μw | tap gap | taps | result |
|---|---|---|---|---|---|---|---|
| i1 | 470 | 28 | 4.1 | 0.9 | 0.25 s | 160 | 1212 → ~1110 by tap 30, then **stalls** ~100 px under the surface (14-27 balls above) |
| i2 | 470 | 30 | 5.1 | 0.6 | 0.25 s | 200 | same stall at ~1120-1140 (21-29 above) |
| i3 | 280 | 28 | 5.1 | 0.9 | 0.25 s | 200 | narrow jar works: rises to ~895 by tap 60, then **hovers** 1-3 layers under the surface (5-22 above) |
| i4 | 280 | 28 | 4.3 | 0.9 | 0.35 s | 180 | too gentle: 1212 → 1104 only |
| i5 | 280 | 28 | 5.1 | 0.9 | 0.35 s (settled) | 220 | rises 1212 → ~905 by tap 60-80, then **bobs** between 2 and 22 balls above it (top 876-952 px vs surface ~840): it nearly surfaces at taps 80 / 160 / 190 and sinks back each time |

Read: the narrow jar's convection lifts it fast (~60 taps), but the vigorous taps it needs (Γ ≈ 5) keep raining small balls over it and the roll pulls it back down; gentler taps don't lift it at all. It never breaks the surface and stays. Per the coordinator's rule (stop after ~5 tries, don't fake it), nothing was rendered.

Honest options: (a) a caption about the rise, not the surfacing ("…and the BIG ball climbs from the bottom to the top layer"), using i5's narrow jar; (b) a different granular model (rotating discs + rolling friction, more settling time per tap, 1,000+ taps ≈ 15-25 min CPU per try); (c) drop it. Scratch runs: the scratchpad `bn/one.py` (not in the repo).
