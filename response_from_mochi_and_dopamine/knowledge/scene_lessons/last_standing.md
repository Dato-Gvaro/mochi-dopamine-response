# last_standing
- New scene (batch40), replacing the rejected "perfect snake" idea. It is the genre's elimination hit structure ("Which ball will be the last one standing?" 18.8M, research/simple_viral_formula.md section 4), built to the BRIEF_batch25 RESEARCH RULES. **PURE MECHANIC, no characters.**
- Caption (baked, `--cap`; `--cap ''` = base): `Every ball that falls out is ^GONE^|~Only ONE survives~`.
- The only other HUD is one row at y 1372 (0.715 h): `LEFT n` plus a roster of all 18 colours. An eliminated ball's dot greys out and gets a red X. At the end the number turns gold and the champion's dot gets a gold ring.

## World (logical px, arena centre 530, 800)
- **Wall:** a circular arena, R0 462 (0.87 w), thickness 14, made of 48 glowing glass segments with a faint rainbow tint. A segment flashes in a ball's colour when that ball hits it.
- **Gap:** 2 missing segments (15°) at the start. Its edges are round caps marked with bright gold glows.
- **Balls:** 18 glossy balls, r 30, one per hue (i/18), with a specular highlight, rim light and halo. Fast balls draw a short light trail. Balls are already flying at frame 0; the first clack lands at 0.00 s.
- **Black stage.** Nothing else is on screen.

## Mechanic (one model; px, s; seeded; dt 1/60, 8 substeps)
- **Physics:**
  - Gravity is 700.
  - Ball-ball collisions are perfectly elastic between equal masses.
  - Wall contacts are elastic. The wall spins (0.42 + 0.035 t rad/s), so its face moves tangentially. A gap-edge cap is a moving obstacle, resolved in its own frame (an honest kick).
- **Rule:** every real wall hit (vn > 60) speeds the ball up x1.05. Speed is capped so the speed at the arena floor stays ≤ 1800, and a limiter holds it at 1.1x that.
- **Elimination:** a ball whose centre gets fully past the wall through the gap is OUT. It flies on and shatters 20 px further out (or 0.3 s later) into 16 shards of its colour plus white glints and a pop ring.
- **Escalation:**
  1. **The arena closes in after every elimination.** The target radius is R_END + (R0 − R_END)·((n−1)/17)^0.75, with R_END 210. The wall moves in at ≤ 50 px/s, as an honest moving wall.
  2. **Gap-edge segments CRUMBLE** at sim 8, 15 and 21 s, alternating sides, so the gap grows 2 → 5 segments. Each crumbling segment falls in 5 pieces.
  3. Balls speed up on every hit, and the spin speeds up over time.
- **Camera:** it follows the closing arena half-way (z = (R0/R)^0.65), so the shrink is visible while the last balls read bigger.
- **Seed search** (`--search N --jobs 2`): the filters are
  - last elimination at 22-30 s;
  - first elimination ≤ 2.2 s;
  - no gap between eliminations ≥ 4.6 s;
  - the last duel ≥ 2.2 s;
  - first clack < 0.35 s;
  - no wall leaks;
  - the note count can be hit exactly.

  600 seeds gave 17 that pass. **s81** is the default: the most even elimination cadence (largest gap 3.0 s) and the most near-misses (36 cap hits).
- **s81 numbers** (clip s):
  - Eliminations: 1.36 · 2.69 · 3.93 · 6.48 · 6.53 · 7.39 · 7.93 · 8.00 · 8.43 · 11.38 · 13.18 · 14.20 · 14.99 · 17.93 · 19.31 · 22.28 · **24.81** (champion: hue 10, sky blue).
  - Per 5 s: 3/6/3/3/2. The last three balls fight for 3.0 s and the final duel lasts 2.5 s.
  - Wall hits per 5 s: 133/136/104/57/28.

## Finale (last elimination + 0 → 4.2 s)
- The champion glides to the centre (Hermite, 1.0 s) and grows 1.0 → 2.25x with a glow halo in its colour.
- The wall floods with its colour, sweeping round from its side in 0.6 s, and the gap closes as the missing segments grow back.
- The arena interior fills with a soft radial wash of its colour (alpha ≤ 0.20).
- At +1.0 s (the crown), 3 rings of light expand to the wall and a crown of 9 gold points appears above the champion.
- Zoom eases to R0/R (the arena returns to its starting size), so the 0.6 s dissolve into the pre-roll matches in scale. The last frame is pre-roll frame −1.

## Sound
- **Melody:** Beethoven, Piano Sonata No. 14 "Moonlight", Op. 27 No. 2, 3rd mvt (Presto agitato), right hand bars 1-8 plus the bar-9 downbeat. That is 114 onsets: the rising C#-minor arpeggios and the sforzando chord pairs, with chords played as chords.
  - **Source:** Mutopia Project `BeethovenLv/O27/moonlight/moonlight-mids.zip` → `moonlight3.mid`. It is the Berners 1908 edition (ed. Winterberger); the composition is PD and the engraving is CC BY-SA 2.5.
  - The file is cached at `<SOUNDFONTS_DIR>\scores\beethoven_moonlight3\`.
  - `--verify`: **LEAD == the source MIDI: True**. The LH bar basses match too.
- **Note mapping:**
  - One onset per wall bounce, thinned greedily with a minimum gap that eases from 1/r0 to 1/(2.2·r0). r0 is bisected so that exactly 113 notes come before the last elimination.
  - Onset 113 (the bar-9 G# dominant arrival: RH C5 G#5 C6 + LH G#1 G#2, plus contrabass and timpani G#) lands ON the final shatter.
  - The crown gets a rich **C#-major** chord (our Picardy close, V → I): strings, choir aahs, rolled piano, harp and a soft boom, with the top note C#5. A glass-harp C#5 chime sits on top.
- **Under it:** a soft string pad and a contrabass root per score bar (C#m C#m G# G# C#7 C#7 F#m A7 → G#). Each bar change lands on the bounce that starts the bar.
- **SFX (synthesized; no hiss, no whoosh):**
  - A glossy **clack** per ball-ball collision (vn > 90): 3 modes at 1.25-1.7 kHz, a 2.5 ms click low-passed at 2.6 kHz and a 380 Hz knock.
  - A soft glass **tok** per non-note wall hit.
  - Impacts closer than 25 ms merge. The level is density-aware: g·(1 + n/8)^−0.5, with n counted in ±0.5 s.
  - A gold **tik** on each gap-edge near-miss.
  - A soft glass **shatter** per elimination (the last one is bigger).
  - A stony **crumble** per falling segment.
  - Every onset is ≥ 12 ms from every note and from each other.
- -14 LUFS (master). The last 1.0 s is digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (0.20) `--search N --from S --jobs J(≤2) --all --verify`. Tuning: `--g --v0 --speedup --vmax --w0 --w1 --gap0 --nseg --crumble --r0 --rend --rspd --br --rateup`.

## Checks (encoded Full HD, `output/last_standing_fhd2_9x16.mp4`)
- h264 yuv420p 1080x1920, 60 fps, 1740 frames = **29.00 s**. The last elimination is at 24.81 s.
- **Audio:**
  - -14.00 LUFS, peak -5.61 dBFS. The last 1.0 s is digital silence.
  - RMS per 5 s: -21.3 / -18.5 / -16.5 / -16.1 / -16.3 (it builds).
  - Energy above 3 kHz is 0.10%, so nothing is shrill. Minimum onset gap is 12 ms.
- flash_check PASS (0 flashes, mean lum 0.008).
- **Loop:**
  - The last frame is pre-roll frame −1 (pre-encode delta 0.0).
  - Pre-encode last → 0 is 2.52 against a normal step of 2.48, so the seam is one ordinary frame step. 18 moving balls make every step about 2.5.
  - Encoded seam 2.78 against a normal encoded step of 2.52.
  - `check_clip` reports a seam of 2.68 and `check_loop` would say "MISMATCH": both expect last == frame 0, the same as ring_burst.
- **Rates per 5 s:**

  | | 0-5 | 5-10 | 10-15 | 15-20 | 20-24.8 |
  |---|---|---|---|---|---|
  | Notes | 22 | 22 | 26 | 26 | 18 |
  | Sound onsets | 155 | 145 | 126 | 77 | 43 |
  | Eliminations | 3 | 6 | 3 | 3 | 2 |

  433 SFX events: 282 clacks, 104 toks, 26 near-miss tiks, 17 shatters, 3 crumbles and 1 chime.
- `--verify`: LEAD == the MIDI. The top melody note is C#6 (85), in 6 sforzando chords only; the arpeggio line tops out at A5.
- Encoded frames read at 0 / 0.5 / 1 / 1.36 (first shatter) / 1.40 / 2 / 3 / 12.5 / 14.5 / 22.3 (duel) / 24.82 (last shatter) / 25.5 / 25.9 / 26.5 / 27.0 / 28.95 / 28.983 s, with 1:1 crops of the first shatter, the clack sparks and the crown.
- **Safe zone:**
  - The caption is at y 172-245 and the arena at y 331-1269 (≤ 0.66 h). The roster row is at y 1372 (0.715 h), x 92-906.
  - Shards falling below the roster fade out (decoration).
  - The arena's right edge (x ≤ 999) and the gap pass through the 0.85 w strip by rotation only.
- Render: ~50 s Full HD (one process). The 600-seed search took ~2 min on 2 workers.
- Delivered `<VIDEOS_DIR>\batch40\last_standing.mp4`. A 4K ship render is NOT made yet (`NF_SCALE=2.0 --label ship` after review).

## Doubts
- **The raw event rate falls late.** That is inherent to elimination: 18 balls become 2. Each ball's own rate climbs (a speed-up per hit and a closing arena), and the note rate holds about 4.4 → 5.2/s, dipping to 3.7/s in the final duel. But total sound onsets go 31/s → 9/s. The last 5 s are the tense 3 → 2 → 1 duel with 2.5-3 s stretches and near-misses, not a crescendo of density. Mitigations already in: the RMS still builds, the arena is visibly closing, and the duel balls read big.
- The melody walks at about half the score's Presto tempo (one note per bounce), so the arpeggios read as "Moonlight 3rd, slower". The sforzando chord pairs land on whatever bounce comes next, not on eliminations.
- The finale's C#-major chord is our Picardy close (Beethoven stays in minor). The cadence it resolves (A7 → G# on the last shatter → C#) is the score's own harmony.
- The finale zoom totals 2.15x: half of it happens during play (the camera following the shrink) and half in the finale. That is needed so the dissolve into the full-size pre-roll matches.
- The last loser shatters near the left edge in s81 (x ≈ 85, fully visible).

Owner review: pending.

Owner review (2026-10-17): "nothing new, we had balls escaping" -> moved to <VIDEOS_DIR>\reserve (kept as a fallback: an elimination format).
