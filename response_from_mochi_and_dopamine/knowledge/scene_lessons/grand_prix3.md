# grand_prix3 — MARBLE CRUSHER FACTORY (Team Mochi vs Team Bolt)

- NEW format for the Grand Prix franchise, made after the owner rejected grand_prix2 ("must not look like the old one, change obstacles completely, more complex"; near-duplicate sequels don't work).
  - ONE fixed screen with no scrolling: a closed-circuit marble MACHINE in steel and brass on a dark violet plate.
  - The marbles lap it again and again.
  - It shares no obstacle with v1/v2: no pegs, spinner, see-saw, gaps or trapdoor.
- Circuit:
  1. bucket ELEVATOR (LIFT, left edge, 1100 px/s, a bucket every 0.25 s);
  2. CONVEYOR BELT (300 px/s, tangential friction to belt speed) under CRUSHER A;
  3. C-bend, then a ramp under a swinging PENDULUM HAMMER (+-1.25 rad, 1.6 s) that swats marbles back or forward;
  4. drop shaft with an absorbing back wall and a J-curve;
  5. LOOP-THE-LOOP (marble-centre radius 52; entry ~920 px/s, needs 661);
  6. C-bend, then the ramp under CRUSHER B;
  7. elevator foot.
- Rule: under a crusher when it slams = SQUASHED flat = OUT. Last team standing wins.
  - The crushers speed up: f = f0 (1 + t/12), with f0 0.50 (A) and 0.55 (B).
  - Each cycle: slam in 0.04 of the cycle, down until 0.45, rise until 0.60, up for the rest.
  - Marbles queue at a lowered crusher (the belt or gravity pushes) and dash under when it lifts. The one caught under pays.
- Physics notes:
  - C-bends, the J-curve and the loop are ANALYTIC circle constraints. Polyline arcs lose ~cos(kink) per joint and kill the loop speed.
  - The loop flag needs a done-latch and a d > RM+30 escape, or it re-captures marbles far away.
  - Crusher side contacts are capped at 650 px/s (the pinch otherwise spat marbles out at 2000+).
  - The drop wall must have e=0, or the bounce lands marbles inside the J and bleeds speed.
- Frame 0 is MID-ACTION: WARM 2.0 s. The marble stream is already on the belt heading into crusher A, and the first squash lands at 0.48 s. Crushers park UP (phase 0.7) until their first cycle.
- Loop: a seamless 0.5 s DISSOLVE into the sim pre-roll, with audio placed the same way. Pre-encode seam 0.73 against neighbours 0.67/0.75. The encoded seam is 1.03 against a normal step of 0.78 (the I-frame step).
- Teams are assigned after the sim over all 252 5/5 splits. The story needs:
  - the end in 12.5-16.5 s;
  - the winner losing at least 2;
  - Score: a 1v1 final, lead changes and ties, first squash under 1 s, both crushers lethal.
  - Search 3000 seeds: 1673 pass, with little variety between seeds. The machine resynchronises through the elevator.
- s1473 (default): squashes 0.48 M(A), 2.27 B(A), 5.41 B(B), 6.62 M+M (a double squash), 9.86 B, 10.83 B, 13.22 M(A), 15.06 M(A).
  - Count: 4-5, 4-4, 4-3, 2-3, 2-2, 2-1, 1-1, then BOLT WINS with 1 marble left.
  - Clip 16.82 s (1009 f).
- Sound: contact sounds only, with NO rolling, whoosh or hiss bed.
  - Glass clicks for marble-track and marble-marble hits.
  - Steel tocks on bends, walls and the J.
  - A wooden BONK for the hammer.
  - A crusher CLANK (synth_clank) on every slam, never dropped.
  - Metal ticks for the elevator pick and drop and the crusher lift.
  - Marimba DING per squash (an octave pair rising through a pentatonic scale), plus a win arpeggio.
- Checks (encoded Full HD):
  - h264 yuv420p 1080x1920 60 fps.
  - -13.95 LUFS, peak -4.08 dBFS. RMS climbs -17.3 to -14.9 dB.
  - flash_check 0 = PASS.
  - Sounded events/5 s: 56/48/40.
- Safe zone: the machine sits at x 90-935 and screen y 395-1290. The HUD is shifted left: faces at x 100/840, the centre label at 470. Nothing key is in the right-edge strip.
- Args: --seed (1473), --label, --cap ("Get SQUASHED = OUT|~Last team standing WINS~"), --voice, --search N [--start], --stats N, --still --frame.
- Delivered <VIDEOS_DIR>\batch35\grand_prix3.mp4 (Full HD). Owner review: pending.

Owner review (2026-10-15): no squashing; instead small openings that let balls out by some logic, otherwise another lap; first team whose balls ALL leave wins -> grand_prix4.
- Owner review 2026-10-15: "instead of squashing, make some small openings based on some logic, and sometimes balls get out from that, sometimes go around another circle; first whose all balls leave wins" -> grand_prix4 (exit factory).
