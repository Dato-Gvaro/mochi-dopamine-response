# beam_clash2 — Mochi vs Bolt as a duel of POWER FORMULAS (anime-style beam clash, no IP), Mozart "Dies irae"

## Why it exists
- Owner feedback on beam_clash (2026-10-10):
  1. The orbiting ribbons around the clash ball read as "floating long noodles" once the ball got big.
  2. Nothing showed WHY one side is stronger.
- beam_clash.py stays as it is. This is a new file that reuses its look, engine and music.

## Rule: two formulas
t is story seconds since ignition (0.75 s).

| | Fighter | Formula | Shape |
|---|---|---|---|
| BURST | Mochi | `P = 8000(1 − e^(−t/2))` | 3,500 by the meet, then saturates at 8,000 |
| COMPOUND | Bolt | `P = 80 · 2^(t/2.6)` | 110 at the meet, doubles every 2.6 s, 40,000 at the final chord |

- Each formula sits on a small plate under its fighter.
- The mini-graph sits between Mochi's plate and the POWER row (378-905 x 1290-1430 px). It shows:
  - both curves on a log power axis;
  - a moving time cursor with a live dot per curve;
  - a gold ring where the curves cross.
- **Curves cross at 18.023 s.** That is the bar-61 downbeat (18.000 s), which repeats "cuncta stricte discussurus". It is flagged "CURVES CROSS!", with a timpani roll and cymbal swell into it.

## How the ball moves
- The clash point x runs from 0 at Mochi's hands to 1 at Bolt's.
- x_eq = 0.5 + 0.44 tanh((Pm − Pb)/15000), and x'' = 6(x_eq − x) − 4x'. Inertia: ω 2.4/s, damping 0.82.
- On every choir onset, whoever is AHEAD shoves: v += ±0.14·(0.4 + 0.6|tanh|). That gives a ripple ring in their colour and a shake kick.
- Shoves: Mochi 36, Bolt 14. Per 5 s: 7, 15, 14, 15.

| time | x | what happens |
|---|---|---|
| 3 s | 0.61 | Mochi's burst drives the ball at Bolt |
| 9 s | 0.75 | still pinned near Bolt (Bolt sweats) |
| 12 s | 0.69 | stalls, then drifts back |
| 15 s | 0.66 | |
| 18 s | 0.56 | the curves cross |
| 19.5 s | 0.43 | |
| 21 s | 0.29 | |
| 22.5 s | 0.12 | |
| 23.9 s | 0.05 | |
| 24.0 s | | breakthrough on the final chord |

- Aftermath (unchanged): Mochi singed, dizzy, then an annoyed stare; Bolt cheers; "BOLT WINS!".
- **Stage, beam width and hue follow log(P).** level = 0.8 + 4.2·log(P/250)/log(160).
  - Mochi reaches stage 3.7 by 2 s and stays there: coral turning part gold.
  - Bolt climbs 0.8 → 5: mint → cyan, beam 22 → 72 px.
  - Stage-up rings snap to the next note onset: Mochi 0.75, 1.5, 2.06 s; Bolt 0.75, 10.5, 15.38, 19.88 s.

## The clash ball, redesigned to scale
- **Removed:** the orbiting arc ribbons.
- **Plasma sphere:**
  - two coloured hemispheres, each sized by that side's share of the power;
  - 34 boiling plasma cells kept inside 0.15-0.72 R;
  - a turbulent surface rim, each colour only on its own half, tight at 0.93 R ± 0.1;
  - a white-hot core.
- **Crackle:** SHORT jagged spikes from the surface. Length is 22-90 px whatever the radius, and each set lives 2 frames.
- **Sparks:** 40-130 sparks flung back along both beams (60%) and sideways (40%).
- **Ripples:** a 0.4 s ripple ring on each shove.
- **Size:** radius follows log(total power), 52 → 230 px. The drawn radius is capped at 70 + 1.1 × the distance to the nearer fighter, so it never swallows a fighter.
- Fighters are drawn over the ball.

## Hook and loop
- Same as beam_clash: everything is a function of story time τ, and both rewinds run τ backwards, so the seam is exact.
- Frame 0 is story 21.12 s: x 0.27, ball r 204, power 8,000 vs 18,250, Mochi sweating, the gold crossing ring already on the graph.
- 0.5 s rewind; ignition 0.75 s; fire 1.5 s; meet 1.875 s.
- Banners sit under the caption, centred at 0.23 h, so the graph has the low zone to itself.
  - Fix 2026-10-11: they had popped in from 0.2x and read tiny at 18.05 s and 24.0 s.
  - Now 88 px logical, starting at 0.8x and overshooting to ~1.2x in 0.12 s.
  - Formula plates are 368x104 (text 38 px). The graph is 530x166 (labels 26 px, curves 6 px).
  - Both are legible at 50 % scale.
- Caption: "Burst vs Compound power" / ~"Last one pushing WINS"~.

## Music
- Same as beam_clash: Mozart, Requiem K. 626, "Dies irae" (1791, public domain).
  - Mutopia MozartWA/KV626/dies_irae; bars 1-8 + 57-64 + the bar-65 downbeat; quarter = 160.
  - Arranged with lib/orchestra.py (MuseScore_General, MIT).
- The only change: the timpani roll and cymbal swell into 12.0 s moved into the crossing at 18.0 s (bar 60 beats 3-4 → bar 61).
- Shoves fire on choir onsets. The breakthrough is on the final chord.

## Args
`--cap`, `--label`, `--still --frame N`, `--report`, `--silent`, `--mux`.

## Checks (encoded Full HD v1)
- h264 yuv420p 1080x1920 at 60 fps, 1608 frames = 26.80 s.
- -14.01 LUFS, peak -5.64 dBFS, last 0.5 s at -84.3 dBFS.
- flash_check: 0 flashes, PASS (mean lum 0.044).
- Re-checked after the banner fix; encoded frames at 18.05 s and 24.0 s read at 50 %.
- Loop seam (encoded mean delta): 1.68 (v2), against 3.2 and 4.8 for the frames on either side. The shake and sparks never stop, so this is continuous motion.
- Encoded frames read at 0, 0.25, 0.5, 1, 2, 3, 9, 13.4, 18.05 (crossing), 18.6, 20.9 (largest ball, 1:1 crop), 21, 23.5 (1:1 crop), 24.3, 25.3 and 26.5 s.
  - The ball reads as a dense plasma sphere at every size. No ribbons.

## Delivery and review
- Delivered: <VIDEOS_DIR>\batch25\beam_clash2.mp4. Owner review: pending.
- **Doubts:**
  - The log power axis on the graph is not labelled as log. The curve shapes still read: one flattens, one keeps climbing.
  - Bolt's number keeps growing after the win (55k by 25.3 s), because the formula keeps running.
  - The music was measured, not auditioned.
- Owner review (2026-10-11): 'that will do' -> APPROVED, 4K.
