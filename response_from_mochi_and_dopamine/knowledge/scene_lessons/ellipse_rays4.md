# ellipse_rays4: THE ELLIPSE SECRET, scored to The Blue Danube on piano

- Built from the owner's review of ellipse_rays3 (2026-10-09): "we need better music, piano maybe, or something familiar." The Canon's slow opening was not recognisable enough.
- The visuals are v3's: same geometry, comet trails, caustic, ladder and HUD. Only the timing grid changes, to the waltz. v1-v3 are untouched.
- **Music:** Johann Strauss II, "An der schönen blauen Donau" (The Blue Danube), Op. 314 (1866). Strauss died in 1899, so the piece is public domain worldwide. It is played by our own synth (`audio.synth_piano`), never a recording. This is the main waltz theme known from "2001: A Space Odyssey".
- **Tempo:** 3/4, one bar = 1.2 s (quarter = 150, dotted half = 50), a natural Viennese-waltz pace.
- **Melody:** it starts ON the theme with a pickup D at 0.10 s, so it is recognisable inside 2 s. A bar line is `|`; `x . y` is a half note then a quarter note; `'` is one octave up and `''` two octaves up.

  ```
  D | D F# A | A . A' | A' . F#' | F#' . D | D F# A | A . A' | A' . G' | G' . C#
    | C# E B | B . B' | B' . G' | G' . C# | C# E B | B . B' | B' . F#' | F#' . D
    | D F# A | D' . D'' | D'' . A' | A' (V7) | rolled D major chord (I)
  ```

  - The final chord is held 1.45 s, released over 0.4 s, then silence.
  - Only the certain main theme is used, through the climb to the high D. The phrase that follows ("D F# A | D' . D' | D' . B | B . E ...") is cut at bar 20 and closed with a V7 -> I cadence of our own.
- **Harmony:** I in bars 1-6 and 16-19, V7 (A7) in bars 7-15 and 20.
- **Waltz left hand:** the bass on beat 1 (D2 or A2), a chord on beats 2 and 3 (F#3 A3 D4 or G3 C#4 E4).
- **Mixing:** the piano is rendered into the bed note by note, so the mixer's thinning and ducking never touch it.
- **Glass:** one soft glint per arrival, an octave above the melody note on that downbeat. Its level is set by note_gain 0.20-0.25, because mix_events floors gain at 0.15. It measures 6-11 dB under the melody. The first try at gain 0.16 was 3-6 dB OVER the tune and masked it.
- **Melody check:** an FFT of the master at all 45 melody onsets reads back the intended pitch, 45/45.
- **Sync:**
  - Volleys fire on downbeats: bars 1, 4, 7, 10 (off-focus), 15 and 19 = 0.5, 4.1, 7.7, 11.3, 17.3 and 22.1 s.
  - Arrivals land on beat 1 two bars later: bars 3, 6, 9, 17 and 21 = 2.9, 6.5, 10.1, 19.7 and 24.5 s. The ray speed is 395 px/s, so the 2a - r path takes exactly 2 bars.
  - The 720 lands on the climb "D F# A" to the high D. The return to Mochi lands on the final D chord.
  - Mochi slides off the focus 10.2-11.2 s and back 15.85-17.15 s. The caustic fades from 14.9 s over 1.3 s.
- **Clip:** 27.50 s (1650 frames).
- **Checks (encoded Full HD):**

  | Check | Result |
  |---|---|
  | Format | h264 yuv420p 1080x1920, 60 fps |
  | Loudness | -13.99 LUFS |
  | Peak | -6.82 dBFS, with peak_db -4. It was -1.98 without that limiter. |
  | Last 0.5 s | -78 dBFS. The sound starts at 0.10 s. |
  | Encoded seam | 0.141 |
  | flash_check | 0 flashes = PASS |

- **Args:** --label, --cap, --off DX,DY, --video-only, --audio-only, --still --frame.
- **Delivered:** <VIDEOS_DIR>\batch22\ellipse_rays4.mp4 (Full HD).
- **Owner review:** pending.
- Owner review 2026-10-10: does not like the music (Blue Danube): too slow and boring, needs energy and drive -> ellipse_rays5.
