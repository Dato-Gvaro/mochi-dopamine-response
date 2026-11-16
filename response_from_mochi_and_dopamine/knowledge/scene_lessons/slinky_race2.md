# slinky_race2: Mochi LETS GO, Bolt's machine YANKS: when does it beat gravity? (batch72b, REBUILD of slinky_race)

- Brief: docs/BRIEF_batch72b.md §3 ("doesn't look like a physics sim at all"). New file `scenes/slinky_race2.py`; it imports `slinky_race.py` (SR1) for the sim, which stays bit-reproducible.
- Physics: unchanged (SR1): 60 coils, 0.215 kg, 1.25 m hanging; T = 290 ms; crossover L/T = 4.3 m/s; yanks 0.5/1/2/4/8 m/s → 494/462/409/299/150 ms; Bolt wins round 5 only.
- Look: a continuous 3D steel helix (wire 4.6 px, back halves at 42 %, a bright streak + a dim glint per coil front, a 10 % coral/mint tint only), motion blur on fast coils, a soft shadow on the back wall, cm rulers, a floor with contact shadows. Mochi: a lab stand + clamp whose padded jaws pinch the top coil and snap open on a quick-release bar. Bolt: a motor rail with a carriage + arm and an LED speed readout (green while it runs). A balloon squashes, then pops with fragments and leaves skin on the floor.
- Timing: ×6 slow-mo (×8 in v1; changed to fit the grip beats). Each round from 2 on opens with a 0.13 s real-time grip (0.78 s on screen), then the release. Round 1 frame 0 = jaws mid-opening. Hold 0.30 s, re-hang 0.15 s, finale 1.5 s, dissolve to frame 0: 16.58 s.
- Audio: our own copy of SR1's bed with the new plan: Mozart K. 522 I top line as pizz + harp, one note per 4 coils stacked (≥85 ms apart per side), a metallic clack per note, a snap at each release, a balloon pop per pop, an F-major chord + timpani on Bolt's win.
- Fix after the first Full HD (b72b): Bolt's "POP!" was drawn under his own stack. POP! is now drawn over the slinkies. Shipped b72c.
- Checks (encoded Full HD, b72c): 995 f = 16.58 s; −14.01 LUFS, peak −2.5; flash PASS; seam 0.77 (a dissolve back to frame 0). Frames read 0.03, 1.80, 3.10, 11.35, 13.66, 15.2 (+ 1:1 crops of the clamp at 0.03 and Bolt's pop at 13.66).
- Doubts: seconds 4-8 are quieter (−27 dB RMS, the slow yanks); the hanging slinky's bottom third is dense (those coils really touch at rest); "slinky" is a trademark, so titles say "metal spring".
- Delivered: <VIDEOS_DIR>\MochiAndBolt\review\batch72b\slinky_race2.mp4. Owner review: pending.
