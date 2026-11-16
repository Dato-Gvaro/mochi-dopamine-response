# ol_longform_domino2 (DopamineEXE long video 1, v2: size-comparison style)

- Brief: docs/BRIEF_dopa_long1b.md. v1 = scenes/ol_longform_domino.py (untouched; v2 only imports the read-only env helpers `Cam`, `text`, `sky_grad`, `ground_fill`).
- File: `scenes/ol_longform_domino2.py` (one file: chain, contacts, camera, stage, silhouettes, HUD, test cut, audio).

## Design (as built)
- **Ratio 1.12 → 586 dominoes**, 1.5 cm → 98 bn ly (domino 586 is the first one taller than the 93 bn ly observable universe). THICK 0.15 h, GAP 0.30 h (first contact at 17.5°), DEPTH 0.5 h. The chain is self-similar about x = 0 (the START).
- **Contact fix:** every domino's NEAR face lies in the plane z = 0 (the boxes extend back to z = D). That plane is an exact 2D cross-section, so each leaning angle is solved there as the smaller of two contacts: its top-front corner on the next domino's back face, or the next domino's top-back corner on its front face (`lean`). Painter order = ascending k (correct for this camera). Silhouettes sit in a lane just in front (z < 0), so they're drawn after the dominoes. Perspective size error is about 1%.
- **Camera:** fixed 3/4 side view, yaw -16°, pitch 3° (was 4.5°, which made the right-edge dominoes lean outward), dist 3.3, f 1250. It zooms about the START, which stays on screen at the left (gold "START 1.5 cm" marker), so every earlier domino and object stays visible, shrinking to sub-pixel. Smoothing sigma 0.45 s. The camera never goes below the ground (pitch > 0, `Cam` lift).
- **Stage:** one day-sky gradient with a warm horizon glow, a slate ground with haze, soft planar shadows, and a faint baseline. Changes with altitude (space etc.) are NOT built yet.
- **Silhouettes:** ink (0.035, 0.045, 0.075) with a thin pale rim. PERSON 1.70 m / 5 ft 7 in (front view, ~7.6 heads; was 1.75 m, but domino 43 is 1.7509 m, a 1 mm "win"). CAR 4.5 m / 14 ft 9 in long (side sedan, faces right, lighter windows). The label is name + metric/imperial above the object; it scales with the object's pixel size and turns gold on the pass. A top-centre banner reads "DOMINO 43 IS TALLER THAN A PERSON" / "DOMINO 52 IS BIGGER THAN A CAR" for 2.6 s.
- **HUD:** big "DOMINO 43" (128 px) + "/ 586" + height in m and ft/in + a "×1.12" pill in the domino's colour, top-left over a soft radial shade (replaced a hard-edged box). Thin log meter at the bottom, 1.5 cm → OBSERVABLE UNIVERSE (goal from frame 0). For the first 4.2 s the rule line reads "EVERY DOMINO IS 1.12× TALLER / from 1.5 cm to the OBSERVABLE UNIVERSE".

## Pacing plan (for the owner to approve with the test)
- Dvořák 9/iv (v1's orchestration; the same 152 bpm clock, t = 0 = beat 0). Hits on the half-beat grid. Hit 0 at 0.79 s; frame 0 already falling.
- Intervals go linearly from 6 half-beats (**1.18 s**) down to 3 (**0.59 s**). Hits per minute: 50, 51, 59, 60, 61, 63, 76, 76, 80 (the rate only climbs).
- The last domino falls over 8 beats and lands on the last chord at **9:07.9**. End **9:14.9** (7 s hold).
- Milestones: 15 cm d22 0:24 · person d43 0:49 · car d52 1:00 · whale 30 m d69 1:20 · Liberty d79 1:32 · Eiffel d90 1:45 · Everest d119 2:18 · 100 km d140 2:39 · Moon d171 3:10 · Earth d183 3:21 · Sun d224 4:02 · 1 ly d363 6:14 · Milky Way d465 7:34 · universe d586 9:05.
- Why 1.12: the zoom speed is fixed by 8-10 min over 66 e-folds. Only a smaller ratio buys more falls per second. At 1.5, 165 dominoes at ≤1.5 s fill only ~4 min. At 1.2 the ≤1.5 s start can't also climb over 9 min.

## Test cut (step 1)
- `--test` renders 2 windows of the REAL timeline: 0:00-0:06 (the hook, minute-1 pace) + 0:43.2-1:05.4 (the person and car passes), ~28 s. Audio = windows of v1's cached bed `output/ol_longform_domino_bed.npy` + v2 clacks, mastered like v1 (`test_audio`).
- Flag for the owner: "4-5 dominoes" at the new pace would last only ~6 s, so the test shows ~23 dominoes of the real chain instead.

## Delivered (2026-11-04): step-1 TEST, waits on the owner
- `<VIDEOS_DIR>/DopamineExe/review/longform1b/test_4dominoes.mp4` + 3 stills (frames from the encoded file) + README.md (pacing plan with milestone times). Built as `--test --label lf1b_t1`: 1696 frames in 85 s (20 fps FHD), ffmpeg 2 threads.
- Fixes after reading the stills: the car's side windows were not mirrored with the body and poked above the windshield (now mirrored and inside the roofline); a stray top-edge highlight showed on tall dominoes with a hidden top face (highlight now only when the top face is visible).
- Checks on the encoded file: h264 yuv420p 1920x1080 60 fps, 1696 frames, PTS step 256 everywhere; aac 28.267 s; -14.02 LUFS, peak -1.97 dBFS; flash_check PASS (0 flashes); clacks median +13.4 dB (min +7.3) over the 60 ms before, 400 Hz-4 kHz; contacts read at 1:1 on hit 41 (+0.025 s, +0.27 s): corner on the face, no overlap.
- Next (after the OK): the object roster (~40-50 silhouettes and astronomical discs), the altitude sky (blue → dark blue → stars → galaxies), the Earth curve then a baseline, the finale (gold domino on the last chord, count card), a full render in resumable chunks, then the usual delivery (README, UPLOAD_notes, 3-4 thumbnails). No 4K.
