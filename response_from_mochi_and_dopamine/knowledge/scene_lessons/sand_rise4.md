# sand_rise4
- **v6 (owner chose option B, 2026-10-23): no x2.** A steady flood: "Every second the room fills with ~MORE~ balls" / "who gets out before the room is ~FULL~?".
  - The counter shows the true ball count. The x2 badges, the giant early count and the +N/s readout are gone.
  - Kept: rooms, ladders, Mochi the 70 % jumper (draw 1150) with her falls and the big late fall, the rope rescue, "again?", the Brahms bar lock, colours.
- **The flood:** a wide shower (240 px, spout at local x 150) from sim 2.0 s, the same pour in both rooms.
  - Its schedule `SCHED_N` (balls out at 0.25 s knots, piecewise linear, non-decreasing, 2,048 at 11.95 s) was calibrated offline by `calibrate(6)`. That is iterative learning over 5 runs: compare the pile level beside Bolt with `surface_target`, shift the schedule by the lagged error, smooth the rate. Best mean error 7.8 px.
  - The pour runs ~190 balls/s (a gentle ease-in), then tops the room up to FULL after the escape.
  - Every second the room holds more balls (true). The rate itself is near-steady, which is why the caption says "fills with MORE balls" and there is no +N/s.
- **Bolt:** a constant rung per beat (88 px/s) from sim 2.35 s, calm and sleepy. The surface target is his feet minus a gap that closes from 60 px at frame 0 to ~8 px by clip 3.8 s and stays there. So from ~clip 2.3 s the balls reach his heels before every step, and he steps up on the beat.
- **Gap feet → surface** (clip s, sampled every 0.25 s; negative = balls up to his ankles):
  - 3: 35, -9, 7, -25 · 4: 30, -5, 24, -4 · 5: 21, 12, -14, -5 · 6: 37, 15, 35, -8 · 7: 26, 8, 20, 7 · 8: 36, -5, 9.
  - He steps out at 8.77 with the balls at his knees (-106 as he leaves).
- FULL! moved to 12.0 sim (bar 13 downbeat) = clip 9.4.
- Timeline (clip s):
  - Mochi: hops 0.4 / 0.9, FALL 1.4, …, the big FALL 7.9.
  - Bolt out 8.77, FULL! 9.4.
  - Rescue: stomp 9.9, tugs 10.4-11.9, pop on the cadence 12.4, "again?" 12.5. Dissolve 13.4-14.0.
- v6 checks (encoded Full HD, 14.00 s):
  - -14.01 LUFS, peak -6.05 dBFS, last 0.5 s -240 dB.
  - RMS/s: -21.3 -19.1 -18.5 -19.0 -19.2 -17.5 -18.2 -17.6 -17.0 -16.3 -17.2 -16.9 -16.7, then -27.2 (tail).
  - Cadence -12.3 vs body -14.5. flash_check PASS (1).
  - Seam 5.55 vs adjacent frames 5.1-5.7 (the shower is ~100 moving comets): one normal step.
  - Frames read at 0 / 1 / 4 / 6 / 7 / 8 / 8.5 / 8.75 (escape) / 9.4 (FULL) / 10.9 (rope) / 12.6 ("again?").

## v5 (superseded by v6)
- **v5 (owner review of v4, 2026-10-23: "Bolt is slow at the start and then rushes; he must have a STEADY speed").** Everything else is as in v4.
- **Bolt: one constant pace.** One rung (44 px) on every beat (0.5 s) = 88 px/s, from sim 2.35 s (before frame 0) to the hatch. No waiting, no speed-ups.
  - Calm, sleepy face throughout. Each step takes 0.15 s (V_CLIMB 300 px/s).
  - A faint pulsing "!" sits at his heels while the balls are within ~40 px of his feet. He does not react.
- **Gap from Bolt's feet to the ball surface** (clip s): 0: 44 · 1: 132 · 2: 220 · 3: 283 · 4: 361 · 5: 428 · 6: 464 · 7: 468 · 8: 293 · 8.3: 94 · 8.5: 85 · 8.6: 53 · 8.7: 27 · 8.75: 14 px → out at 8.77.
  - The gap grows while the pile is small, then the doubling closes it from ~470 px to ~14 px in ~0.8 s.
  - A long near-touch stretch is not possible with an honest x2 pour and a steady climber: the pile height doubles every second, so it only catches a linear climber in the last surge. Starting Bolt later or slower just buries him.
- The EXIT sign is drawn behind the balls and climbers; it covered Bolt's face at the hatch.
- Lead banners only from sim 6.5 s, cut at the escape.
  - Race banners (clip s): MOCHI LEADS 5.1, BOLT LEADS 5.95, MOCHI LEADS 7.6, BOLT LEADS 8.45.
- Timeline (clip s):
  - Mochi: hops 0.4 / 0.9, FALL 1.4, …, the big FALL 7.9 (one rung under the hatch).
  - Bolt escapes 8.77. 2,048 at 8.4, FULL! 8.9.
  - Rescue: stomp 9.9, tugs 10.4-11.9, pop on the cadence 12.4, "again?" 12.5. Dissolve 13.4-14.0.
- v5 checks (encoded Full HD, 14.00 s, 840 frames):
  - -14.01 LUFS, peak -6.2 dBFS, last 0.5 s -240 dB.
  - RMS/s: -21.5 -18.7 -18.6 -19.0 -19.1 -17.5 -18.2 -17.7 -16.8 -16.6 -17.3 -16.9 -16.8, then -27.2 (hold fade + silent dissolve).
  - Cadence -12.4 vs body -14.4. flash_check PASS (1).
  - Seam 1.35 (Mochi is mid-hop at frame 0; adjacent frames there differ by 0.9-1.5).
  - Rooms inside 0.10-0.84 w.
  - Frames read at 1, 4, 6, 7, 8, 8.5, 8.7, 8.8 (escape), 8.9, 10.9, 12.6 s.

## v4 (superseded by v5)
- **v4 (owner review of v3, 2026-10-23).** Kept: x2 rainbow balls, rooms, ladders, FULL line, counts, Brahms sync, rope rescue.
  - The spout is back on the far side (local x 82). Next to the ladder its heap swamped Bolt.
- **MOCHI = the jumper.**
  - A jump on every beat (quarter = 0.5 s) from sim 1.5 s. Each jump is a 70 % draw from her own seeded RNG (`mochi_plan`, `MOCHI_SEED` 1150).
  - Hit = 3 rungs up in a 0.26 s hop. Miss = she reaches, misses, and tumbles 3-4 rungs down in 0.40 s (spinning, shocked face, then dizzy), and loses the next beat.
  - On screen: a small "70%" next to her for 0.16 s, then a green check or a red "FALL!" (gone by 0.5 s).
  - The draw was chosen with `plan_ok`: ahead early, two or more tumbles, the big tumble near the top late, never at the hatch first, overall hit rate 60-80 %. Draw 1150 hits 10 of 14 (71 %).
- **BOLT = the calm one.** Neutral face, sleepy lids (blink ≥ 0.42), no panic. He checks his feet on every 16th note and steps up only when the balls reach them (≥ 5 px above), clearing the level by up to 4 rungs. So the pile touches his feet at nearly every step; in the final surge it reaches his knees for ~0.4 s.
- **Ending:** Bolt pulls her out as before, but her line is now an annoyed **"again?"** speech bubble (white bubble, tail to her, 42 px), not "thanks.".
- Sound: Mochi hop = a short rising sine "hop" + a soft rung tick on landing. Tumble = 4 rung knocks falling in pitch + a falling bloop, then a soft thump. Bolt step = a soft tick + a light thump. No noise.
- Timeline (clip s; clip 0 = sim 2.6, 14.00 s, 840 frames):
  - Mochi hops 0.4 / 0.9, FALL 1.4, hop 2.4, FALL 2.9, hops 3.9 / 4.4 / 4.9, FALL 5.4, hops 6.4 / 6.9 / 7.4 (one rung under the hatch).
  - **Big FALL at 7.9** (rung 18 → 14). The pile swallows her.
  - Bolt's steps at 1.4, 4.8, 5.9, then several per second from 6.5.
  - Bolt takes the lead at 8.6 and **escapes at 8.7**. 2,048 at 8.4, **FULL! at 8.9**.
  - Rescue: stomp 9.9, tugs 10.4-11.9, pop on the final tonic at 12.4, "again?" from 12.5. Dissolve 13.4-14.0.
- v4 checks (encoded Full HD):
  - -14.01 LUFS, peak -6.0 dBFS, last 0.5 s -240 dB.
  - RMS/s: -22.5 -18.8 -19.5 -19.2 -19.1 -17.7 -18.1 -17.6 -16.7 -16.3 -17.1 -16.7 -16.6, then -27.1 (hold fade + silent dissolve).
  - Cadence -12.2 vs body -14.5. flash_check PASS (1).
  - Seam 1.36. The adjacent frames at the start already differ by 0.91 / 1.49 (Mochi mid-hop), so the seam is one normal step.
  - Frames read at 0 / 0.45 (hop + check) / 1.55 (FALL) / 2 / 5 / 7.95 (the big fall) / 8.3 (Bolt at the top, balls at his feet) / 8.7 (escape) / 8.9 (FULL) / 10.9 (rope) / 12.6 ("again?").

## v3 (superseded by v4)
- **v3 (owner review 2026-10-23: "nope — they swim up like it's nothing, needs something else there").**
  - Nobody floats now. Mochi and Bolt are heavier than the balls. The only way out is a LADDER on the back wall up to the hatch (local x 252, rungs every 44 px).
  - The spout moved over the ladder (local x 196), so the x2 pour rains on the climbers.
  - Kept: x2 balls, rooms, FULL line, counts, Brahms sync, the rope rescue.
- Climb model (`simulate`; tuned for seed 6, now the default):
  - Mochi pulls on every eighth note (0.62 rung). Bolt pulls a full rung on every quarter note. They start up at sim 1.8 s.
  - Every pull costs grip: a base amount, plus each ball that hit the upper body since the last pull, plus the quicksand drag (the pile level around the body, 0 at 0.15 R up to 1 at chest-deep).
    - Mochi: 0.02 + 0.0025/hit + 0.40·drag. Bolt: 0 + 0.0005/hit + 0.03·drag.
    - When grip runs out: SLIP! (Mochi down 2 rungs and a 0.45 s pause; Bolt 1 rung and 0.35 s).
  - Deep in the pile a pull can fail (strain, STUCK!).
  - Poses: pull-up stretch, slip shock (wow face, wobble), worried and sweating when buried, panic at chest-deep.
  - The loser buried > 1.2 R shows only the top of the head until the rope comes.
- Clip starts at sim 2.60 s (`CLIP0`, 5 balls; x2 → 8 at 0.4 s, 16 at 1.4 s, 32 at 2.4 s). Clip **14.00 s (840 frames)**.
- Timeline (clip s):
  - Mochi takes the lead at 0.95 (MOCHI LEADS!).
  - Mochi SLIP! at 5.15. Mochi SLIP! at 7.40, one pull from the hatch (the near miss).
  - Bolt passes at 7.90 and escapes at 7.93. Mochi is 0.31 m short; her hatch reads LOCKED at 8.13.
  - 2,048 at 8.4. FULL! at 8.9. Mochi is buried near the top.
  - Bolt hops 9.15-9.9 and stomps the hatch open at 9.9. Rope 9.9-10.3. Tugs 10.4 / 10.9 / 11.4 / 11.9.
  - Mochi pops out on the final tonic at 12.4: bored face, "thanks.", SAVED.
  - Hold to 13.4, dissolve to 14.0 (loop to the new frame 0).
- Sound additions: a rung grab = a soft glass tick an octave below the click pitch + a light thump (Bolt louder, on quarters; Mochi on eighths). A slip = a falling tonal bloop + a small clank + 3 ticks. A strain = a low thump.
- v3 checks (encoded Full HD):
  - h264 yuv420p 60 fps, 14.00 s. -14.01 LUFS, peak -6.0 dBFS, last 0.5 s -240 dB.
  - RMS/s: -21.2 -19.1 -18.7 -19.5 -19.1 -17.4 -18.1 -17.2 -16.7 -17.3 -17.3 -16.8 -16.7, then -27.1 (the hold fade + the silent dissolve).
  - Cadence -12.3 vs body -14.6. flash_check PASS (1). Seam 1.07.
  - Frames read at 0 / 1 / 2 / 5 / 5.2 (slip) / 7.45 (slip near the top) / 7.95 (escape) / 8.9 (FULL) / 10.9 (rope) / 12.5 (out).
- Doubts:
  - Bolt escapes 1 s before FULL, so he is not waist-deep when he gets out. The pile only reaches the climbers in the last surge (an exponential overtakes any steady climber at the very end). Mochi is the one caught by it.
  - The burial reads from ~9.0 s; at the FULL! frame her face is still visible for a moment.

## v2 (superseded by v3)
- **v2 (coordinator 2026-10-23, owner rule "no slow start"): the clip starts LATER in the SAME sim.** Clip 0 = sim 2.90 s (`CLIP0`): 7 balls out and pouring, the giant count on screen. The x2s land at clip 0.1 (8), 1.1 (16), 2.1 (32) … 8.1 (2,048). Nothing after it changed.
  - The music starts at bar 4 (bar-locked: every x2 still on a downbeat, cadence still on the rescue pop). Notes that start in the 0.15 s before the cut are kept, clamped to 0.
  - 2.90, not 3.00: at 3.00 frame 0 carried the fresh x2 badges and the 7→8 change, so the seam measured 2.82.
  - **Clip 13.70 s (822 frames).** Times in clip seconds = the v1 times below minus 2.9:
    - SINKING 4.08 / 5.40 / 6.65 / 7.92.
    - Lead changes B 6.93, M 7.50, B 7.98.
    - Bolt escapes 8.32 (Mochi 0.15 m short). 2,048 at 8.1, FULL! 8.6.
    - Stomp 9.6, tugs 10.1-11.6, pop + cadence 12.1, hold to 13.1, dissolve 13.1-13.7.
  - **v2 checks** (encoded): -14.01 LUFS, peak -5.95 dBFS, last 0.5 s -240 dB.
    - RMS/s: -22.6 -20.2 -19.7 -20.5 -17.3 -17.3 -17.4 -16.8 -16.3 -17.0 -17.1 -17.0 -17.0 (then the silent dissolve).
    - Cadence -12.2 vs body -14.2. flash_check PASS (1).
    - Seam mean delta 1.21. Adjacent frames at the start already differ by 0.95 (the glowing comets move), so the seam is ~1.3 normal steps, not a visible cut. It reads above check_clip's 1.1 band for that reason.
  - Frames read at 0 / 0.5 / 1 / 2 s / last: 7 / 10 / 14 / 29 / 7, with x2 on 0.1, 1.1 and 2.1.
- v1 (below) is the 16.60 s cut that started at sim 0.
- One-change sequel of sand_rise3 (6.5K views, our best after press_split2), inside the 14-day window. Same rooms, characters, choice and rope rescue. **The change: the sand is now glossy rainbow BALLS and the count in each room is exactly 2^t**: 1 at 0 s, 2 at 1 s ... 2,048 at 11 s. 2,048 balls fill a room, so the rooms stay nearly empty for ~7 s and then fill explosively (half the balls arrive in the last second).
- Caption (in-scene, fit to the side safe width): "Every second the balls ~DOUBLE~" / "who gets out before the room is ~FULL~?" (DOUBLE gold, FULL red).
- New file `scenes/sand_rise4.py`. No lib/, tools/ or sand_rise3 changes.

## Layout (side safe zone)
- Rooms 360 x 914 px, interiors x 128-488 and 528-888 (walls to ~121 / ~895), inside 0.10-0.84 w. Banners clamp to x 220-795; the caption fits 108-907.
- Floor y 1352, ceiling 438, roof 400. Spout at the outer side (local x 82), hatch 236 ± 52. Characters R 58.
- A red dashed FULL line under each ceiling plus a "FULL 2,048" label, visible from frame 0 (the end state).
- HUD: names and EXIT n m under the rooms, a centre "BALLS n" counter, and "x2" pops on every downbeat (under the counter and at both spouts).
- For t < 6.3 s, a giant gold count (250 px) with "BALLS" and a big "x2" sits across both rooms. It fades by ~7.9 s, when the pile takes over.

## Physics (sim once, ~11 s)
- Per-room position-based ball solver (press_split2 family), r = 6.5 ± 7 %:
  - Jacobi, 8 iterations, 2 substeps; the lower ball of a pair moves 0.3x.
  - A pairwise inelastic velocity pass (approaching speed removed, separating speed removed).
  - A touching ball may fall freely but not be launched: up ≤ 60 px/s, sideways ≤ 200 px/s.
  - Lone balls bounce off the floor and glass (e 0.62).
  - Sleep: still and supported for 8 frames → frozen. It wakes near a character or when touched by a fast ball.
- Lessons, measured: without the up-cap the pile boils. An absolute contact drag makes the jet hang in mid-air. Symmetric weights let a deep pile compress ~35 %.
- Pour: ball k leaves in the 16th-note slot ending at or after log2 k (spread over the last 60 % of the slot). So every downbeat m has exactly 2^m balls out (the counter is the spawned count).
  - Each ball takes the highest free slot in the stream under the nozzle, with the matching fall speed.
  - When the stream column is packed (the last ~0.3 s), it takes a random free spot above the pile.
  - The nozzle widens with the rate (stream width ≤ 230 px).
- Both rooms get the identical pour (fair test). The characters are kinematic discs that push balls.
  - Mochi out-jumps: hops, digs in on landing, sinks into the pit (SINKING! → POP!).
  - Bolt rides: he floats 0.3 R deep on the contiguous pile surface (a 6 px occupancy grid; balls in the air are not surface), plus small steps.
- Colour by arrival order: hue = 330°·sqrt(k/2048). Red/yellow strata at the bottom, magenta on top; the jet stirs the middle.
- Early balls (n < ~400) get comet trails and a glow (glow off by n ≈ 110), so 1-16 balls read on a phone.

## Timeline (seed 1, label fhd)
- 0.0 s: count 1 (ball in the air), Mochi mid-jump, Bolt mid-step. x2 at 1, 2, 3 … 11 s.
- SINKING 6.98 / 8.30 / 9.55 / 10.82 s.
- Lead changes: Bolt 9.83, Mochi 10.40, **Bolt 10.88**.
- **Bolt escapes at 11.22 s, Mochi 0.15 m short** (both read EXIT 0.2 m a moment before).
- 2,048 at 11.0 s (last x2, valves close). **FULL! at 11.5 s** (timpani hit), when the rooms are visibly packed. Mochi's hatch slams at 11.42 (LOCKED).
- Rescue: Bolt hops 11.75 / 12.0 / 12.25; stomps the lid open at 12.5; rope 12.5-12.9; tugs 13.0 / 13.5 / 14.0 / 14.5 (Mochi rises through the packed balls).
- **Mochi pops out on the final tonic, 15.0 s**, bored face, "thanks.", a few balls tumble off. SAVED.
- Hold to 16.0, then a 36-frame dissolve into the pre-roll. **Clip 16.60 s (996 frames).**

## Sound (music first)
- **Brahms, Hungarian Dance No. 5** (pub. 1869; d. 1897, PD). Bars 1-16, melody notes read from the score file `<SOUNDFONTS_DIR>\scores\brahms_hungarian5_dl\brahms-hungarian-dance-no5.mid` (flutetunes.com, F# minor, 2/4; SOURCE.txt there).
- One steady tempo: quarter = 0.5 s, bar = 1 s. Every x2 is a downbeat; the cadence (bar 16 tonic) = the rescue pop.
- Arrangement (lib/orchestra, MuseScore_General MIT), ours:
  - Violin melody for bars 1-8; strings + violin + clarinet an octave down for bars 9-16.
  - Pizzicato oom-pah plus contrabass (cello for bars 1-2).
  - Timpani on the downbeats from bar 5, a roll into 11 s, a reverse cymbal + crash on 11.0, timpani on FULL.
  - Horns + choir pads from bar 9.
  - Tutti F#m cadence at 15.0 (timp, boom, crash).
- SFX: tonal ball clicks only, no noise beds. Each click is a sine + 2.76x partial, 8-11 ms, pitched to a chord tone of the current bar at 1.1-2.2 kHz, rate-capped 34-42 ms.
  - Mochi landings: click clusters + a soft thump. Sink: a low bloop. Pop: a tonal blip.
  - Doubling: a soft glass ping climbing the chord.
  - Hatch: clank. Hops: poks. Tugs: thumps. A soft pfff after the pop.
- master(peak_db=None); post-master fade so the last 0.5 s is digital silence.

## Checks (encoded Full HD, output/sand_rise4_fhd_9x16.mp4)
- h264 yuv420p 1080x1920, 60 fps, 16.60 s.
- -14.01 LUFS, peak -6.0 dBFS, last 0.5 s -240 dB.
- RMS per second: -22.0 -20.9 -20.5 -19.8 -19.0 -19.3 -19.7 -17.2 -16.9 -17.0 -16.4 -16.2 -16.9 -16.9 -16.8 -17.1 (the 16th second is the silent dissolve). Climbing, no second below -24.
- Cadence short-term -12.1 vs body median -14.7 (+2.6 dB).
- flash_check PASS (1 flash max per second). Seam mean delta 0.64.
- check_clip: events per 5 s 93 / 192 / 57 (rescue section); 51 melody notes, 13 distinct.
- Frames read from the encoded file at 0, 0.5, 1, 2, 6, 10.4, 11.25, 11.5, 13, 15.1, 16.58 s, plus 1:1 crops at 10.4 and 11.2 s.
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch48\sand_rise4.mp4`. Owner review: pending.

## Doubts
- The honest exponential makes the first ~6 s sparse (1-64 balls). The giant doubling count, the comet trails and the music carry it. If the owner finds the start empty, the next step is a different ball size or room (fewer doublings), not faking the count.
- 16.6 s is the honest ladder (11 doublings + rescue).
- Melody source is a flutetunes transcription (as galton_board), not Mutopia/IMSLP; none of those has a MIDI of this piece.

Owner review (2026-10-23): "nope, they swim up like it is nothing, needs something else" -> rework: make the escape a real struggle.

Owner review (2026-10-23): "Mochi jumps/skips rungs fast with a chance to fall several steps (explain the % on screen if short, or in the comments); Bolt climbs calmly while the balls almost catch him every time (stressful); at the end Mochi says "again?" instead of thanks" -> v4.

Owner review (2026-10-23): v4 "Bolt is slow at the start then rushes; he must have a steady speed that keeps the balls nearly catching him" -> v5.
