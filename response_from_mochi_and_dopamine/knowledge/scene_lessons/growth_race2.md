# growth_race2 — "Mochi starts at 1,000 and DOUBLES" / "Bolt multiplies by the ROUND number"

- Franchise ep. 2 (batch67). Nameable change: "now Bolt multiplies by MORE every round" (x1, x2, x3 ... = n!). New file `scenes/growth_race2.py`; growth_race untouched.
- New container (brief: different look): two TOWERS on a x10 ruler. Every grid line is 10x the one below, so a block's height = log10 of its multiplier: Mochi's x2 blocks are all 0.30 floor, Bolt's x10 is exactly one floor. The ceiling = 100 BILLION.
- **Setup change vs the brief:** Mochi gets a 1,000 head start. With both starting at 1, Mochi (2^n) leads only rounds 1-3 (8 vs 6) and n! passes at round 4 — 3 of 13 rounds. With 1,000 she leads 9 rounds, so the "leads... until it doesn't" arc is long. The rules themselves are the brief's.
- Counts are exact Python ints: r9 512,000 vs 362,880 (near miss) · **r10 1,024,000 vs 3,628,800 (LEAD CHANGE)** · r14 16,384,000 vs 87,178,291,200 (just under the ceiling) · **r15 32,768,000 vs 1,307,674,368,000 (through it)**.

## Layout
- Towers x 132-412 and 604-884 (0.12-0.82 w), ruler labels between them (x 508), floor y 1330, 74 px per floor, ceiling y 516 ("100 BILLION" at x 330).
- Blocks grow in 0.20 s at the top (small overshoot), colour by round (one hue per round in both towers), "x n" label inside. Bolt's x1 has zero height: "x1 = no change" pops.
- Characters ride on their tower tops. Banners take the ROUND line (y 352).
- Ceiling: a glass slab; when Bolt's x15 block passes it, 46 shards fly, a warm glow, a 0.45 s shake.

## Timeline (clip 16.27 s = 976 frames)
- Round k on bar k of the polka: Mochi's block on the downbeat, Bolt's on beat 2. Rounds 0.05 ... 10.81 s.
- LEAD CHANGE 7.75 s (round 10). Round 15: Mochi 10.81 s, Bolt's x15 waits for beat 32 (12.07 s, a pulsing "x15" over his head) = ceiling break, "1.3 TRILLION!", then "BOLT WINS!". Dissolve 15.67-16.27.

## Sound
- Johann Strauss II, "Unter Donner und Blitz" polka Op. 324 (1868, PD; Mutopia #610 piano score), beats 0-31 (intro + first strain), accelerando 132 -> 196 bpm.
- Intro: brass chords + tremolo strings + timpani roll; theme: violin + flute (top voice), clarinet (inner), pizz + horns (off-beat chords), contrabass + tuba; trumpet doubles from beat 24; timpani every bar from beat 8, roll into beat 32.
- Beat 32 (the tonic G) = ceiling break: G-major tutti, choir, timpani, boom, crash + two glass breaks.
- A wooden thock per block (lower for bigger blocks). Last ~1.2 s silent.

## Checks (encoded Full HD `output/growth_race2_b67_9x16.mp4`)
- h264 yuv420p 1080x1920 60 fps, 976 frames = 16.27 s. -14.01 LUFS, peak -4.90 dBFS, last 0.5 s -73 dBFS.
- RMS/s -19.9 -16.3 -19.3 -20.1 -17.4 -17.4 -16.4 -17.0 -17.6 -16.4 -16.3 -17.1 **-12.9 -13.6** -18.0.
- flash_check 0. Seam 0.44. Notes 44 / 8 distinct / top 31.8 % (the polka's repeated chord stabs; tune as written).
- Frames read: 0, 0.6, 7.8, 12.1, 12.3, 16.25 (+ Fast stills 11.6, 12.25, 14.0).

## Doubts
- Log scale: honest and labelled ("each line x10"), but some viewers may read it as linear.
- Bolt's side is empty for round 1 (x1).
- The 1.3 s wait before the x15 (the cadence) is a deliberate drum-roll beat.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch67\growth_race2.mp4`. Owner review: pending.
