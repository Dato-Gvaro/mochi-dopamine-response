# Niche: character-fill-up

**Status:** candidate — scores BELOW the 22 bar as framed (21/35)
**One-line pitch:** BOLT holds a glass jar under a ball tap; the flow speeds up
every second, the jar's fill line climbs, the counter races — at 100% the jar
overflows into a confetti burst and empties for the loop.

Researched 2026-10-03.

## Hard filters
- [x] Code-renderable at quality — balls into a container = `lib/physics2d.py`
      circles + static segments (container walls). Sand needs a grid
      (falling-sand) module; liquid needs SPH or particles — new.
- [~] Episodes differ by a nameable change — material / container shape / flow
      rule give names, but "now with sand" is close to a re-skin. Thin.
- [x] No borrowed IP.
- [x] Short payoff (fill -> overflow -> empty = loop) AND compilation.
- [!] Advertiser-friendly — ONLY if the character HOLDS the container. A
      character whose BODY is filled until it bursts is the core trope of the
      inflation-fetish animation genre (see Risks). As the owner phrased it
      ("IS or holds"), the "IS" half fails this filter in practice.

## Scores (0-5, evidence required)
| Axis | Score | Evidence |
|---|---|---|
| Demand | 3 | Direct comps are thin. Best: parent priors "521 bounces until the arena is solid" 158k, "When the square fills, it gets bigger" 152k, "It painted the box, then it became the box" 122k (fill mechanics, mid-tier for the parent). Adjacent: **Dino_3DCG** (5.71k subs, started 2026-06-01) soft-body drops 7.4M / 3.6M; **3Ds Marble Show** "30,000 cubes in glass box" only 53k. The big "character gets filled" hits are fetish-adjacent: **Balloon Toons** (770k) "Gem has a problem" 65M. No clean small channel found with a character + fill. |
| Supply gap | 3 | Searches "how many balls to fill it", "fill the container satisfying", "#fillup", "#ballpit", "#fallingsand" return kids toys, slime, crafts, Minecraft sand (#fallingsand tops at 31k) — empty, but empty may mean no demand. |
| Our edge | 4 | Exact fill % and counts, accelerating tap rate, per-ball pitch climbing with the fill level, perfect empty-to-frame-0 loop — all native to the engine. |
| Episode depth | 3 | Material (balls / sand / water / blocks / jelly), container (jar, backpack, bathtub, rocket tank), flow rule (doubling tap, multiple taps, leaking hole). ~20-30 honest ones; beyond that it is re-skins. |
| Long-form RPM | 2 | Fill compilations work as background, but the fetish-adjacent neighbourhood (recommendation graph next to inflation channels) risks ad-suitability and audience quality. No comp long-form evidence. |
| Build cost | 4 | Balls-into-jar: ≤1 day (physics2d + toon). Sand/liquid episodes: new particle module, 1-2 days each. |
| Policy safety | 2 | Original and human-reviewed, but (a) re-skin risk is the highest of the three (material swap = cosmetic), (b) fill-a-character is a recognised fetish trope: Balloon Toons 65M / 28M / 14M "<character> has a problem" (character inflates with pudding then bursts — ref_fill-up_2), WolfyGoofyToons "Slime Inflation" 690k, "Weight Limit Test" 702k. Would be 3 if strictly "holds a container" — but then it is the parent's fill sims with a mascot standing next to them. |
| **Total** | **21/35** | Under 22: not worth a test clip as framed. |

## Comparable channels
| Channel | Subs | Started | Top Shorts (views) | Notes |
|---|---|---|---|---|
| Balloon Toons | 770k | — | 269M, 65M, 28M, 18M, 14M | 2D characters inflate with liquid until burst — fetish-adjacent; the trope to AVOID |
| Dino_3DCG | 5.71k | 2026-06-01 | 7.4M, 3.6M, 868k | 3D soft-body spheres dropped into containers, red vs green |
| 3Ds Marble Show | 6.02k | 2026-08-26 | 12.7M (race), "30,000 cubes in glass box" 53k | fill-in-box clip was its weak format |
| Ball Simulations Shorts | 1.88k | 2025-10-18 | 1.0M, 705k | 2D emoji balls; not fill, but faces-on-balls in a sim |
| Satisfying 2D Sims (parent) | ~10k | 2026 | fill episodes 158k / 152k / 122k | prior only |

## Reference videos decoded
- `ref_fill-up_2` (Balloon Toons, gzdT8KSKaRw, 13 s): a woman's trousers are filled from a hose with pudding, swell to giant, burst — confirms "character fills until it bursts" = inflation genre. Owner should see this before choosing any body-fill framing.
- `ref_fill-up_1` (Ball Simulations Shorts, bkNfVXhCHiY, 24 s): emoji balls queue down a neon spiral on black; particle burst ending. Faces help a 2D sim; but this is the parent's look.

## The characters (if pursued, holds-only)
- **BOLT** holds the jar / wears a backpack container; eyes go from calm to
  wide to sweat-drop as the fill line rises; leaf sprout droops under weight.
- **MOCHI** runs the tap (greedy: keeps opening it wider = the escalation rule).
- From `lib/toon.py`. The CONTAINER is a prop (glass jar with ink outline),
  never the character's body.

## 10 episode ideas (each with its nameable change)
1. **Doubling tap**: the tap doubles its rate every 3 s. "The tap doubles every 3 seconds."
2. **Leaky jar**: a hole drains it — fill must outrun the leak. "Can the tap beat the leak?"
3. **Two jars**: Bolt vs Mochi race to 100%. "Who fills first?"
4. **Growing jar**: every 100 balls the jar gets wider. "The jar grows every 100."
5. **Sand**: falling-sand grains piling at angle of repose. "This time it's sand."
6. **Tetromino blocks**: blocks stack, full rows clear. "Full rows vanish."
7. **Shrinking balls**: each ball is smaller than the last — infinite capacity? "Every ball is smaller."
8. **Splitter funnel**: balls split into 2 jars, 4, 8. "Every funnel splits the flow."
9. **Weight scale**: jar sits on a scale vs Mochi on the other side. "When does the scale tip?"
10. **Bucket chain**: full jar pours into the next, bigger jar. "Each jar fills the next."

## Engine changes needed
- look: `lib/toon.py` (glass jar prop: translucent fill + ink outline + shine).
- layouts: single centred container — trivial in 9:16 and 16:9.
- audio voice: plink per ball pitched by fill level (rising pitch = tension), overflow = PD melody cadence, drain = descending glissando then silence.
- new lib module: falling-sand grid; particle liquid (only if water episodes are wanted).

## Risks
- **Fetish adjacency (main risk)**: body-fill = inflation genre. Holds-only is mandatory.
- **Cannibalisation vs parent**: highest of the three — fill-the-arena is already a parent mechanic (158k / 152k / 122k). With holds-only framing the character is a bystander, so the channel's distinctness rests on look alone.
- **Re-skin risk**: material swaps are cosmetic; inauthentic-content exposure.
- Low demand proof for clean versions.

## Cheapest proving test clip
Not recommended at 21/35. If the owner wants one anyway: idea 1 "Doubling tap"
as an EPISODE inside `pet-grows`/`character-chain-reaction` (Mochi's candy jar),
not as a channel concept — 25 s, balls only, ≤1 day.
