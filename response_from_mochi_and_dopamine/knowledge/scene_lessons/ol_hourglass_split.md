# ol_hourglass_split (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). Skeleton: ×2 growth toward a named end state (research/early_breakouts.md). A PRESS pushes rainbow grains down through an hourglass neck; every grain through the neck becomes 2, so the bottom fills twice as fast as the top empties, jams full, and the pressure breaks the glass.
- Caption (baked, `--cap`; `--cap ''` = base): `Every grain through the neck ^SPLITS^ in 2|until the glass ^BREAKS^`. Highlights in the current grain hue.
- Delivered: `<VIDEOS_DIR>\channel2\ol_hourglass_split.mp4` (Full HD, v2, seed 5, label fhd2). No 4K yet.
- **v2 (owner review 2026-10-22):** "it does not look natural for the glass to break just from pouring". Changes:
  - Added the press; it is the honest driver now (neck wear set to 0).
  - The break is caused by the press against a jammed bottom.
  - Caption line 2 is now BREAKS, the meter goal is BREAK.
  - Colour rule: smooth gradient at S 0.75.
  - Added a tonal push pulse.
  - v1 (pour only, neck wear, OVERFLOWS) is superseded; its file is backed up in the session scratchpad only.

## World (logical 1080x1920)
- **Glass:** one thin white line (2.5 px, 85%), centre x 508.
  - Top chamber: straight walls, half-width 330 (x 178-838), open at y 372 with small rim lips. It narrows in a 156 px funnel (0.40 H) to the neck (half-width 26, y 762).
  - Bottom bulb: rounded, half-width 305 (x 203-813), domed into the base plate at y 1152.
  - A faint full-width table line at y 1152.
- **Press:**
  - Fixed head at y 330-354 (240 wide).
  - Rod 56 wide with faint ribs every 8 px; one rib leaves the head per push pulse.
  - Plate 24 px tall, full chamber width, thin white outline.
  - The one warm accent: a gold face line, plus a gold pressure fill inside the plate that grows from the centre with the push force (smoothed).
- **Grains:**
  - 2,275 polydisperse discs (r 4.45-5.55).
  - Hue is a smooth gradient by start height: 40 steps from red at the neck to violet at the top (HSV S 0.75, V 1).
  - Glossy bead sprites. Children keep the parent's hue.
- **Split:** a grain crossing y 769 becomes 2 same-size grains (±12 px/s), with a small light ring at the neck (0.12 s).
- **HUD:**
  - FULL meter at y 1252 (x 170-846): rainbow fill, white marker, gold cracked-pane icon + "BREAK" from frame 0, "N% FULL" above it.
  - Counter at y 1478: "N" + "GRAINS" + a "×2" pill labelled "SPLIT" in the current hue, pulsing per split.
  - Watermark at (900 right, 1338), 35% alpha.

## Physics (DEM, fixed dt 1/60, 24 substeps)
- Grains: linear spring-dashpot (k 2.2e5, ζ 0.6), Coulomb-capped viscous friction (μ 0.7 grain/funnel, 0.15 on the smooth chamber glass and the plate), no rotation, g 1700. The grains settle 0.9 s first (not shown).
- **Press:**
  - The plate (mass 400) is pushed with F(t) = 1.8e6·e^(t/7.5 s), capped at 2.4e7, with hydraulic damping.
  - The grains push back; the plate moves only as fast as grains leave through the neck.
  - More force gives a faster flow at a FIXED neck: splits 35 → 140/s.
  - The plate stops at y 602 (the funnel); it reaches 592 at the end.
- **Jam:** ≥ 4 slow bottom grains right under the split line. The meter is bottom grains / grains at the jam (1,866).
- **Break:**
  - From 95% full, hairline cracks run up the bottom glass (8 trunks + branches).
  - 0.12 s after the jam, the bottom glass breaks into shards and the confined heap bursts out (radial impulse) across the table.
  - The press keeps pushing, the top keeps splitting onto the pile, and the rate is still rising.
- Sim cache: `output/_ol_hourglass_split_sim_v2_*.npz` (~50 s to rebuild, `--resim`).

## Timeline (clip s)

| Clip s | What happens |
|---|---|
| 0 (sim 4.68 s, same run, no rewind) | Press already down and pushing (plate y 428, force 13% of cap). Stream pouring. Bottom 18% (336 grains). First split 0.042 s; push pulse at 0.08 s. |
| 0.5 / 1 / 2 | Plate y 431 / 434 / 440; 24 / 35 / 69 splits; fill 21 / 22 / 25%. |

- Splits per second: 35, 34, 41, 45, 48, 45, 59, 58, 69, 77, 81, 78, 92, 98, 124, 140 (climbing to the end).
- 7 s: plate y 481, force 34%, fill 51%.
- Cracks from 12.53 s.
- **JAM 13.03 s**: 1,866 grains, force 77% of cap, top still 1,342 of 2,275.
- **BREAK 13.15 s.** Counter ends at 2,462.
- Push pulses: 22, from ~1/s to ~2/s.
- Hold 2.4 s, then a 0.6 s dissolve to the pre-roll. **16.15 s, 969 frames.**

## Sound
- **Melody:** J. S. Bach, Prelude in C minor BWV 847 (WTC I).
  - Source: Mutopia "Mutopia-2006/07/02-550" (Breitkopf & Härtel 1866), Public Domain.
  - Files: `<SOUNDFONTS_DIR>\scores\bach_prelude_c_minor\` + `SOURCE_mutopia_550.txt`.
- **Walk:** bars 1-4, then bars 1-3 again, giving 112 sixteenth slots, one per sampled split (6 → 11 notes/s).
- **Cadence:** the run ends on the vii°7 and resolves on the BREAK, on the prelude's final C-major chord: rolled piano with strings, oohs, contrabass, timpani C3 and a boom (`--fin` 5.0).
- **Arrangement:**
  - Piano, celesta on the top notes, contrabass, strings_slow bar chords (oohs join on the repeat).
  - Timpani on the bar-1 downbeats, plus a G2 roll into the break.
  - After the break: a celesta C-major tink per sampled split.
- **SFX:**
  - Glassy bead "tk" per split (tonal 1.4-2.3 kHz, no noise, ≥ 12 ms apart, density-scaled).
  - Push pulse per rib: a soft low "thum" on C3 with a C2 sub, 3% glide, 1.2 kHz low-pass, no hiss or creak; its gain rises with the force.
  - 22 tonal glass tinks on the break.
- Mastering: `audio.master(peak_db=None, reverb=0.5)`. The last 0.6 s is zeroed; the wav is padded +0.1 s for the mux.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 969 frames, 16.15 s. **flash_check PASS** (0 flashes, mean lum 0.031).
- **Loudness:** −14.00 LUFS, peak −5.29 dBFS, last 0.5 s digital silence. Energy > 6 kHz: 0.002%.
- **RMS per second:** −19.0, −18.7, −18.8, −18.6, −18.2, −17.9, −17.9, −17.5, −15.9, −15.9, −15.4, −15.9, −14.7, −13.6 (the break), −13.9, −23.7 (the faded, silent tail). No dead second.
- **Cadence lift:** 13.15-14.65 s is −13.6 vs the late body (10-13.1 s) at −15.3, i.e. +1.7 dB, or +2.3 dB vs the 11-12 s second. The rising push pulses and the climbing body eat into the lift.
- **Seam:** encoded mean 1.70. It is one motion step of a dense bead field; v1's pre-encode seam measured 1.46 against normal steps of 0.90-1.41.
- **Frames read from the mp4:** 0, 0.5, 1, 2, 7, 13.0, 13.3, 14.5 and 16.13 s, plus a 1:1 crop of the chamber and press at 2 s.

## Flags
- General: `--label --cap --still --frame a,b,c --dry --resim --sound 0 --sfx (0.30) --fin (5.0)`.
- Clip: `--fill0 (0.18) --hold (2.4)`.
- Sim (changing these changes the run; re-check the press stroke):
  - `--seed (5) --n0 (26) --wear (0) --g (1700) --fill (0.99) --fl (0.40) --wb (305) --kick (12)`
  - `--pf0 (1.8e6) --ptau (7.5) --pfmax (2.4e7)`

Owner review 3 (2026-10-22): "might work" -> first batch.

Owner review 4 (2026-10-22): ok -> Dopamine.exe schedule.
