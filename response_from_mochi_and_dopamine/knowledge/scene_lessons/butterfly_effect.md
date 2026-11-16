# butterfly_effect — double pendulums released 0.001° apart

- New-direction format (2026-10-08, brain-satisfying physics). Phenomenon: sensitive dependence on initial conditions.
- Physics: the real double-pendulum equations (equal masses, equal arms, g/L = 16 s^-2). Vectorised classic RK4 at a fixed dt of 1/480 s (8 sub-steps per frame). Max relative energy drift per release is 3e-7. Neighbouring arms differ by 0.001° in theta1 (theta2 is equal).
- Stage: pivot (540, 0.42h), arm 230 px (reach 0.85 of the width), dark plum radial gradient, dashed reach circle, additive (OPERATOR_ADD) arms. Overlapping arms sum to WHITE and split into the rainbow (Bolt's mint -> sky -> violet -> magenta -> Mochi's coral). Riders r 40 sit on arm 0 (Bolt) and the last arm (Mochi); when coincident they sit cheek to cheek.
- Ladder (N, release theta1/theta2, run):

  | N | Release θ1 / θ2 | Run | Split / bloom (spread > 25 px) |
  |---|---|---|---|
  | 2 | 150° / 110° | 7.0 s | 4.23 s |
  | 10 | -170° / -140° | 3.7 s | 2.25 s |
  | 100 | 150° / 170° | 4.0 s | 1.62 s |
  | 1000 | -170° / -90° | 4.6 s | 1.00 s |

  More arms means a wider total spread, so each bloom comes sooner. Release poses alternate sides.
- Phase 1 has tip trails (mint + coral that add up to a white trail and fringe apart at the split). The label line swaps to "SPLIT after 4.2 s!" for 1.9 s.
- Morph between releases: 0.6 s. Collapse at the end: 2.2 s.
  - Each arm leaves with its true velocity (a decaying momentum term). The pull towards the next pose is EXPONENTIAL (k 7 for a morph, 4.5 for the collapse), i.e. the butterfly effect in reverse: chaos -> fan -> ribbon -> one arm.
  - Old -> new arm set crossfades at u 0.70-0.93 (collapse 0.80-0.95). The new set rides the old arms' index-mapped trajectories. The counter pops at the crossfade.
- Moods: smile + looking at each other in sync -> wow at the split -> worried + sweat -> dizzy (X eyes) as the spread grows. Back to the frame-0 smile at collapse u ≥ 0.62. No blinks within 0.4 s of the seam.
- Sound: a bed built in the scene. The sidecar's 200 events are note_gain 0, so regen_audio cannot rebuild it. Bach Toccata BWV 565, held as a scene-local PD note list:
  - Each release plays the A-G-A mordent (doubled an octave down on the 1000).
  - Ticks walk the run G F E D C# D -> the lower answer, one glass bell per "a tip swings under the pivot". In sync the pair's ticks land on the same frame and sound as ONE note; after the split they interleave.
  - The split gets a rolled D-minor chord plus a soft organ.
  - Each bloom gets a rising D-minor arpeggio (5/7/9 notes) plus the organ. Before the 1000 bloom the diminished roll plays.
  - Flips over the top: soft pings (A5-A6). The split into the next N: a 4-note shimmer.
  - Collapse: a 6-note falling arpeggio, then silence.
  - Rate caps per phase: ticks 0 / 0.17 / 0.12 / 0.085 s, flips 0.20 / 0.13 / 0.08 / 0.055 s.
- Event rate (sidecar /5 s): 24, 36, 55, 85. It climbs through the last run; the final 2.2 s are the collapse.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920 60 fps, 23.30 s (1398 frames).
  - Audio: -14.00 LUFS, peak -8.1 dBFS, last 0.5 s -72 dBFS (below -48 from T-1.0 s).
  - flash_check: 0 flashes = PASS (mean luminance 0.011).
  - Seam: pre-encode mean delta 0.017, between the neighbouring steps (0.018 / 0.039). Encoded 0.178.
  - Render time ~60 s.
- Args: --cap ("a|~b~", default "Start 0.001° apart|~Watch what CHAOS does~"), --label, --still --frame. Deterministic: no seed.
- Delivered <VIDEOS_DIR>\batch19\butterfly_effect.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-09: Start at 100, go to 1000+, but move SLOWER for eye candy; space/violin classical music -> butterfly_effect2.
