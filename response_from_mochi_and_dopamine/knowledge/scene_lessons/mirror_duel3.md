# mirror_duel3 — one by one, cleaner (batch28, 2026-10-11)

## Owner's review of mirror_duel2
> "too much text on screen — we don't need 'BOLT: text here', users will guess it by colour and the temperature info at the bottom. Also don't jump the sun like that, make it move smoothly. We can have the temperature in the centre near the boiler and make it rise smoothly with 0.01 data — increasing numbers."

## Changes vs mirror_duel2 (physics, music, structure and cold open unchanged)
- **Text:** every label, formula, HITS counter and explainer banner is gone. What remains:
  - the 2-line caption;
  - "BOIL!" at the climax;
  - the colour coding: Mochi coral (her mirror tint, readout and bar outline), Bolt mint;
  - small side-by-side heat bars at y ≈ 1330, with a coral tick on Bolt's bar marking Mochi's final temperature;
  - the two characters.
- **Temperature readout:** a 58 px live `47.83°C` beside each boiler, left-aligned so the digits roll in place.
  - Each volley's heat soaks into the water linearly over one beat after it lands. The curve is continuous (piecewise linear) and the display moves in 0.01 steps every frame.
  - Bolt's last volley lands at j=55 and its soak ends exactly on the bar-15 downbeat, where the readout reaches 100.000 and the boiler blows.
  - Final: Mochi 72.38 °C, Bolt 100.00 °C. Bolt passes Mochi at 23.33 s.
- **Sun:** `sun_phi(t)` runs one smoothstep sweep from -26° to +16°, from Bolt's slide-in (12.44 s) until the last volley reflects (~25.8 s); it is still otherwise.
  - The heliostats track it every frame (`aims(sun_phi(t))`).
  - The faint steady web is re-traced live every frame (160 rays) against the current sun and mirror angles.
  - Each volley is traced at the sun angle of its own reflection moment.
- **Twist kept:** the first volley still goes out with the mirrors FLAT and only 6/60 hit (direct sun). Aiming is now one smooth 0.4 s sweep (13.83-14.23 s) instead of a flick.
- Hits per volley are unchanged: circle 53-54%, heliostats 81-86% (gaps and blocking traced).

## Music
- "Waiting", Syn Cole & KAZHI, NCS: 0:48.007 → 1:16.44, 0.2 s fade, then silence.
- 135.0 BPM, drop at 0:49.784 (detected; `output/mirror_duel3_musicgrid.json`).

**DESCRIPTION** (must contain verbatim):
```
Song: Syn Cole, Kazhi - Waiting
Music provided by NoCopyrightSounds
Free Download/Stream: http://ncs.io/s_waiting
Watch: https://ncs.lnk.to/s_waitingAT/youtube
```

## Verification (v1, Full HD)
- Delivered file: `<VIDEOS_DIR>\batch28\mirror_duel3.mp4`.
- Format: h264 yuv420p 1080x1920 @ 60 fps, 1799 frames = 29.98 s.
- Audio: -14.02 LUFS, peak -4.99 dBFS, last 0.5 s at -240 dBFS.
- Loop seam: mean |delta| 0.491 (good band).
- flash_check: 0 flashes, mean luminance 0.016.
- Encoded frames read: 0, 0.5, 2, 8, 13.4 (flat miss), 14.1 (aiming sweep), 20, 26.75 (BOIL), 29.97 (= frame 0).

## Shipped (2026-10-12, owner: "ok ship it")
- 4K render (label `ship`, 8 parts on 2 workers): `<VIDEOS_DIR>\Schedule\2026-10-14\2_mirror_duel3.mp4`.
- Format: h264 yuv420p 2160x3840 @ 60 fps, 29.98 s.
- Audio: -14.02 LUFS, peak -4.99 dBFS, last 0.5 s at -240 dBFS.
- Loop seam 0.513; flash_check 0 flashes.

## Titles / pinned comment
- One curved mirror vs 21 flat mirrors: who boils first? ☀️🔥 #satisfying #physics #shorts
- 21 FLAT mirrors beat a curved one at catching the sun 🌈 #satisfying #physics #shorts
- 72.38°C vs 100.00°C: circle mirror vs a field of flat mirrors ☀️ #satisfying #physics #shorts

Pinned comment: "Every ray is traced exactly. Mochi's circle mirror loses its edge rays to spherical aberration: 53% of the light hits her boiler. Bolt's 21 flat mirrors each tilt halfway between the sun and the tower and follow the sun: 81-86% hits. That's how real solar tower plants work. 🎵 Waiting, Syn Cole & KAZHI (NCS)"

## Lessons
- A smooth readout needs a smooth heat model: per-ray arrival steps jump, so let each volley's share soak in over a beat. Sync the soak end to the climax downbeat by landing the last volley one beat earlier.
- A continuously moving sun means the steady web cannot be cached: re-trace a small live fan (160 rays, ~15k segment tests) every frame. It is cheap.
- Owner review (2026-10-12): 'ok ship it' -> APPROVED, 4K (Oct 14 slot 2).
