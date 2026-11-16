# funnel_race3 — funnel_race2 with a real DROP and a steel-ball (roulette) sound

- Built from the owner's review of funnel_race2: (1) "after they reach the edge they must FALL, not go around in a straight line"; (2) "try some other sound, like a METAL BALL or CASINO-like ball sound". funnel_race2.py is untouched.
- Hole: R_HOLE 40 (was 24) is an open tube. The ball tips in at r < 54, when its edge reaches the lip (it was 35, with tight 0.15 s orbits and a 75 rad/s spin while falling). The fall takes 0.24 s: the ball slides inward 80 % along its momentum, its spin dies (theta' x e^(-9u)), it sinks 1.2 x the throat depth, and it is clipped into the hole ellipse, so it vanishes down the tube. No more orbiting after the lip.
- Visual depth profile: the 1/r well outside RK 130, then a STRAIGHT cone inside it at 0.92 x the steepest slope the 50 deg camera still sees. The near wall therefore never hides the ball (v2 hid it for half of each late lap). Throat depth 163 px (104 px screen drop). The marbles darken less with depth (0.22*d^2).
- Physics re-tuned for the bigger hole: C_DRAG 0.029 (was 0.038). The final lap period is ~0.33 s (it was 0.15) and each marble finishes on ~30 laps.
- s30: Mochi leads, 8-7 at 10 s and 30-26 when it drops at 19.50 s. Bolt passes at 20.96 s and drops at 21.01 s: Bolt wins 31-30. Clip 24.65 s (1479 frames).
- Sound = a BED from the trajectory (new additive lib/audio.py: synth_metal_tick, synth_metal_drop, metal_roll_bed). Nothing existing changed, so other scenes stay bit-identical.
  - Roll: two band-passed noise layers (body 350->850 Hz, sheen 2.2->4.8 kHz) with a 45 Hz grain. Centre and level follow speed (480-1180 px/s), panned by x.
  - A steel fret TICK per quarter lap, bigger on full laps.
  - The DROP: a clack on the lip + a 212 Hz tube tonk + a 4-tick rattle closing in.
- Events (subtle): mountain_king, one note per FULL lap at gain 0.16-0.24, and every quarter during the solo chase. Plus the flick pok and the win arpeggio. regen_audio cannot rebuild the bed from _events.json alone; re-render instead.
- Sounded (ticks + notes) per 1 s from 14 s: 22, 22, 23, 29, 28, 28, 26 (the race ends at 21.0 s). Fret ticks per 5 s: 24, 41, 68, 101. The chase is ~flat, not rising: one ball left. The roll's pitch and level still rise to the drop.
- Measured on the Full HD encode: h264 yuv420p 1080x1920 60 fps, -14.07 LUFS, peak -7.6 dBFS, last 1.3 s -91 dB, last 0.5 s silent. flash_check PASS (0). Pre-encode seam 0.11 (the flick frame); encoded seam 0.38.
- Delivered <VIDEOS_DIR>\batch10\funnel_race3.mp4 (funnel_race2.mp4 removed from batch10). Owner review: pending.
- Owner review 2026-10-04 (batch 11): Click/tick sound is GOOD; remove the constant shushing roll sound. Balls should circle longer at a big radius and, near the centre, drop in faster (fewer spins near the centre, not a faster ball). TODO.
