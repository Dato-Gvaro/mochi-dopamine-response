# sluice_race2 — HEAVY WATER: Mochi vs Bolt ride boats down two flooded shafts

- From the owner's review of sluice_race (2026-10-07): "good starting idea; play more with the water physics, make it heavier". sluice_race.py is untouched. This file has a new water engine, 4 bigger chambers (+ basin) and bigger characters.
- Geometry: shaft centres x 270/810, interior 410 wide, walls 24. Chamber pitch 400, slab 34, basin 430. Water volume per shaft: depth 200 x 410. Characters r 46 (CHR 32 x BS 1.45), hull half width 99. Camera spring-follows the boats (CAM0 -560 -> CAM1 687).
- Water engine:
  - Each chamber is a 1-D shallow-water solver (Saint-Venant): 82 cells, MUSCL + Rusanov, SSP-RK2, CFL-subdivided, reflective walls, light friction 0.35/s.
  - Torrents are parcel sheets: Torricelli outflow per open cell (Cd 0.55). Each landing adds mass plus outward plunge momentum, which throws surge waves that run across, climb the far wall and rebound.
  - Splash particles fly up and fall back. They are drawn as unions of soft discs (one foamy mass) or drops. There is mist at the foot of each fall, and foam from impacts, steep fronts and fast flow.
  - Low-flux sheets narrow, so drips read as drips.
  - The aqueduct pours softly (plunge momentum x0.12) so the top chamber is not piled against one wall.
- Boat: dragged by the local current, slides down the surface slope, slams off walls (thunk + wave), and bobs under buoyancy (free fall above the surface, damped spring below).
- 4 gates, each a different water machine:
  1. **BOLTS:** the plate is strained by the water load. Creaks, then 3 bolts pop with sparks (da-da-da), then the plate is shoved into the wall pocket (DUM). Identical on both sides, so the start is synced; the burst is at 1.09 s.
  2. **WHEEL:** the torrent pounds a mill wheel set in the outer wall, and the falling boat is struck and flung by it. The wheel winds a chain (seeded slack, gear and friction) to a pinion that slides the next plate open.
  3. **FLOAT:** a float on a lever rides the surge waves. A big enough wave trips it (the threshold drops over time) and the bung is yanked up, making a whirlpool. The boat swirls and is swallowed (dizzy face).
  4. **DAM:** twin leaves hold the reservoir. Strain builds and the leaves sag; 8 creaks; 4 rivets pop; then it bursts and a huge wave hits the basin.
- While their gate holds (FLOAT, DAM), the characters stomp in their boat, making waves that load the gate or float. They look worried and sweaty when the strain is above 0.25.
- Loop:
  - Hold 1.9 s after the loser lands. Then the basin outlet lifts and the water and boats are swept out.
  - All gates ease shut and the shafts' leftover puddles drain away. The wheel snaps to a whole paddle, so the wheel, chain and pinion repeat.
  - The camera flies to the top, and the last 2.0 s replay the pre-roll (aqueduct refill + boats off the chute) = frame 0.
  - Pre-encode seam 2.93 against a 2.76 normal step. Encoded seam 3.28 against ~2.8-3.2 for neighbouring steps (the water is always moving).
- Sound:
  - Notes: beethoven_5 (PD) on piano, one note per landing, burst, plug pop, bolt pop and stomp. Synced pairs make a fifth chord; the winner gets 4 notes, the loser 2.
  - Bed (built in the scene, not regenerable from `_events.json`), all discrete:
    - a heavy water BOOM per torrent impact and per boat landing, plus a short gush
    - stick-slip creaks
    - a metal ping per bolt
    - wooden thocks per mill-wheel paddle, and rack ticks as the plate winds
    - wall thunks and stomp thumps
  - Events: a clank on each burst and slam, a latch on the float trip and the gate opening, a deep plop when the plug pops, splashes.
  - Nothing sounds after T-1.3 s.
- s476 (default):
  - Synced through chamber 2: both boats land at 2.30 s.
  - Chamber 3: Mochi by 0.05 s. Bolt's float trips first (7.58 against 7.79), so Bolt leads into the dam chamber (8.78 against 9.09; LEAD CHANGE!).
  - The dams burst almost in sync (12.76 / 12.82). Mochi's boat drops first: **MOCHI WINS by 0.09 s** (13.77 against 13.86).
  - Clip 18.07 s (1084 f).
  - Mixed events per 2 s: 16, 8, 8, 12, 5, 13, 20; the dam stage is densest. The bed adds booms, creaks and thocks.
- Search: `--search N` keeps Mochi wins with a margin of 0.05-0.35 s, at least 1 lead change with the last one at the basin, and the loser landing at 13-17.5 s. Only 5 of 1500 seeds pass, and s476 is the only one with 2 lead changes.
- Checks (encoded Full HD): h264 yuv420p 1080x1920 60 fps, 1084 frames; -14.01 LUFS, peak -6.5 dBFS; last 0.5 s silent; flash_check 0 flashes = PASS (mean lum 0.033).
- Args: --seed (476), --label, --cap "line1|~line2~", --melody, --voice (piano), --search N, --still --frame N[,N...].
- Delivered <VIDEOS_DIR>\batch17\sluice_race2.mp4 (Full HD). Owner review: pending.
