# core_drop
- New scene (batch38). It follows research/simple_viral_formula.md recipe A with the structure changed from spiral to TOWER. **PURE MECHANIC, no characters:** it is the A side of the characters-vs-simple test, and spiral_roll is the character side. Caption (baked, `--cap`; `--cap ''` = base): `Every drop is ^HEAVIER^ than the last|Only one breaks the ^CORE^`.
- **World** (black stage):
  - 44 glass layers span x 54-1026 (0.9 w), with tops at y 452 → 1232 (pitch 18.1).
  - Each layer is thicker than the one above: 9.5 → 16 px.
  - A glowing octagon CORE (gold-white, pulsing halo) sits at (530, 1300). Thin side rails and a floor line keep the tower's outline as it is eaten.
  - The drop column is x 530.
- **Colour:** rainbow from top to bottom (hue 0 → 0.8). It re-spreads over the layers still standing at each attempt, rotated by +0.14 hue, as a 0.5 s top-down wave. So every attempt starts on a full rainbow and there are 6+ hues on screen until the meteor.
- **HUD row** (x 88-916, y 278-390): white object icons with mass labels 5 g · 60 g · 0.5 kg · 7 kg · 100 kg · 2 t. The current one has a ring in the attempt hue. A red X is stamped 0.16 s after each rest. The meteor gets a gold ring at the core hit.
- **Debris:** each broken layer splits across its full width into 12-25 jagged fragments, plus 8 chips at the impact point. Debris moves in physics time and fades as it lands on the remaining stack. A stall layer keeps white cracks whose length scales with the near-miss ratio (KE/S).

## Physics (one model; px, s, kg; G 1500 px/s²)
- Every contender is released from rest at y 120, hidden behind the HUD. The meteor has a 900 px/s entry speed.
- A layer breaks if 0.5mv² ≥ S_i, and the contender keeps v' = √(v² − 2S_i/m).
- Otherwise it bounces (restitution: marble .45, rubber .62, steel .32, bowling .16, anvil .08, meteor .04) and comes to rest: STALL.
- S_i = 30·exp((i+1)^0.75), rising strictly with depth. S_core = 1.2·S_43.
- Broken layers stay broken, so each heavier contender falls through the eaten shaft. The sim raises an error if any non-meteor reaches the core, if the meteor stalls, or if a layer breaks after a stall.
- **Speed ramp:** real-time free fall, then ×0.065 slow motion from 0.04 physics-s before contact until 0.07 s after the last break (0.035 s after a stall). One physics clock (tau) drives everything; only the playback rate changes.
- s3 (deterministic; the seed changes only debris and cracks):

| Contender | Breaks | Stall layer | Near-miss KE/S | Clip s (release → rest) |
|---|---|---|---|---|
| Marble 5 g | 5 | 5 | 0.83 | −0.60 → 2.68 |
| Rubber ball 60 g | 6 | 11 | 0.65 | 3.13 → 7.25 (5 bounces) |
| Steel ball 0.5 kg | 6 | 17 | 0.49 | 7.70 → 11.03 |
| Bowling ball 7 kg | 8 | 25 | 0.31 | 11.48 → 15.12 |
| Anvil 100 kg | 8 | 33 | **0.97** | 15.57 → 18.25 |
| Meteor 2 t | 11 + CORE | — | KE/S_core 1.20 | 18.7 → core 21.39 |

- **Finale:**
  - The core cracks for 0.32 s, then shatters.
  - 160 rainbow shards burst out.
  - 12 rainbow rings (alpha 0.55) bloom out of the core, with a soft gold glow.
  - The camera zooms 1.0 → 1.3 on the core over 2.2 s. Light shake comes on heavy breaks.
  - Core hit + 3.75 s → a 0.6 s dissolve into the pre-roll (the marble falling behind the HUD over the full tower).
- Clip 25.73 s (1544 frames). The first break is at 0.08 s.

## Sound
- **Melody:** Beethoven, *Für Elise* WoO 59, bars 1-8 (first ending), with both hands merged into 47 onsets.
  - **Source:** Mutopia Project id 931 (Breitkopf & Härtel 1888), Public Domain: `mutopiaproject.org/ftp/BeethovenLv/WoO59/fur_Elise_WoO59/fur_Elise_WoO59.mid`. Read with `orc.read_midi`, and the list in the scene is verified equal to the MIDI.
  - Onset j plays on layer break j. Onset 44 (A4+A2, the phrase's cadence) lands on the core hit. E3 and A3 plus a rolled A-minor chord (A1-A4) follow the shatter.
  - Highest note E5. Soundfont piano (MuseScore_General, MIT).
  - Note gaps: min 0.07 s, median 0.2 s, which is about the piece's real 16th-note pace.
- **Under it:**
  - A soft string pad holds the current harmony (Am / E) through every stall, so there is no dead air.
  - Strings swell on the finale chord, with a timpani A on the core hit and a soft boom on the shatter.
- **SFX (synthesized):**
  - A glass crunch per break, offset +12 ms from the note: 4 inharmonic partials at 0.9-2.6 kHz, a low-passed 22 ms snap, and a body thump that deepens with layer thickness.
  - A thud on each stall bounce (pitch falls with mass), a woody stamp on the HUD X, and an A5 glass-harp chime on the shatter.
  - No hiss, whoosh or bed noise. Energy above 3 kHz is 0.13%.
- -14.00 LUFS, peak -5.1 dBFS. The last 1.0 s is digital silence.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --sound 0 --sfx` (SFX level, 0.16). Physics: `--g --s0 --r --pp --slow`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1544 frames.
- flash_check PASS (0 flashes).
- Seam: pre-encode last→0 is 0.068 against a normal step of 0.078 (check_loop: "effectively exact"). Encoded 1.33 (I-frame).
- Sound onsets per 5 s: 15/13/13/19 + the finale. Breaks per 5 s are highest in the meteor run.
- Safe zone: caption y 172-245, HUD 278-390, world clipped to y ≥ 392. The core's bottom is at 1344 (0.70 h). The finale zoom pushes rings and shards past it, which is decorative only.
- Render ~1 min (Full HD).

## Doubts
- **Length is 25.7 s, not 45-60.** A vertical drop through thin layers resolves in ~0.3 physics-s per attempt. The ×0.065 slow motion already stretches each crunch to the melody's natural pace. Going longer would mean padding (longer holds, slower slow-mo, drifting debris). That conflicts with "never pad" and with our own data (shorter wins).
- The anvil's 0.97 near-miss is the "so close" beat. The rubber ball's 5 bounces (about 1.7 s) are the slowest stretch.

Delivered `<VIDEOS_DIR>\batch38\core_drop.mp4`. Owner review: pending.

Owner review (2026-10-16): approved -> 4K (after spiral_roll2 + 2 new research videos are delivered).
