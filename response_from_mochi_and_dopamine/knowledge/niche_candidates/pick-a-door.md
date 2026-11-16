# Niche: pick-a-door

**Status:** candidate. **Recommend REJECT (15/35, under the 22 bar).**
**One-line pitch:** our character "Knob" stands before three doors, opens one, and what's behind escalates door after door.

Owner fit (satisfying + 1-2 recurring characters): **poor.** The format runs on narrative suspense and outcome reveals, not satisfaction. Every working example is horror or kids' content.

## Hard filters
- [x] Code-renderable: technically yes, but only as flat doors with abstract outcomes. The proven versions depend on photoreal or 3D AI imagery (see the frames).
- [~] Nameable change per episode: yes ("doors are now buttons"), but the hook is the viewer's guess. The channel rule forbids a viewer-prediction caption, which strips out the format's core.
- [x] No borrowed IP.
- [~] Loop/payoff: a payoff exists; the loop is weak because a reveal doesn't reset naturally. Compilations work.
- [~] Advertiser-friendly: the horror versions (drowning, grasping hands) are borderline. The kids versions are made-for-kids.

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 3 | Real demand, but in the wrong shape. @pick-a-door-liminal (77.9k subs, started 2026-03-06, 148 shorts) has a median of 284k and a top of 991k (2026-07-20), but its newest shorts are at 10k-32k (decaying). It is Japanese AI liminal horror. @WhoopeeDoopyShorts (2.14M) gets 6.2M for "Open the Cardboard Doors!", but that is AI kids content. @PickADoorYT (151 subs) tops out at 11k. |
| Supply gap | 1 | Flooded with AI generation. A "How To Create VIRAL Pick A Door AI Shorts (in 60 seconds)" tutorial exists, and Purr-Purr, Cats Family and Katy&Co all run kids door videos this month. |
| Our edge | 1 | Code-drawn flat doors can't compete with photoreal liminal scenes. With no voice-over we lose the narration the leaders use (on-screen Japanese text over AI visuals). Determinism adds nothing to a story reveal. |
| Episode depth | 4 | Doors, buttons, paths, boxes and elevators give infinite variants, but each outcome must be hand-written, not simulated. |
| Long-form RPM | 2 | Horror and kids audiences; made-for-kids kills mid-rolls and comments. Leaders show no long-form. |
| Build cost | 2 | Needs illustrated rooms, a character walk cycle and per-door outcome vignettes. Our engine is a physics and event engine, not a scene illustrator. Several days to a first clip. |
| Policy safety | 2 | The format is a known template that templated AI channels mass-produce, the exact profile of the inauthentic-content policy. The caption rule removes "which door would YOU pick?". The kids framing brings made-for-kids/COPPA risk. |
| **Total** | **15/35** | Below 22; not worth a test clip. |

**Cannibalisation vs parent:** low, since the audience is different. That doesn't help when the format doesn't fit our engine or the owner's satisfying brief.

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @pick-a-door-liminal | 77.9k | 2026-03-06 | 991k, 763k, 646k, 608k, 599k | Japanese AI liminal horror, about 64 s, narrated text; recent 10-32k |
| @WhoopeeDoopyShorts | 2.14M | older | 9.4M, 6.8M, 6.2M (doors) | AI 3D kids cartoon, made-for-kids |
| @PickADoorYT | 151 | 2026 | 11k, 11k, 3.2k | "Would You Survive Your Door?" |

## Reference videos decoded
- `ref_pick-a-door_1` (pick-a-door-liminal, 991k, 64 s). A girl in a school uniform points at a red door (written 溺死, "drowning", with grasping hands) and a blue door. Then a corridor, hands in a flooded room, and a cistern with dolls. Japanese subtitles carry the story. It is all generative imagery. There is no mechanic, only narrative.
- `ref_pick-a-door_2` (WhoopeeDoopyShorts, 6.2M, 60 s). An AI felt-craft world: a crying blue cat, cardboard doors with helper stickers (fireman, police, builder), and a girl fixing a dollhouse. Kids' "which helper?" lesson.

## Characters (if pursued)
**Knob:** a small round body with a big door-knob nose and antenna. Drawn as a circle, an ellipse nose and a line-plus-circle antenna. It emotes with its eyes (dots → wide circles for surprise), antenna droop, and a body shake.

## 10 episode ideas (each with its nameable change)
1. Every door adds +1 ball to Knob's room; how full does it get after 10?
2. Doors become buttons that each change gravity.
3. Each door doubles the room's contents.
4. Doors on a spinning wheel.
5. Elevator floors instead of doors.
6. Every door shrinks Knob.
7. Doors that rearrange.
8. 100 doors, 1 s each.
9. Doors open onto the previous room (recursion).
10. Boxes instead of doors.

## Engine changes needed
- look: illustrated room backdrops, door art, a walk cycle (new)
- layouts: a stage layout (floor line, doors row)
- audio voice: door creak, latch (`synth_latch` exists), reveal stingers
- new lib module: `lib/character.py` plus a scene and prop library. This is the largest build of the three candidates.

## Risks
- The format is owned by AI horror and AI kids channels.
- The caption rule removes the core hook.
- Made-for-kids classification.
- Weak loop.
- The leader is already decaying (newest shorts 10-32k against a 284k median).

## Cheapest proving test clip
Not recommended. If forced: "Knob opens 10 doors, each one DOUBLES the balls in the room." This turns the reveal back into our physics mechanic, which shows the format's value was never the doors.
