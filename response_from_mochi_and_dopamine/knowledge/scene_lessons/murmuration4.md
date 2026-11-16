# murmuration4 — 15,000 starlings at sunset, two gliders, Clair de lune (batch28)

Owner review of murmuration3 (2026-10-11): "remove the tag game — they are just chilling, flying around, slower and smoothly; and use some other music." New file; it imports murmuration2 (flock, `Ink` look, background) and murmuration3 (jetpack, layer, depth occlusion) unchanged.

- **No game:** no score, no IT marker, no banners. Caption `15,000 starlings at sunset | ~just watch them FLOW~`. This is an owner override of the "line 2 = a stake" caption rule and of the duel format, for this video only.
- **Flock (the hero):** m2's boids and density silhouette. The ribbon roost is re-timed so EVERY motion is periodic in the clip length:
  - spine swings T/2, T/3;
  - twist T/2, T/3;
  - yaw T, pitch T/2;
  - width wobble T/4;
  - centre drift T, T/3.
  The end shape therefore returns to the start shape. `--ph` = the roost phase (11.92 s picked from a 24-step sweep: a wide dome with a dark curl).
- **Gliders:** Mochi and Bolt on m3's jetpacks (slower flame flicker, a softer plume). Each flies a CLOSED Catmull-Rom loop through 8 timed 3-D waypoints. A loop runs from near the camera (z -640, big) through the flock (z ~0, the birds part softly) out to far behind the cloud (z +1100, small, occluded by the birds in front) and back. Side by side at the start and end.
  - Calm faces: normal/smile, with a slow happy closed-eye smile now and then; they glance at each other when close.
  - Soft interaction: scare radius 100, flee 650, clearance 38; the ripple amplitude is 0.7 with 0.95 per hop, and the glow is 1.4 (m2: 2.5).
- **Camera:** sway 45 px (one cycle per clip) and 14 px vertical (T/2), slower than m3.
- **Loop:** frame 0 = state 0: the big fold with both gliders near the camera. The gliders' paths and every roost motion are periodic in T, and the last 0.8 s dissolves into frame 0. That gives an exact loop with no rewind.
- **Music:** Claude Debussy, "Clair de lune" (Suite bergamasque L. 75, III). Published 1905 (Fromont); Debussy d. 1918, so public domain.
  - Notes are parsed at runtime with `orc.read_midi` from the Mutopia Project MIDI (Mutopia-2010/12/21-1778, source E. Fromont 1905, engraving licence Public Domain). The cached copy is at `<SOUNDFONTS_DIR>\scores\debussy_clair\`, with SOURCE.txt.
  - Excerpt: bars 1-8, plus the D-flat chord that opens bar 9 as the cadence (held 1.9 s), then a ~1.5 s silent tail. 9/8 at dotted quarter = 56.25 (bar = 3.2 s). The first note sounds at 0.02 s.
  - Arrangement (lib/orchestra.py):
    - melody (upper voice) on strings plus a solo violin;
    - inner voice on strings and violas;
    - bass = the lowest inner note an octave down on cello, and two octaves down on contrabass (with a sine sub);
    - harp flowing eighths on the pitches WRITTEN at each dotted beat (lowest three, top notes an octave down);
    - "oohs" pad;
    - a soft cymbal swell into the cadence.
  - Dynamics: velocity 0.62 rising to 0.84 by bar 7, easing into the cadence. Top note Ab5.
- **Render:** `NF_SCALE=1.0 python scenes/murmuration4.py`. Flags: `--still --frame a,b`, `--silent-only`, `--reuse` (re-mux), `--audio-only`.
- **Checks (Full HD v1, 2026-10-11):** h264 yuv420p 1080x1920 60 fps, 1717 frames = 28.62 s · -14.01 LUFS, peak -5.9 dBFS, last 0.5 s -90 dBFS · flash_check 0 = PASS (mean lum 0.17) · seam last->first 0.42 = normal frame-to-frame median 0.42 · glider scale 0.59..1.63, world speed median 160-185 px/s · closest bird 38 px · encoded frames read at 0, 0.5, 2, 8, 15, 21, 25.3, 28.5.
- Weak spot: around 15 s the cloud contracts into a smaller blob plus a sparse spray (ribbon edge-on), the least frame-filling moment.
- **Delivered:** `<VIDEOS_DIR>\batch28\murmuration4.mp4` (Full HD). Owner review: pending.
- Owner review (2026-10-12): they look like slow motion; instead of flying, Mochi and Bolt sit on the ground watching a predator (a good-looking bird, not ugly) fly through the flock while the flock avoids it -> murmuration5.
