# ellipse_rays6: THE ELLIPSE SECRET, struck to Beethoven's Fifth

- Built from the owner's music rejections of v3/v4/v5: Canon, Blue Danube ("too slow / boring"), William Tell ("don't like this song"). v1-v5 are untouched.
- Kept: the v2-v5 ellipse, the exact ray tracer, the rainbow comets, the off-focus caustic and the small characters.
- New: the music, the payoff-first cold open, a continuous count ladder, and the "steps closer" twist.

## Music
- **Piece:** Beethoven, Symphony No. 5 in C minor, Op. 67, 1st movement (1807-08).
  - Beethoven died in 1827, so the composition is public domain worldwide.
  - It is played by our own `audio.synth_piano`; no recording is used.
- **Score source:** the Mutopia Project's "Symphony no. 5, Piano reduction" (Augener's Edition), licensed Public Domain.
  - URL: `mutopiaproject.org/ftp/BeethovenLv/O67/beethoven_fifth_op67/beethoven_fifth_op67.mid` (LilyPond-generated MIDI).
  - Parsed with mido. The notes are embedded verbatim in the scene (`SCORE_OPEN`, `SCORE_CODA`).
- **Passages used:**
  - Bars 1-24: the motto "G G G | Eb" and "F F F | D", the continuation in imitative cells, the ff chords, and the ff restatement "Ab Ab Ab | F".
  - The coda's last bars (reduction beats 987.5-1010): three chord mottos "G G G -> C minor", the alternating G / C minor chords, and the final C minor chord.
- **Tempo:** half = 108 (the MIDI's tempo, Allegro con brio), so an eighth = 0.139 s.
- **Fermatas held:** +0.75 s after the Eb, +0.30 s after the D, +0.50 s after the bar-21 G chord, and +0.60 s after the restated F.
- **Our arrangement:**
  - The register is LOW: the top note is C5 and the range is G1-C5.
  - The motto plays as written: G2 / G3 / G4 octaves, then Eb2-Eb4.
  - Bars 6-21 are an octave down, with a soft upper octave only where it stays at or below C5.
  - The restatement's right hand is an octave down.
  - The coda's right hand is an octave down, except the last two chords, which the reduction already writes low.
  - A root bass (C2 / G2 / G1) is added under the held chords of bars 7-18.
  - Eighths are detached (80 % length plus a 90 ms damper).
  - The final chord is held 1.30 s, then released over 0.35 s.
- **The motto starts at 0.000 s.** All notes end at 23.10 s, followed by 1.40 s of silence.
- **Pitch check:** an FFT of the bed at the 50 melody onsets returns the score's pitch class 49/50 times. The one miss is an Eb over a held C, both chord tones.
- **Mixing:** the piano is rendered into the bed note by note. The sidecar events carry the notes with note_gain 0, so the mixer never thins or ducks the piano.

## Sync: "da-da-da" fires, DUM converges
- Every cell of three short notes plus a long note is one volley.
  - The volley fires on the 1st short. Mochi pulses on all three shorts, and the comet heads flare with each.
  - The long DUM is the instant every ray reaches Bolt, because |F1P| + |PF2| = 2a.
- The flight is exactly 3 eighths (0.417 s), so v = 2275 px/s. The light is a strike.
- The 1000 px trail is longer than the 948 px path, so the WHOLE ray is lit at the DUM. It then drains into Bolt over 0.4-2.2 s, longer on held notes.
- A 0.045 rad cone aimed straight at F2 is skipped. Those rays would land early.

| Volley | Music | Fire | DUM / landing | Result |
|---|---|---|---|---|
| 720 cold open | bars 1-2, G G G \| Eb | 0.000 s | 0.417 s | Burst. The web REWINDS into Mochi (0.62-1.30 s) and the counter rolls 720 -> 40 |
| 40 | bars 3-5, F F F \| D | 1.861 | 2.278 | ALL 40 HIT BOLT |
| 60, 80, 100 | bars 6-9, one cell per bar | 3.83 / 4.38 / 4.94 | 4.24 / 4.80 / 5.36 | ALL 100 HIT BOLT |
| 120, 150, 180 | bars 10-13 | 6.05 / 6.61 / 7.16 | 6.47 / 7.02 / 7.58 | ALL 180 HIT BOLT |
| 210, 240, 270, 300 | bars 14-17 (the tenor cells = 240, 300) | 8.27-9.94 | 8.69-10.36 | |
| 360 | bar 18, ff chords G G G -> C minor | 10.494 | 10.911 | ALL 360 HIT BOLT |
| (twist) | bars 20-21, dim chord + G fermata | | | Mochi slides 130 px CLOSER to Bolt (11.52-12.30 s) |
| 480 off the focus | bars 22-24, ff Ab Ab Ab \| F (fermata) | 13.217 | 13.633 | A caustic envelope with cusps. "OFF THE FOCUS: ONLY 148 OF 480 HIT". Bolt laughs; Mochi gives an annoyed stare and slides back (14.41-15.38 s) |
| 540 | coda chord motto 1 | 15.483 | 15.900 | ALL 540 HIT BOLT |
| 630 | coda chord motto 2 | 16.594 | 17.011 | ALL 630 HIT BOLT |
| 720 CLIMAX | coda chord motto 3 | 17.706 | 18.122 | ALL 720 HIT BOLT. The web STAYS lit |
| G / Cm chords + final C | coda | 18.40-21.46 | | Call and response: a coral ring on Mochi on each G chord, a mint ring on Bolt on each C minor chord, the web flaring. Bolt shakes, dizzy, then settles |

## Hook and loop
- **Frame 0:** the full lit 720-ray rainbow web converging into a white-hot Bolt (shocked face), with "RAYS: 720" and "ALL 720 HIT BOLT".
  - This is exactly the end state, so the seam is payoff -> payoff.
  - A wavefront runs over the web during G G G, the burst lands at 0.42 s, and the rewind runs at 0.6-1.3 s.
- **Loop:** frame T (rendered virtually) equals frame 0 exactly, with a pixel diff of 0.0. The last-frame -> frame-0 step is 0.11, against a normal step of 0.18.
  - Mochi's fire anticipation squash wraps the seam.
- **Caption:** "Every ray finds Bolt|~ALL 720 at ONCE~". HUD: "RAYS: N" at 0.752h and a verdict badge at 0.795h.

## Clip and checks
- Clip: 24.50 s (1470 frames).
- Render: Full HD, ~45 min, single process. The 720-ray frames are heavy.
- Checks on the encoded Full HD file:

| Check | Result |
|---|---|
| Format | h264 yuv420p 1080x1920, 60 fps, 1470 frames = 24.50 s |
| Loudness | -14.00 LUFS, peak -5.64 dBFS (with peak_db -4) |
| Audio head | audible from 0.00 s (peak -6.9 dBFS over 0-50 ms) |
| Silence | 23.2-24.5 s peaks at -52 dBFS; the last 0.5 s at -84 dBFS |
| Encoded seam | 0.665, inside the 0.12-0.72 band. It is high because frame 0 is a fire frame, whose comets start moving, while the last frame is a static hold |
| flash_check | 0 flashes, mean luminance 0.017 = PASS |
| Events per 5 s (sidecar notes) | 48 / 80 / 84 / 64 |

- `tools/check_loop.py` does not find this scene's still names, so the seam was checked by rendering frame T directly through draw_frame.

## Args
- `--label`
- `--cap` ("a|~b~"; '' = none)
- `--video-only`, `--audio-only`: re-sounds `output/<name>_silent.mp4`.
- `--still --frame N`

## Delivery
- Delivered: <VIDEOS_DIR>\batch23\ellipse_rays6.mp4 (Full HD).
- Owner review: pending.
- Owner review (2026-10-10): good, but the music is not what we want here -> ellipse_rays7.
