# edge_slide
- New scene (batch37). It is a slide-to-the-edge game, not the rejected thin_ice (cracking ice).
- Rule: "Every round the ice gets SLIPPERIER". Caption (baked, `--cap`): `Every round the ice gets ^SLIPPERIER^|~Closest to the edge WINS~`.
- Choice:
  - Mochi: a big run-up and a late BRAKE.
  - Bolt: an exact, calculated push.
- World:
  - An ice slab on a cliff top at twilight, with snowy mountains, a moon and icicles under the slab. A deep snow drift lies at the cliff foot (bottom-left).
  - Two lanes in a 3/4 view: Bolt in the back lane (y 880), Mochi in the front lane (y 1040).
  - The EDGE is on the LEFT (x 215-236), clear of the Shorts buttons.
  - The start mat is on the right (gold line at x ≈ 812).
  - A ruler sits on each lane: 1 cm ticks for the last 10 cm, 5 cm ticks beyond.
  - The leader's best mark is a lane-coloured flag on the ice.

## Physics (1.55 px/mm, blob radius 50 mm, g = 9.81 m/s², 8 substeps per frame)
- Each round Bolt goes first, then Mochi. The best mark that stays on the ice leads.
- After every round a polisher bar sweeps the slab and mu drops: 0.12 → 0.09 → 0.06 → 0.04.
- Mochi:
  - She reaches 1.26 m/s (±3%) on the mat, belly-flops onto the ice and glides at mu.
  - She brakes when the edge is v²/(2·5·mu_feel·g) + margin away. Digging in gives mu_brake = 5 mu. Her margin is 91-103 mm by feel.
  - mu_feel is the PREVIOUS round's mu (her feel lags one polish). So her real braking distance v²/(2·5mu·g) is longer than she thinks, and she stops closer every round: 9.6 → 5.6 → 0.8 cm.
  - At mu 0.04 her brake needs 39 cm but only 34 cm of ice is left. She cannot stop, even braking at once.
- Bolt:
  - He pushes from rest with v = √(2·mu·g·d), d = start distance − aim, with push precision ±0.4%.
  - His aim is 6.8 cm while he leads, and half of Mochi's best (min 0.45 cm) when she leads.
- Falling:
  - A blob is supported until its CENTRE passes the edge. Once the front is past the edge it tips forward about the edge (up to −0.9 rad).
  - It then falls at real g into the drift: POOF, then buried with only the eyes and curl showing, annoyed stare.
- Honest gag: the winner's cheer-hop landing on mu 0.04 slides him 1.6 mm closer to the edge (0.4 → 0.2 cm) and he wobbles.
- Drama is robust: 221 of 500 seeds pass `good()`.
  - Mochi goes over in round 4 and Bolt wins.
  - At least 4 lead changes, and both characters teeter.
  - Mochi's round-3 mark is 0.3-1.4 cm and Bolt's round-4 mark is ≤ 0.9 cm.
  - Clip 15-20 s.

## s488 (default)
- Marks (Bolt, Mochi), cm:

  | Round | mu | Bolt | Mochi |
  |---|---|---|---|
  | 1 | 0.12 | 6.6 | 9.6 |
  | 2 | 0.09 | 7.1 | 5.6 (MOCHI LEADS) |
  | 3 | 0.06 | 3.3 (BOLT LEADS) | 0.8 (TEETERING, MOCHI LEADS) |
  | 4 | 0.04 | 0.4 (TEETERING, BOLT LEADS) | OVER |

- Mochi's braking distance per round: 11 → 15 → 26 → 39 cm. A bracket on her lane shows it ("brake needs 26 cm"). In round 4 it turns red past the edge: "brake needs 39 cm (ice left 34 cm)".
- Hook:
  - Frame 0 is round 1 with Mochi braking hard: angry grin, shavings spraying ahead, speed streaks, warm contact glow, and the live readout "14 cm".
  - Bolt is already parked at "6.6 cm!" with a worried look. The skrrt starts at 0.00 and her stop ping is at 0.14.
  - SLIPPERIER! μ = 0.09 (polisher sweep) appears at 0.77 s.
- Clip 16.02 s (961 frames):
  - Mochi goes over at 12.48 and falls at 12.65.
  - POOF at 12.82. BOLT WINS! at 13.10, then confetti, a cheer, and the slip-wobble at 14.4.
  - The last 0.6 s dissolves into the pre-roll (Mochi's round-1 run-up).
- HUD:
  - μ ladder (y 352) with the current value boxed and shining.
  - Bolt's calc bubble `v = √(2·μ·g·d)` / `μ 0.09 · d 29 cm → 0.72 m/s`, with its tail tracking him.
  - Live distance readouts: Bolt's above his head, Mochi's under her lane.
  - Scoreboard (y 1362-1514): name, method and BEST, with a gold crown on the leader.
- Banners start at 0.85x scale:
  - y 478: SLIPPERIER! / TEETERING! / X WINS!
  - y 590: X LEADS! / OVER THE EDGE!
  - Vote: y 600.

## Sound
No music, no beds, no whoosh, hiss or creak. Everything is synthesized in the scene:
- Glide tick: a clean sine blip (f + 2f + a glassy 2.76f), 7 ms decay.
  - One tick per ruler mark crossed: every 5 cm, then every 1 cm in the last 10 cm. The ticks slow down with the slide (prize-wheel feel).
  - Pitch rises 1.9 → 3.6 kHz toward the edge.
- Brake skrrt: a train of 6 ms ice-crystal sine bursts (4-8.5 kHz) every 5.5-15 ms. It is denser and louder at speed and thins out as she slows.
- Stop ping: a glass harp note, MIDI 76-92, higher = closer to the edge.
- Flag-plant tink when a mark is a new best.
- Footstep taps (muted 230-290 Hz tone plus a tiny click) for run-ups and hop-backs. Belly-flop plop, push pok, two calc blips.
- Polisher: a rising run of 5 soft glass tings. Lead ting. Teeter: 5 alternating ticks.
- POOF: a 160 → 70 Hz fwump plus a puff low-passed at 260 Hz.
- Win chime: glass-harp major arpeggio, rung out by 1.25 s, plus 3 confetti tinkles.
- Onsets kept ≥ 12 ms apart. `master(peak_db=-6)`. No events in the last 1.0 s; the tail fades over 0.6 s.

## Flags
- `--seed` (488), `--label`, `--cap 'a|~b~'`.
- `--vote`: "Team Mochi or Team Bolt?" plus a drawn gold arrow at y 600, from win+0.45 s to the dissolve. Default OFF; `--vote 0` also means off.
- `--search N --from S`, `--dry`, `--still --frame N` (negative = pre-roll), `--sound 0`.
- Tuning: `--mus --kb --vm --mlo --mhi --safe --sigb`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 961 frames, 16.02 s.
- -14.01 LUFS, peak -7.1 dBFS, last 0.5 s peak -58.9 dBFS.
- flash_check PASS (0 flashes).
- Seam:
  - Pre-encode -1 → 0 is 1.31 against a normal step of 1.23, and frame -1 is closer to 0 than to 1 (1.66), so the loop is perfect.
  - Encoded seam is 1.89 against steps of 1.23-1.53 (I-frame bump; high-motion opening).
- Events per 5 s: 43 / 52 / 27 (122 sound events). The longest gap is 0.60 s.
- Safe zone:
  - Caption y 196-270. The slab, faces and labels sit at y 700-1260; the drift and buried Mochi at ≤ 1300.
  - The scoreboard ends at 1514 (0.79h).
  - The edge and all close calls are at x < 450. Only the start mat, Mochi's wait/wind-up spot and the start of the polisher sweep cross x > 918.

Delivered <VIDEOS_DIR>\batch37\edge_slide.mp4 (no vote). Owner review: pending.

Owner review (2026-10-16): "ok let's try, not much hope" -> APPROVED, but hold the 4K until more videos are added.

Owner review (2026-10-16): approved -> 4K (NF_SCALE 2.0, label ship, seed 488, vote OFF). 2160x3840 h264 yuv420p 60 fps, 961 frames, 16.017 s, -14.01 LUFS, peak -7.1 dBFS, flash_check PASS -> <VIDEOS_DIR>\Schedule\2026-10-20\3_edge_slide.mp4.
