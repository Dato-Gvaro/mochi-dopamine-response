# monty_hall2 — "Stay = 1 door. Switch = 2 doors." / "Stay or Switch?"

- **Why v2:** the owner reviewed monty_hall: "I don't get how STAY works, maybe it's overcomplicated." v2 uses the classic intuition: switching = getting BOTH other doors. The rule reads at a glance. monty_hall.py is unchanged so the two can be compared.
- **One row of 3 doors** (violet, azure, rose), centred on the side safe zone (x 108-907):
  - Door 1 always glows CORAL with "MOCHI: 1 door".
  - Doors 2 + 3 glow MINT under one bracket, "BOLT: 2 doors".
  - The characters stand under their doors: Mochi at door 1, Bolt between 2 and 3.
- **HUD:** two race bars to 100 ("MOCHI n/100", "BOLT n/100"), and a split win-rate bar (coral % | mint %) with a dashed guide at 1/3.
- **Honest game:**
  - Mochi always picks door 1. The prize door is uniform, so this loses no generality.
  - The prize is placed at random by a seeded draw.
  - The host always opens a dud from Bolt's pair: the other one if the prize is in his pair, or a seeded coin flip if it is behind door 1.
  - Bolt switches to the closed door of his pair, so he wins whenever the prize is in his pair (2/3).
- **Round 1 (spelled out on the polka's intro chords):**
  - 0.15 s: door 1 lights coral and "MOCHI: 1 door" pops. The glow is already ramping at frame 0.
  - 0.99 s: doors 2 + 3 light mint with the bracket, "BOLT: 2 doors".
  - 2.25 s: the host opens door 3 (a deflated balloon). The mint label turns into "still 2 chances!".
  - 3.51 s: reveal. The trophy is behind door 2, in Bolt's pair: BOLT 1, win rate 0% | 100%.
  - Round 2 reveals at 5.19 s. Then the rounds speed up: 1 beat, ½ beat, then ¼ beat (~15/s). Coins fly to the winner's count.
- **Seed 46291** (searched 0-59,999: Bolt wins round 1, Mochi then leads, exactly one late lead change, 150 rounds):
  - Mochi leads by up to 5 (4-1 at 6.8 s; it is level at 10-10 by round 20).
  - LEAD CHANGE at round 33, 10.71 s.
  - 100! at 18.56 s (round 150, 100 vs 50; the bar turns gold and a coin fountain starts).
  - SWITCH = 2 DOORS / WINS 2/3! at 18.87 s.
  - Clip 21.87 s (1312 frames). The last 0.6 s dissolves into the pre-roll (doors unlit).
- **Music:** the same Strauss II "Thunder and Lightning" arrangement as monty_hall (Mutopia #610, PD engraving; bars 1-27, 57, 58, 60; −5 to D major).
  - Tempo: 0.42 s/beat to beat 12, accelerating to 0.265 by beat 26, with a ritardando into the cadence.
  - The 100th win lands on the cadence; the third chord lands on the finale banner.
- **SFX:** the same synths as monty_hall:
  - A tick as each colour lights.
  - A latch click (slow rounds) plus a wooden knock per dud door.
  - A chime at the prize door and a bonk at the loser's balloon.
  - Fountain clinks.
  - All onsets are ≥12 ms apart and ducked by density.
- **Checks** (encoded Full HD):
  - Video: h264 yuv420p 1080x1920 at 60 fps, 21.87 s.
  - Loudness: −14.00 LUFS, peak −7.23 dBFS, last 0.5 s at −66.8 dBFS.
  - flash_check: 0 flashes, PASS.
  - Loop seam: encoded mean delta 0.246. Pre-encode: 0.037, against 0.041 for a normal step.
  - Frames read at 0, 0.5, 1, 2.5, 3.8, 7, 10.75, 18.6 and 19.3 s.
- **Laptop:** 1 Python process, x264 at 2 threads. The render takes ~35 s.
- **Commands:**
  - `NF_SCALE=1.0 NF_FAST=1 python scenes/monty_hall2.py --still --frame N`
  - `NF_SCALE=1.0 python scenes/monty_hall2.py`
  - `--report`
- Delivered `<VIDEOS_DIR>\batch42\monty_hall2.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-19): approved (picked over monty_hall v1) -> 4K.

Owner review (2026-10-19): APPROVED ("let's use this one"; v1 dropped) -> 4K: output/monty_hall2_ship_9x16.mp4 (2160x3840, 60 fps, 1312 frames, 21.867 s; -14.00 LUFS, peak -7.23 dBFS; flash_check PASS; seam 0.165).
