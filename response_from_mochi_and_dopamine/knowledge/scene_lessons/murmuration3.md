# murmuration3 — jetpack TAG through 15,000 starlings (batch27)

Owner review of murmuration2 (2026-10-11): "good, but the wings make them weird: small jetpacks or gliders. Instead of diving into birds, let them CHASE EACH OTHER: sometimes far and smaller, sometimes closer to us, diving into the birds and out again." New file; murmuration2 is imported unchanged (flock sim helpers, `Ink` look, background, orchestral bed).

- **Characters:** Mochi and Bolt fly small JETPACKS: a grey pack on the back opposite the motion, two nozzles with flickering flames, and an exhaust plume in their colour (Mochi hot pink, Bolt cyan). The plume is thin and hot at the nozzle and widens and fades behind (0.57 s). No wings.
- **Game = TAG in 3-D:** whoever is IT chases the other along the leader's own flight line, a delayed copy of it. The lag is 0.42 s and closes to 0.07 s at a tag or 0.24 s at a miss.
  - After a tag the tagged one hovers 0.30 s (stunned), then gives chase. After a miss the leader jinks sideways and the chaser overshoots.
  - The leader's path per segment, through timed 3-D waypoints (Hermite):
    - FAR leg: z +1250, scale 0.57, small and behind the cloud.
    - THROUGH the densest patch of the flock: the birds part with the escape ripple.
    - NEAR: z -820, scale ~1.9, big in the foreground, where the tag happens. Tags alternate left and right of the frame.
  - **Depth:** each hunter (jetpack, plume, body) is drawn on its own layer. It is composited under the ink of the birds IN FRONT of it, so a hunter behind or inside the cloud is occluded by the birds nearer the camera.
  - **Parallax:** a slow lateral camera sway (70 px, 13 s; 22 px vertical, 9 s).
- **Birds:** the same flock as murmuration2: 15,000 boids on the twisting ribbon roost, density silhouette, sunlit escape waves.
  - Each hunter scares birds within 115 px in 3-D (flee 1100) and triggers the neighbour-to-neighbour alarm wave.
  - A hard 40 px clearance sphere means no bird is ever touched. The min logged distance is 40.0.
  - Lesson: hunters flying through the cloud CONSTANTLY spread it (dotty, less dense) far more than 7 dives did. The scare radius and force went down from 150 / 1500 to keep the folds dark.
- **Events (= the m2 dive beats + the cadence):**

| Event | Time (s) | Bar | What happens | Score |
|---|---|---|---|---|
| E1 | 2.22 | bar 7 | Mochi tags Bolt | M1 |
| E2 | 6.67 | bar 9 | Bolt tags Mochi | B1 |
| E3 | 10.00 | bar 10 b3 | Mochi tags Bolt | M2 |
| E4 | 13.33 | bar 22 b3, C roll | MISS: Bolt misses, "MOCHI DODGES!" (the twist) | |
| E5 | 15.56 | | Bolt tags | B2 |
| E6 | 17.78 | | Mochi tags | M3 |
| E7 | 20.00 | double-dive beat with the boom | Bolt tags | 3-3 |
| E8 | 22.40 | the cadence | Mochi tags | "MOCHI WINS 4-3! / BOLT is IT!" |

  Mochi starts as IT.
- **HUD:**
  - Caption: `Jetpack tag through 15,000 starlings | ~Who TAGS who?~`.
  - An "IT" marker over whoever is IT.
  - Event banners under the caption ("MOCHI TAGS BOLT!", "MOCHI DODGES!"), plus a "TAG!" or "MISS!" burst ring at the contact point. Banners are at full alpha from their first frame, with a 0.08 s scale pop.
  - The TAGS scoreboard (with the IT pill) at y 1405-1528.
  - Blank during the rewind; the final banner and board fade over the last 0.4 s.
- **Hook:** frame 0 = the end state. Both hunters swoop big (z -700) leftwards across the dark fold, Mochi in front, Bolt (IT) right behind. A 0.75 s rewind runs back to the start; E1 lands at 2.22 s.
- **Music:** murmuration2's bed unchanged (`m2.build_bed`). Vivaldi "Winter" RV 297 I, PD; Mutopia id 351 notes; full strings + contrabass sub, timpani roll under each chase approach plus a hit and a stab chord on each tag/miss, taiko, booms, choir pads, cadence; quarter = 108. The events sit on the same beats, so every tag lands on a stab.
- **Render:** `NF_SCALE=1.0 python scenes/murmuration3.py`. Flags: `--still --frame a,b`, `--report`, `--silent-only`, `--reuse` (re-mux only). The sim prints each segment's waypoints (screen x, y and z).
- **Checks (Full HD v1, 2026-10-11):**
  - h264 yuv420p 1080x1920 60 fps, 1518 frames = 25.30 s.
  - Audio: -14.01 LUFS, peak -5.1 dBFS, last 0.5 s at -81 dBFS.
  - flash_check: 0 = PASS (mean lum 0.17).
  - Loop seam: last -> first mean delta 0.92 vs normal frame-to-frame median 0.75 / p90 1.30.
  - Hunter scale 0.57..2.24; 3-D gap at the tags 23-81 px, at the miss 233; closest bird to a hunter 40.0 px.
  - Encoded frames read at 0, 0.25, 0.5, 1, 2, 2.22, 3, 5, 12.6, 13.33, 20.0, 22.4, 24.5.
- **Delivered:** `<VIDEOS_DIR>\batch27\murmuration3.mp4` (Full HD). Owner review: pending.
- Owner review (2026-10-11): remove the tag game; they just chill, flying around slowly and smoothly; use other music -> murmuration4.
