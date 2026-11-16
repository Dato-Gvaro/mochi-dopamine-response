# siege_duel3: siege_duel re-paced for scroll-stop (batch31b)

- **Why:** owner review of siege_duel2 (2026-10-13): "the start is slow, make it faster; at the finish don't use slow motion - let the castle wall get destroyed fully, to the ground, don't cut there; use better stone sounds; for shooting use tik-tik or something better." Rules: research/scroll_stop.md.
- **Build:** `scenes/siege_duel3.py` imports siege_duel2 (and through it siege_duel, both unedited). It sets the shot grid to 160/min (was 140) before simulating, and swaps two Sim methods at run time:
  - `support`: on the breach topple, the lean-out is x0.55, plus a seeded horizontal jitter of +/-1.8 m/s and spin, so the wall crumbles apart instead of sliding out as a slab;
  - `freeze`: rubble packs as a flat mound (45 % of the piece's height); pieces resting above 1.4 m don't stack, so no stone towers.

  Stones are drawn x1.7 and boulders x1.2 so they read on a phone.
- **Timeline:** video t = sim tau - 1.10 s, real speed throughout.
  - Frame 0: a catapult stone in flight at the wall (impact 0.40 s), the trebuchet mid-swing on its too-short first boulder.
  - LEAD CHANGE at 6.4 s; BREACH at 17.12 s.
  - The whole section topples and crumbles to a rubble mound by ~20.3 s, then a ~1.8 s hold on the settled rubble with drifting dust.
  - A 0.6 s dissolve back to frame 0 = the loop. Clip 22.72 s.
- **Sound (no music, our own synthesis, seeded per repeat):**
  - stone hit = modal crack + granular crunch + low thud (boulder: + sub + rumble) + debris trickle/pebbles;
  - every block's ground landing = deep thud + crunch;
  - breach = a 3.6 s rubble cascade;
  - "tik-tik" pawl ratchets: catapult 16/s while re-cocking, trebuchet 9/s + rope creak through each wind-up;
  - a sharp wooden snap on every release (trebuchet: + a low body + sling whoosh);
  - soft whistles in flight; subtle wind and torches; banner flutter.
  - Onsets >= 12 ms apart; silent from D - 1.4 s.
- **Checks (Full HD, encoded):** 22.72 s, h264 yuv420p 60 fps; -14.02 LUFS, peak -2.3 dBFS, last 0.5 s -81 dBFS; flash 0 = PASS; seam 0.460; walls at 0.62-0.78 W. Frames read at 0, 0.4, 6.45, 17.4 and 20.5 s.
- **Delivered:** <VIDEOS_DIR>\batch31b\siege_duel3.mp4 (Full HD). **Owner review:** pending.
- Owner review (2026-10-15): ok -> APPROVED, 4K (Oct 17 slot 3).
