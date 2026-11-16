# beam_clash — anime-style beam struggle, Mochi vs Bolt, Mozart "Dies irae" arranged for orchestra + choir

- **Brief:** batch25, 2026-10-10. Owner asked for "pop culture without copyright": anime, cyberpunk or gaming. See BRIEF_batch25.md, BRIEF_brain.md and research/hooks.md.
- **IP-safe:** it uses only the generic beam-clash trope (auras, beams meeting in a clash ball, power levels).
  - No names, attacks, poses, hair or signature designs from any anime.
  - Text on screen: caption, "POWER", "BOLT DIGS IN!", "BREAKTHROUGH!", "BOLT WINS!".
  - Power numbers peak at 11,870. No meme numbers.

## Rule
A real tug-of-war. The clash point x runs from 0 at Mochi's hands to 1 at Bolt's, and obeys:
- x'' = 3.0 (Fm - Fb)/(Fm + Fb) - 3.2 x'
- F = P^3 / beam length, so a shorter beam pushes harder and x settles where the powers balance, with inertia.
- POWER steps up only on note onsets (`SCRIPT`), and each step adds a 0.12 s shove.
- The tug bar on the HUD is x itself.

## Story (Bolt wins)
| time | x | what happens |
|---|---|---|
| bars 3-6 | 0.42 ↔ 0.78 | even trades |
| bar 7 (9.0 s) | 0.88 by 11.25 s | Mochi's stage-3 rush (four shoves on the descending choir line) drives the ball into Bolt's face |
| 11.25-12.0 s | | Bolt DIGS IN on the orchestra-only timpani roll (crouch, sweat, cracks) |
| 12.0 s (jump to bar 57) | 0.30 by 13.5 s | Bolt goes white-hot and drives the ball all the way back |
| 15.75 s | | Mochi answers on the sopranos' high G (stage 4) |
| 18-21 s | 0.50 | dead-even standoff at max power |
| 21.75 s (bar 63, beat 3) | 0.15 by 23.9 s | Bolt hits stage 5 (FULL POWER) |
| 24.0 s (final chord) | | breakthrough: Mochi is blasted (dizzy, then singed and smoking, annoyed stare); Bolt cheers twice; "BOLT WINS!" |

- **Escalation:** stage-ups grow the aura (flame tongues, rising particles, speed lines, a ring burst), thicken the beam (24 → 68 px core), and shift the colour.
  - The colour shift is a hue shift, not brightness: coral → gold, mint → cyan.
  - Clash ball r 52 → 230. Floating rocks lift with total power. Shake grows. A shockwave ring fires on every push.
  - Pushes per 5 s: 5, 11, 13, 13.
- **Hook:**
  - Frame 0 is story 22.03 s: both at stage 5, x = 0.42, ball r 219, rocks up, POWER 6,500 vs 8,280, under the Dies irae's first tutti chord.
  - 0-0.5 s: REWIND (◀◀ icon). Story time runs back to the power-up.
  - 0.75 s: ignition on the second tutti chord.
  - 1.5 s: both fire. 1.875 s: the beams meet.
- **Loop:** everything is a function of story time τ. The clip ends with the same rewind, from the aftermath (26.0 s) back to the frame-0 standoff, so the seam is exact by construction.
  - Encoded seam delta is 2.37, against 5.5 and 7.5 for the frames on either side. The shake and sparks never stop, so this is continuous motion, not a jump.

## Layout (logical 1080x1920)
- Mochi at (165, 1215) on the left mesa; Bolt at (915, 735) on the tall right mesa; character r 50.
- The beam is a 32° diagonal, ~780 px long.
- A dim moon, storm clouds and a canyon with distant mesas.
- HUD at 0.77 h: power numbers and the tug bar. Banners at 0.725 h. Caption 2 lines at 0.105 h.

## Music
Mozart, Requiem in D minor K. 626, Sequentia "Dies irae" (1791; Mozart died 1791, so public domain).
- **Source:** Süssmayr completion, as printed in Breitkopf & Härtel 1877 (Brahms). Notes copied from the Mutopia Project edition MozartWA/KV626/dies_irae (Mutopia-2014/03/24-364, public domain), via its MIDI, into `SCORE` in the scene.
- **Excerpt:** bars 1-8, then bars 57-64, plus the downbeat of bar 65 as the cadence.
  - The join is a true V→i: bar 8 ends on A major and bar 57 opens on D minor.
  - Quarter = 160. The final D is held 1.25 s (fermata).
- **Arrangement** (lib/orchestra.py, MuseScore_General MIT):
  - Choir SATB on oohs + aahs.
  - Violins on strings + violin, viola. Notes above C6 are dropped an octave.
  - Basset horns → horns; bassoons; trumpets + trombone an octave down; timpani as written.
  - Continuo on contrabass + sub octave + synth sub + tuba.
  - Booms on 8 phrase starts and stage-ups. Timpani rolls into 12.0 s and 23.25 s. Cymbal swells into 12.0 s and 24.0 s.
  - From bar 57, an aah pad swells into the final chord.
- **Sync:** every power step is a score onset (median 16 ms from a detected audio onset). Stage-ups are on phrase starts and the breakthrough is on the final chord.
- Silent from T - 1.5 s.

## Args and commands
- Args: `--cap`, `--label`, `--still --frame N`, `--report`.
- Silent video: `NF_SCALE=1.0 python scenes/beam_clash.py --silent`.
- Music onto the kept silent render: `NF_SCALE=1.0 python scenes/beam_clash.py --mux` (re-mux without re-rendering).

## Checks (encoded Full HD v1)
- h264 yuv420p 1080x1920 at 60 fps, 1608 frames = 26.80 s.
- -14.01 LUFS, peak -5.69 dBFS, last 0.5 s at -84.3 dBFS.
- flash_check: 0 flashes, PASS (mean lum 0.047).
- Encoded frames read at 0, 0.25, 0.5, 1, 2, 3, 9.8, 11.5, 13.4, 16, 19, 22.5, 23.9, 24.3, 25.2 and 26.5 s.

## Delivery and review
- Delivered: <VIDEOS_DIR>\batch25\beam_clash.mp4. Owner review: pending.
- **Doubts:**
  - Section A is already tutti, as Mozart wrote it, so the music builds less from thin to full than the brief's trailer rule asks. Section B is fuller: pads, rolls, louder dynamics.
  - The music was not auditioned by ear here. It was measured only (levels, onsets).
- Owner review (2026-10-10): the orbiting string arcs at the clash point look weird when large ('floating long noodles'); wants a visible reason one side is stronger: one formula strong at the start, the other compounding and pushing at the end -> beam_clash2.
