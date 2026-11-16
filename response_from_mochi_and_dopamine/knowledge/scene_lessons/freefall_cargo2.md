# freefall_cargo2 — one parachute left: big leaps vs safe hops down the falling cargo (Wagner, Ride of the Valkyries)

## Why
- Owner review of freefall_cargo (2026-10-12): "good visuals but I can't see the challenge."
- The owner asked for:
  - no arms or legs on the characters;
  - the cargo falls with them, and they hop from object to object down to the chute;
  - the winner puts the chute on, grabs the other, and the canopy opens;
  - the grabbed one is annoyed, the grabber happy.
- freefall_cargo.py is unchanged. It is imported for:
  - the sky, sea and islands;
  - the plane and the ramp burst;
  - the cargo drawings and the HUD text;
  - the clock;
  - the orchestral Valkyries arrangement (`v1.arrangement` with our own BOOMS + SFX).

## Physics (in the frame falling WITH the cargo)
- Every body is near terminal speed, so the field barely moves relative to itself:
  - each object drifts at ±18-30 px/s and tumbles at ±0.25 rad/s;
  - the rising pallet moves at −175 px/s, the sinking jeep at +760 px/s.
- The characters are slightly denser: they sink at g_eff = 150 px/s². Relative motion is air-damped (linear, τ = 1.6 s).
- A hop: the launch velocity is SOLVED so the closed-form drag trajectory meets the target object's real (drifting, rotating) top at the landing time.
  - Landing pushes the object (momentum share 1/(1+m_obj)) and torques it (off-centre landing).
  - Pushing off recoils it.
- 40 px = 1 m on the HUD.

| | Mochi: BIG LEAPS (risky) | Bolt: SHORT HOPS (safe) |
|---|---|---|
| rhythm | lands on bar downbeats, launches on beat 2 (1.23 s air, a full flip) | lands on every beat (0.40 s air, zig-zag) |
| drop per move | ~12-14 m | ~3.5-4 m |
| launch speed | up to 809 px/s | 452-857 px/s |
| misses | 1 (bar 65) | 0 |

## Race (story s = clip t − 0.8)
| bar | s | what happens |
|---|---|---|
| 60 | 0 | Ramp burst, "ONE PARACHUTE LEFT!". The pack is visible at the bottom ("THE ONLY CHUTE ↓ 106 m"), plus the left race meter. |
| 61-64 | 1.85-7.4 | Mochi leads by up to 7 m. A jeep sinking at 760 px/s tumbles past her mid-leap (bar 63 pos 6, centre gap 290 px): NEAR MISS. |
| 65 | 9.25 | BAD LANDING: a drum tumbling at 1.6 rad/s, top tilted 21°. She bounces (e = 0.85) to (−125, −194) px/s and drifts, dizzy, until a slow-falling pallet rising through the field catches her (bar 66). |
| 65-69 | 10.2-18.6 | Bolt leads |
| 69 | 16.65 | NECK AND NECK (Mochi 1 m behind) |
| 69 pos 6 | 17.88 | ALL-IN LEAP. She passes Bolt at s 18.6. |
| 70 pos 3 | 19.12 | She lands on the pack, one beat before Bolt's next hop. GOT THE CHUTE (it snaps onto her back, with a harness strap). |
| 70 pos 6 | 19.73 | Pushes off to Bolt and latches him (tether + belt): GRABBED BOLT |
| 71 | 20.35 | The canopy pops on the climax chord (boom + cymbal swell). They rise against the still-falling cargo. MOCHI WINS. Bolt gives the annoyed stare into the camera; Mochi grins. |

## Hook / loop
- Frame 0 = both under the open canopy, cargo tumbling around and below, "MOCHI WINS!", at a 1.3× zoom centred on the pair.
- A 0.8 s rewind (veiled and faded, flash-safe). The ramp bursts at 0.80 s, they leap at 0.95 s, and Mochi's first flip is at 1-2 s.
- Everything is a function of story time.
  - Pre-encode, the seam is exact: 0.562, against a normal step of 0.551.
  - Post-encode, check_clip reads 1.19. That is the frame-0 I-frame effect, as in v1.

## Music / sound
- Music: v1's arrangement, unchanged. Wagner, Ride of the Valkyries (1856, PD). rvalkyri.mid (midiworld), bars 59-71.
- Booms land on ramp 60, bounce 65, 68, and canopy 71.
- SFX:
  - wooden "tok" landings: 31 for Bolt on the beats, 9 for Mochi on the downbeats;
  - a soft bounce thump and the jeep whoosh;
  - pack-snap and latch clicks, the canopy fwump;
  - soft wind, the rewind whoosh.

## Checks (v1, Full HD → <VIDEOS_DIR>\batch31\freefall_cargo2.mp4)
- h264, yuv420p, 1080x1920, 60 fps, 1503 frames = 25.05 s.
- -14.01 LUFS, peak -5.66 dBFS, last 0.5 s at -80.8 dBFS.
- flash_check PASS (worst 2 in one second).
  - Earlier renders failed. The causes were fast-scrolling white sky puffs and the 27× rewind.
  - Fix: puffs scroll at 3.5 px/m with alpha ≤ 0.55, speed lines are capped at 0.18 alpha, and the rewind is faded and veiled.
- Encoded frames read at 0, 0.5, 1, 2, 3, 7.55, 10.5, 18.4, 20.0 and 21.4 s.

## Lessons
- flash_check accumulates per-cell extremes. Any large, high-contrast content scrolling fast (white clouds on the dark sea) adds up to "flashes" even without blinking. Keep fast parallax low-alpha.
- A near-miss gap must clear the object's rotated extent (a jeep is 270 px long), not just its centre distance.
- Owner review (2026-10-13): remove the music, add material-based SFX (wood/metal); the reversing start doesn't look nice -> freefall_cargo3.
