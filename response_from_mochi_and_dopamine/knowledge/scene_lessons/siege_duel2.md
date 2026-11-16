# siege_duel2: siege_duel with an ASMR foley track, no music (batch31)

- **Why:** owner review of siege_duel (2026-10-12): "remove the music and have some good ASMR sound effects."
- **Build:** `scenes/siege_duel2.py` imports `scenes/siege_duel.py` (importlib, registered as `siege_duel` so its sim pickles) and only replaces the soundtrack. Visuals, story, timing, hook and loop are unchanged; `--video output/siege_duel_v1_9x16.mp4` reuses siege_duel's identical picture (mux takes video stream 0 only).
- **Sound (all our own numpy synthesis, each repeat its own seed):**
  - ambience: wind bed (breathing low-passed noise + soft gusts), torch crackle on both sides;
  - trebuchet: deep wooden THWUMP at the counterweight drop + sling whoosh into the release, a settling knock, rope/timber creak + ratchet clicks through each wind-up;
  - catapult: twisted-rope twang, arm slam on the crossbar, quick ratchet clicks while re-cocking;
  - flight: soft whistle (stones), low whoosh (boulders), release to first contact;
  - impacts: catapult = warm sharp crack + grit + pebbles rattling down + dust hiss; trebuchet = deep crunch + sub + rumble + long trickle + hiss; pass-through contacts quieter;
  - breach: long collapse rumble, every block's hard landing as a stone knock on the VIDEO clock (slow motion), a settling trickle, the falling banner's flutter; the opening rewind = a soft reversed whoosh.
- **Rules:** sim times mapped with `t_of_tau`; every layered onset >= 12 ms from the others (`Onsets`; float-safe compare: an exact `< GAP` test looped forever). Bed via `orc.render` (reverb 0.12, air -3 dB), silent from 24.5 s.
- **Checks (Full HD, encoded):** 26.00 s, h264 yuv420p 60 fps; -14.01 LUFS, peak -4.0 dBFS, last 0.5 s -84 dBFS (window RMS -51 dB at 24.5 s, -73 at 25 s); flash 0 = PASS; seam 0.592. Impact windows jump +5-7 dB on the beats (1.70, 8.6, 20.6 s).
- **Delivered:** <VIDEOS_DIR>\batch31\siege_duel2.mp4 (Full HD). **Owner review:** pending.
- Owner review (2026-10-13): slow start; no slow motion at the finish; let the castle collapse fully to the ground (don't cut); better stone sounds; tik-tik for firing -> siege_duel3.
