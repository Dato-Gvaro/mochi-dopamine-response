# ellipse_rays5 — THE ELLIPSE SECRET at a gallop (William Tell finale, piano)

- Built from the owner's review of ellipse_rays4 (2026-10-09): "I don't like the music — too slow / boring, needs energy and drive, like the Für Elise run in tesla_duel4." v1-v4 are untouched. The ellipse look, the ladder (8 -> 36 -> 180 -> caustic 360 -> 720 -> return) and the loop are kept.

## Music
- Piece: Gioachino Rossini, William Tell Overture, finale (galop), 1829. Rossini died in 1868, so the piece is public domain worldwide. It is played by our own synth (`audio.synth_piano`), never a recording.
- Tempo and key: E major (the original key), 2/4, quarter = 150, so one bar = 0.8 s.
- Melody: ONLY the certain main motif is used, "B B B  B B B | B B E  F# G#". It is the galloping 16-16-8 figure three times, then the rising E F# G# in eighths (the bank's `william_tell` has the same notes). No continuation is guessed.
- Variety comes from our arrangement:
  - 2x the motif mid-register.
  - 2x an octave up with diatonic thirds below.
  - The miss is set as the same motif sequenced onto IV (A major, "E E E ... A B C#"), 3x.
  - Back in E, then 2x high and loud.
  - Bar 20: the motif's first bar. Bar 21: B7 stabs in the gallop rhythm (D# D# F#  A A B; our cadence).
  - Bar 22: one big E major chord across the keyboard (E1-E5), held 1.15 s, released over 0.35 s, then silence.
- Left hand drives throughout: bass on every beat (root / fifth), a chord on every off-eighth.
- The piano is rendered into the bed note by note, so the mixer never thins or ducks it.
- Mix choices:
  - The melody is boosted (x1.12). The thirds sit at 0.40 and the off-beat chords at 0.23, so the tune stays in front.
  - An FFT of the master at the 50 accented melody notes reads back the right pitch class 47 times. The 3 misses are A5 in the IV sequence, masked by the ringing E5 repeats.
  - Glass: one soft glint per arrival (E6, or A6 over IV), with note_gain 0.20-0.25, about 8-10 dB under the tune.

## Visuals (tightened to the music)
- Rays move at 592 px/s (v2-v4: 395), so the 2a - r path is exactly 2 bars (1.6 s). The trail is 540 px.
- A volley fires every 3 bars, on bar downbeats: bars 0, 3, 6, 9 (off-focus), 15, 20 = 0.1, 2.5, 4.9, 7.3, 12.1, 16.1 s.
- Arrivals land on downbeats: bars 2, 5, 8, 17, 22 = 1.7, 4.1, 6.5, 13.7, 17.7 s. The return to Mochi lands on the final E chord.
- The caustic lingers from 7.3 s and fades from 10.5 s over 1.2 s.
- Mochi slides off the focus at 6.56-7.24 s and back at 11.06-11.9 s.
- Bolt overloads for 2.4 s (bars 17-20).
- Each verdict badge now ends 0.3 s after the next volley fires.
- Clip: 20.50 s (1230 frames).

## Checks (encoded Full HD)
| Check | Result |
|---|---|
| Format | h264 yuv420p 1080x1920, 60 fps |
| Loudness | -14.01 LUFS |
| Peak | -7.08 dBFS |
| Last 0.5 s | -84 dBFS (the sound starts at 0.10 s) |
| Encoded seam | 0.170 |
| flash_check | 0 flashes = PASS |

## Args
- --label, --cap, --off DX,DY, --video-only, --audio-only, --still --frame.

## Delivery
- Delivered: <VIDEOS_DIR>\batch22\ellipse_rays5.mp4 (Full HD). ellipse_rays4.mp4 was removed from batch22 as asked.
- Owner review: pending.
- Owner review (2026-10-09): doesn't like the song (William Tell) -> ellipse_rays6.
