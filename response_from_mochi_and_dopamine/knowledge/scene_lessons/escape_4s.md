# escape_4s
- New scene (batch40). It rebuilds the genre hit "each ball has only 4 seconds to escape" (36.7M, research/simple_viral_formula.md §4) to the BRIEF_batch25 RESEARCH RULES. **PURE MECHANIC, no characters.** It is the opposite of ring_escape2 (dark, small, text-heavy): one big rainbow ring on pure black, 2 caption lines, 1 readout and 1 icon row.
- Caption (baked, `--cap`; `--cap ''` = base): `Each ball gets only ^4 SECONDS^|~Escape, or it SHATTERS~`.
- HUD:
  - The readout `LEVEL n/4 · TRY n` sits at y 1386. In the finale it reads `ALL 4 LEVELS ESCAPED` and fades out before the loop dissolve.
  - The queue row at y 300 holds one ball per try, in rainbow order. A ball is bright while it waits, an empty socket while it plays, a dim chip once shattered, and gold-ringed once escaped (the escaped ball flies back to its slot).

## World (logical px, ring centre 520, 842)
- **Rings:** the outer ring has R 440 and a tube 18 thick, spanning x 71-969 (0.83 w); the nested inner ring has R 292.
  - Each ring is a full rainbow along its arc, which turns with the ring. The hue offset changes per level.
  - Rings are drawn as 40 segments × 5 strokes: glow, dark edge, core and sheen.
- **Countdown:** an arc at R 482 drains clockwise from the top, from 4.0 to 0. It goes white → gold → coral, has a bright bead at the tip and brightens on every second tick.
  - A big faint digit (4/3/2/1, alpha 0.13) sits behind the ring centre.
  - The arc's outer edge reaches x 1006 and brushes the right strip as decoration.
- **Ball:** r 27, coloured by its queue hue, with a white-hot core, a hugging halo and a 6-11 point trail.
- **Debris and banners:**
  - TIME! = 16 ball-colour triangles + 10 chips.
  - A ring break = curved rainbow arc pieces + 10 chips.
  - Banners are 96 px and start at 0.9x scale.
  - Shards fade out before they reach the caption.

## Physics (one model; px, s; G 2600)
- Perfectly elastic and frictionless. A ring is a thick arc with round end caps. The inner face moves tangentially, so it adds no energy. A gap EDGE is a moving obstacle, resolved in its own frame (an honest kick). 12 substeps per frame.
- **Ball n:** released at the centre in a seeded direction at v = 2200 · 1.045^n px/s (2200 → 3129 for ball 9).
- **TIME!:** after 4.0 physics-s the ball shatters, and the next ball is released 0.32 s later. It flies in from its queue slot for 0.30 s.
- **Escape:** the ball's centre clears the outer face (R + TH/2 + 2) of the level's last ring → ESCAPED!, and the ring shatters.
  - The next level's ring forms at +0.14 s (scale 1.18 → 1, 0.3 s), and the next ball is released at +0.62 s.
  - On the nested level, passing the inner ring shatters it. It re-forms for the next ball.
- **Levels** (gap of arc, spin rad/s):

| Level | Rings | Gap | Spin |
|---|---|---|---|
| 1 | one | 34° | 0.85 |
| 2 | one | 26° | −1.25 |
| 3 | one | 20° | 1.70 |
| 4 | two nested | 34° inside / 22° outside | −1.5 / +1.15 (counter-rotating) |

- Measured per-try escape chance (300 tries): L1 0.60, L2 0.48-0.62, L3 0.36-0.60, L4 0.21-0.43. A faster ball hits more often, so the gaps shrink faster than the balls speed up.
- **Seed search** (`--search N --jobs 2`, ~4 min for 40k seeds). Filters:
  - The note count at the final escape equals a melody CADENCE index (101/111/135/203).
  - Length 30-48 s.
  - Tries per level non-decreasing, with the last level ≥ 3 and more than the first.
  - Rate in the last 6 s ≥ 1.3x the first 6 s.
  - vmax < 3800, ≥ 4 gap-edge near-misses.
  - The first escape is at ≥ 1.0 s clip, no escape comes in < 0.9 s, and the final escape has ≤ 1.2 s left.
  - Result: 8 of 40,000 seeds pass.
- **s19664** (default):

| Try | Level | Clip s | Outcome |
|---|---|---|---|
| 1 | 1 | 0.05 → 4.05 | TIME |
| 2 | 1 | 4.37 → 5.58 | ESCAPED |
| 3 | 2 | 6.20 → 10.20 | TIME |
| 4 | 2 | 10.52 → 14.46 | ESCAPED with 0.06 s left |
| 5 | 3 | 15.08 → 19.08 | TIME |
| 6 | 3 | 19.40 → 21.96 | ESCAPED |
| 7 | 4 | 22.58 → 26.58 | TIME |
| 8 | 4 | 26.90 → 30.90 | TIME |
| 9 | 4 | 31.22 → 34.99 | ESCAPED with 0.23 s left |

  - Tries per level: 2/2/2/3.
  - 135 bounce notes; the first bounce is at 0.215 s.
  - Notes per 5 s: 13 / 12 / 15 / 15 / 23 / 29 / 28 (2.3/s → 5.8/s).
  - 7 gap-edge near-misses, vmax 3330 px/s.

## Finale (final escape + 0 → 3.5 s)
- The outer ring shatters (1.3x shard speed), and the timer arc and the digit fade out.
- The winner curves to the centre over 1.25 s, while 70 motes (14 per ring, in the ring hues) swirl in from the old ring radii.
- At the BLOOM there is a soft gold glow (alpha ≤ 0.32), and 7 rainbow rings of light expand out to R 164-440. The ball grows 1.45x, turns gold and bobs.
- The camera zooms 1.0 → 1.14 → 1.0. A 0.6 s dissolve leads into the pre-roll: ball 1 flies from the queue into the level-1 ring.

## Sound
- **Melody:** J. S. Bach, Badinerie (Orchestral Suite No. 2 in B minor, BWV 1067; PD).
  - **Source:** the IMSLP PMLP99998 "Menuet & Badinerie (organ, Gouin)" MIDI `PMLP99998-Bach_1067_7.Badinerie.mid`. Its licence is CC BY-SA 4.0 (Pierre Gouin, Les Éditions Outremontaises 2015). The composition is PD; we take only the note data and credit the file.
  - IMSLP's /images/ host is behind a bot check, so the file came from the Wayback copy. Its sha1 `57fa4533…e06` equals the sha1 IMSLP's API reports. It is cached in `<SOUNDFONTS_DIR>\scores\bach_badinerie\`, together with the 2-harpsichord Gouin MIDI.
  - Track 1 (the flute line) gives LEAD: 242 onsets, A section + repeat + start of B. Track 2 gives BASS (Bach's bass, 149 onsets). `--verify`: **both match the MIDI: True.**
  - The melody is an octave down (F#3-D5, top note D5); the bass is folded to C2-F#3.
- One note per wall bounce, with contacts closer than 45 ms counted as one. Note 135 (B3, the bar-22 cadence on the tonic, beat 43) lands on the FINAL escape.
- Bach's bass is placed between the bounce notes by beat (piecewise-linear beat → time), so the harmony is the score's own.
- **Instruments:**
  - Soundfont piano lead; the velocity rises per level, and a near-miss accents it.
  - From level 3 a harp doubles the tune at pitch.
  - Pizz bass + a soft strings_slow line an octave up.
- **ESCAPED!:** a rising harp run B3-D4-F#4-B4-D5 + a celesta touch. Final: contrabass B1 + timpani B2. Bloom: a rich B-minor chord (strings, choir, rolled piano, harp; top D5) + a soft boom + a B4 glass-harp chime.
- **SFX (synth, +12 ms off every note):**
  - A soft wood-block tock at 3/2/1 s left (1.18 kHz; the last one is 0.99 kHz and a touch louder).
  - TIME! = a glassy shatter with tinkles. ESCAPED! = a bigger, brighter shatter. A small shatter plays on the inner-ring break.
  - A soft glass tik on each near-miss. No hiss or whoosh.
- Mastering: `master(reverb 0.5, peak_db −6)`, −14 LUFS, the last 1.0 s is digital silence. Energy above 3 kHz is 0.12%.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (0.20) `--search N --from S --jobs J (≤2) --all --verify`. Physics: `--g --v0 --vk --gap1 --gap2 --gap3 --gap4i --gap4`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 2346 frames = 39.10 s.
- −14.00 LUFS, peak −8.0 dBFS. The last 0.5 s is digital silence; the last non-zero sample is at 38.08 s. RMS per 3 s: −18.1 → −15.6 (it builds).
- flash_check PASS (0 flashes, mean lum 0.008).
- **Loop:** encoded seam mean delta 0.69 (good band 0.12-0.72). The last frame is pre-roll frame −1.
- The first audio onset is at 0.215 s, equal to the first bounce (0.215 s).
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 4.1 (TIME!) / 5.65 and 14.5 (ESCAPED!) / 33.5 (nested level) / 36.4 (bloom). Fast stills were also read at the inner-ring break, the final escape, the bloom rings and the dissolve.
- Safe zone:
  - The caption is at y 172-245 and the queue row at 283-317.
  - The ring and timer span y 360-1324 (≤ 0.69 h). The readout is at 1386 (0.72 h).
- Render ~3 min at Full HD, single process, x264 at 2 threads.

## Doubts
- Frame 0 shows ball 1 just released at the centre (0.05 s before the release completes); its first bounce is at 0.215 s. It is moving, but not yet "mid-bounce".
- Tries per level are 2/2/2/3: they rise only on the last level. With the first three levels at 1 try each (more common), the video would be all failures in level 4.
- 39 s is longer than the 15-20 s data rule, but it fits the attempts format (30-50 s, brief). Every TIME! costs a fixed 4 s by definition.
- The MIDI is CC BY-SA, not "PD dedicated". The note data of a PD work is not copyrightable, but the pinned comment credits the file anyway.
- The queue row icons are small (r 13). They are readable as a progress row, but not individually at a glance.

Delivered `<VIDEOS_DIR>\batch40\escape_4s.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-17): "boring, just circle and ball escape, already done" -> dropped.
