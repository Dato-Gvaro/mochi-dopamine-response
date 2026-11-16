# ellipse_rays3: THE ELLIPSE SECRET, scored to Pachelbel's Canon on piano

- Built from the owner's review of ellipse_rays2 (2026-10-09): "good, but the music sucks; we need music people know, something familiar classical." It follows the tesla_duel4 recipe: a real piece on piano, real rhythm, natural tempo, ending on a calm cadence, with events landing on the notes.
- v2's visuals are unchanged (geometry, comet trails, caustic, ladder, HUD). v1 and v2 are untouched.

## Music
- **Piece:** Johann Pachelbel, Canon in D (c. 1680-1706). Pachelbel died in 1706, so the composition is public domain worldwide. The notes are synthesized by our own `audio.synth_piano`; no recording is used.
- **Tempo and harmony:** quarter = 75 bpm, 0.8 s per beat, grid origin 0.10 s. One ground-bass chord per beat: D A Bm F#m G D G A, with the bass on D3 A2 B2 F#2 G2 D2 G2 A2. The left hand adds a soft broken chord on the off-eighths.
- **Right hand:** the theme as the violins play it, one quarter note per bass note.
  - Cycle 1: F# E D C# B A B C#.
  - Cycle 2: D C# B A G F# G E.
  - Cycle 3: both lines together. This is the canon itself, sounding in thirds.
  - Cycle 4 (beats 24-28): the theme again.
- **Ending:** a plagal G -> D cadence. The D chord is rolled on beat 29, held 1.45 s, then released over 0.4 s.
- **Dynamics:** 0.50 / 0.58 / 0.68 / 0.56 per cycle.
- **Certainty:** the ground, the two theme lines and their canon pairing are the well-known opening of the piece and are certain. The later 8th/16th-note variations are NOT used. The broken-chord left hand and the final cadence are our arrangement.
- **Mix:** the piano is rendered into the bed note by note, so the mixer's thinning and ducking never touch it.
- **Glass:** one soft glassharp glint per arrival, an octave above the current melody note, so it is always consonant. There are no other accents.
- **Pitch check:** an FFT of the mix at each beat reads back the intended melody notes. On the arrival beats the glint's octave double is the loudest pitch.

## Sync (beats)
Every volley's fire is a melody note and every arrival is a melody note. The ray speed is 395 px/s, so the 2a - r path takes exactly 3 beats.

| Volley | Fire | Arrival |
|---|---|---|
| 8 | beat 0 (0.10 s) | beat 3 (2.50 s) |
| 36 | beat 4 (3.30 s) | beat 7 (5.70 s) |
| 180 | beat 8 (6.50 s) | beat 11 (8.90 s) |
| 360 off-focus | beat 12 (9.70 s) | — |
| 720 | beat 20 (16.10 s) | beat 23 (18.50 s) |
| return | beat 26 (20.90 s) | beat 29 (23.30 s), the final D chord |

- Mochi slides off the focus between beats 11 and 12, and back on between beats 18 and 19.
- The caustic fades from beat 16 (12.90 s) over 1.6 s.
- Direct-ray pre-hits: 7.87, 10.74, 17.47 and 22.27 s.

## Clip and checks
- Clip: 26.30 s (1578 frames).
- Checks on the encoded Full HD file:

| Check | Result |
|---|---|
| Format | h264 yuv420p 1080x1920, 60 fps |
| Loudness | -14.00 LUFS, peak -4.59 dBFS |
| Silence | from ~25.2 s; last 0.5 s at -73 dBFS |
| Seam | encoded 0.143 |
| flash_check | 0 flashes = PASS |

## Args and delivery
- Args: --label, --cap, --off DX,DY, --video-only, --audio-only, --still --frame.
- Delivered: <VIDEOS_DIR>\batch21\ellipse_rays3.mp4 (Full HD).
- Owner review: pending.
- Owner review 2026-10-10: the music needs to be better, piano or something familiar -> ellipse_rays4 (Blue Danube on piano).
