# bubble_burst — "Every bubble popped releases 3"

- The breakout formula (research/breakout_formula.md) on a NEW mechanic: soap-bubble foam in two tall glass tanks. Nothing visual is reused from press_split; only the techniques (pre-roll frame 0, dissolve loop, note per event, lead-change/overflow staging).
- **Rule:** popping a bubble releases 3 bubbles at 0.64 x its radius (3 x 0.64² = 1.23, so every pop makes the foam 23% bigger). Gen 7 (r 5.6) is too small to pop. Start: one r 138 bubble per tank, floating on soapy water.
- **Mochi = NEEDLE:** darts to the nearest poppable bubble and pops it, one at a time. Rate 5/s + 0.9/s per second (needle top speed 2600 px/s). She leads from 0.3 s until the late lead change.
- **Bolt = SOUND WAVE:** a speaker in the water fires a ring (1050 px/s, 80 px touch band). The ring pops EVERY bubble it touches, so each pulse multiplies his tank by 3 (1, 3, 9 ... 729, 2187: exact). Pulse gaps shrink: 3.70, 3.60, 3.45, 3.30, 3.15, 3.00 s.
- **Foam physics:** the press_split PBD solver re-tuned for light bubbles: G 900, air drag, a gentle per-bubble wobble (jostle), newborns puff up 50 px/s, contact corrections feed almost no velocity back (CORR_V 40), so a pulse PUFFS the foam up and it settles back. Overflow = the foam top (3% area quantile) above FULL for 20 frames (a pulse's puff must last, not flicker). Then the foam erupts over the rim and floats away (buoyant, G -380).
- **Geometry:** tanks x 36-456 / 488-908 (nothing key right of 0.85 w; everything centred on x 472), rim 420, FULL 505, water 1262, floor 1330 (0.693 h). Labels 1398, counters 1476 (0.77 h).
- **Palette:** iridescent thin-film rims (6-stop swirling hue gradient, specular window glint, inner film band) on black. Mochi's film runs magenta-red-gold, Bolt's cyan-blue-violet, so the frame is multi-hue. Violet-tinted glass, coral needle with a bead head, mint speaker and rings.
- **Frame 0 mid-action:** a 0.6 s pre-roll. At frame 0 the needle is mid-dart and the speaker is charging (shaking). Both first pops land at 0.20 s; the counters read 5 / 3 by 0.5 s.
- **Loop:** a dissolve. In the last 0.6 s the stage cross-fades into the pre-roll, which flows straight into frame 0. The HUD switches at the midpoint. The encoded seam scores 0.435 (good band 0.12-0.72).
- **Seed 0** (searched 0-7; every seed gives the same shape: Bolt wins at 21.33-21.40 s, with one lead change at 17.63-17.65 s). Clip time:
  - Pulses at 0.19, 3.89, 7.49, 10.94, 14.24, 17.38 and 20.38 s. Bolt's count goes 3, 9, 27, 81, 243, 729, 2,187.
  - Mochi: 23 at 2 s, 229 at 12 s, 321 at pulse 5 (Bolt 243, the closest call), 409 at the lead change.
  - LEAD CHANGE at 17.65 s, mid-sweep of pulse 6.
  - OVERFLOW at 21.35 s: Bolt has 2,187 vs Mochi's 555, and Mochi's foam top is 834 (330 px under FULL). The foam erupts at 21.65 and SOUND WAVE WINS! shows from 21.95.
  - Dissolve from 23.07 s. Clip length 23.67 s (1420 frames).
- **Sound** (everything sits in the bed; events go to the sidecar only):
  - **Pops:** a tonal "plip" (a damped sine whose pitch flicks up, a soft lower body and a 1 ms tonal tick; no noise). Pitch is set by radius (300 Hz at r 138, ~1 kHz at r 10). Onsets are at least 12 ms apart overall, ducked by density.
  - **Pulse:** a clean low "whomp" (55-100 Hz falling, with 2nd and 3rd harmonics). A riser runs into the last pulse.
  - **Notes:** one note group per pop, merged to at most 1 per 60 ms. They walk Saint-Saëns, *Le carnaval des animaux* VII "Aquarium" (1886, PD), bars 1-4: the piano-2 rippling arpeggio plus the strings' E-D#-E-D#-E-A tune on the beats, both an octave down (A2-F#5).
    - Source: the Wikimedia Commons MIDI "Camille Saint-Saëns The Carnival of the Animals Aquarium opening.mid" by User:Hyacinth, Public domain. Cached with SOURCE.txt at <SOUNDFONTS_DIR>\scores\saintsaens_aquarium\ and read with orchestra.read_midi (tracks 4 and 5).
    - Voice: lib/audio glass harmonica (the piece's own colour), trimmed to 0.75 s.
  - **Overflow:** a whomp, then a rolled A-minor chord (A2-C5) plus a soft sustained pad, and a flurry of plips as the foam erupts.
  - **Tail:** the bed fades over the dissolve; the last 0.2 s is silent.
- **Checks** (encoded Full HD):
  - Video: h264 yuv420p 1080x1920 at 60 fps.
  - Loudness: -14.00 LUFS, peak -7.1 dBFS.
  - Notes per 5 s: 42, 70, 85, 43. The last bin is 3.7 s of finale.
  - flash_check: 0 flashes = PASS (mean luminance 0.012).
  - Frames read at 0, 0.5, 1, 3, 12, 17.7 (lead change), 21.4 (overflow) and 23.0 s, plus 1:1 crops of both tanks.
- **Render:** the encoder runs with `-threads 2` (CoolWriter, owner: keep the laptop cool). The sim is cached in output/ for stills.
- Args: `--seed` (default 0), `--cap`, `--label`, `--still --frame a,b`, `--report`, `--search a b`.
- Delivered <VIDEOS_DIR>\batch41\bubble_burst.mp4 (Full HD). Owner review: pending.

Owner review (2026-10-18): dropped.
