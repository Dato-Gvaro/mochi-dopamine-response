# ol_black_hole (DopamineEXE, channel 2)
- Batch 59 (docs/BRIEF_batch59.md #4). A face-on spiral galaxy of 1,400 stars orbits a small black hole. Stars spiral in; **every star that crosses the event horizon adds its mass and the horizon grows with the mass** (Schwarzschild r_s ∝ M). A bigger hole pulls harder, so the swallowing runs away until the last star falls in on the cadence. Accretion disc = a glowing gold ring (beamed brighter at the bottom), stars smear into arcs inside 1.9 r_h (tidal stretch).
- Caption (baked, `--cap`; `--cap ''` = base): `Every star it swallows makes it ^BIGGER^…|until it eats the ~GALAXY~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_black_hole.mp4` (**v2: the lensed finale**, Full HD, seed 3, label fhd2, **12.08 s, 725 frames**). v1 archived as `archive\ol_black_hole_v1.mp4` (11.18 s; `--lens 0` reproduces it). No 4K yet.

## v2 (2026-10-30, batch60): the gravitational-lensing finale
- Owner on v1: "ok, but can we have the famous space-movie black hole look at the end?" Brief: a glowing disc bent over and under the hole, a photon ring, warm orange-gold; a physics visual, not a copy of a film frame.
- **0-8.89 s unchanged** (same sim, same frames). After the last star (+0.15 s) the camera **tilts from face-on to 83°** and pulls back (shadow 198 -> 124 px) over 1.2 s (`--lt0 0.15 --ldt 1.2 --inc 83 --shend 124`); the full lensed view holds ~1.25 s, then the 0.6 s dissolve to frame 0. HOLD 1.7 -> **2.6 s** (12.08 s clip).
- **The disc image is ray-mapped per pixel (numpy raster, ADDed over the starfield):** Beloborodov's (2002) light-bending approximation 1 - cos α = (1 - cos ψ)(1 - r_s/r), b = r sin α / sqrt(1 - r_s/r). Solved for r it is a quadratic, so each pixel finds the disc radius it sees directly (primary image: the far side of the disc appears bent OVER the shadow). The light that went under the hole (secondary image) sits just outside the shadow: b runs from the Einstein-ring value 2 sqrt(r) (ψ = 180°) down to the shadow edge (a fitted falloff, exp(-4.5 x)): it makes the arc UNDER the shadow. Shadow b = 3 sqrt(3)/2 r_s (black), a thin photon ring at 1.015 x that.
- Disc: thin-disc emissivity r^-3 (1 - sqrt(r_in/r)), r_in 3 r_s (ISCO), r_out 7.6 r_s (blended from the v1 face-on annulus over the tilt); **Doppler beaming** (1 - β cos)^-2.4 with the orbital speed at each r: the side coming toward us is brighter and whiter, the other dimmer and redder (this is the physics the famous film left out, so ours is not a copy). Orange-gold colour map by temperature, 6 px glow, swirl streaks that orbit faster inside (Kepler), clocked from the last star so they wind gently.
- The face-on v1 disc cross-fades into the raster over 0.3 s at the start of the tilt. The background stars follow the pull-back and are point-lensed (Einstein radius 1.15 x the shadow, ramped with the tilt); 600+ extra stars outside the old frame come into view. The finale's gold rings and sparkles lie in the disc plane (they tilt and shrink with it).
- Sound: unchanged up to the F-minor tutti; the tutti holds 0.9 s longer; a soft celesta + harp rise (F minor) as the lensed view arrives (+0.81 s after the last star).

### Checks v2 (encoded Full HD, fhd2)
- h264 High yuv420p 1080x1920, 60 fps, 725 frames, 12.08 s. **flash_check PASS** (0 flashes, mean lum 0.0105).
- **-14.00 LUFS**, peak -6.98 dBFS, last 0.5 s digital silence. RMS/s -17.1, -16.8, -16.9, -16.7, -16.7, -16.8, -16.7, -16.9, -16.9, -15.2 (cadence), -16.4, -31.2 (fade), silence. 373 SFX events (unchanged).
- Frames read from the mp4 at 0, 4.5, 8.85, 9.3 (tilt), 9.8, 10.3, 11.0 (full lensed view), 11.6, 12.05 (dissolve); stills at 8.83, 9.13, 9.42, 9.75, 10.25, 11.0.
- Side safe zone: the edge-on disc spans x ~150-885 (inside 108-907).

### Doubts v2
- The full lensed view is on screen ~1.25 s before the dissolve (the tilt itself is 1.2 s). Longer = `--hold`.
- The approaching (right) side is clearly brighter than the left (beaming, physics). The film's look is symmetric; if the owner wants it more even, lower the beaming exponent (2.4) in `_emission`.
- A dark gap between the photon ring and the disc's inner edge (the ISCO's image) is physical; it reads as a thin ring inside the shadow.
- The secondary image falloff is a fit, not a ray trace; the primary image is the standard approximation (accurate to a few % outside ~2 r_s).
- Raster cost: ~0.1 s per finale frame at Full HD (4K ~4x).

### Flags v2
`--lens (1; 0 = v1) --hold (2.6; v1 1.7) --lt0 (0.15) --ldt (1.2) --inc (83) --shend (124)`.

### Upload draft v2
- Titles: "Every star it swallows makes it BIGGER… until it eats the GALAXY 🌌 #satisfying #physics #shorts" (95 chars, at the limit) · "1,400 stars vs one black hole ✨ #satisfying #physics #shorts" · "Watch the black hole bend light at the end 🕳️ #satisfying #physics #shorts" (74).
- Pinned comment: "every star it ate made it bigger, and at the end you can see gravity bend the light: the arc over the top is the BACK of the disc… at what size would you have run?"

## World (logical 1080x1920, static camera)
- Galaxy centre (508, 776), radius 392: 2 log-spiral arms (pitch 21°, 72% of stars) + scattered disc + a 5% bulge. Star size 2.0-5.3 px (cubic: few big ones, those get a soft glow + sparkle); colour by STARTING radius: warm gold core → peach → rose → violet → blue → teal rim (S 0.42-0.68): ordered, so the eaten order reads as a colour sweep. 210 faint static background stars.
- Hole: black shadow r_h, photon ring 1.03 r_h, disc 1.08-1.75 r_h (gold → orange → fade), 34 orbiting swirl streaks, a faint ripple on the horizon per swallow. r_h 22 px at M0 → 198 px (×9).
- Finale (8.89 s): 3 thin gold rings expand from the horizon + 12 sparkles on the disc; counter 0 in gold, meter "GALAXY EATEN!". No full-frame flash.
- HUD: meter y 1300 = EATEN % → gold GALAXY goal from frame 0. Counter y 1500 = STARS LEFT + "SIZE ×M" pill (pops per swallow). Watermark 35%.

## Model (`simulate`, seeded, fixed dt 1/240)
- Orbit: v² = GM/r + V0² r/(r+70) (Kepler near the hole, flat disc outside; V0 128 px/s, GM(M0) = 280² × 40). Inflow dr/dt = -K (M/M0)^1.7 (392/r)^1.6, ×(1 + 3(1.6 - r/r_h)) inside 1.6 r_h (the plunge). Swallowed when r ≤ r_h; M += (9-1)/1400 M0 per star; r_h = 22 M/M0.
- K solved by bisection so the LAST star crosses the horizon exactly at the cadence (8.887 s vs 8.889 s). Cached `output/_cache_ol_black_hole_<hash>.pkl` (`--resim`).
- Honest parts: the horizon radius is linear in the swallowed mass; inner stars orbit faster (differential rotation winds the arms); a heavier hole pulls harder. Stylised: the inflow law (real galaxies are not eaten like this).

## Timeline (clip s, seed 3)
- Frame 0: 1,347 stars, hole r 29 px, first swallow at 0.008 s. Swallows/s 60, 54, 70, 71, 117, 132, 148, 275, 420 (last 0.89 s). Left at s: 1,347, 1,286, 1,233, 1,163, 1,092, 975, 843, 694, 418 → **0 at 8.89 s**.
- r_h px at s: 29, 37, 43, 52, 61, 76, 92, 111, 146 → 198. The outer galaxy stays wide until ~7 s (r95 379 → 322 px at 7 s), then the last ~400 stars stream in as arcs. Hold 1.7 s (the disc keeps turning), 0.6 s dissolve to frame 0.

## Sound
- **Music:** J. S. Bach, chorale prelude "Ich ruf' zu dir, Herr Jesu Christ" BWV 639 (c. 1713-15; d. 1750, PD), the music of the space film "Solaris". Mutopia `Ich_ruf_zu_dir.mid` (Bach-Gesellschaft 1893; edition CC BY-SA 3.0, only the PD notes are used), saved at `<SOUNDFONTS_DIR>\scores\bach_ich_ruf_bwv639\` + .rdf + SOURCE.txt (downloaded 2026-10-29). Score beats 0-8 (bars 1-2: the chorale's first line over the flowing 16ths, half cadence on C) at a steady quarter = 54, landing on bar 3's F minor = the last star. Not on any used list; not kid-coded; not banned.
- Arrangement: violin on the chorale line (flute 8va very soft), piano + harp on the 16ths, cello + contrabass on the pedal, soft organ chords, "oohs" from bar 2; timpani roll into the end. The last star = F minor tutti: strings, piano, horns, oohs, timpani F, harp sweep, falling celesta.
- SFX: per swallow a soft glassy chime that bends down a little (no noise), on a note the score sounds there (C5-D6); big stars add a round low "whum". Sampled ≥ 14 ms apart (+0-12 ms), gain / (rate/6)^0.45. Finale: 8 falling chimes. `level_bed` (+5 dB crescendo, cadence +5 dB), `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 671 frames, 11.18 s. **flash_check PASS** (0 flashes, mean lum 0.01).
- **-14.00 LUFS**, peak -7.16 dBFS, last 0.5 s digital silence. RMS/s (audio test) -17.1, -16.8, -16.9, -16.7, -16.7, -16.7, -16.6, -16.8, -16.7, -15.2 (cadence), -26.4, silence. SFX events/s 32, 31, 36, 35, 50, 42, 42, 52, 46.
- Seam mean |delta| 0.425.
- Frames read from the mp4 at 0, 0.5, 2, 4.5, 7.5, 8.6, 8.95, 10.8 s; 1:1 crop of the disc + infalling streaks at 7.6 s.
- Side safe zone: stars x 129-887 (r95), disc ≤ 346 px from x 508, HUD 166-884: inside 0.10-0.84 w.

## Doubts
- The SFX are thinned to ≥ 14 ms, so the audible swallow rate tops out ~50/s while the visual rate reaches ~420/s.
- From ~7.5 s the remaining stars are arcs around the disc rather than a galaxy shape (they are being swallowed); the counter carries the last second.
- BWV 639 is slow and solemn (quarter 54); it fits "calm space", but it is a chorale, not a dance.

## Flags
`--seed (3) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0) --hold (1.7)`. Model `--ns (1400) --rgal (392) --rh0 (22) --grow (9) --v0 (128) --gmk --q (1.7) --p (1.6) --bulge (0.05) --plunge (3.0)`. Clock `--bpm (54)`.

## Upload draft
- Titles (≤95 chars): "Every star it swallows makes it BIGGER… until it eats the GALAXY 🌌 #satisfying #physics #shorts" · "1,400 stars vs one black hole ✨ #satisfying #physics #shorts" · "This black hole grew 7× bigger in 9 seconds 🕳️ #satisfying #physics #shorts".
- Pinned comment: "every star it ate made it a little bigger, and bigger means hungrier… at what size would you have run?"

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/ol_black_hole.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 725 frames 12.08 s; -14.00 LUFS, peak -6.98 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed fhd2. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-08\2_ol_black_hole.mp4`, 16:00 local Nov 9 (= 07:00 US East Nov 9). FHD review copy → `DopamineExe\archive\ol_black_hole_fhd.mp4`.
