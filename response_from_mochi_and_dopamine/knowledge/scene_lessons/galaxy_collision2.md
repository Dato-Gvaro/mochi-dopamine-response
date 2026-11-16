# galaxy_collision2 — Mochi's galaxy vs Bolt's galaxy, the spectacular cut (batch25)

Rework of galaxy_collision (owner, 2026-10-10: "very good idea, a bit more spectacular: larger, some effects; the music sucks, something epic with bass and vocal"). The music was then switched by the owner to an NCS track (below). The original scene file is untouched.

## What changed vs galaxy_collision
- **Bigger and denser.** 2 x 25,000 stars (was 2 x 10,000), plus 2 x 6,000 gas and 2 x 4,000 dust tracers. The pair fills ~0.85-0.9 of the width from the first forward frame (zoom 240-360 px/unit, was 150 → 90).
- **Gas and dust.** Each disk carries gas on its spiral arms, rendered as a blurred glowing nebula (rose for Mochi's galaxy, azure for Bolt's). Dust lanes sit on the arms' inner edge and absorb (exp(-tau)) the starlight and the gas.
- **Starbursts (real physics).** Pink H-alpha knots light up where gas is compressed: the Lagrangian density rises over 8 frames, or the two galaxies' gas overlaps. They are boosted x3.5 as the cores merge (merger-driven inflow), live 1.1-2.4 s and ride on their gas particle.
  - 21,395 knots in total; peaks of ~4,000 alive after the first pass and ~3,000 at the merger.
  - The knots are precomputed and deterministic, as functions of the forward frame, so the rewind and the seam are exact.
- **Shockwaves.** An expanding luminous ring from the centre of mass, with radial lensing of the image at its front and a ring of triggered knots as it sweeps the gas (a ring galaxy). There is a small camera kick on the strong rings.
  - Strong rings: the drop / first pass (1.0), phrase 2 (0.85) and the merger (1.0).
  - Lighter density ripples on the 4-bar sub-phrases (0.55).
- **Glowing cores with bloom.**
  - Each core has a white-hot centre, an owner-tinted halo and 4 faint diffraction spikes, plus a merger flare that grows as the separation drops.
  - The cores throb on every kick of the track (detected low-band onsets).
  - Bloom runs at three levels: 1/2, 1/8 and 1/16 resolution.
- **Camera.**
  - Push-in for the first pass (240 → 300 px/unit), ease out for the swing-out (255), and a push-in through the merger (300 → 360).
  - A 28° roll over the clip.
  - Everything is a function of sim time, so the rewind and the loop are consistent.
  - The view is rolled -160° (was -28°) so the pass is diagonal and the merger axis near-horizontal: it fills the 9:16 width.
- **Depth.** Three parallax star layers (0.10 / 0.22 / 0.40 of the camera motion), 11 faint distant spiral galaxies, and a dim nebula backdrop sampled with parallax 0.08.
- **Exposure.** The exposure lifts by up to x1.7 through the merger, so the payoff state (= frame 0) is the brightest.
- **Trails.** Shorter star trails (decay 0.88, weight 0.07), so the outer debris no longer reads as hair-like streaks.

## Physics and contest
- Same orbit as galaxy_collision (`PHYS`, seed 347): restricted N-body (Toomre & Toomre 1972) with dynamical-friction drag.
  - First pericentre at tau 4.51 (sep 1.29), swing-out at 6.38 (1.48), lock at 8.78 (sep 0.60).
- The forward part starts at tau 2.55 (sep 2.23), when the two disks already touch. The approach is not shown.
- Count rule unchanged: a star is kept by the core it is energetically bound to, and the count locks at sep 0.60. Counts are real star counts (25,000 each), not scaled.
  - At 0.83 s the counts are already 24,565 vs 25,435: the disks touch and Bolt's core is already pulling stars. This is honest physics, though it does not show 25,000 / 25,000.
- Timeline (clip s):
  - Bolt leads from the start.
  - **Mochi takes the lead at 16.74 s.**
  - **Bolt retakes it at 27.96 s.**
  - Lock at 28.14 s: **Mochi 21,285 vs Bolt 21,367, Bolt wins by 82.**

## Music
- **Egzod, Lost Sky, Alaina Cross: "Fight In Me" [NCS Release].**
  - Owner-provided file: `<VIDEOS_DIR>\music\Fight In Me\...mp3`.
  - Excerpt: track **1:31.066 → 2:02.505**, i.e. 31.44 s = 3 bars of breakdown + the 16-bar drop phrase, cut at the phrase boundary.
  - The last hit (bar 15 downbeat, 2:00.851 = clip 29.78 s) rings 0.06 s, then a 0.28 s cosine fade. The track is silent from 30.13 s, i.e. the last 1.31 s.
- **Licence:** NCS (NoCopyrightSounds). The video DESCRIPTION must carry the credit text from `<VIDEOS_DIR>\music\Fight In Me\Description Text.txt`:
  ```
  Song: Egzod, Lost Sky, Alaina Cross - Fight In Me
  Music provided by NoCopyrightSounds
  Free Download/Stream: http://ncs.io/fightinme
  Watch: http://ncs.lnk.to/fightinmeAT/youtube
  ```
- **Beat grid detected from the audio** (`music_grid()`, cached in `output/galaxy_collision2_musicgrid.json`).
  - Method: spectral-flux onset envelope with a grid fit over 1:36-2:00, giving **145.04 bpm** (beat 0.4137 s, bar 1.6547 s).
  - The drop is the first beat >8 dB louder than the 4 beats before it: **1:36.030**. The excerpt start is the downbeat 3 bars earlier: **1:31.066** (owner: "from 1:31").
  - Kicks are beats with a 30-140 Hz onset: 55 of them, each with a strength.
- **Sync:**
  - The rewind (0-0.83 s, 2 beats) and the approach play under the quiet breakdown.
  - **First pericentre + the big shockwave = the drop at 4.96 s.**
  - Density ripples at 11.58 s and 24.82 s (4-bar marks).
  - The phrase-2 shockwave is at 18.20 s.
  - **Merger + lock + the merger shockwave = bar 14 downbeat, 28.13 s.**
  - The cores throb on every kick.
  - The loop seam falls exactly on the 16-bar boundary (the clip is 19 bars).
- Loudness: plain gain to -14 LUFS (stereo). `audio.master()` was not used: its pedalboard limiter squashed the drop against the breakdown (measured 11 dB → 3 dB of contrast). No added synth or accents.

## Hook
- Frame 0 is the final state. It shows:
  - the two blazing cores (mint and coral) locked together;
  - the merged, star-forming body filling ~0.85 of the width, with pink starburst knots;
  - the final counts, "BOLT KEEPS MORE!", Bolt grinning and Mochi with an annoyed stare.
- An eased rewind (2 beats, motion-blurred) lands on two clean spiral galaxies already touching. The collision is under way from 0.83 s, and the big pass and shockwave hit on the drop.

## Args
- Visual tuning: `--n`, `--ngas`, `--ndust`, `--tau0`, `--after`, `--rot`, `--tilt`, `--turn`, `--zoom z0,zp1,zapo,zlock,zend`, `--bright`, `--gas`, `--dust`, `--knot`, `--krate`, `--expo`, `--bggal`.
- Clip and run control: `--cap`, `--label`, `--still --frame a,b,c [--warm]`, `--report`, `--silent`, `--mux-only`, `--fresh`, `--m0`.

## Checks (Full HD v1, `--label v1 --par 3`)
- Format: h264 yuv420p 1080x1920 at 60 fps, 1886 frames = **31.43 s** (19 bars of the track). File size 80 MB (dense star texture at crf 18).
  - Length is over the brief's 20-30 s. That is the price of the owner's 1:31 start plus a phrase-boundary cut: the 8-bar option ends at 18.2 s and the 16-bar option at 31.4 s.
- Audio (muxed mp4):
  - -14.02 LUFS, peak -8.14 dBFS.
  - From 30.13 s the peak is -96 dBFS; the last 0.5 s is -240 dBFS (silent).
  - The drop's level jump sits at 4.96-4.98 s on the encoded audio, which is the first-pass frame.
- flash_check: 0 flashes (mean luminance 0.018), PASS. The rings are thin and the kick throb is on the cores only.
- Loop seam:
  - Pre-encode, frame 0 = the last frame's state by construction (same forward frame; trail primed by 90 frames, residual < 1e-4).
  - Encoded seam mean delta 1.51 (check_clip). Normal steps in the same clip measure 1.26-1.94, against 2.97 in the rewind. This dense star texture's codec noise is above the channel's 0.12-0.72 band, but the seam is no bigger than an ordinary step.
- Encoded frames read at 0, 0.25, 0.5, 1, 2, 3, 4.97 (drop), 5.6, 10, 15.7, 18.25, 24, 28.15 (lock), 28.6 and 30.5 s, plus 1:1 crops of 5.6 s and 0 s. The galaxies are big from frame 0.
  - The drop frame shows the pass, the bridge and the first ring.
  - 28.6 s shows the merger ring with the pink starburst knots.
  - Mid-clip (10-18 s, widest swing-out) the pair spans ~0.7 of the width.
- Render: the sim takes ~45 s and is cached in `output/galaxy_collision2_simcache_<hash>/` (1.4 GB: XY + colour mix).
  - Full HD costs ~2.5 s/frame on the loaded machine.
  - `--par 3` renders 3 frame chunks in parallel (each warms the trail 90 frames before its start) and concatenates them losslessly: ~25 min.
- Delivered: `<VIDEOS_DIR>\batch25\galaxy_collision2.mp4`. Owner review: pending.
- Owner review (2026-10-11): PERFECT, but make it about SHARING, not competition; remove the numbers -> galaxy_collision3.
