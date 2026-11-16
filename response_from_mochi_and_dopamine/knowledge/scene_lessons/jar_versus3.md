# jar_versus3 — CHAINSAW vs JACKHAMMER, both dropped in (batch70)

- Brief: docs/BRIEF_batch70.md §1 (owner on jar_versus2: the saw must DROP in from high and bounce around much more; Bolt gets a JACKHAMMER, no blender: dig to the bottom, JUMP back up, dig again). New file `scenes/jar_versus3.py` (from jar_versus2.py; v2 untouched).
- Caption: "Every ball the tool touches ~SPLITS~ in 2" / "~CHAINSAW~ or ~JACKHAMMER~: who finishes first?"; "GOAL: 100% small balls" from frame 0.

## Rules (one set for both jars)
- Same settled pile (27 big balls r 36, seed 1; settled with proper PBD velocities, so not v2's pile). A tool touch splits a ball in 2 (r/√2, area kept); a ball hit with closing speed > 650 px/s splits too (v2: 900). 5 splits to "small" (1 big = 32 small, r 6.4). Meter = % of ball area at the smallest size.
- Both tools: 18 big balls' mass, dropped from just under the lid already falling at 240 px/s (frame 0 = mid-fall, first contact ~0.5 s). Same dial: 25 % → 100 % over 8 s.
- CHAINSAW: v2's rigid body + chain friction; engine shake 8,000 px/s² (v2 3,000); NEW: jar hits are bouncy (impulse at the contact, restitution 0.55, so corner hits spin it).
- JACKHAMMER: upright free body (translation only). The bit slides out 22 px in 0.015 s (a blow, 1,470 px/s) and back; 9 blows/s × the dial. Contacts are mass-weighted PBD: a blow into the pile moves the light balls; a blow onto the rigid jar floor moves the HAMMER (the floor does not give) = its jump. No scripted jump.

## Honest result (seed 1)
- % small saw/hammer per s: 0/0 0/2 21/18 33/46 44/58 60/61 68/75 91/76 97/80 100/84.
- Lead changes: JACKHAMMER 2.1 s, SAW 6.13 s. **100 % SMALL at 10.42 s: MOCHI (saw) WINS**; the hammer is at 84 % then, 87 % at the end.
- Hammer cycle (tip y): floor (1,270-1,288) → jumps to ~770-880 (~400-500 px up) → digs back down, every ~1.3-1.5 s, 7 cycles. The saw is thrown up to y 520-560 several times.
- Seeds 2 / 3: saw wins at 12.2 / 13.9 s (hammer 94-97 %). The hammer drills one column and only gets the side balls that fall into its hole: it loses the tail every time.

## Sound
- Mozart, Figaro overture (PD; midiworld note source as ol_brick_breakout, our arrangement): bars 1-7 (theme, lifted ×1.9) + bars 12-17 (tutti), one tempo (quarter 0.2 s), bar 18's D-major downbeat on 100 %, + D-major tutti/timp/boom/crash. Split clicks (v2) + a tonal 118 Hz knock + 760 Hz tick per jackhammer blow that touches something.

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 817 frames = 13.62 s. −14.01 LUFS, peak −5.1 dBFS, last 0.5 s −67 dBFS. flash_check 0 = PASS. Seam 0.59.
- RMS/s −18.7 −18.2 −17.6 −18.4 −18.3 −17.9 −16.8 −17.6 −17.8 −19.3 −14.1 −14.0 −28.1 (hold/dissolve).
- Frames read: 0, 0.6, 2.2, 2.5 (1:1 crop), 6.2, 10.45, 11.6.

## Doubts
- Split rate peaks at 1-6 s and falls in the last 3 s (91 → 100 %): the coupon-collector tail. The rule "rate climbing to the end" is not met.
- 650 px/s impact splitting is what makes the cascades; 500 turns it into a chain reaction that ends in 5 s; 800 runs 17 s.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\jar_versus3.mp4`. Owner review: pending.
