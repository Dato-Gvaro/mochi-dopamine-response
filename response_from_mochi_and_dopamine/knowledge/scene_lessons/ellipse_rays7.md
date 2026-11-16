# ellipse_rays7: THE ELLIPSE SECRET, struck to Handel's Hallelujah

- Built from the owner's verdict on v6 (2026-10-10): "good, but music kinda not what we want here". The owner wants EPIC: bass, a choir. v1-v6 are untouched.
- Kept from v6: the ellipse, the exact ray tracer, the rainbow comets, the off-focus caustic twist, the small characters, the payoff-first cold open, the payoff -> payoff loop and the caption.
- New: the music (choir + orchestra via `lib/orchestra.py`), every volley retimed to the choral accents, a one-quarter flight, the grand-pause light wave and the Adagio call and response.

## Music
- **Piece:** Handel, *Messiah* HWV 56, "Hallelujah" chorus (1741).
  - Handel died in 1759, so the composition is public domain worldwide.
  - It is played by our own arrangement through `lib/orchestra.py` (MuseScore_General.sf2, MIT). No recording is used.
- **Score source:** the Mutopia Project, "Hallelujah Chorus from Messiah", typeset by Joshua Koo (Mutopia-2015/01/17-459), license **Public Domain**.
  - URL: `mutopiaproject.org/ftp/HandelGF/hallelujah/hallelujah-mids.zip` (`combined-score.mid`: SATB, oboes, bassoon, trumpets, timpani, violins I/II, viola, cello).
  - Parsed with mido. The notes are embedded verbatim in the scene (`SCORE`, as score beat / quarters / midi).
- **Passages used** (spliced on the beat; times are ours):

| Part | Score bars | Text | Time |
|---|---|---|---|
| A | 4.1-7.4 | "Hallelujah! Hallelujah! Hallelujah, Hallelujah, Hallelujah!" | 0.00-9.375 s |
| B | 33.4-35.3 | "The kingdom of this world" (the quiet chorale; "world" held 3 beats) | 9.375-14.375 s |
| C | 51.1-54.2 | "King of Kings... for ever and ever, Hallelujah! Hallelujah!" | 14.375-22.50 s |
| pause | 92.2-92.4 | the grand pause (2 beats; only the hall reverb decays, -16 -> -45 dB) | 22.50-23.75 s |
| D | 92.4-94.1 | Adagio "Hal-le-lu-JAH" (I - IV - IV - I, plagal cadence) | 23.75-27.43 s, held to 28.83 s |

- **Tempo:** quarter = 96 (Allegro, a brisk period-performance tempo), so a quarter = 0.625 s. The Adagio broadens to 0.72 / 0.72 / 0.80 s per beat.
- **Our arrangement** (all pitches and onsets from the score; only the orchestration is ours):
  - **Choir:** every sung note on `oohs` (the fast vocal), SATB. Alto/tenor/bass legato on `choir` aahs as the harmony pad (soprano aah added from C), with a CC11 swell into the pause.
  - **Strings:** violins I/II + viola on `strings` (nothing above A5: the violins' D6/C#6/B5 go down an octave); `strings_slow` pad under the quiet chorale.
  - **Brass:** the score's trumpets (C, D); a trumpet doubles the soprano and horns double alto/tenor in A. Trumpet top note F#5.
  - **Bass:** the cello/bassoon line on `cello`, plus contrabass an octave down with the sub octave and a sine sub (`octave_bass`), plus trombone for the attack (not in B).
  - **Timpani:** the score's part (C, D) plus D/A strokes on A's six accents.
  - **Trailer weight:** `boom` on the four biggest beats only (frame 0 HAL, KING, the 720 climax, the final JAH); a cymbal swell INTO the 720 climax; a timpani roll from "lu" into JAH; a concert-cymbal crash on JAH.
  - **Dynamics:** A forte (the hook is big from 0.0 s), B piano (-23/-25 dB RMS against -16), C a crescendo to ff, D the fullest (-14).
- **Ending:** the final D major chord at 27.43 s, held, then `silent_from = T - 1.5 s` (orchestra.TAIL_SILENCE_S).
- **Pitch check:** chroma at the 36 soprano onsets of the bed: the score's pitch class is in the top 3 for 32/36. The 4 misses are passing tones (B4 on "lu", the 16th D4 of "this").
- **Mixing:** `kit.deliver(bed=...)` with no `peak_db` (the orchestra doc's rule). The sidecar events are the 49 accent times, silent (`note_gain` 0).

## Sync: the rays fly on the rest, they land on the accented syllable
- Every volley FIRES on the rest one quarter before a choral accent and every ray reaches Bolt ON the accent (|F1P| + |PF2| = 2a).
- The flight is exactly one quarter (0.625 s), so v = 1517 px/s. The comet heads and Mochi flare on each syllable sung in flight (the "Hal-le" pickups).

| Volley | Lands on | Fire | Land | Result |
|---|---|---|---|---|
| 720 cold open | bar 4.1 "HAL-" | (prev. loop) | 0.000 s | The lit web flares on HAL; it REWINDS into Mochi during "-le-lu-jah" (0.40-1.56 s); the counter rolls 720 -> 40 |
| 40 | 5.1 "HAL-" | 1.875 | 2.500 | ALL 40 HIT BOLT |
| 80, 120 | 6.1 / 6.3 "LU" | 4.375 / 5.625 | 5.000 / 6.250 | ALL 120 HIT BOLT |
| 160, 200 | 7.1 "LE" / 7.3 "JAH" (cadence) | 6.875 / 8.125 | 7.500 / 8.750 | ALL 200 HIT BOLT |
| (twist) | "The kingdom of" (p) | | | Mochi creeps 130 px CLOSER to Bolt (9.75-11.63 s) |
| 300 off the focus | 35.1 "WORLD" | 11.875 | 12.500 | Caustic envelope with cusps: "OFF THE FOCUS: ONLY 92 OF 300 HIT". Bolt laughs; Mochi stares and slides back (13.05-13.67 s) |
| 360 | 51.1 "KING" | 13.750 | 14.375 | ALL 360 HIT BOLT (boom) |
| 420, 480, 540 | 52.1 "Kings" / 52.3 "for EV-er" / 53.1 "and EV-er" | 16.25 / 17.50 / 18.75 | 16.875 / 18.125 / 19.375 | ALL 540 HIT BOLT |
| 630 | 53.3 "Hal-le-LU-jah" | 20.000 | 20.625 | |
| 720 CLIMAX | 54.1 "Hal-le-LU-jah" | 21.250 | 21.875 | ALL 720 HIT BOLT (boom + cymbal swell). The web STAYS lit |
| grand pause | silence | | 22.50-23.75 | A slow wave of light runs along the held web from Mochi into Bolt |
| Adagio | Hal / LE / lu / JAH | | 23.75 / 24.47 / 26.63 / 27.43 | Call and response: a coral ring on Mochi on "Hal" and "lu", mint rings on Bolt on "LE" and "JAH", the web flaring; Bolt overloads (dizzy shake), then settles |

## Hook and loop
- **Frame 0:** the full lit 720-ray rainbow web converging into a white-hot Bolt (wow face), "RAYS: 720", "ALL 720 HIT BOLT", the first "HAL-" with a boom at 0.0 s. This is exactly the end state.
- **Loop:** frame T (rendered virtually through draw_frame) equals frame 0 exactly (pixel diff 0.0). Every burst/ring/flare has a 2-frame attack, so frame 0 itself is the clean end state and the motion starts at frame 1.
- **Caption:** "Every ray finds Bolt|~ALL 720 at ONCE~". HUD: "RAYS: N" at 0.752h and a verdict badge at 0.795h.

## Clip and checks
- Clip: 30.33 s (1820 frames). It is 0.3 s over the brief's 30 s: the Adagio ending plus the 1.5 s silent tail.
- Render: Full HD, three frame-range parts in parallel (`--part i --parts 3`, then `--join 3`), ~20 min wall time. The 720-ray part is the slowest.
- Checks on the encoded Full HD file:

| Check | Result |
|---|---|
| Format | h264 yuv420p 1080x1920, 60 fps, 1820 frames = 30.33 s |
| Loudness | -14.01 LUFS, peak -5.17 dBFS (no peak_db, per docs/orchestra.md) |
| Audio head | audible from 0.00 s (peak -5.8 dBFS over 0-50 ms: the HAL + boom) |
| Grand pause | hall reverb decays -16 -> -45 dB RMS over 22.5-23.7 s |
| Silence | the last 0.5 s peaks at -80.8 dBFS |
| Per-second RMS | A -15..-17, B -22..-24 (the quiet chorale), C -16..-19, D -14..-16 |
| Landing sync | the music's onset at all 17 landings/accents is within +-35 ms except two (+52, +64 ms, the strings' slow attack on "EV-er" / "LU") |
| Pre-encode seam | frame T == frame 0 exactly (diff 0.0) |
| Encoded seam | 0.698, inside the 0.12-0.72 band (frame 0 -> 1 starts the HAL burst; the last frame is a static hold) |
| flash_check | 0 flashes, mean luminance 0.017 = PASS |
| Encoded frames | 0 / 0.25 / 0.5 / 1 / 2 / 3 / 12.6 / 15 / 21.9 / 23.2 / 27.5 s read: web at 0-0.5 s, rewind at 1 s, 40 in flight at 2 s, ALL 40 at 3 s, caustic at 12.6 s, 360 web at 15 s, 720 landing at 21.9 s, pause wave at 23.2 s, JAH overload at 27.5 s |

## Args
- `--label`, `--cap` ("a|~b~"; '' = none)
- `--video-only` (`--part i --parts n` renders a frame range; `--join n` concatenates the parts into `_silent.mp4`)
- `--audio-only` re-sounds `output/<name>_silent.mp4`; `--bed-only` writes a mastered preview of the bed
- `--still --frame N`

## Delivery
- Delivered: <VIDEOS_DIR>\batch25\ellipse_rays7.mp4 (Full HD).
- Owner review: pending.
- Owner review (2026-10-10): poor music; and overall 'we just don't need animations, we need physics, and to show users the difference between what one character chose and what the other did, and one beats the other' -> replaced by mirror_duel (parabola vs circle mirror, NCS 'Waiting').
