# ellipse_rays2 — THE ELLIPSE SECRET, with more space, slower light and music

- Built from the owner's review of ellipse_rays: "we need a good melody and more space; make the characters smaller, let the lines travel a better distance." v1 is untouched; v2 is its own file.
- Same law and the same exact ray tracer:
  - Every ray from F1 reflects into F2.
  - |F1P| + |PF2| = 2a, so all reflected rays arrive at the SAME instant.
- Geometry: ellipse a 486, b 396 (0.9 of the width), centre (540, 905), foci +-281.7.
- Characters r 27 (v1 50); the hit circle is r 24.
- Light:
  - Rays move at 380-420 px/s (v1 560-700), so a volley takes ~2.3 s to arrive.
  - Each ray is a 430 px comet trail. The trail is one gradient stroke per ray plus a wide glow, with ADD blending.
  - A faint residue of the whole path keeps the geometry readable. After arrival it drains into the target at 1.0 v.
  - Each ray has its own strokes, so the light adds up.
- NO skipped cone (v1 skipped 9 deg). The rays aimed straight at the other focus are drawn. They land first, as a small "pre-hit" (a glow pulse plus a high tick): 180 -> 2 direct rays at 8.40 s, 720 -> 10 direct rays at 18.03 s. The 8- and 36-ray fans contain no direct ray.
- Ladder:

  | Volley | Fire | Arrival | What happens |
  |---|---|---|---|
  | 8 | 0.10 s | 2.59 s | ALL HIT |
  | 36 | 3.55 s | 5.98 s | ALL HIT |
  | 180 | 7.05 s | 9.42 s | ALL HIT |
  | 360, Mochi slid 130 px off the focus | 11.25 s | — | The rays are traced to 2a + 1500, so they keep bouncing and the caustic envelopes keep forming until a fade at 14.35-15.95 s. Stray hits come in clusters at 12.27 / 13.3 / 13.95 / 14.97 s. A live badge reads "OFF THE FOCUS: ONLY k OF 360 HIT" (k = 56 -> 110). Bolt laughs; Mochi gives an annoyed stare |
  | 720, back on the focus | 16.75 s | 19.01 s | Bolt overloads: the halo grows and thin rings expand, no flash |
  | reverse 720, from Bolt | 20.90 s | 23.16 s | ALL light returns to Mochi; Mochi's eyes widen, Bolt laughs |

  Then 3.0 s of settling into frame 0.
- Clip: 26.15 s (1569 frames).
- Sound:
  - Bed: `lib/bgm.py` gymnopedie_1 (Satie, PD), violin + pad, start_beat 12 (the melody enters at ~0.86 s), gain 0.7, plus a very soft D-chord swell under the overload.
  - Accents: soft glassharp notes in D, scaled by ACCENT 0.45 so they sit under the tune. The bed measures -23.2 LUFS and the accents about -24 before mastering.
    - Volley fire: 78 / 81 / 83 / 81 / 86 / 86.
    - Arrival: 86 + 74. The 720 arrival adds an 81 chord; the return lands on 90 + 86.
    - A glint per caustic hit cluster.
  - Clair de lune is NOT in bgm (not shipped: the transcription was uncertain).
- Loop:
  - The bgm fades and ends 1.3 s before the seam (exact zeros).
  - Mochi settles to frame 0's glow, and the fire anticipation squash wraps the seam.
  - Pre-encode seam 0.008.
- Checks (encoded Full HD):
  - h264 yuv420p 1080x1920, 60 fps.
  - -14.00 LUFS, peak -4.91 dBFS; last 0.5 s at -78 dBFS; the audio is audible from 0.1 s.
  - Encoded seam 0.142.
  - flash_check: 0 flashes = PASS.
- Args:
  - --label, --cap ("a|~b~", '' = none).
  - --off DX,DY.
  - --video-only (keep the silent render); --audio-only (re-sound `<name>_silent.mp4`, e.g. `ffmpeg -i clip.mp4 -an -c:v copy <name>_silent.mp4`).
  - --still --frame.
- Render time: ~4 min Full HD.
- Delivered: <VIDEOS_DIR>\batch20\ellipse_rays2.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-09: Good, but the music is bad (the synth violin Gymnopédie); needs familiar classical -> ellipse_rays3.
