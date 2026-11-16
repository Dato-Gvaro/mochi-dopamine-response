# ol_planet_ring (DopamineEXE, channel 2)
- Batch 57 (docs/BRIEF_batch57.md). An asteroid hits a moon orbiting a planet; the moon breaks into 22 chunks; **every chunk that collides with another splits in 2 (3 on a hard hit)**; Kepler shear (inner pieces orbit faster) smears the debris along the orbit until its two ends meet = a closed RING.
- Caption (baked, `--cap`; `--cap ''` = base): `One hit ^SHATTERS^ the moon…|until it becomes a ~RING~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_planet_ring.mp4` (Full HD, seed 7, label fhd, **10.82 s, 649 frames**). No 4K yet.
- **Shipped 4K (batch58, unchanged):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-06\2_ol_planet_ring.mp4` (seed 7, label ship), 16:00 local Nov 7 (= 07:00 US East Nov 7); owner: "interesting; may get better but let's not overcomplicate". FHD review copy archived as `archive\ol_planet_ring_fhd.mp4`.
- 4K checks: h264 High yuv420p 2160x3840, 60 fps, 649 frames, 10.82 s; **flash_check PASS** (0 flashes); **-14.00 LUFS**, peak -5.13 dBFS, last 0.5 s digital silence; seam mean |delta| 0.151. Frames read at 0.1, 0.5, 3, 6, 7.7 (+ 1:1 crop of the ring), 10.7 s.

## World (logical 1080x1920, static camera)
- Planet centre (508, 772), r 128: deep blue banded sphere lit from the upper left, thin atmosphere rim. The orbit plane is seen tilted (screen y = y x 0.50): the back half of the ring passes behind the planet, the front half in front. Faint static stars.
- Moon r 30 (grey, craters) on a circular orbit a = 300, period 4.4 s. Goal from frame 0: its orbit as a faint dotted ellipse; every 3° arc that already holds debris is drawn solid (the ring visibly closing), gold at RING COMPLETE. Ring x span ~ 150-870 (inside 0.10-0.84 w with the outermost dust at the edge).
- Debris colour by orbit (semi-major axis): inner sky blue -> teal -> pale gold -> amber -> coral outer (S ~0.42-0.58): the ring is an ordered rainbow, inner = fast = blue. Pieces >= 3.2 px are tumbling rock polygons (rock grey tinted by orbit colour); smaller = dust dots.
- Impact: the asteroid streaks in from the upper left (warm trail), a small local warm glow (r <= 75 px) + a thin shock ring. No full-frame flash.
- Finale (7.62 s): 3 gold shimmer waves run round the ring, 14 sparkles on the orbit, the solid ghost arc turns gold, counter gold.
- HUD: meter y 1290 = ring complete % (share of 3° arcs with >= 3 pieces), "RING n%" -> "RING COMPLETE", gold RING goal from frame 0. Counter y 1488 "FRAGMENTS" + "×2" pill (pops on every split). Watermark DOPAMINE.EXE 35%.

## Physics (scenes/ol_planet_ring.py `simulate`, seeded, exact)
- Point gravity GM/r² from the planet (GM from a = 300, P = 4.4 s), leapfrog at dt 1/240. Debris = test particles (no self-gravity). Pieces that reach r < 128 fall into the planet.
- The hit: 22 chunks (Dirichlet split of the moon's volume) with a velocity spread of 6% of the orbital speed (tangential + radial) + a 25 px/s outward blast.
- Collisions once per frame (cKDTree): inelastic (restitution 0.10). Normal impact speed > 3 px/s splits each piece (radius / 2^(1/3); 3 pieces on a hit > 12 px/s) unless it is dust (r <= 0.8 px) or split in the last 0.30 s; the pieces part at 0.3 x impact speed + 1 px/s.
- After RING COMPLETE the ring settles (no more splits; gravity only), so the count freezes.
- Seed choice: NCH 22, SIG 0.06 scanned over seeds 1-8 and a 32-way parameter grid; seed 7 = the only one with early splits (the first within 0.5 s), a doubling count to the end and a narrow ring (5-95% of the debris at 0.88-1.16 a). `output/ol_planet_ring_sim_<hash>.pkl` caches the sim (3 min).

## Timeline (clip s)
- 0.18 s the hit. Fragments at s: 1, 30, 110, 254, 915, 4,828, 16,168, 31,573, **39,569** (complete). Splits/s 4, 48, 84, 434, 3,236, 10,337, 14,454, 7,569 (in 0.62 s).
- Ring % at s: 0, 4, 12, 22, 36, 49, 77, 88 -> **100 at 7.62 s** = the cadence. Hold 2.6 s (the ring keeps orbiting and evens out), 0.6 s dissolve into frame 0.

## Sound
- **Music played as music:** E. Grieg, "Morning Mood", Peer Gynt Suite No. 1 Op. 46 (1875/88; d. 1907, PD), score beats 3-15: the flute's famous theme (bars 1-4) to the strings' E-major entrance at beat 15 = RING COMPLETE. Steady **95.3 bpm** (quarter; dotted quarter 63.5). Source: midiworld.com `1_morng.mid`, saved at `<SOUNDFONTS_DIR>\scores\grieg_morning_mood\` + SOURCE.txt. Not on any used list; not kid-coded; not banned.
- Arrangement: 2 flutes, clarinet, 2 bassoons, horn, viola from the score + a soft string pad + harp; timpani roll into the cadence. Cadence = E-major strings (as the score enters) + the oboe's answer (B-G#-F#-E), horns, harp roll, falling celesta, timpani E.
- SFX: the hit = a soft deep tonal thud (E2/E3 sine, short pitch drop) + a timpani E. Per split: a soft crystalline chime (bell partials < 5.5 kHz) on a note the score sounds there, higher for smaller pieces; big rocks (r >= 4) a round stony knock (low sines). Sampled >= 12 ms apart (+0-16 ms jitter), gain / sqrt(rate/6). Finale: 8 falling chimes.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 649 frames, 10.82 s. **flash_check PASS** (0 flashes, mean lum 0.011).
- **-14.00 LUFS**, peak -5.13 dBFS, last 0.5 s digital silence. RMS/s (audio test): -16.5 (hit), -19.4, -18.7, -18.6, -18.7, -17.3, -17.1, -16.4, -13.4 (cadence), -15.1, silence. SFX events/s 3, 18, 27, 34, 33, 34, 35, 25 (to 7.6 s).
- Seam (check_clip): mean |Δ| **0.202**.
- Frames read from the mp4 at 0.1, 0.5, 1, 2, 5, 7.6, 8.5, 10.7 s; fast stills at 0.2, 0.7, 1.5, 3.3, 5, 7, 7.6, 8.3 s.

## Doubts
- At RING COMPLETE (7.6 s) the ring is closed but lopsided: dense on the left, a thinner blue inner stream on the right; it evens out during the 2.6 s hold (min 15° arc 4% of the mean at completion, ~30% by the end). A stricter "complete" would need ~2 s more splitting (60k+ pieces).
- The first 2 s are the hit + 22-110 rocks drifting along the orbit (few splits, small sparkles); the count climbs fast from 3 s.
- Physics simplifications: no debris self-gravity; collisions resolved once per frame; the split rule (any > 3 px/s hit) is the video's rule, not a fracture model.

## Flags
`--seed (7) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0) --hold (2.6)`. Physics `--kt (0.50) --rp (128) --a0 (300) --p0 (4.4) --rm (30) --nch (22) --sig (0.06) --sigr (1.0) --vexp (25) --en (0.10) --vsplit (3) --kick (0.3) --kick0 (1.0) --rmin (0.8) --xs (1.0) --cool (0.30) --bins (120) --binmin (3) --th (146)`.

## Upload draft
- Titles: "One hit shatters the moon… until it becomes a RING 🪐 #satisfying #physics #shorts" · "1 moon became 39,568 pieces… and they made a ring 🪐 #satisfying #physics #shorts" · "This is how planets get their rings 🪐 #satisfying #physics #shorts".
- Pinned comment: "every piece that hit another one split in two and the orbit did the rest… would you rather have the moon or the ring?"
