# glass_tower2
- This reworks glass_tower after the owner's review (2026-10-17): "booooring — maybe instead of water we drop a large amount of small balls and overflow it? to catch attention in 2 seconds". glass_tower.py is untouched; this file imports only its verified melody and text helpers.
- **Nameable change:** the liquid becomes a torrent of thousands of small glossy rainbow balls, and every glass must OVERFLOW.
- Caption (baked, `--cap`): `Every glass must ^OVERFLOW^|~Even the last one~`.
  - The coordinator asked for "Even the last corner". In ball physics the last glasses are the bottom MIDDLE ones (see Physics), so "corner" would be a false promise.
- Readout: `GLASSES FULL n/21` at y 1432, plus a pulsing gold `2 LEFT` / `1 LEFT`.

## World (logical px)
- 21 coupes in rows 1-6.
  - Rim width 104, pitch 148, so the gap between two rims is 44 px (6.9 ball diameters). The bowl is a half-ellipse 50 deep, and rows are 158 apart.
  - The axis is x 470. The tower spans x 18-922, with the right corner rim at ≤ 0.85 w. The floor is y 1352 = 0.704 h.
- Row hues: red, orange, yellow, green, sky, violet. A ball shows the hue of the row of the glass it is in. Balls in the pour, and balls on the floor, show their own random hue, so the stream, the heaps and the floor sea are rainbow.
- The balls are r 3.2, glossy sprites (48 hues).
- A glass tube (x 474, mouth y 304) releases the torrent.
- Stems and feet are drawn behind the balls and are visual only.

## Physics (s2; px, s)
- **Solver:** position-based dynamics, 6 substeps per frame.
  - Gravity is 2400, with a terminal speed of 1250 (air drag, and no tunnelling).
  - Ball-ball contacts use a cKDTree pair search. They are inelastic: restitution 0.08, plus pairwise friction 0.3.
  - Bowls are thin two-sided walls: 16-segment half-ellipse polylines, looked up through a 16 px cell table. Walls and floor have restitution 0.15.
  - The frame edges are walls, so the spill stays on screen as a sea.
- **In 2D a foot spans the gap it stands over.** Colliding feet would plug the cascade, so feet don't collide.
- **Full rule:** a glass counts as full (overflowing) when its bowl holds ≥ 86 balls (filled to the rim) for 6 frames.
- **Pour:** Q = 130·exp(0.008 t + 0.0003 t²) balls/s, which is 130 at frame 0 and about 230 at the last glass.
  - The torrent runs 8 s before frame 0. Frame 0 shows rows 0-2 full and heaped, row 3 filling, 1120 balls, and the readout at 5/21.
- **Emergent order:** the bottom-MIDDLE glasses are last.
  - Earlier tunings had 3-diameter gaps. There the balls arched across the gaps and jammed. The 44 px gaps fixed that, but balls rolling over the heaps still cross the gaps sideways instead of dropping into them. So the glasses under the gaps get less than the binomial share.
  - This held for every seed and gap tried (A 48-58).
- **s2 fills:** row 2's last glass at 0.15 s; row 3 at 3.3-5.8; row 4 at 9.4-11.9; row 5 at 15.2 … then (5,2) at 19.55, and **(5,3) at 21.65**.
  - 2 LEFT lasts 0.82 s and 1 LEFT lasts 2.10 s.
  - Fills per 5 s: 4/3/3/5/1.
- **Finale:**
  - **Dump:** the tube opens to 5x for 1.2 s. Balls pour over every full glass down the whole pyramid and flood the floor; at most 5459 balls.
  - Every glass glows, with a rising band of light and sparkles.
  - The camera zooms 1.0 → 0.93 and back.
  - At last glass + 3.4 s a 0.6 s dissolve runs into the pre-roll.
- The clip is **25.73 s (1544 frames)**. The sim takes about 50 s, one process. It is cached as `output/glass_tower2_sim_<args>.pkl`; `--resim` forces a new run.

## Sound
- **Rattle (ASMR):** at most one merged contact event per frame.
  - It holds 1-5 micro-clicks over about 10 ms. Each click has 3 modes with millisecond decays: a ball-ball plastic tik at 1.05-1.5 kHz, a ball-glass tink at 1.3-1.75 kHz, and a floor tok at 520-760 Hz. There is no noise.
  - A frame's chance of getting an event follows its contact count, so the rate climbs: 132 → 150 → 188 → 218 → 249 per 5 s.
  - Level follows the frame's impact energy, and is density-aware.
- **Melody:** the same Vivaldi Spring line as glass_tower (Mutopia 301, violin I bars 1-10, −12, 73 onsets; verified with `python scenes/glass_tower.py --verify`).
  - It plays as a clean crystal ting at the note +12, topping out at C#6. Overflows are brighter and louder. Between overflows, the onsets land on a glass's first balls and on its pile passing eighths of a full bowl.
  - Notes per 5 s: 17/16/19/18/3. The last glass is onset 72, the cadence E.
  - A soft harp doubles the overflow notes.
- **Cadence:** a rolled E-major harp chord, a strings + oohs swell, a soft timpani, and a glass chime (E5 + B5).
- Onsets are ≥ 12 ms apart. `master(peak_db=-6)`. Energy above 3 kHz is 0.32%.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1544 frames = 25.73 s.
- -14.01 LUFS, peak -8.36 dBFS. The last 0.5 s is digital silence.
- flash_check PASS (0 flashes).
- **Loop:** the last frame is identical to pre-roll frame -1. Pre-encode, last→0 is 0.736 against a normal step of 0.731 (perfect).
  - check_clip's encoded seam is 1.055, just under its 1.1 "broken" line, because every normal frame step is large: thousands of balls are moving.
- Encoded frames read at 0, 0.5, 1, 2, 3, 12, 21.65 and 23.2 s (the dump).
- Single process throughout: sim about 50 s, Full HD render a few minutes.

## Doubts
- **"Last corner" became "last one".** The physics does not starve the corners with balls. The coordinator should decide whether to keep this honest caption or rework the geometry.
- Fills per 5 s are flat. What climbs is the rattle and the pour.
- The floor sea is a thin layer until the finale dump. The balls are tiny (6.4 px), chosen for "thousands"; individually they read only as glitter on a phone.
- 0-3 s: the fill counter moves only 5 → 6/21. The motion carries the hook, not the counter.

Delivered `<VIDEOS_DIR>\batch40\glass_tower2.mp4`. Owner review: pending.

Owner review (2026-10-17): fewer rows; start empty; Mochi & Bolt on top pour two colours; which colour stays more in the glasses -> glass_tower3 (frame 0 = pour already hitting the empty top glass).
