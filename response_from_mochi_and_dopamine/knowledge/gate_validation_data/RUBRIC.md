# Feature-extraction rubric (blind coding of shipped Shorts)

You code what each shipped Short SHOWS, from its sanitised scene doc + UPLOAD.md section. You never see, look up or guess
its views/retention. Code the SHIPPED version (docs often list v1, v2, v3: use the last approved/shipped one; the
length given in the CLIP header is the uploaded length). If a fact is not stated, infer from the timeline / story /
pinned comment; if still unknown, use your best reading and set confidence "low".

Output ONE JSON object per clip, one per line (JSONL), keys exactly as below, values 0/1 unless stated.

| key | meaning |
|---|---|
| clip | the clip name from the `### CLIP:` header |
| f0_mid | 1 = frame 0 already shows the mechanic in motion (mid-action), not a static setup, empty arena, title card, intro, or a rewind/payoff jump-cut; AND the first mechanic event (hit / split / drop / pour / fire / push) lands at ≤ 1.0 s. Otherwise 0 |
| f0_first_event_s | number (seconds) if stated or derivable, else null |
| meter_type | the MAIN on-screen progress readout, one of: `FILL` (a level / pile / count rising toward a marked MAX / FULL / OVERFLOW line or a brim), `PCT100` (a % or fraction readout heading to 100 % / complete), `COUNT_TARGET` (a count toward a stated finite target: "N of 64", "back" to the original picture, sides → circle, reach a named number), `CLEAR` (something counting DOWN to zero / destroyed: HP, bricks left, ice left), `RACE` (distance/position toward a finish line, or who is ahead), `SCORE` (an open-ended tally, score, timer, temperature or chart with no fixed end), `NONE` |
| meter_end_visible_f0 | 1 = the end state of that meter (MAX line, target number, target outline/mould, finish line, the intact picture) is visible at frame 0 |
| xN | 1 = a multiplicative rule drives the progression (each hit ×2, splits into 3, doubles, grows 1.5× per step, ×N per round) |
| ladder | 1 = a stepped parameter ladder visibly moves toward the target (0 → 25 → 50 → 100 %, round 1/2/3 each with a bigger setting, an upgrade each try) |
| speedup | 1 = the actions/hits visibly come FASTER over the clip (stated: period shrinking, accelerating strikes, cadence speeding up) |
| sequel_of | the scene/clip name if this Short is an episode / sequel / rematch / round N / comment-request remake of an EARLIER uploaded Short of ours (say which), else "" |
| famous | 1 = a famous real-world object, place or extreme is central (the Sun, Moon, Earth, a black hole, a national flag, a famous painting, Everest, the galaxy, light-year scale, a famous landmark). Generic everyday objects (ice cube, sandcastle, jar, bridge) = 0 |
| iconic_end | 1 = the clip ENDS with the object BECOMING or RETURNING TO a recognisable one-word named shape/object (circle, wheel, star, heart, flag, snowflake, sphere, crown, the original picture "back"). Overflow, FULL, a winner, a broken/destroyed/dust state = 0 |
| iconic_end_word | that word, or "" |
| press_family | 1 = repeated pushes or impacts: the SAME physical action (press, hammer, push, slam, drop, strike) again and again, each one bigger or doing more |
| discrete | 1 = discrete, countable actions (hits, presses, drops, shuffles, cuts, pours, splits on contact, shots) drive EVERY change, and each one is both SEEN and HEARD (a sound per action). 0 if the main change is a continuous flow / melt / growth / drift / spreading |
| continuous | 1 = the MAIN mechanic is a continuous or emergent process (melting, flowing liquid, accretion, flocking, orbiting, diffusion, smooth growth, a temperature curve, spreading/flood-fill, rain, chaotic motion, an algorithm exploring). `discrete` and `continuous` are never both 1; both 0 is allowed for a genuine mix |
| everyday_any | 1 = the question is about everyday real life (drinks, food, home, sports, shopping, beach, weather) |
| everyday_spectacle | 1 = an everyday question settled by a visible SPECTACLE (melt, flood, wave, smash, collapse, burst, overflow). A queue / path / route / score / timing simulation = 0 |
| finale | 1 = a big finale or reveal the clip builds to and you wait for (overflow eruption, the full picture revealed, a final burst/collapse, a black-hole swallow, "IT'S A X!"). A small result banner alone = 0 |
| attempts | 1 = the structure is repeated TRIES that fail and reset (try 1, try 2 …; level after level that restarts) |
| attempts_param_climb | only if attempts = 1: 1 = each try visibly raises a parameter that closes the gap toward the target (softer each drop 0/45/75/100 %, heavier each try), so each reset is a rung up; else 0 |
| abstract | 1 = an abstract puzzle or maths / algorithm / probability demo whose stake is a rule or a number rather than a physical outcome (Monty Hall, Tower of Hanoi, maze-solving or sorting algorithms, Chladni/maths art, penny-doubling maths) |
| method_duel | 1 = two (or more) sides use DIFFERENT methods / strategies / tools on the same task and the clip compares which works better |
| race | 1 = two or more competitors progress on a common meter toward a finish / MAX / target, so a leader exists at each moment |
| lead_change | if race = 1: 1 = the lead changes at least once (doc, timeline or pinned comment says so), 0 = the same side leads throughout; null if race = 0 |
| chain_break | 1 = the "until it breaks" family: load or steps are added one after another UNTIL a structure breaks / fails / collapses / turns to dust, and the break is the payoff |
| dead_stretch | 1 = a stretch of ≥ 3 s where nothing new happens (the doc admits a slow/dead middle, a long wait, or the timeline shows a ≥ 3 s gap between events) |
| main_mechanic | ≤ 12 words |
| end_state | ≤ 8 words: what the last seconds show |
| confidence | "high" / "med" / "low" |

Notes:
- Code each key independently; do not reason about whether the Short "should" do well.
- `meter_type` is the main readout the viewer tracks. A container visibly filling to a marked line counts as FILL even if there is also a counter.
- `press_family` is narrower than `discrete`: a split cascade triggered by ONE impact is discrete but not press_family; a press/hammer/pusher striking again and again is both.
- For DopamineEXE clips (no characters), `method_duel` and `race` are usually 0 unless two lanes/methods are compared.
