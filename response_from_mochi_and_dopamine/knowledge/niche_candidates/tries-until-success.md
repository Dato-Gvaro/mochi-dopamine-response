# Niche: tries-until-success

**Status:** candidate — **AT THE BAR (22/35), second choice**
**One-line pitch:** a little ragdoll blob attempts one physical task (jump the gap, hit the button, climb the step), fails in floppy ways while an ATTEMPT counter climbs, and finally nails it — a real optimiser in the sim, not a fake montage.

## Hard filters
- [x] Code-renderable at quality — 2D verlet ragdoll + cairo; needs a hand-rolled physics layer (no physics engine in requirements.txt)
- [x] Episodes differ by a nameable change — a new TASK or a new BODY each episode
- [x] No borrowed IP — own character; the "AI learns to X" format is generic (AI Warehouse does not own it)
- [~] Short loop/payoff AND 8+ min compilation — payoff = success; loop = success pose dissolving back to attempt #1 (weaker loop than a sim). Long-form: proven by AI Warehouse (13.7M on a 520 s video)
- [x] Advertiser-friendly — slapstick falls, no gore

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 2 | Format is proven at scale: AI Warehouse (832k subs) Shorts "AI Learns to Dodge" **11.79M** (2024-07-20, 40 s, 523k likes), "Insane Way to Jump" 7.48M (2024-03-25, 49 s), "AI vs Spinner" 2.9M. But **no small channel found breaking out**: bones-dev (2.47k subs) "AI learns…" Shorts top out at 1.1k / 1.0k / 662; AI Conor long-form 651 views. Search for small "attempts"/"AI learns" Shorts at 100k+ in the last 90 days returned nothing. |
| Supply gap | 3 | Incumbents (AI Warehouse, Code Bullet, b2studios 1.7-4.0M long-forms, yoshtm 5.97M) are 3D/long-form heavy and post rarely; a 2D, crisp, satisfying, high-cadence version is open — but the incumbents set viewer expectations. |
| Our edge | 3 | Deterministic seeded optimiser = reproducible "attempt N" frames and exact counters; 4K60. But Unity ML-Agents 3D (ref frames) looks richer than a 2D cairo ragdoll, and real learning is slow to compute in pure Python. |
| Episode depth | 4 | task (jump, climb, balance, throw, swing, kick into goal, land on a platform, push a box) × body (2 legs, 4 legs, one wheel, spring) × obstacle. 50+ fine. |
| Long-form RPM | 4 | AI Warehouse long-forms 8.66M / 5.12M / 13.7M (498-851 s); tech/"AI" audience skews adult → better advertisers, low MFK risk. |
| Build cost | 2 | Need: verlet ragdoll with joint limits + ground contact, a controller parametrisation, an honest optimiser (hill-climb/GA over jump impulses/joint torques) whose attempt history is replayed, and a montage cutter (attempts 1, 2, 5, 20, 117…). First clip > 1 day. |
| Policy safety | 4 | Original. Must NOT title "AI learns" unless a real learner produced the attempts — a scripted fail-montage labelled "learning" would be a misleading claim. |
| **Total** | **22/35** | Exactly at the bar. |

**Cannibalisation vs parent:** low. Different promise (a character learning, not an abstract escalation), different audience (AI/tech curiosity skews older). Distinct look: warm daylight "test chamber" with floor tiles, NOT neon-on-black.

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @aiwarehouse | 832k | n/c (Shorts seen 2024) | 11.79M, 7.48M, 2.9M, 1.8M, 1.5M | Albert = orange cube w/ eyes; Kai = blue rival w/ angry brows; text-only commentary; only 7 Shorts — long-form is the product |
| @b2stud (b2studios) | n/c | n/c | (no Shorts tab) | "AI Invents New Bowling Techniques" 3.98M long-form |
| @CodeBullet | n/c | n/c | — | "A.I. Learns To Play HAPPY WHEELS" 3.43M (voiced — not our format) |
| @bones-dev | 2.47k | n/c | 1.1k, 1.0k, 662 | small copycat: did NOT break out |

## Reference videos decoded
- `ref_tries-until-success_1` (AI Warehouse "AI Learns to Dodge", 40 s, 11.8M): white 3D test room, orange cube (Albert) vs blue cube (Kai) throwing; top caption "AI learns to dodge" persists; "Hour 1 → 4 → 6 → 7 → 9 → 12" label is the escalation; scoreboard counter; hits shatter the cube into small cubes (satisfying burst); ends with a Subscribe pill. No voice.
- `ref_tries-until-success_2` (AI Warehouse "Insane Way to Jump", 49 s, 7.5M): ragdoll box-man must reach the green button across a gap; subtitles explain reward/punishment ("his goal is to hit this button", "punished for falling"); counters: attempt/score 0 → 2 → 64 → 172 → 533 → 1298 → 2547 → 3253; fast-forward glyph "x2250", "x8500"; payoff "After 105 days of training…" lands the jump. **Lesson: the climbing counter + fast-forward glyph is the escalation; the failure poses (faceplants) are the comedy.**

## Character proposal — "Bodge"
- **Shape:** round head (circle, cream) on a 5-capsule ragdoll (torso + 2 legs + 2 arms), thick outline, stubby limbs so falls read cute not violent.
- **Face:** same eye/brow/mouth rig as `character-survival`'s Pip (shared `lib/character.py`): determined brows before a try, "o" mouth mid-air, spiral eyes + 3 stars after a faceplant, huge grin + confetti on success.
- **Emotes:** attempt counter ticks with a "pok"; each fail = a different pitched "bonk"; success = PD-melody resolve phrase.
- Optional duo: "Nib" (orange triangle) holds the attempt counter clipboard and facepalms.

## 10 episode ideas (each with its nameable change)
1. Jump the gap — the gap widens after every success.
2. Hit the button on the high ledge.
3. Climb one stair — then the stairs get taller.
4. Balance on a see-saw.
5. Kick a ball into a goal from the far wall.
6. Bodge has ONE leg this time (pogo).
7. Ice floor — no friction.
8. Moon gravity — floaty jumps overshoot.
9. Land on a moving platform.
10. Bodge vs Nib — two learners race the same task.

## Engine changes needed
- look: new palette (light test-chamber floor tiles, cream/orange character)
- layouts: rectangular room / side-view layout (no circle arena); counter + "x1000" fast-forward glyph slot
- audio voice: `synth_pok`/`synth_squash`/`synth_slam` for impacts; counter tick; success jingle from PD MELODIES
- new lib modules: `lib/ragdoll.py` (verlet points, distance + angle constraints, ground/platform collision, fixed dt), `lib/learner.py` (seeded hill-climb/CMA-lite over controller params, logs every attempt for replay), shared `lib/character.py`

## Risks
- **No small-channel breakout evidence** — the only proof is one big incumbent; copycats (bones-dev) stalled at ~1k.
- Honest learning in pure Python may need minutes-hours of compute per episode; faking it is a policy/trust risk.
- 2D look may read as "cheap AI Warehouse".
- Loop is weak (success ≠ frame 0).
- Event rate: fails slow down as it learns — the counter must accelerate (fast-forward ×) to keep the "rate still climbing" rule.

## Cheapest proving test clip
`bodge_gap`: side view, Bodge must jump a gap to a green pad; controller = 2 params (crouch time, jump angle) hill-climbed with a fixed seed; show attempts 1, 2, 3, 7, 15, 40, 112 with fast-forward glyph between, landing at ~40 s, dissolve to attempt #1. ~2 days (ragdoll + learner are new).
