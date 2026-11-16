# corner_hit2
- Owner rework of corner_hit (2026-10-15): both badges in ONE simple arena; "don't make heavy background visuals, just simple". New file; corner_hit.py is untouched.
- Look:
  - A plain dark background (0.035, 0.035, 0.065) with one thin glowing violet rectangle (x 64-894, y 330-1190).
  - Corner brackets (gold when Mochi grazes or approaches a corner; Bolt's target pulses teal).
  - No room, TVs, scanlines or ghosts. Each badge has only a soft colour glow.
- Badges: 190x140 with the character's face (r 53, a pale tint of the badge colour). The colour changes on every wall hit: Mochi coral/gold/orange/pink, Bolt teal/mint/cyan/blue/violet. A squash on each hit.
- The badges PASS OVER each other (screensaver ghosts). There are no collisions, so each one's corner maths stays exact and independent.
- Caption: `First to hit the ^EXACT^ corner WINS|~Luck or maths?~`.

## Maths (analytic, event-driven)
- Free travel is W 640 x H 720. A corner is hit exactly when the travelled x is a whole number of W AND the travelled y a whole number of H at the same moment (within 0.5 px).
- Mochi: a random steep angle (56-72°) and a random start, 950 px/s, x1.035 per wall hit (cap x2.3). Speed never changes her path, only how many tries she gets per second.
- Bolt: from the bottom-left corner at exactly 45°, 350 px/s per axis. He reaches the bottom-right corner after lcm(640, 720) = 5760 px (9 W = 8 H): 15 bounces, then the corner at sim 16.46 s.
  - A dotted predicted path is shown for the next 3 segments.
- Seed search (`good()`): a Mochi win at clip 11.8-15.8 s with Bolt 1-2 contacts short, at least 3 near-misses of 12 px or less, and a longest event gap of 0.70 s or less. 43 of 100,000 seeds pass, so her corner really is luck.

## s75805 (default)
- Mochi's angle is 69°. Her near-misses creep toward the corner: 4.2 → 3.1 → 2.1 → 1.0 px, at 0.38, 4.13, 6.84 and 9.38 s.
- Corner at 11.92 s, on her 48th wall contact (47 bounces).
- Bolt is at CORNER IN 1 at that moment: "Bolt: 1 HIT SHORT!".
- Frame 0 (sim T0 = 3.86 s): both are bouncing, and Mochi is flying at the bottom-right corner, which glows in anticipation. SO CLOSE! 4.2 px! comes at 0.38 s.
- Banners (at least 0.85x scale):
  - SO CLOSE! + px at the centre (y 710/800).
  - MOCHI FASTER! x1.5 / x2.0 at y 580 (never on top of a SO CLOSE).
  - BOLT: CORNER IN 3/2/1 at y 1030.
- Payoff:
  - CORNER!! (gold, 112 px) with a ring burst plus 80 confetti and stars from the corner. MOCHI WINS! at +0.45 s.
  - The proof line `x = 15 W,  y = 35 H → both whole!`.
- Loser fate (+0.55 s):
  - Bolt's badge greys out with an annoyed face (0.25 s), then shrinks to a grey dot (r 62) with his annoyed face squashed in it (0.2 s).
  - The dot drops at 2600 px/s² to the arena floor, with a soft low thunk on landing, one small hop, and stays there. His HUD dims.
- Clip 15.22 s (913 frames). The last 0.6 s dissolves into the pre-roll.
- HUD: two columns under the arena (y 1256-1362):
  - Name (48 px) with the method (28 px): Mochi "random 69° · x2.3" with live speed, Bolt "45° · lcm(W,H)".
  - `HITS: n` (42 px).
  - Mochi `CLOSEST: 1.0 px` / Bolt `CORNER IN: n` (42 px).

## Sound (no music, beds, whoosh/hiss/creak, nothing shrill)
- Wall boop per hit: Mochi MIDI 60-69, Bolt 55-64, rounder.
- "ooh" rising cluster of clean soft tones on near-misses.
- Soft up-blips for the FASTER and CORNER IN banners.
- A warm strummed C major chord plus a soft chime pair for the corner, then 3 quiet tinkles.
- A soft falling two-note "aww" when the loser greys out, and a low clean thunk when the dot lands.
- Onsets are at least 12 ms apart, `master(peak_db=-6)`, nothing in the last 1.0 s, and a 0.6 s tail fade.

## Flags
- `--seed` (75805), `--label`, `--cap`.
- `--vote`: "Team Mochi or Team Bolt?" plus a gold arrow at y 1020, from loser-off +0.95 s to the dissolve. Default OFF.
- `--search N --from S`, `--dry`, `--still --frame N`, `--sound 0`.
- Tuning: `--vm --acc --capv --vb`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 913 frames, 15.22 s.
- -14.00 LUFS, peak -7.66 dBFS, last 0.5 s peak -60.8 dBFS.
- flash_check PASS (0 flashes, mean luminance 0.015).
- Seam:
  - Pre-encode: the last frame equals frame -1 exactly, and -1 → 0 is 1.74, the same as a normal step (0 → 1 is 1.73), so the loop is perfect.
  - The encoded seam is 1.94 (I-frame bump on a moving opening).
- Events per 5 s: 22 / 29 / 16 (67 sound events). The longest gap is 0.60 s.
- Safe zone: caption at y 150-290, arena at y 326-1194, HUD ends at about 1365 (0.71h). Everything is at x ≤ 898.

Delivered <VIDEOS_DIR>\batch38\corner_hit2.mp4 (no vote); the old corner_hit.mp4 was removed. Owner review: pending.

Owner review (2026-10-16): moved to reserve by the owner.
