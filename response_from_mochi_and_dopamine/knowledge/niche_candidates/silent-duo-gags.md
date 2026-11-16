# Niche: silent-duo-gags

**Status:** candidate — **NOT RECOMMENDED (18/35, under the 22 bar)**
**One-line pitch:** two simple blob characters, one silent slapstick gag per Short (Lamput / Simon's Cat / Larva style).

> Owner clarification (2026-10-03): the channel must be SATISFYING content.
> Pure gag comedy is not satisfying content — its payoff is a joke, not a
> clean physical process. Scored as briefed, then noted what a satisfying
> version would be (it collapses into `character-survival`).

## Hard filters
- [x] Code-renderable at quality — technically yes (flat 2D shapes), but slapstick lives on hand-timed acting (anticipation, takes, holds); procedural tweening reads stiff
- [x] Episodes differ by a nameable change — every gag is a new premise ("the umbrella", "the piranha")
- [x] No borrowed IP — if our own characters
- [~] Short loop/payoff AND 8+ min compilation — payoff yes; a seamless LOOP is hard for a punchline (ends on a reaction, not on frame 0). Compilations: proven (Lamput marathons)
- [x] Advertiser-friendly — but see MFK risk below

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 3 | Big: Lamput (890k subs) Shorts 3.63M (2026-07-27, 14 s) and 1.66M (2026-06-15). Small: JDsof (154 subs, first Short 2026-06-08, 77 Shorts) best = "Piranha Trap" 46.7k (2026-09-29, 5 s), "Birthday Flex" 33.5k — **no small original-character channel found at 100k+**. The Little Tramp (1.3k subs) 198k/110k/101k — but it borrows Chaplin, not an original duo. |
| Supply gap | 2 | Crowded by studios with decades of IP: Lamput, Oddbods (11.9M subs), Simon's Cat (6.6M; Shorts only 89-202k), Pencilmation, Larva, Cartoon Box (34-37M-view compilations); plus a flood of AI-cartoon channels (search results full of "AI 3D cartoon" uploads at <100 views). |
| Our edge | 1 | Gag comedy rewards acting and timing, which a hand animator does better and faster than a code rig. Determinism/4K60/precision buy nothing a viewer laughs at. |
| Episode depth | 4 | Premises are effectively unlimited and each is nameable — but every one must be WRITTEN and ACTED; no generator makes them. |
| Long-form RPM | 2 | Compilations clearly work (Lamput "Lazy Sunday" marathon 1.1M, 74 min; "Task Failed Successfully" 262k, 85 min) — but silent cartoon slapstick is kid-coded: Lamput Shorts show comments DISABLED (comment_count NA) = Made-for-Kids. MFK kills comments + personalised ads → low RPM. |
| Build cost | 2 | Needs a rig (limbs, squash, eye/mouth poses), a keyframe/tween timeline, props/backgrounds per gag. First clip > 1 day; every later clip is hand-authored (no seed/rule reuse). |
| Policy safety | 4 | Original authored gags are clearly not re-skins. Risk only if gags become templated ("X falls in water" ×50). |
| **Total** | **18/35** | Under 22 → not worth a test clip as briefed. |

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @Lamput_Official | 890k | studio IP (n/c) | 3.63M, 1.66M, 175k, 140k | orange blob vs 2 doctors, silent, 14 s; MFK (comments off); 30-130 min marathons |
| @SimonsCat | 6.59M | 2008-era IP | 202k, 132k, 119k, 114k | even a huge silent brand gets ~100-200k per Short |
| @JDsof | 154 | 2026-06-08 | 46.7k, 33.5k, 6.1k, 3.3k | stick-figure silent traps, 5-9 s, one-word quoted titles, "WAIT FOR END" text; no long-form |
| @the.littletramp | 1.32k | n/c | 198k, 110k, 101k, 94k | Chaplin-styled 3D slapstick (borrowed persona, likely gen-AI) |
| @Oddbods | 11.9M | studio IP | 494k, 107k, 99k | Shorts now mostly crafts; MFK lane |

## Reference videos decoded
- `ref_silent-duo-gags_1` (Lamput "Still Not Seeing It", 14 s, 3.6M): two grey doctors grab orange blob → blob steals the glasses → doctor dizzy (spiral eyes), chases. Mechanic = one prop swap; escalation = 3 beats; ending = chase off-frame (NOT a loop); text none; expressions carry it (spiral eyes, gritted teeth, squint). Pastel-pink blurred bg.
- `ref_silent-duo-gags_2` (JDsof "Piranha Trap", 5 s, 46.7k): thief stickman reaches into piranha water for a bucket, fisherman watches → explosion cloud of piranhas on the thief, fisherman laughs. Text "WAIT FOR END" in red. Clip-art background. Payoff = karma; no loop.

## 10 episode ideas (each with its nameable change)
1. The umbrella — only one umbrella, rain follows whoever doesn't have it.
2. The last cookie — jar on a shelf, each tries a taller stack.
3. The trampoline — one bounces, the other keeps moving it.
4. The magnet — one wears a metal hat.
5. The see-saw — the big one sits down.
6. The balloon — inflating, both stare.
7. Gravity flips — the room turns upside down mid-gag.
8. The mirror — the reflection stops copying.
9. The door — push vs pull war.
10. The domino line — one sets up, the other sneezes.

## What a SATISFYING version would look like
The duo as two characters INSIDE a crisp physics process: one (builder) stacks / sets up a domino run / fills a jar; the other (chaos) triggers the cascade; sound per collision, counter on pieces toppled, rate climbing. That is the `character-survival` engine with a second character — i.e. the gag survives only as a 1-2 s cold open + reaction. Recommend folding this idea INTO `character-survival` as the "duo episode" variant rather than running it as its own niche.

## Engine changes needed
- look: pastel flat backgrounds (non-parent), thick outlines — new palette
- layouts: stage/floor layout (no circle arena)
- audio voice: cartoon foley (synth_pok/squash/slam/bounce exist) + PD melody bed; new "boing", "whoosh", "gulp" stingers
- new lib module: `lib/character.py` rig (body, eyes w/ pupils, brows, mouth bezier, limbs), `lib/tween.py` keyframes/easing timeline — the expensive part

## Risks
- Made-for-Kids designation (Lamput evidence) → comments off, low RPM, no personalised ads.
- Not "satisfying" — misses the owner's channel definition.
- Every episode hand-written: the factory's leverage (rules + seeds) is lost.
- Loop rule conflicts with punchline endings.
- Cannibalisation vs parent: none (different audience) — but also no transfer of the parent's know-how.

## Cheapest proving test clip
Don't build. If the owner overrides: a 12 s "last cookie" gag, two blobs, one prop, rewind-loop to frame 0 — ~1.5 days including the rig.
