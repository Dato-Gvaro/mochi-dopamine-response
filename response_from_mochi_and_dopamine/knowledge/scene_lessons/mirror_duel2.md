# mirror_duel2 — "Whose mirrors catch the sun?" ONE BY ONE (batch27, 2026-10-11)

## Owner's review of mirror_duel v1 (2026-10-11)
> "good, but both of them in one scene is too much; we need them to do it ONE BY ONE or split into two Shorts, so the visual effects and colours are more visible. Also the parabola is not doing much visually"

What changed:
- Two **full-screen turns** that slide in on the beat grid.
- Bolt's parabola is replaced by a **heliostat field**: 21 flat mirrors and a tower. The rays cover the whole frame as a rainbow web, and the mirrors flick to track a moving sun.
- The side-by-side result is two heat bars, always on screen, with Mochi's final temperature marked on Bolt's bar.

## The duel (exact tracing; same boiler r = 24 px; the same total sunlight per turn)

**Turn 1, Mochi's CIRCLE mirror** (`x² + y² = r²`):
- Aperture 920 px (0.85 W), r = 575, f = 287.5, sun exactly on its axis (her best case).
- Spherical aberration: the edge rays cross short of the focus (the full-screen caustic) and splash past her boiler.
- **53-54%** hits (6/12, 32/60, 128/240, 538/1000).

**Turn 2, Bolt's HELIOSTAT FIELD:**
- 21 flat mirrors, 36 px wide on a 42 px pitch, aim at a boiler on a 600 px tower.
- Each mirror normal is the bisector of "to the sun" and "to the tower".
- The sun crosses the sky (-26° → +16°, one step per bar) and the mirrors FLICK to re-aim.
- The tracer includes:
  - the gaps between mirrors (those rays hit the ground);
  - blocking by neighbours' backs;
  - direct sun on the boiler.
- **81-86%** hits, depending on the sun angle.

**Twist:** Bolt's first volley goes out with the mirrors still FLAT. The light bounces back into the sky and only 6/60 hit (direct sun). Mochi laughs. On the next beat every mirror flicks to aim.

**Heat:**
- Each turn's volleys are normalised to one unit of sunlight; heat = sunlight × hits / N.
- Mochi's turn ends at **72 °C**. Bolt passes her mark at 23.3 s and boils (**100 °C**) on the bar-15 downbeat.
- Why he wins: 81% of the light delivered vs 53%.

## Timeline (clip s; beat 0.444, bar 1.778)
| t | music | picture |
|---|---|---|
| 0.00 | 0:48.007, pre-drop bar | **cold open = end state.** Bolt's field at full blaze: 21 rainbow beams converge on the steaming tower boiler, "BOIL!", 823/1,000, bars 72 °C vs 100 °C. Banner "THE FLAT MIRRORS BOIL FIRST!" |
| 0.22-0.86 | | the web retracts into the sun |
| 0.86-1.22 | | slide to turn 1. Banner "TURN 1: MOCHI'S CIRCLE MIRROR" |
| 1.778 | **drop** | first 12-ray volley lands: 6/12 |
| bars 1-6 | | 12 → 60 → 240 → 1000 rays, one-beat flights on every kick. Banners "THE EDGE RAYS MISS HER BOILER", "CIRCLE: ONLY 54% OF THE LIGHT HITS". Bolt laughs |
| 12.44 (bar 7, quiet) | | slide to turn 2. Banner "TURN 2: BOLT'S 21 FLAT MIRRORS" |
| 13.33 | | flat-mirror fiasco: 6/60 HIT, Mochi laughs |
| 13.83 | beat | FLICK, every mirror aims. 240-ray volleys land 206/240 |
| 16.00 (bar 9 crash) | | 1000 rays, two-beat flights, rainbow wavefronts climbing to the tower. Banner "THE MIRRORS TRACK THE SUN: 82% HITS". The sun moves and the mirrors flick each bar |
| 23.32 | | Bolt passes Mochi's 72 °C (coral tick on his bar). Banner "BOLT PASSES MOCHI'S 72°C" |
| bars 13-14 | | volleys on the 8ths, the boiler shakes. Banner "ABOUT TO BOIL..." |
| 26.665 (bar 15) | | **BOILS:** burst glow, 4 shock rings, steam jet, "BOIL!". Bolt cheers then laughs, Mochi stares |
| 28.442 (bar 16) | last hit | second ring; music cut, 0.2 s fade |
| 28.68-29.98 | silence | held payoff = frame 0 |

Banners pop at full alpha on their first frame: a scale pop 1.14 → 1.0 over ~0.1 s, then a 0.2 s fade out.

## Music
- "Waiting", Syn Cole & KAZHI, NCS; the owner-provided track.
- Excerpt: 0:48.007 → 1:16.44, the same cut as mirror_duel.
- Beat grid detected from the audio: 135.0 BPM, drop at 0:49.784 (cached in `output/mirror_duel2_musicgrid.json`).
- Loudness: a plain gain to -14 LUFS.

**DESCRIPTION** (must contain verbatim):
```
Song: Syn Cole, Kazhi - Waiting
Music provided by NoCopyrightSounds
Free Download/Stream: http://ncs.io/s_waiting
Watch: https://ncs.lnk.to/s_waitingAT/youtube
```

## Verification (v1, Full HD)
- Delivered file: `<VIDEOS_DIR>\batch27\mirror_duel2.mp4`.
- Format: h264 yuv420p 1080x1920 @ 60 fps, 1799 frames = 29.98 s.
- Audio: -14.02 LUFS, peak -4.99 dBFS, last 0.5 s at -240 dBFS (silent from 28.68 s).
- Loop seam: post-encode mean |delta| 0.574, inside the good band.
- flash_check: 0 flashes, mean luminance 0.018.
- Encoded frames read: 0, 0.25, 0.5, 1, 1.5, 2, 3, 8, 12.6 (slide), 13.5 (fiasco), 14.3 (flick), 17, 23.4 (pass), 26.75 (boil), 29.97 (= frame 0).
- check_clip's sidecar note-health step does not apply (music clip; the events file is a dict).
- Render: 4 parallel parts, ~15 min wall on a shared machine.

## Titles / pinned comment
- One curved mirror vs 21 flat mirrors: who boils first? ☀️🔥 #satisfying #physics #shorts
- 21 FLAT mirrors beat a curved one at catching the sun 🌈 #satisfying #physics #shorts
- Circle mirror vs a heliostat field: 1,000 sun rays race ☀️ #satisfying #physics #shorts

Pinned comment: "Every ray is traced exactly. Mochi's circle mirror loses its edge rays to spherical aberration: 53% of the light hits. Bolt's 21 flat mirrors each tilt halfway between the sun and the tower, re-aiming as the sun moves: 81-86% hits. The rest falls in the gaps. That's how real solar tower plants work. 🎵 Waiting, Syn Cole & KAZHI (NCS)"

## Lessons
- With a 1000-ray volley the incoming leg is a solid sheet. Dim comets AND their heads until the first reflection (×0.3), so the bright part is the bounce: rainbow wavefronts climbing to the tower.
- A twist needs time: the fiasco volley must land a full beat before the flick, or its banner gets zero frames.
- Owner review (2026-10-11): too much text; drop the 'BOLT: ...' labels (colour + temperature say it); the sun must move smoothly, not jump; temperature in the centre near the boiler, rising smoothly in 0.01 steps -> mirror_duel3.
