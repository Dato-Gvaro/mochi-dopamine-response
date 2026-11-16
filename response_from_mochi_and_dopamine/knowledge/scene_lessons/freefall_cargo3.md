# freefall_cargo3 — freefall_cargo2's hop race, scroll-stop cut, material ASMR (no music)

## Why
- Owner review of freefall_cargo2 (2026-10-13):
  - "Remove the music; add sound effects based on what they jump on (wood, metal)."
  - "Why is it reversing at the start? It does not look nice."
- Owner goal: brainrot Shorts that stop an aimless scroller (research/scroll_stop.md).
- freefall_cargo2.py is imported unchanged: physics, choreography, race, near miss, bounce, chute grab and the annoyed Bolt. It is patched at run time:
  - `tau_of` = identity;
  - no rewind badge;
  - banners on story time.

## Timing (clip t = story s − 1.0, no slow motion)
- **Frame 0:** s 1.0. Both are mid-hop out of the plane, "ONE PARACHUTE LEFT!", and the chute is marked below. A wooden crate tumbles past TOWARD the camera, growing exponentially (looming) and capped at 3.6× so it never covers a big area (flash-safe).
- **First landing sound:** 0.23 s, then a landing every beat.
- **Canopy:** pops at 19.35 s. The clip runs 2.8 s further (the annoyed stare) and ends at 22.15 s.
- **Loop:** the last 30 frames DISSOLVE into the scene's own pre-roll (story s 0.5 → 1.0). The final frame is one step before frame 0.
  - Pre-encode seam 2.57, against a normal opening step of 2.54 (high-motion opening).
  - check_clip reads 3.10 post-encode.

## Sound (all synthesised in the scene; every repeat varied ±6 % pitch, ±10 % level, new noise)
| event | sound |
|---|---|
| wooden crate | hollow 3-mode wood tok + a small creak (80 %) |
| ammo box | metal clank, inharmonic 1 / 2.76 / 5.40 / 8.93, warm low-pass |
| drum | boomy cylinder modes 165 Hz + 78 Hz body, long ring |
| jeep (Mochi's bar-68 landing) | big clank + 3 rattles + 62 Hz body |
| pallet | 4-tick slatted clatter |
| net | rope-grain creak + soft thud |
| chute pack | fabric thud + buckle click |
| bad landing (drum) | scrape + boing (240 Hz falling) + thud + drum boom |
| jeep near miss, looming crate | whooshes |
| pack on / grab | buckle click; velcro rip + strap click |
| canopy | fabric FWUMP (low-passed burst + 58 Hz + flap) + strap snap |
| wind | soft roar, rising 0.35 → 0.8 through the race, dropping when the canopy opens |

- Mochi pans left, Bolt right.
- Simultaneous onsets are nudged ≥ 14 ms apart (the mixer's 10 ms rule).
- Audio is cut 1.75 s before the end so master()'s reverb has died by the last 1.3 s.

## Checks (v1, Full HD → <VIDEOS_DIR>\batch31b\freefall_cargo3.mp4)
- h264, yuv420p, 1080x1920, 60 fps, 1329 frames = 22.15 s.
- -14.01 LUFS, peak -2.97 dBFS, last 0.5 s at -84.3 dBFS.
- Wind floor about 10 dB under the landing hits.
- flash_check PASS (worst 2 in one second).
- Encoded frames read at 0, 0.3, 1, 5.8, 8.4, 18.2, 19.6 and 21.9 s.
- Owner review (2026-10-15): ok, let's try it -> APPROVED, 4K (Oct 16 slot 2).
