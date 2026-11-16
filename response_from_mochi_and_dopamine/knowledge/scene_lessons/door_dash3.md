# door_dash3: a short race down 12 levels, a different glowing part on each

- Built from the owner's review of door_dash2: "good but repetitive, make the fall WAY shorter, or change things along the way". It also uses the new look direction (ring_escape2: jewel glow on a dark stage). door_dash.py and door_dash2.py are untouched.
- Rule: two shafts (Mochi left, Bolt right), one steel ball each. 12 levels, 260 px apart, and every level is a DIFFERENT part. The first ball to land on the checkered gate wins. The shaft is a ring (the finish gate is the start gate), so the loop is perfect, and the camera is a centred gaussian over the periodic timeline (v1/v2 machinery). Caption "12 levels, 12 DIFFERENT parts|~First to the bottom WINS~".
- Parts, top to bottom. Each has its own jewel colour and sound:
  1. door (amber): sliding halves. Latch click.
  2. trap (ruby): flaps drop open. Clunk.
  3. bumpers (orchid): kick 140, e 0.6. Glass bell.
  4. shuttle (teal): a plate whose 100 px hole slides in from the wall. Slide + stop ticks.
  5. wheel (citrine): 4 vanes, carries the ball round. Vane ticks.
  6. flip (amethyst): a floor that turns 180 deg in 0.46 s and dumps the ball. Clunk + tick.
  7. ramps (peridot): zig-zag, gravity roll. Roll ticks.
  8. piston (sapphire): a ram shoves the ball off a ledge into a wall hole. CLANK.
  9. belt (emerald): carries the ball to the far hole. Slat ticks.
  10. disc (fire opal): one notch. The ball waits wedged at the wall until the notch comes round, then rides it down. Clunk.
  11. pins (ice): 2 centre pins + 2 wall pins. Pings.
  12. funnel (rose): a V into a timed gate. Click.
- Timed parts (door, trap, shuttle, flip, piston, funnel) are steered by the v2 DIRECTOR. Flip and piston are always waits (a "pass" would mean landing mid-motion).
- Geometry lessons (ball 88 px, shaft 292 px):
  - Every passage must be >= ~96 px.
  - The ramps need >= 98 px between ramp A's tip and ramp B (v1 of the layout wedged the ball at 85 px).
  - A centre-pivot tilting tray cannot work in this width: the gap at the wall stays < 88 px until the tray is near vertical.
  - A pendulum hammer can pin the ball against the wall.
  - Rolling friction 0.9995 per substep (0.997 made the ramps crawl).
- Look:
  - Stage: navy -> plum with faint specks. Dark glass shafts tinted warmer with depth; the jump is hidden under the gate.
  - Parts: glowing jewel tubes (glow strokes -> dark edge -> core -> sheen), plus a glow kick (0.35 s) when a part fires on a ball. Bumpers and pins flash.
  - Hits: a bloom + 4-8 sparks in the part's colour.
  - Balls: steel with a halo and a short trail in the owner's colour. Walls carry an owner-colour neon line.
  - Floor: dark with a lilac edge. Banner "BOLT" (150) over "WINS!" (170).
- s42: Bolt wins at 14.22 s, Mochi lands 0.35 s later.
  - Story: Mochi leads early and again around 8-9 s; Bolt takes the lead at 12.2 s.
  - Syncs at 4.97 s (shuttle) and 9.67 s (piston); synced passes at 5.35, 6.03, 9.93, 10.77 s, each a centred chord + "SYNC!".
  - Lead changes 4, max spread 2 levels. Clip 17.02 s (1021 frames).
- Passes/5 s (both): 10, 13. Sounded/5 s: 54, 102.
- Sound: Habanera (PD Bizet) marimba note per level passed; woody TOK (ratchet) on wood/plate landings. Everything else is a scene-side bed: metal ticks, synth_latch, synth_clank, synth_ratchet, glassharp bells and pings. Stem RMS: notes -23, toks -34, bed -27 dB.
- Checks (Full HD encode): h264 yuv420p 1080x1920 60 fps.
  - Loudness: -14.01 LUFS, peak -5.8 dBFS. Last 1.3 s -47 dBFS, last 0.5 s -84 dBFS.
  - flash_check 0 = PASS (mean lum 0.028).
  - Seam 2.00 vs neighbours 1.81 / 2.15 (continuous scroll).
  - Onsets 76/76 events within 30 ms.
- Search `--search N`: Bolt wins, t_w 12.8-16 s, gap 0.12-0.8 s, both syncs, spread <= 2, >= 2 lead changes. Only ~2 % of seeds pass. Any geometry change reshuffles every seed (bumpers and pins are chaotic).
- Args: --seed (42), --label, --cap, --melody, --voice, --search, --still --frame.
- Delivered <VIDEOS_DIR>\batch14\door_dash3.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-06: OK, but replace the 12-level score with progress toward a FINISH LINE (a track line with a finish at the end, showing each ball's progress) -> door_dash4 (shipped 4K for 2026-10-10).
