# mirror_duel — "Whose mirror catches the sun?" (batch25, 2026-10-10)

Built from the owner's note on ellipse_rays7: "we need PHYSICS, and to show the difference
between what one character chose and what the other did, and one beats the other."

## The choice duel
- **Mochi picks a CIRCLE mirror** (`x² + y² = r²`), the intuitive choice. **Bolt picks a PARABOLA** (`y = x²/4f`).
- Both get the same sun, the same aperture (2a = 452 px), the same focal length (f = 141 px: the circle's paraxial focus r/2 equals the parabola's focus) and the same glass boiler (r = 12 px) at that focus.
- The circle's depth is set by a = 0.8 r. The two dishes look almost identical; that is the point.
- **The tracer is exact.** Every ray drops vertically from the sunlight line. It gets an analytic ray/curve intersection and a mirror-law reflection, with up to 8 bounces (the circle's rim rays bounce twice). A ray hits if its path enters the boiler disc.
- **Why the parabola wins:** every parallel ray reflects through its focus. Its optical path is also equal for all rays, so a parabola volley lands on the boiler in the same instant, exactly on the beat.
- **Why the circle loses:** spherical aberration. Its outer (blue/magenta) rays cross the axis short of the focus, building the caustic cusp, and splash past the boiler.

Tracer results:

| Mirror | Boiler position | Hits |
|---|---|---|
| Parabola | focus | 1000 / 1000 |
| Circle | paraxial focus | 54% (6/12, 32/60, 130/240) |
| Circle | sweet spot, 27 px toward the mirror (Mochi's fix) | 78% (186/240, 778/1000) |

The sweet spot is the best boiler height on the axis, found by scanning 0-60 px.

**Heat model:**
- Each volley is the SAME sunlight split over N rays; N is a sampling resolution.
- The sun brightens S = 1.0 / 1.25 / 1.5 / 2.0 up the rungs.
- A boiler gains S × hits / N per volley, applied per ray at that ray's real arrival time.
- The scale is normalised so Bolt reaches 100 °C on the final volley.
- Result: Bolt 100 °C vs Mochi 75 °C.

## Timeline (clip s; beat = 0.4444 s, bar = 1.778 s)
| t | music | picture |
|---|---|---|
| 0.00 | track 0:48.007, the pre-drop bar (dip) | **cold open = the end state.** Both 1000-ray webs are lit: Bolt's clean fan blazing into a boiling boiler (steam, "BOIL!", 100 °C, HITS 1,000/1,000), Mochi's caustic with violet rim rays flaring out (HITS 778/1,000, 75 °C). Badge: "THE PARABOLA BOILS FIRST!" |
| 0.22-1.20 | dip | rewind: the light retracts along every path as one wavefront back into the sunlight line. Heat drains, the counters roll down, Mochi's boiler slides back up to the focus |
| 1.778 | **the DROP** (0:49.78) | first volley (12 thick rays) lands: Bolt 12/12, Mochi 6/12 |
| bars 1-2 | | 12 rays per kick. Bolt laughs; badge "CIRCLE: THE EDGE RAYS MISS THE FOCUS" |
| bars 3-4 | | 60 rays per kick |
| bars 5-6 | | 240 rays per kick. Badge "PARABOLA: EVERY RAY HITS ONE POINT" |
| bar 7 (12.44) | the quiet bar | **TWIST:** Mochi hops and slides her boiler 27 px down to the sweet spot. Badge "MOCHI'S FIX". Her hits jump 130 → 186 of 240 and Bolt sweats |
| bar 8 beat 4 (15.55) | the kick drops out | no volley |
| bar 9 (16.00) | the crash, the loudest bar | **1000 rays**. Badge "BETTER: 78% HIT, UP FROM 54%... NOT 100%" |
| bars 13-14 | | volleys on the 8ths (rate doubles), Bolt's boiler shakes. Badge "BOLT'S BOILER IS ABOUT TO BLOW" |
| bar 15 (26.665) | downbeat | **CLIMAX:** Bolt hits 100 °C and the boiler BLOWS: shock rings, burst glow, the steam jet starts, "BOIL!" pops. The last web stays lit. Bolt cheers then laughs; Mochi gives the annoyed stare |
| bar 16 (28.442) | downbeat, last hit (1:16.45) | a second ring and the web flares. Music cut with a 0.2 s fade |
| 28.68-29.98 | silence (1.30 s) | the held payoff = frame 0 |

- Every volley LANDS on a detected kick (`music_grid()`; the only kick-less beat in the 16 bars is bar 8 beat 4).
- Flight = exactly one beat, so each volley fires on the previous beat.

## Music
- "Waiting", Syn Cole & KAZHI, NCS; the owner-provided track.
- Source: `<VIDEOS_DIR>\music\Waiting\Syn Cole, KAZHI - Waiting [NCS Release].mp3`
- Excerpt: track **0:48.007 → 1:16.44** (bar-16 downbeat), with a 0.2 s cosine fade to zero by clip 28.68 s, then 1.30 s of silence.
- Beat detection (cached in `output/mirror_duel_musicgrid.json`):
  - Detected from the audio: kick-band (30-150 Hz) onset flux, with a tempo + phase fit over 49-77 s.
  - Tempo: **135.0 BPM**. The coordinator's estimate was 137.5; the full-band flux fit also gives 135.0.
  - Drop: the first beat after 0:48 that is more than 6 dB above the 4 beats before it = **0:49.784**.
  - Start: the downbeat nearest 0:48 = 0:48.007, one bar before the drop.
- Loudness: a plain gain to -14 LUFS, measured with pyloudnorm on the stereo excerpt. No limiter: the track is already mastered.

**VIDEO DESCRIPTION** (must contain this verbatim):

```
Song: Syn Cole, Kazhi - Waiting
Music provided by NoCopyrightSounds
Free Download/Stream: http://ncs.io/s_waiting
Watch: https://ncs.lnk.to/s_waitingAT/youtube
```

## Commands
```
NF_SCALE=1.0 NF_FAST=1 python scenes/mirror_duel.py --still --frame 0,800,1600
NF_SCALE=1.0 python scenes/mirror_duel.py --report
NF_SCALE=1.0 python scenes/mirror_duel.py --part i --parts 4   (x4 in parallel, ~1 s/frame each)
NF_SCALE=1.0 python scenes/mirror_duel.py --join 4
NF_SCALE=1.0 python scenes/mirror_duel.py --audio-only           (muxes the track onto _silent.mp4)
```

## Verification (v1, Full HD)
- Delivered file: `<VIDEOS_DIR>\batch25\mirror_duel.mp4`.
- Format: h264 yuv420p 1080x1920 @ 60 fps, 1799 frames = 29.98 s.
- Audio: -14.02 LUFS (muxed mp4), peak -4.99 dBFS, last 0.5 s at -240 dBFS (silent from 28.68 s).
- Loop seam: post-encode mean |delta| 0.436, inside the good band (frame 0 is rendered as the state at T).
- flash_check: 0 flashes, mean luminance 0.015.
- check_clip: its sidecar note-health step crashes because this scene's `_events.json` is a dict (music clip, no notes). The video and audio rungs above all printed.
- Encoded frames read: 0, 0.25, 0.5, 1, 2, 3, 13.4 (fix), 15, 26.72 / 26.9 (blow), 29.97 (= frame 0 state), plus a 1:1 crop of both foci at the blow.
- Render: 4 parallel parts at ~1-2 s per frame on a shared machine, ~7 min wall.

## Titles / pinned comment
- Circle mirror vs Parabola mirror: only one boils the water ☀️🔥 #satisfying #physics #shorts
- They look identical... but only the PARABOLA focuses the sun 🔥 #satisfying #physics #shorts
- 1,000 sun rays vs a circle mirror and a parabola mirror ☀️ #satisfying #physics #shorts

Pinned comment: "Every ray is traced exactly. A circle mirror only focuses near its centre: its edge rays cross too early (spherical aberration). Even at the best spot it catches 78% of the light. The parabola sends 1000 of 1000 into one point. That's why solar furnaces and satellite dishes are parabolas. 🎵 Waiting, Syn Cole & KAZHI (NCS)"

## Lessons
- A rewind by `frac × each ray's own length` leaves blocky black silhouettes, because hits and misses have different lengths. Retract every ray to one common arc-length front (`S_FRONT`) instead: it reads as a wavefront running backwards.
- A 1000-ray comet volley with a long trail reads as a solid slab. Use a 150 px trail at 0.7 alpha: a falling sheet of light.
- Counters must turn over on the beat (`t_land`), not on the first arrival: the few rays that hit the boiler top directly arrive ~0.2 s early.
- Owner review (2026-10-11): good, but both in one scene is too much -> one by one (or split into two Shorts) so the effects/colours show; the parabola is visually dull (one dot), so Bolt needs a design whose rays go places around -> mirror_duel2.
