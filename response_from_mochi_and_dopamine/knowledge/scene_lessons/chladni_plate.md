# chladni_plate — glowing sand on a vibrating steel plate, one Chladni mode per bar of Bach's Prelude in C

- New scene (brain-satisfying physics brief, 2026-10-09/10). Built autonomously while the owner slept; the music direction was updated mid-build ("needs energy and drive") -> brisk quarter = 92.
- Physics:
  - Square steel plate, top view, clamped at the centre post. Free-plate Chladni approximation u = cos(n pi x) cos(m pi y) +/- cos(m pi x) cos(n pi y), x, y in 0..1.
  - One mode per bar, always with a node at the clamped centre, climbing in intricacy: (1,3)+ (1,3)- (2,4)- (3,5)+ (1,5)- (3,5)- (2,6)- (3,7)+ (3,7)- (4,8)- and the cadence (5,7)+.
  - Grains descend u^2, distance-normalised (v = -K u grad u / (|grad u|^2 + 0.002 G2), K 5/s, capped 1 plate/s), so every line pulls at the same rate. Plain u grad u (first try) left bright clumps at line crossings.
  - Jitter: antinode dance 0.003 A |u|^1.5, floor 0.0014 (line width ~3-4 px), and 0.006 ALONG the lines (spreads the inherited clumps evenly, never widens a line). A = plate excitation: base 0.55 + a 0.09 s kick per piano note, so the sand dances to every 16th.
  - Morph: ~35-45 % of the grains on the new lines (< 6 px) by 0.5 s, ~85 % by 0.8 s; each pattern then holds for ~1.8 s of the 2.6 s bar.
- Sand: 5,000 grains at frame 0 (uniform), poured to 20,000 by the cadence (count^1.25 ramp from 0.5 s). Fresh grains land white-hot (0.22 s). Colour by distance from the centre post (jewel rainbow), hue rotating one full cycle per clip (seamless).
- Look: float light buffer (bilinear splat, trails 0.84/frame at 0.14, two-radius glow, hue-preserving tone-map) on a dark violet stage; brushed dark steel with a diagonal sheen, bevel, centre post; the antinodes glow faintly (0.022 A u^2, cross-faded 0.25 s on a mode change).
- Characters (r 28): Bolt bows the plate's bottom edge with a violin bow (one stroke per half bar, a long down-bow over the cadence), Mochi watches from the lower right. WOW on bars 4, 8 and the cadence; happy while the sand dissolves; frame-0 smile at the seam.
- HUD: caption "Each chord shakes the sand into a shape | ~11 chords = 11 PATTERNS~"; label "mode (n, m) +/-" (pops on each bar); counter "GRAINS: N".
- Loop: cadence pattern held 1.45 s, then the plate falls silent and the sand dissolves over 2.0 s: the 5,000 originals glide (Hermite) back to their frame-0 spots arriving with frame 0's drift velocity, the 15,000 poured extras fade as they spread, the counter falls 20,000 -> 5,000, trails blend into frame 0's steady state over the last 0.45 s.
- Music: J.S. Bach, Prelude in C major, BWV 846 (Well-Tempered Clavier, Book I, 1722; Bach d. 1750) — public domain composition, played by our own `audio.synth_piano` (no recording, no bed, no accents).
  - Bars 1-10 in the real figure (per half bar: a b c d e c d e as 16ths), pedal per bar (each note rings to its own re-strike or the bar line), + the bar-11 downbeat G major chord, lightly rolled and held = the cadence of the first phrase (ii7-V7-I in G).

    | Bar | Chord | Notes (a b c d e) |
    |---|---|---|
    | 1 | C | C4 E4 G4 C5 E5 |
    | 2 | Dm7/C | C4 D4 A4 D5 F5 |
    | 3 | G7/B | B3 D4 G4 D5 F5 |
    | 4 | C | C4 E4 G4 C5 E5 |
    | 5 | Am/C | C4 E4 A4 E5 A5 |
    | 6 | D7/C | C4 D4 F#4 A4 D5 |
    | 7 | G/B | B3 D4 G4 D5 G5 |
    | 8 | Cmaj7/B | B3 C4 E4 G4 C5 |
    | 9 | Am7 | A3 C4 E4 G4 C5 |
    | 10 | D7 | D3 A3 D4 F#4 C5 |
    | 11 (downbeat) | G | G3 B3 D4 G4 B4, rolled, held |

  - Quarter = 92 (brisk, flowing; 2.61 s per bar), a 0.24 s ritardando over the last two beats of bar 10. Light dynamics per bar. Everything faded 1.35 s before the end.
- Args: --seed (7), --tempo (92), --k (5.0), --jit, --j0, --jt, --reg, --gw, --cap, --label, --still --frame a,b,c [--warm 40], --report.
- Checks (encoded Full HD, v1, seed 7):
  - h264 yuv420p 1080x1920 60 fps, 29.80 s (1788 frames). Render ~25 min on a busy machine.
  - Audio: -14.00 LUFS, peak -5.2 dBFS, last 0.5 s silent (-240 dBFS). 165 notes, 17 distinct pitches, 37 notes / 5 s (steady 16ths).
  - flash_check: 0 flashes = PASS (mean luminance 0.014).
  - Encoded seam 0.74 (just above the 0.72 "good" band): the dancing sand makes every normal step 1.0-1.3 at the start, so the seam is quieter than ordinary motion. The last ~0.1 s is nearly still (the dissolve eases into frame 0), then the sand starts dancing on the first note.
  - Read encoded frames 0 / 0.5 / 1.5 s / 15 s / 27.3 s, a 1:1 crop of the climax (the grains stay granular through the encode) and a mid-morph sequence (bar 8).
- Doubts: the piece ends on the G-major cadence of bar 11 (a perfect cadence in the dominant key, the end of the first phrase), not on the home C. The "+/-" in the mode label is a little cryptic. Bolt is small and the bow reads best at 1:1.
- Delivered <VIDEOS_DIR>\batch22\chladni_plate.mp4. Owner review: pending.
- Owner review (2026-10-09): needs a hook and engagement, a better song, more grains and more beautiful forms -> chladni_plate2.
