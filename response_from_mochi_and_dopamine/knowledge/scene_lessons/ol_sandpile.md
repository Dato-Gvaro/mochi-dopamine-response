# ol_sandpile (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). Mechanic: the Abelian sandpile (Bak-Tang-Wiesenfeld, self-organised criticality). Skeleton: ×N growth toward an overflow. One grain can set off an avalanche of 100K+ topples, and the pile spills off the table EDGE.
- Caption (baked, `--cap`; `--cap ''` = base): `Every pile of 4 ^TOPPLES^|until it spills off the ^EDGE^`. Highlights are in the current hue.
- Delivered: `<VIDEOS_DIR>\channel2\ol_sandpile.mp4` (Full HD, label fhd). No 4K yet.

## World (logical 1080x1920)
- Table: **97×97 cells, 8 px each** (776 px), x 122-898 (inside 0.10-0.84 w), y 372-1148. One thin white outline (2.5 px, 85%) is the EDGE. Integer cell px at Fast/FHD/4K, so the numpy sprite blit is exact.
- Cells are glossy rounded squares. Empty table cells are faint dark dots (the table surface).
- Colour: hue = a radial rainbow from the centre (gold) to the CURRENT front (red), smoothed τ 0.35 s, so the mandala is a full rainbow at every size. Height offsets on that hue: 0 = +0.33 (S .45), 1 = +0.50 (S .70), 2 = +0.06 (V .70), 3 = base. The 2/3 checkerboards read as one hue, and the 0/1 cells draw the fractal lines.
  - Rejected: fixed 4-hue palettes. Red/yellow/cyan/violet was speckle noise at this size; pink/violet was monochrome.
- Cells with ≥ 4 grains (mid-topple) are drawn 50% toward white, so the avalanche front is visible. Toppled cells glow +16%, decaying ×0.72 per frame. Colours lerp 0.55 per frame (gradual re-colouring).
- Pour: white beads fall from y 340 onto the centre cell. Each bead lands at the exact time its grain is added (sampled ≥ 1/300 s apart), with a small ring every ≥ 0.11 s.
- Spill: every grain thrown off the table is one falling particle (6,048 in v2). Each moves outward from its boundary cell, with gravity 1500 px/s², 2.6 s life, colour from that edge cell's palette.
- HUD (same look as ol_spiral_center):
  - EDGE meter at y 1236, x 170-846: rainbow fill, white marker, a table icon + "EDGE" goal from frame 0. Value = (max Chebyshev radius of toppled cells + 1)/(C + 1), so it hits 100% at the first spill.
  - "AVALANCHE ×N" pill at y 1312 in the current hue: the biggest avalanche in progress, held 0.4 s. After the pour stops it holds the finale's peak.
  - TOPPLES counter at y 1482 (118 px), black under-stroke.
  - Watermark under the table's bottom-right.

## Simulation (exact integers, deterministic, no RNG in the maths)
- Grains drop on the centre ONE at a time. Each avalanche is relaxed in synchronous waves (every cell ≥ 4 topples once per wave) until the table is stable, then the next grain drops. Grains toppled off the boundary leave the table.
- Playback units = 1 per grain drop + 1 per wave. Rate r0·e^(t/τ), τ 4.2 s, solved so that the first spill wave plays at 8.20 s. After the EDGE the pour opens up ×2.6 (eased over 0.5 s) for 1.25 s, then stops. The last avalanche finishes, then a hold.
- Avalanches therefore ripple outward over several frames: ~15 units/frame at the start, ~400 in the finale.
- Raw sim (36,000 grains, 255K units) is cached at `output/_ol_sandpile_raw_G97_N36000.npz` (~10 s to rebuild).

## Timeline (clip s)
- v2 (coordinator, 2026-10-21): frame 0 starts LATER in the same simulation, because v1's frame 0 (1,611 grains, meter 31%) read too empty on a phone.
- Frame 0 = **5,224 grains** on the table: the mandala is ~57% of the table width, meter 0.55, counter 500,626, badge ×6,659. The pour is already falling and the first topple is on frame 0. The pre-roll (-0.6 s) is the dissolve target.
- Topples per second: 138K, 199K, 257K, 361K, 496K, 720K, 1.03M, 1.32M, then 3.5M at the EDGE + finale pour (climbing to the last pour frame).
- Grains per second: 670 → 2,404 (7 s) → 5,300 (finale).
- Meter: 0.57 (0 s), 0.67 (2 s), 0.78 (4 s), 0.90 (6 s), **EDGE 8.20 s** (5.37M topples).
- Badge peaks: 23K (0-1 s) → 44K (4 s) → 96K (7 s) → 139K (finale).
- The pour stops at 9.45 s (grain 25,971). Total 11.34M topples; **6,048 grains spilled** off all 4 edges.
- Dissolve 10.65-11.25 s. **11.25 s, 675 frames.**

## Sound
- **Melody:** Schubert, Impromptu in E-flat D 899 No. 2 (Op. 90/2, 1827), bar 8's rising scale into phrase 2, through bar 16 (MIDI beats 31.33-55: F4 G4 Ab4 ... into the theme's return at beat 34), both hands. v1 used beats 9-55 (136 slots); v2 starts later so the E-flat arrival still lands on the EDGE.
  - Source: Mutopia "Mutopia-2008/09/28-1551" (Breitkopf & Härtel 1888, Ph. Raynaud), Public Domain. Files in `<SOUNDFONTS_DIR>\scores\schubert_impromptu_d899_2\` + `SOURCE_mutopia_1551.txt`.
- **Walk:** 71 RH slots, one per sampled avalanche (avalanches of ≥ 8 topples). A greedy min gap shrinks 50% over the build: 7 → 12 notes/s, close to the piece's real tempo.
  - The avalanche size sets the note's loudness (log-scaled). The top 12% by size add a low-octave doubling (17 notes).
  - The LH follows the same beat→time map: piano, contrabass on downbeats, strings on the phrase-2 chords, timpani Eb2 at phrase 2. Oohs swell into the edge.
- **EDGE (8.20 s):** bar 16's E-flat arrival as a rolled Eb major chord (Eb1-Eb5) + strings, oohs, contrabass, timpani Eb2 and boom (`--fin` 2.4).
- **SFX:** a tonal glass-bead "tk" per sampled topple wave (f 1.5-2.5 kHz + 2.76f partial, 7-14 ms, 0.6-0.9 kHz body, **no noise**).
  - Min gap 40 → 13 ms (≥ 12 ms), gain by the frame's topples ÷ √(rate/25): 24 → 61 ticks/s.
  - Lower bead patter (1.1-1.9 kHz) for the spill.
  - No cymbal/riser (no whoosh).
- `audio.master(peak_db=None, reverb=0.5)`, sfx ×0.30. The last 0.6 s is zeroed; the wav is padded +0.1 s so the mux's `-shortest` keeps every frame.

## Checks (encoded Full HD, v2)
- The mp4 is h264 yuv420p 1080x1920, 60 fps, 675 frames, 11.25 s.
- flash_check PASS (0 flashes, mean lum 0.027).
- **Audio:** -14.00 LUFS, peak -4.36 dBFS, last 0.5 s digital silence. RMS 0-3 s -20.4, 3-6 s -20.0, 6-8.1 s -15.4, EDGE + spill 8.2-9.6 s **-12.1** (+3.3 dB over the late build), hold -15.8.
- **Seam:**
  - Pre-encode (Fast): last→0 mean 2.07, against normal steps 0→1 2.63 and 673→674 1.87. One step of motion.
  - Encoded: 3.18, against encoded steps 2.1-2.7. The I-frame accounts for the gap; the scene is busier from frame 0 now.
- Frames read from the mp4 at 0, 1 s, 4.1 s, the EDGE (8.2 s), the spill (8.8 s, 10.0 s) and the last frame (1:1 crops at frame 0 and the EDGE). Frame 0 shows the mandala at ~57% of the table width with the bead stream falling. The last frame equals the pre-roll before frame 0.
- v1 (16.65 s, frame 0 at 1,611 grains): flash PASS 0, -14.00 LUFS, peak -4.68, seam pre-encode 0.70 vs steps 0.57-1.06. Superseded by v2.

## Flags
`--label --cap --still --frame a,b,c --dry --sound 0 --sfx (0.30) --fin (2.4)`. Timeline: `--g0 (5212) --tau (4.2) --te (8.2) --b0 (31.33) --pour (1.25) --boost (2.6) --hold (2.45)`. Look: `--offs --sats --vals2 --pal radial|fixed --hues --vals`. Sim: `--grid (97) --nmax (36000)`. `--stable` is a test that shows only stable states.

Owner review (2026-10-21): "not so interesting, maybe later when the channel is more popular" -> reserve.
