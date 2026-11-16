# Niche: character-survival

**Status:** candidate — **LEADER (28/35)**
**One-line pitch:** one cute recurring blob ("Pip") inside a crisp 2D physics arena while the hazard escalates — more balls, faster saws, rising water — "How long can PIP survive?", timer + hit sounds climbing to the last frame.

## Hard filters
- [x] Code-renderable at quality — it IS the parent engine (2D sims, cairo, events→sound) plus a drawn face
- [x] Episodes differ by a nameable change — each episode = a new hazard or a new rule ("this time the floor is lava", "the saws chase him")
- [x] No borrowed IP — our own character (competitors' weak spot: Pikachu / Steve / Ronaldo faces)
- [x] Short loop/payoff AND 8+ min compilation — survive-until-overwhelmed → rewind/dissolve to frame 0; compilations = "Pip vs 20 hazards"
- [x] Advertiser-friendly — cartoon peril, no gore: Pip "poofs" into stars, never bleeds

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 4 | DariaFX (4.55k subs, first Short **2026-09-03**, 41 Shorts): "What happens at 100% softness?" **5.65M** (2026-09-24, 13 s), 667k, 486k; its CHARACTER episodes ("Pikachu edition") 546k / 486k / 357k / 282k — a character inside a satisfying physics test breaks out from zero. Dino_3DCG (5.71k, first Short 2026-06-01): 869k, 629k, 393k. FootMazeLabs (7.26k): "RONALDO & HAALAND… Can they survive?" 830k. Not a 5: no small channel found doing an ORIGINAL character at 100k+ — the breakouts borrow faces. |
| Supply gap | 4 | The lane is filled by (a) faceless 3D Blender softbody clones (NextGen3D 3.67k subs: dozens of near-identical "0% vs 100%" titles, 0.6k-69k) and (b) IP-borrowing character sims (Pikachu, Steve, footballers' faces — demonetisation/claim risk for them). An owned, recurring, expressive 2D character in a crisp 4K60 sim is not visibly taken. |
| Our edge | 4 | Parent engine already ships escalating 2D sims with per-event sound, seed search to calibrate a survival time, deterministic 4K60, and 0→10k-sub know-how (parent evidence, prior). Character reacts to the sim procedurally (pupils track nearest hazard, sweat at distance < k) — cheap for us, laborious for keyframe animators. |
| Episode depth | 5 | hazard (balls, saws, lasers, water, lava, spikes, meteors, bees, magnets, crushers) × arena (circle, box, spinning, shrinking) × rule (hazard count doubles / speeds up / chases / splits). 50+ distinct, each sayable aloud. |
| Long-form RPM | 3 | Satisfying sim compilations watch as background (parent prior: long-form RPM $1.79, 90% of revenue). Competitors' long-form is weak (DariaFX "Steve" long videos 3.1k / 218 views) → unproven, not disproven. Cute character skews young → MFK risk to manage (see Risks). |
| Build cost | 4 | `scenes/_template.py` already is "dot in circle, accelerating events, dissolve loop". Add `lib/character.py` (circle body + squash-stretch ellipse, 2 eyes, pupils, brows, mouth bezier — all `Canvas` circle/poly/line primitives) and a dodge steering rule. First test clip ≤ 1 day. |
| Policy safety | 4 | Each episode has a named hazard/rule. Risk: "Pip vs 10 balls → Pip vs 20 balls" is a re-skin — count bumps must be framed as records within one episode, never as the episode's change. |
| **Total** | **28/35** | |

**Cannibalisation vs parent (neon-on-black 2D sims):** real but containable — same "satisfying sim" viewer pool. Distinct by (1) a named face the viewer roots for (survival stakes, not abstract balls), (2) a different look: warm pastel/paper backgrounds, outlined flat shapes, NOT neon-on-black glow, (3) titles about Pip ("Can PIP survive the saws?"), never the parent's "ball escapes circle" phrasing. Don't reuse parent mechanics 1:1 with a face glued on.

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| @darya8124 (DariaFX) | 4.55k | 2026-09-03 | 5.65M, 667k, 546k, 486k, 357k | Blender softbody, 11-13 s, "0% SOFT → 66% SOFT" big label; Pikachu reacts (crying/smiling sprite swaps) — character = IP |
| @Dino_3DCG | 5.71k | 2026-06-01 | 869k, 629k, 393k, 268k | "0% vs 100% Softness" faceless spheres, 24-25 s; no videos tab |
| @FootMazeLabs | 7.26k | n/c | 830k, 88k, 33k | "Can they survive?" maze + trap button; real footballers' faces (likeness IP), HELP/comment/like buttons on screen |
| @Digital3DPixel | 91.9k | n/c | 2.1M ("Ball Trapped in a Perfect Loop", 7 s), 586k | faceless Blender physics |
| @NextGenAnimation3D | 3.67k | n/c | 976k (one), rest 0.6-69k | templated clone titles — what NOT to become |
| @gravitylab-e6h | 62 | n/c | 10k, 5.3k | 2D ball sims (our parent's lane) without character — flat |

## Reference videos decoded
- `ref_character-survival_2` (DariaFX Pikachu, 9.5 s, nDF179VsJYg): hammer on a spring-arm smashes a ball through a ring on a wood stump; label steps 0% → 30% → 66% SOFT; Pikachu sprite sits on the arm and swaps expression per outcome (smile → stretched scream with tears → wide-eyed grin → crying). Escalation = softness label; ending = character's reaction (no loop). **Lesson: the face's reaction IS the payoff — it turns a physics test into a story in 1 frame.**
- `ref_character-survival_1` (FootMazeLabs, 21 s, 830k): top-down maze, face tiles move, a red button triggers a cloud-fight; "HELP" + comment/like buttons drawn on screen at the end (engagement bait). Mechanic = who reaches/escapes; IP faces are the hook.

## Character proposal — "Pip"
- **Shape:** a marshmallow-white rounded blob (circle radius r, drawn as an ellipse with squash-stretch along velocity: sx = 1+k·|v|, sy = 1/sx), 3-4 px dark outline, soft drop shadow ellipse beneath.
- **Face (cairo):** two tall oval eyes (white + dark pupil `circle`), pupils offset toward the nearest hazard (clamped), brows = short `line`s whose angle maps to fear; mouth = quadratic bezier via `poly` points (smile → flat → "o" → gritted zigzag). Blink every 2-4 s (seeded).
- **Emotes, all procedural from sim state:** distance-to-nearest-hazard → fear 0..1 (brows up, mouth "o", sweat-drop teardrop); near-miss event → eye-widen + tiny hop + "whew" pitch blip; hit → squash flat + star particles + dizzy spiral eyes 0.4 s; final overwhelm → "poof" into confetti stars (not death imagery).
- **Optional duo (episode variant):** "Nib", a small orange triangle who causes the hazard (presses the button, pours the balls) — absorbs the silent-duo idea.

## 10 episode ideas (each with its nameable change)
1. Pip vs bouncing balls — one more ball every time a ball hits the wall.
2. Pip vs saws — saw speed doubles every 5 s.
3. Pip vs rising water — Pip must hop on floating crates as the tank fills.
4. Pip vs lasers — beams sweep, one more beam each pass.
5. Pip vs the shrinking circle — arena radius shrinks per hit.
6. Pip vs meteors — the sky darkens with each impact.
7. Pip vs the spinning arena — the arena spins faster, hazards fling outward.
8. Pip vs magnets — Pip swallowed a bolt; magnets pull harder each lap.
9. Pip vs splitters — every ball that hits Pip splits in two.
10. Pip AND Nib — Nib keeps adding hazards; Pip keeps dodging (duo episode).

## Engine changes needed
- look: new `studio.PALETTE` (warm pastel bg, outlined flat shapes, no glow); paper-grain bg optional
- layouts: keep circle arena; add box/tank arena variant for water/meteor episodes
- audio voice: per-event SFX already exist (`synth_bounce`, `synth_pok`, `synth_squash`, `synth_slam`, `synth_splash`, `synth_zap`); add Pip's non-verbal blips (short pitched sine chirps: "eep" on near-miss, falling "wahh" on hit — synthesized SFX, not voice); PD melody bed via MelodyWalker for timer seconds
- new lib module: `lib/character.py` — `draw_pip(canvas, x, y, r, vel, look_at, fear, state)` + state machine (idle/fear/hit/poof); dodge steering (repulsion from hazards + wall avoidance) in the scene's simulate()

## Risks
- **MFK**: cute blob + cartoon peril can be judged child-directed. Mitigate: no nursery music, no kid keywords/titles, satisfying/"how long" framing, set "not made for kids" honestly — and accept YouTube may still classify.
- Re-skin trap: count/speed bumps are not episodes (see Policy).
- Dodge AI must look clever but lose: seed-search survival time 30-50 s so the clip ends while the hit rate climbs.
- Cannibalisation vs parent (see above).
- Unverified long-form: nobody in this exact lane shows long-form traction yet — the compilation is a bet backed only by parent priors.

## Cheapest proving test clip
`pip_balls`: 9:16, circle arena, Pip dodges; every wall bounce spawns one more ball (the parent's proven escalation), timer counter "PIP SURVIVED 0:00", hits = squash + "eep"; seed-searched so Pip is overwhelmed at ~45 s while bounce rate is still climbing → poof → dissolve to frame 0. Caption: "Every bounce adds a BALL / How long can PIP survive?". ~1 day: `lib/character.py` + a copy of `_template.py`.
