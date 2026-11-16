# corner_hit
- New scene (batch38). It is the 90s bouncing-screensaver "will it hit the corner?" meme as a choice duel. There are no names or logos: each badge is a rounded badge with a character face, not a DVD logo.
- Rule (caption, baked, `--cap`): `First to hit the ^EXACT^ corner WINS|~Luck or maths?~`.
- World:
  - A dark room with two stacked CRT TVs (Mochi on top, Bolt below) on a wooden stand, with rabbit-ear antennas.
  - The glass is rounded, with a curvature vignette, scanlines and a reflection. Each bezel glows in the team colour (coral or teal), with a soft wall halo.
  - Each TV has a control panel with a name and method plate, an LED HUD (`WALL HITS`, `CLOSEST`, `SPEED`/`CORNER IN`, `ANGLE`) and knobs.
- Badge: 160x120 in a picture of 760x370, so the free travel is W 600 x H 250.
  - The badge colour changes on every wall hit: Mochi uses the coral/gold/orange/pink family, Bolt the teal/mint/cyan/blue/violet family.
  - A squash on each hit, a phosphor afterglow (3 ghosts) and a local glow.

## Maths (analytic, event-driven, no frame-step error)
- Unfold the bounces and the badge moves in a straight line. It hits a corner only when the travelled x is a whole number of W AND the travelled y is a whole number of H at the same moment.
- A live OSD on each screen shows this: `x = 3.09 W   y = 13.39 H`. At the win it reads `x = 9 W   y = 37 H  both whole!`.
- "Exact" means within 0.5 px (the HUD then reads 0 px).
- Mochi: a random steep angle (56-72°) and a random start. Her speed is x1.035 per wall hit (cap x2.4). Speed never changes her PATH, only how many tries she gets per second.
- Bolt: launched from the bottom-left corner at exactly 45°, 182 px/s per axis. x and y travel equally, so he lands in a corner after lcm(600, 250) = 3000 px (5 W = 12 H): 15 bounces, then the bottom-right corner at sim 16.48 s.
  - A dotted predicted path is shown for the next 3 segments, the target corner bracket pulses, and the OSD reads `x = y = 1806 px` / `corner at lcm(600, 250) = 3000`.
- Seed search: `good()` needs a Mochi win at clip 11.8-15.8 s with Bolt 1-2 contacts short, at least 3 near-misses of 12 px or less, and a longest event gap of 0.62 s or less. 24 of 20,000 seeds pass, so her corner really is luck.

## s13798 (default)
- Mochi's angle is 59°. Her path is nearly periodic, so the near-misses CREEP toward the corner: 4.0 → 3.6 → 3.1 → 2.7 → 2.2 → 1.8 → 1.3 → 0.9 px. Their intervals shrink as she speeds up: 2.4, 2.0, 1.7, 1.4, 1.3, 1.25 s.
- Corner at 13.00 s, after 43 wall hits.
- Bolt: 14 hits, CORNER IN: 2 at that moment, so "2 HITS SHORT!".
- Frame 0 (sim T0 = 1.92 s): Mochi's badge is heading at the bottom-right corner, which glows in anticipation. The first SO CLOSE (4.0 px) comes at 0.38 s.
- Banners (all popped at 0.85x or larger):
  - SO CLOSE! + `n px!` per near-miss (the two touches of one corner approach are merged and the smaller value shown).
  - FASTER! x1.5 / x2.0 (never on top of a SO CLOSE).
  - CORNER IN 3/2 on Bolt's screen.
- Payoff:
  - 13.00 s: CORNER!! (gold, 104 px), a gold ring burst, 80 confetti and stars from the corner (spilling out of the TV), and a happy squash.
  - 13.45 s: MOCHI WINS!
  - 13.55 s: Bolt's TV switches off (CRT shut-down). The picture squeezes to a bright line in 0.16 s, the line shrinks to a dot in 0.2 s, and Bolt's annoyed face sits squashed (1.45 x 0.62) in the dot, which fades. The bezel, halo and LED dim.
  - 14.1 s: "2 HITS SHORT!".
- Clip 16.30 s (978 frames). The last 0.6 s dissolves into the pre-roll.

## Sound (no music, no beds, no whoosh/hiss/creak, nothing shrill)
- Wall boop: a sine with a quick downward pitch settle plus soft 2nd/3rd harmonics, 75-95 ms decay.
  - Mochi: MIDI 60-69. Bolt: MIDI 55-64, rounder.
  - The note follows the colour index.
- Near-miss "ooh": a rising cluster of 3-4 clean soft-attack tones (MIDI 62/64 + 4, 7, 12) with slight vibrato. Smaller misses of 12-30 px get a 2-note ooh.
- FASTER and CORNER IN: two soft up-blips (MIDI 64-72).
- Corner: a warm strummed C major chord (C3-C5, 6 harmonics) plus a soft glassharp chime at 76 and 79, then 3 quiet tinkles.
- CRT off: a low thunk (130 → 55 Hz glide, 85 ms decay), no whine.
- Onsets are at least 12 ms apart, `master(peak_db=-6)`, no events in the last 1.0 s, and a 0.6 s tail fade.

## Flags
- `--seed` (13798), `--label`, `--cap 'a|~b~'`.
- `--vote`: "Team Mochi or Team Bolt?" plus a drawn gold arrow at the top of the dead TV (y 952, x 80-870), from the off-switch +0.95 s to the dissolve. Default OFF.
- `--search N --from S`, `--dry`, `--still --frame N` (negative = pre-roll), `--sound 0`.
- Tuning: `--vm --acc --capv --vb`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 978 frames, 16.30 s.
- -14.00 LUFS, peak -7.75 dBFS, last 0.5 s peak -68.7 dBFS.
- flash_check PASS (0 flashes, mean luminance 0.018).
- Seam:
  - Pre-encode: the last frame equals frame -1 exactly, and -1 → 0 is 0.81, the same as a normal step (0 → 1 is 0.80), so the loop is perfect.
  - The encoded seam is 1.42 (I-frame bump).
- Events per 5 s: 22 / 29 / 17 (68 sound events). The longest gap is 0.57 s.
- Safe zone:
  - Caption at y 150-290.
  - Both screens are at y 332-1246, the HUD panels end at 1334 (0.69h) and the stand top is at 1342.
  - All content is at x ≤ 906; the vote arrow is at x ≈ 850.

Delivered <VIDEOS_DIR>\batch38\corner_hit.mp4 (no vote). Owner review: pending.

Owner review (2026-10-15): put both characters in ONE screen, both bouncing and both going for a corner. "Don't make heavy background visuals, just simple." -> rebuilt as corner_hit2 (docs/scenes/corner_hit2.md). This file stays bit-reproducible. The batch38 corner_hit.mp4 was removed (replaced by corner_hit2).
