# rocket_stages
- New scene (batch37). Rule: "Every tank he drops makes him FASTER". Choice: Mochi flies ONE big tank, Bolt flies 4 STAGES and drops each one when it runs empty. Caption (baked, `--cap`): `Every tank he drops makes him ^FASTER^|~One big tank or stages?~`. Strip under it: `SAME FUEL, SAME ENGINE  Δv = vₑ·ln(m₀/m₁)  TIME ×20`.
- World: a vertical race from the sea to the SPACE RING at 100 km. The sky goes from blue through indigo to starry black. Gulls (~1 km), clouds (2-11 km), weather balloons (24 and 31 km), small satellites (71, 84 and 93 km). No agency names or logos.
- Rockets: the pilot sits in a gold-rimmed glass dome (dome r 78, pilot r 53). Mochi has a coral body, Bolt teal/mint stages. Each tank has a gold fuel window. Flames are warm coral/gold.
- HUD per rocket (y 1360-1534, Bolt's panel ends at x 916):
  - ALTITUDE: n km, SPEED, MASS.
  - A mass bar split into capsule | empty shells (dead weight, grey) | fuel (gold).

## Physics (integrated in SI units, nothing scripted until the apex)
- Both rockets carry the same 1,500 kg of fuel and the same engine: 31.0 kN, vₑ 3,000 m/s, 10.3 kg/s. So both burn exactly 145.3 s and run dry at the same moment.
- Equations: a = F/m − g(h), with g(h) = g0·(R/(R+h))². Midpoint integration in 0.01 s steps, split exactly at the fuel boundaries.
- Mochi: capsule 1,000 kg + engine 42 kg + tank shell (0.12 × fuel) = 2,722 kg at launch. She carries the 222 kg shell all the way up.
- Bolt: 4 engines, 4 shells, 3 decoupler rings of 20 kg = 2,908 kg at launch (+186 kg). His thrust-to-weight is 1.09 vs Mochi's 1.16, so Mochi leads early (honest).
- Each drop removes 107 kg, plus a 1 m/s decoupler spring. Spent stages fall ballistically from the drop point.
- Time-lapse ×20: 1 s of video = 20 s of flight. Frame 0 is flight time 26.3 s, so the first drop lands at 0.5 s.
- Parameter search (`--eng --eps --dec --tw`):
  - Goals: Mochi's apex 96.5-98.5 % of Bolt's; Bolt passes her; Bolt reaches 100 km.
  - Result: E 42 kg, ε 0.12, d 20 kg, T/W 1.16.
  - E 44 or more: Bolt never reaches 100 km. E 40: he docks at 150 m/s, 0.5 s before Mochi stalls.
- Timeline (s7):
  - Stage drops at 0.50 / 2.32 / 4.13 s.
  - BOLT IS FASTER! at 5.03 s.
  - OUT OF FUEL! (both) at 5.95 s: 983 vs 1,033 m/s, Mochi still about 3.8 km ahead.
  - Coasting; BOLT LEADS! at 9.38 s.
  - DOCKED! at 10.92 s (82 m/s, jaws clamp shut), BOLT WINS! at 11.54 s.
  - Mochi tops out at 98.53 km ("1.5 km SHORT!") at 11.09 s, free-falls 0.6 s, then POP! parachute and she ditches the tank.
  - Fast-forward chute descent 11.69-14.22 s (not physics; clouds fade while the camera zooms out), SPLASH!, then the annoyed stare with the canopy floating beside her.
  - 36-frame dissolve into the pre-roll. Clip 16.27 s (976 frames).
- Deviation from the brief: with honest equal engines, both run out of fuel at the same moment (mid-race, 5.95 s), not just short of the top. The loser's comic beat near the top is the STALL ("1.5 km SHORT!"), not fuel-out.
- Camera:
  - Anchored at the midpoint of the two domes.
  - Zoom S = min(330/gap_km, 1800/scroll, 1400) px/km, smoothed in log.
  - Near the ring the pair drops 140 px and the gap tightens, so the ring clears the caption.
  - During the descent the anchor is Mochi's dome at y 880.

## Sound (no music, no beds, no whoosh/hiss/roar)
- puff: an engine pulse, a clean low thump (78/92 Hz with a pitch drop, plus 2 harmonics), one per visible flame pulse. Rate = 0.22 × F/m, so 2.5/s rising to 6.3/s, and Bolt's rate jumps at each drop.
- clack: stage separation, a metallic plate CLACK plus a clean downward pop 55 ms later.
- Altitude ticks:
  - A soft tik every 1 km to 9 km, every 5 km to 90 km, then every 1 km.
  - A bell ting every 10 km.
  - Descending ticks every 10 km during the chute ride.
- Other events:
  - sputter: 3 dry ticks at burnout, for both rockets.
  - Gull double-tweet, cloud "pomf" (tonal), satellite/balloon tings, and a ting for FASTER and for LEADS.
  - Docking beeper over the last 2.6 s before docking, rising in rate and pitch.
  - Dock: a heavy metal CLUNK plus 2 latch clacks, then a bell arpeggio.
- The loser:
  - uh-oh: 2 soft falling notes at the stall.
  - Parachute: a cork pop plus a tonal canopy fwop.
  - Soft splash, fully tonal (owner tweak 2026-10-15, no hiss): a low "bloop" (150 -> 70 Hz with 2 harmonics) plus 6 rising water-drop plinks (0.7-2.5 kHz). The filtered-noise body is gone.
- Mixing: onsets kept ≥ 12 ms apart. `master(peak_db=-6)`. No events in the last 1.05 s; the fade ends at the dissolve, so the loop point is silent.

## Flags
`--seed` (7; cosmetic only: clouds, birds, stars), `--label`, `--cap 'a|~b~'`, `--vote 1` ("Team Mochi or Team Bolt?" + a drawn arrow from splash+0.15 s to the end; default OFF; `--vote-y` 1110), `--dry` (sim + stats + sound-event counts), `--still --frame N` (negative = pre-roll), `--sound 0`. Tuning: `--eng --eps --dec --tw`.

## Checks (encoded Full HD, s7)
- h264 yuv420p 1080x1920, 60 fps, 976 frames, 16.27 s.
- -14.01 LUFS, peak -5.9 dBFS, last 0.5 s silent (after the splash tweak).
- flash_check PASS (1 flash).
  - The first build failed twice. Fast-scrolling white clouds failed at 1-2 s. The sea entering below a brightening sky failed during the descent.
  - Fixes: 8 smaller clouds at α 0.8 that fade when zoomed out, a brighter sea with a flat gradient, and a 2.5 s descent.
- Loop: pre-encode seam 1.10 against a normal step of 1.08 (perfect). Encoded seam 1.54; frame 0 is a fast-scroll frame.
- Events per 5 s: 74 / 59 / 25.
- Safe zone: leader dome ≥ y 440, the ring and banners stay out of the strip at x > 918, content ends at 1360.

Delivered <VIDEOS_DIR>\batch37\rocket_stages.mp4 (no vote). Owner review: pending.

Owner review (2026-10-16): nope -> removed.
