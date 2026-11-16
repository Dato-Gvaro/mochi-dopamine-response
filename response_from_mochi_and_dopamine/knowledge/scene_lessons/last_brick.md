# last_brick
- New scene (batch38), built on the research rules (research/simple_viral_formula.md; docs/BRIEF_batch25.md RESEARCH RULES). **PURE MECHANIC, no characters.** Persistence to COMPLETION: the box has to be emptied to the very last brick.
- Caption (baked, `--cap`; `--cap ''` = base): `Every brick must go|~Even the LAST one~` (line 2 gold). One readout: `BRICKS LEFT n` (y 326, gold + pulsing for the last 10). Nothing else, apart from a `100%` pop in the finale.

## World (black stage)
- Box interior x 60-1020 (0.89 w), y 352-1352 (bottom 0.704 h). 24 x 50 = **1200 bricks**, cells 40 x 20, drawn 37 x 17 with a light top edge.
- Rainbow: hue = 0.83 x (0.78 row + 0.22 col), red top-left → violet bottom-right. 6+ hues at frame 0.
- Frame 0: the full wall with ONE glowing ball (r 9) already in a small tunnel at the centre (17 bricks carved in a 0.6 s pre-roll), breaking a brick every few frames.

## Physics (one model; px, s)
- Constant speed 1000 px/s; elastic reflection off the walls and off bricks (the averaged contact normal of the bricks touched in the substep). **Every brick a ball touches breaks.** Balls pass through each other.
- **Escalation (one rung type): every ball splits in two** (same speed, ±0.5 rad) when the broken count passes 30, 90, 200, 350, 550, 800, 1050 → 1, 2, 4 … 128 balls. Each split shows a small gold ring per ball and a soft timpani D.
- Substep 1/480 s, positions recorded at 240 Hz. The seed sets only the launch angle (+ debris).
- Speed ramp: real time, except a mild ×0.5 from 0.40 physics-s before the final brick (owner rejects slow-mo finishes: never go below 0.5); ×0.65 through the finale. One physics clock.
- The last 10 bricks glow and pulse; with 1 left a pulsing gold ring marks it and it gets a white rim after every near miss (a ball passing within 26 px without touching).

## Finale
- The final brick bursts into a 150-shard rainbow fountain, a soft glow, and 5 rainbow rings.
- Each ball bursts into 6 sparks as a wave (1500 px/s) from the last brick passes it.
- `100%` pops in gold (170 px, starting at 0.85x).
- Rainbow light refills the box from the last brick outward, as a ghost of the wall at alpha 0.24. The brightness only rises from here to frame 0, which keeps it flash-safe.
- Zoom 1.0 → 1.05 on the box centre. Final brick + 3.0 s → a 0.6 s dissolve into the pre-roll (full wall, ball just starting) = frame 0.

## Sound
- **Melody:** J.S. Bach, *Toccata and Fugue in D minor* BWV 565, beats 0-44 (bars 1-12): the Adagio opening, the Prestissimo triplets, the diminished chord and the run down to the D-minor cadence. That is **179 onsets** after merging the three staves.
  - **Source:** Mutopia Project id 1780 (Bach-Gesellschaft Ausgabe 1867), Public Domain: `mutopiaproject.org/ftp/BachJS/BWV565/ToccataFugue/ToccataFugue.mid` (local copy `<SOUNDFONTS_DIR>\scores\bach_toccata\`). It is read at runtime with `orc.read_midi`.
  - Two ornaments are realised from the LilyPond source (`ToccataFugue.ly`) because the MIDI does not play them: the `\prall` on each opening A as A-G-A, and the `\arpeggio` on the bar-2 diminished chord as an upward roll.
  - Octave doublings above G5 are dropped, so the top note is G5 (79).
- **Note per break:** the breaks are clustered into exactly 179 onsets. Greedy, with a min gap shrinking 0.20 → 0.07 s across the clip (scaled by bisection), which makes an accelerando.
  - The **final brick is always the last onset = the D-minor cadence** (D2 D3 D4 F4).
  - Each note is held until the onset where its written duration ends (capped at 1.4 s), so the score's pedal D and held chords sound.
  - Instrument: Church Organ (MuseScore_General, MIT), warmed. The whole bed goes through a zero-phase 2nd-order Butterworth low-pass at 2.6 kHz (`--lp`), and the SFX through one at 3.2 kHz. The owner dislikes shrill sound; without this the organ put 4.6% of its energy above 3 kHz.
- **Finale:** a rich D minor is added: strings swell (D2-F4), voice oohs, contrabass D2, timpani D2 and a soft boom.
- **SFX:** a glassy crunch per break cluster (min gap 45 ms; gain grows with cluster size), core_drop's recipe (partials 0.9-2.6 kHz + a low-passed 18 ms snap + a body thump). It is placed +12 ms off the notes and never within 10 ms of a melody onset. No hiss, whoosh or drone.
- -14 LUFS (master), with the last 1.0 s digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (SFX level 0.16). Physics: `--v --splits`.

## Seed 9 (default): numbers
- Clip 29.68 s (1781 frames). The first break comes at 0.0 s; 17 bricks are broken in the pre-roll.
- Splits at 0.79 / 3.83 / 8.39 / 12.22 / 16.07 / 19.47 / 21.95 s (→ 128 balls).
- Breaks per 2 s: 43 33 49 50 72 77 117 87 150 168 193 133 | 9 1.
- Melody notes per 2 s: 9 10 11 10 12 13 14 15 18 18 21 22 | 5 1 (accelerando). Gaps: min 0.071 s, median 0.128 s.
- Hunt: 10 left at 23.99 s, 1 left at 24.98 s. The final brick is the top-left corner cell (0,0), at **26.08 s**. 10 left → 0 takes 2.09 s; the last one takes 1.09 s (incl. the 0.5x), with 2 near misses (22 and 25 px).
- The last brick is always a corner cell (balls rarely enter corners). Seeds whose last brick lands in col 23 (the right-edge UI strip) are out; seeds 6 (32.0 s, 3 near misses) and 2 (last brick bottom-left) are alternatives.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1781 frames. Render ~45 s.
- -14.00 LUFS, peak -4.35 dBFS, last ~1 s digital silence. Energy above 3 kHz is **0.29%** (core_drop 0.13%).
- flash_check PASS (1 flash in the worst second: the dissolve back to the full wall at 29.3 s).
- Seam: pre-encode last → 0 has a mean delta of 0.222, the same as a normal 0→1 step (0.214), so the seam is exact by construction. check_loop prints MISMATCH only because one frame of motion is more than its 0.2% pixel threshold. Encoded seam: 1.50 (I-frame).
- Safe zone: caption y 172-245, readout 326, box y 352-1352 (≤ 0.704 h). The finale zoom (1.05) pushes the box edge to ~1376, which is decorative only.

## Doubts
- The break rate falls over the last ~4 s (100 left → 0) because the leftovers sit in corners. 10 → 0 is the intended ~2.4 s hunt. The 24-26 s stretch (the mop-up) is the softest moment.
- 128 balls at the end is a swarm. It reads as "everything hunting one brick", but it is dense.
- The organ is low-passed to 0.29% above 3 kHz and not transposed (top note G5). If it now sounds muffled, raise `--lp`.
- The Toccata has already been used on the channel (chladni_plate2, halloween_switch, neon_trails).

Delivered `<VIDEOS_DIR>\batch38\last_brick.mp4` (since superseded by last_brick2).

## Owner review (2026-10-16)
"ok — make our characters appear somewhere, and instead of music use a tik-tik ASMR sound of breaking." Built as last_brick2 (spectators Mochi & Bolt + ASMR breaking, no music), which replaced last_brick.mp4 in batch38. Earlier coordinator fixes in this file: the final hit 0.3x → 0.5x (the owner rejects slow-mo finishes) and the organ low-passed.
