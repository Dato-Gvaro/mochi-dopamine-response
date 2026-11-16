# ol_moon_fill (DopamineEXE, docs/BRIEF_shorts_1115.md D3)
- New file, forked from `ol_ring_multiply.py` (ball engine, HUD helpers, sound helpers). FILL + ×2 + picture reveal. Caption (post-render overlay; base `--cap ''`): `Every bounce = ^2 balls^|until it's a ~FULL MOON~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_moon_fill.mp4` (FHD, seed 6, base `output/ol_moon_fill_fhd2_9x16.mp4`, captioned `..._fhd2cap_9x16.mp4`; fhd2 = fhd1 video + audio re-mux after the timpani fix). 12.70 s, 762 frames.
- 4K (2026-11-15, owner: schedule filler): `<VIDEOS_DIR>\DopamineExe\reserve\ol_moon_fill_4k.mp4` + `ol_moon_fill_4k_UPLOAD.md`. Base `output/ol_moon_fill_4k_9x16.mp4` (`NF_SCALE=2.0 --label 4k --cap ''`), caption `--capimg output/ol_moon_fill_cap_4k.png` overlay. 2160x3840, 762 f, -14.01 LUFS, flash PASS, frames match the FHD. The FHD moved to `archive\reviewed_2026-11-15\`.

## World (logical 1080x1920)
- Ring centre (508, 770), R 360 (x 148-868): silver 3 px line over a dark under-stroke. Moon ghost 8% inside from frame 0.
- Balls r 7 fixed. **N_FULL = int(0.82 (R/r)²) = 2,168** (FULL = ball area / (disc area × 0.82)).
- Colour by generation (splits back the line): 7-knot sweep coral → amber → gold → green → teal → blue → violet, S ~0.6-0.75, scaled to the gen p99. Children are born at the wall, so the pack is ordered by radius (old core, new rim). That is not confetti.
- HUD: phase row y 366 (8 icons NEW → FULL, x 214-802, the FULL icon gold from frame 0, the current one ringed, pops when reached at fill k/7). Counter y 1296 (112 px) + ×2 pill / BALLS / FILL % at 1346. Watermark 868 right, y 1226.
- Finale: gold counter at FULL. A wave front (soft silver band) sweeps x 148 → 868. Each ball recolours over 0.14 s (with a silver lift) to the Moon at its position. The ghost rises to 30% behind the revealed part. The rim glow is an annulus R → R+52 (warm silver), never a disc. The FULL MOON gold pill replaces the BALLS row.

## Physics (`simulate`, seeded, dt 1/60 × 4 substeps, cached `output/_cache_ol_moon_fill_*.pkl`)
- One ball from the centre at 640 px/s; gravity 300 px/s² until FULL.
- Wall: elastic reflection. **A split = a real bounce:** normal speed > 150 px/s (`--vnmin`) and > 0.08 s since that ball's last split (COOL).
  - Without it, balls pressed on the wall by gravity split every substep: 77 → 2,168 in < 1 s, gen max 44.
  - The two children sit touching at the contact. Each leaves at the reflected velocity ±16° (×0.75-1.25), or unfanned if that would graze the wall.
- Ball-ball: equal-mass elastic impulses on cKDTree pairs + 50/50 overlap correction (2 passes above 600 balls). Speed cap 1,400.
- At FULL: gravity off, damping τ 0.16 s → the pack rests in ~0.4 s.
- The doubling ACCELERATES as it fills (rebounds off neighbours send balls back to the wall). That is physics, not tuning.
- Seed search (timing only): seeds 1-6 × v 640/720. Seed 6 / v 640 has the fastest opening (2, 6, 12, 35 at 0-3 s). FULL 7.4-8.5 s across seeds.

## Timeline (clip s, seed 6)
- Frame 0 = sim 1.58 s, 0.20 s before the 2nd split (2 balls mid-flight).
- Balls at s: 2, 6, 12, 35, 95, 266, 657, 1,423 → **2,168 at 7.64**. Splits/s 4, 6, 23, 60, 171, 390, 761, 751 (in 0.64 s). Gen max 34.
- Wave 8.06-9.77; G#7 9.77; **FULL MOON 10.39**; hold 1.5 s; 0.8 s dissolve into the pre-roll (frame 0's past), so the last frame leads into frame 0.

## Sound
- **Music:** Beethoven, Piano Sonata No. 14 "Moonlight", Op. 27 No. 2, iii Presto agitato (1801; Beethoven d. 1827, PD).
  - Notes: Mutopia Project `BeethovenLv/O27/moonlight` `moonlight3.mid` (Berners 1908 ed.; engraving CC BY-SA 2.5, the PD notes only), cached `<SOUNDFONTS_DIR>\scores\beethoven_moonlight3\` (no SOURCE.txt there; provenance per docs/scenes/last_standing.md).
  - Previously used by paint_reveal, sort_wheel and last_standing. The brief chose it.
- **Clock:**
  - One RH 16th per split (splits ≥ 0.09 s apart) until the splits outrun 2.3 beats/s. That is 3 notes, to 1.50 s.
  - Then a linear tempo ramp 2.30 → 2.34 beats/s, so that **beat 15 (bar 4's sf chord, the G# dominant) = FULL**.
  - Steady through bar 5 (the wave, beats 16-20), then a ritardando: a G#7 (piano + strings) at beat 20, then the **C#-minor tonic at beat 21 = FULL MOON**.
  - The brief's plan (bar 6 sf = FULL, wave bars 7-8) needed 5.4 beats/s, so it was rejected.
- **Arrangement:**
  - piano RH/LH from the score (sf chords +0.12 velocity);
  - cello + contrabass on the bar's bass from bar 3;
  - strings_slow pad on each bar's RH pitch classes;
  - a timpani roll into FULL and a timpani G# on it (fhd1 had C#, a 4th under the G# chord: fixed by audio re-mux);
  - for the wave, an 18-note celesta + harp rise on the harmony;
  - for FULL MOON, strings_slow, strings, oohs, a rolled piano, a harp sweep, falling celesta, cello/contrabass C# and soft horns.
- **SFX (own waves, < 5.5 kHz, no noise):**
  - a glass-marble "tik" per split (2.3 kHz modes + a 760 Hz body), thinned ≥ 14 ms (+0-12 ms), gain ÷ √(rate/6);
  - a "pip" on a sounding note per split (all of the first 66, then ≥ 50 ms apart);
  - soft packing clicks (ball-ball contacts > 60 px/s, ≤ 25/s) FULL-0.6 → FULL+0.7;
  - a soft synthesized gong on C#2 at FULL MOON.
  - 362 events: 205 tik, 136 pip, 20 click, 1 gong.
- Mix: `level_bed` (+5 dB crescendo, cadence +4 dB) + SFX × 0.55 → `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence.

## Checks (encoded FHD, fhd2cap)
- h264 High yuv420p 1080x1920 @60, 762 frames, 12.70 s.
- **-14.01 LUFS**, peak -5.98 dBFS, last 0.5 s silent. RMS/5 s -19.8, -16.9, -15.2.
- **flash PASS** (0, mean lum 0.023).
- Seam 0.261.
- Onsets (> 1.5 kHz flux) in 0-5 s: 22/22 within 30 ms of a split event.
- Frames read at 0-12.68 s (sheet); 1:1 crops at 0, 6.5 (phases, counter), 7.3 (the jammed pack), 8.9 (the wave front) and 11.0 s.
- The base (no caption) has no stray text.

## Moon image
- `assets/ol_moon_fill/lroc_color_poles_1k.png` + SOURCE.txt.
  - Source: NASA SVS "CGI Moon Kit" (SVS 4720), the LROC WAC colour mosaic, US-gov PD; credit "NASA's Scientific Visualization Studio".
  - Equirectangular 1024x512, lon 0 at the centre.
- Near side by orthographic projection (bilinear), display tone `rgb^0.85 × 1.10 × (1.02, 1, 0.95)`.
- Ball colours come from a 9 px box-blurred copy (720 px grid), batched into 41 brightness bins.
- **4K:** the ghost surface is built at device px (2R × NF_SCALE) and drawn under a `2R/npx` scale inside the logical ctx (no identity_matrix mixing), so it stays the same size at any scale.

## Flags
`--seed (6) --label --cap --capimg <png> --still --frame a,b --dry --audio --resim --sound 0 --sfx (0.55)`. Physics: `--R (360) --rb (7) --g (300) --v (640) --fan (16) --vnmin (150)`. Clock: `--bfull (15) --rsw (2.3) --hold (1.5)`.

## Caption pass
`NF_SCALE=1.0 python scenes/ol_moon_fill.py --capimg output/ol_moon_fill_cap_fhd.png`, then `ffmpeg -i base.mp4 -i cap.png -filter_complex "[0:v][1:v]overlay=0:0:format=auto,format=yuv420p" -c:v libx264 -crf 18 -c:a copy`. The highlight is a fixed coral (gen-1 hue).

## Doubts
- The opening is 2-12 small balls for 2 s (the brief's frame 0). The streaks and spark rings carry it, but it is the weakest second.
- FULL is 7.6 s vs the brief's 9.2 s (see Physics).
- The packed Moon shows a ~18% black gap lattice between balls. The ghost underlay softens it.

## Outcome
- (fill after review)
