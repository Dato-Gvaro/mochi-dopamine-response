# ol_friction_pour (DopamineEXE, batch62 #3)

**Superseded by `ol_friction_pour2` (2026-11-01, see `docs/scenes/ol_friction_pour2.md`).** Owner at review: "interesting to watch but can't figure out what's the difference". v1 stays runnable and bit-reproducible (`scenes/ol_friction_pour.py`); its review file was moved to `DopamineExe\archive\ol_friction_pour.mp4`.

## v1 (2026-10-31)
Two identical jars, the same balls poured in at the same rate, which doubles every 2 s. Left: friction 0% (μ 0). Right: friction 100% (μ 1.0 ball-ball and ball-glass, rolling resistance 0.1). It ends when a jar overflows; the spouts close 0.25 s later.

- Caption (baked; `--cap ''` = base): `0% vs 100% ^FRICTION^: the pour DOUBLES…|until one jar ~OVERFLOWS~`. True.
- **Truth over brief: the brief's twist did not happen.** With round balls that can spin, friction barely changes how much a jar holds: the 0% jar overflows first in this run (8.34 s vs 8.48 s, **+0.14 s**), and across seeds it is a coin flip (seed 1: 0% first by 0.12 s; seed 2: 100% first by 0.06 s; seed 3: 0% first by 0.14 s). The 100% side makes only a low mound (~4 cm over the rim at its overflow); the 0% side is flatter but the pour also domes it. No "packing 90% vs 78%" or "heaps like sand" claim is made on screen.
  - Why: 2-D frictional discs that can ROLL have a low angle of repose; "sand-like" heaps need grains that can't roll. An earlier no-rotation build (sticky discs) did heap and the 100% jar overflowed first in 4/4 seeds (by 0.1-0.23 s), but it grew unphysical standing ball columns under the stream, so it was dropped.
  - The owner should decide whether this is worth shipping (the two jars look alike for most of the clip), or switch the right jar to rough non-rolling grains (a different, nameable change: "round vs rough").
- Equal counts: one fixed spout column pattern feeds both jars identically (same jitter, same radius sequence); the counter is the true per-jar total (58 at frame 0 → 1,220 at the overflow → 1,336 when the spouts close).

## Model (`simulate`, seeded, ~80 s CPU)
- 1 m = 1000 px, g 9.81 m/s². Balls r 5-7 px (uniform; equal discs crystallise into stable 60° stacks). 8 substeps/frame, 8 Jacobi projection iterations (×1.5 relaxation), contacts never add speed (inelastic clamp), thin glass that can only be left over the rim.
- Friction (right jar): position-level Coulomb at the contact points of spinning discs (mass ∝ r², I = m r²/2): the surface slip of the substep (linear + spin) is cancelled while below μ × the normal correction, else reduced by it; rolling resistance torque 0.1 × r × N against the spin. Glass contacts: position-level Coulomb (no spin).
- Pour: R(t) = 3.4 × 2^((t + 5.6)/2) balls/s per jar (pre-roll 5.6 s), spout 104 px wide at y 430, balls leave it at 900 px/s; spawn columns refire after 2r + 1 px of fall.
- Overflow = a ball leaves the jar over the rim while that jar's pile top (1st-percentile height of the slow balls) is ≥ 97% of the rim height (an early splash does not count).
- Jars: inner x 200-460 / 620-880, rim y 640, floor y 1160 (52 cm × 26 cm), table y 1166. Seed **3**.

## Timeline (seed 3)
- 0 s: 58 balls per jar, both streams pouring · ×2 every 2 s (pill pops at 0.4, 2.4, 4.4, 6.4 s) · 4 s 265 · 6 s 539 (levels 48% / 51%) · 7 s 767 (68% / 71%) · **8.34 s OVERFLOW! (0%, 1,220 balls)** · 8.48 s the 100% jar spills too ("+0.14 s later") · spouts close 8.59 s · 1,336 per jar · 10.75 s end (spilled 137 vs 115). Dissolve 0.6 s. **645 frames.**

## Screen
- Balls coloured by pour band (one hue per doubling: red → orange → … → violet), the bands show the flat vs mounded layering. Jars + funnels thin white; gold dashed rim lines from frame 0.
- Under each jar: "FRICTION 0% / 100%", "μ = 0 · slides" / "μ = 1.0 · sticks", a LEVEL bar with a gold RIM mark (100% = level with the rim; it reads above 100% when the pile mounds over).
- Counter y 1500 "BALLS IN EACH JAR" + "×2 POUR" pill; gold "OVERFLOW!" over the first jar, "+0.14 s later" over the second.

## Sound (ASMR only, owner rule for pours)
- Per jar, landing ticks (≤3 per frame, density-scaled): 0% = a soft rounded patter, 100% = a dry short click; D-major pentatonic, low/mid. A bright shimmer per ball spilling over a rim; a soft wooden tok on every doubling. 1,718 events. No music bed.

## Checks (encoded mp4)
- h264 yuv420p 1080x1920 60 fps, 10.75 s; **-13.98 LUFS**, peak -6.25 dBFS, last 0.5 s digital silence; flash_check PASS (0); seam mean |Δ| 0.234. RMS per 5 s -21.6 → -16.0 (rising).
- Stills read at 0, 4, 7, 8.33, 8.58, 9.33, 10.33 s; 1:1 crop (encoded) of both rims at 9.0 s.
- Side safe zone: jars + labels x 200-880 (0.19-0.81w); only spilled balls run wider.

## Flags
`--seed` (3), `--mu` (1.0), `--mur` (0.1), `--r0` (3.4), `--pre` (5.6), `--vp` (900), `--spw` (104), `--iter` (8), `--hold` (1.8), `--tmax`, `--resim`, `--dry`, `--audio`, `--still --frame`, `--cap`.

## Upload draft (true to this run)
- `0% vs 100% friction: same balls, which jar overflows? 🫙 #satisfying #physics #shorts`
- `Same balls, same jar… only the friction is different 🫙 #satisfying #physics #shorts`
- `The pour doubles every 2 seconds until a jar overflows 🫙 #satisfying #physics #shorts`
- Pinned: `same number of balls in both jars the whole time. which one did you think would spill first?`
