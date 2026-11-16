# neon_trails3 — neon spiral line-art duel (batch28, 2026-10-11)

Built from the owner's review of neon_trails2: "music is too boring and slow. Also make some other movement — let them finish in some beautiful lines drawn." v1 and v2 are untouched.

## Look / movement
- Two riders only, on a 16x21 grid. There are no neutral bikes.
- Mochi starts at the near-left corner heading right; Bolt starts at the far-right corner heading left (180° symmetric).
- Both ride straight until a wall is ahead. Together they wind an **interlocking double spiral**: alternating coral and mint concentric rings that tighten toward the centre, so the turn rate accelerates to the end.
- **Line art:**
  - Walls are low (0.42 cell).
  - The trail behind each head is white-hot over the last 9 cells and fades to deep colour.
  - There is no floor tint and no bars. The HUD is only the two riders with their rules, the caption and banners.
- Steps run on the music's 16ths (9.33 cells/s); there is no jitter.
- **Hook / loop:** frame 0 = the finished spiral. It de-rezzes to the start by 0.72 s, "GO!" appears at 0.96 s, and the clip ends on the same frozen spiral. The seam is exact.

## Duel (deterministic; no seed)
- **MOCHI "MOST SPACE":** flood-fills each possible move and takes the most reachable cells; ties go to hugging the walls, then straight.
- **BOLT "ALWAYS LEFT":** straight until blocked, then turn left.
- The two rules choose the same turns until step 164, in the last coils.
- At step 167 (18.86 s) Mochi hits the wall. **"BOLT WINS! with ONE cell left in the arena."** The simple rule beats the brain.
- Board-size scan (14-20 x 18-24):
  - On odd x odd boards the first mover always wins by parity, so the strategy doesn't decide; those boards are rejected.
  - 16x21 gives a decisive 1-cell finish.

## Music: "Night Drive 140" (ORIGINAL, written in the scene, owned)
- **Key and length:** A minor, 140 bpm, 12 bars.

| Bars | Section | Chords | What plays |
|---|---|---|---|
| 0-3 | Hook | Am F C G | Driving saw-lead hook in 8ths/16ths (top note D5) + square an octave below |
| 4-5 | Build | F G | Held lead; snare roll goes 8ths → 16ths; riser; the kick drops out in bar 5 |
| 6-9 | Drop (10.29 s) | Am F C G | Full band: brass stabs, 16th arp, claps, open hats, tom fills |
| 10 | Climb | E | Lead climbs |
| 11 | Final | A minor | The loser's crash (18.86 s) |

- **Throughout:** 16th octave synth bass, warm pad and synth strings.
- **Drums:** our numpy LinnDrum-style kit with gated-reverb snare and toms (from neon_trails2).
- **Every turn of a bike** = a celesta pluck on the 16th grid: chord tones, Mochi high, Bolt low.
- Instruments: lib/orchestra.py (MuseScore_General, MIT).
- **Sync, measured onsets:**

  | anchor | anchor time (s) | onset (s) |
  |---|---|---|
  | launch | 0.964 | 0.955 |
  | drop | 10.286 | 10.272 |
  | final crash | 18.857 | 18.843 |

## Checks (<VIDEOS_DIR>\batch28\neon_trails3.mp4, Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1356 frames = **22.60 s**.
- LUFS -14.03, peak -2.53 dBFS, last 0.5 s -90.3 dBFS.
- flash_check: 0 flashes.
- Seam: post-encode 0.635 (good band); pre-encode 0.047, equal to the normal frame delta of 0.047, so the loop is exact.
- Stills read at 0 / 0.5 / 3 / 10 / 16.5 / 18.95 s; encoded frames read at 0.25 / 10.3 / 15.9 / 18.9 s.

## Args
- `--cols 16 --rows 21 --bpm 140` (defaults).
- `--still --frame ...`, `--silent`, `--audio-only`, `--report`.

## Doubts
- **The opening rings are long straight runs.** For the first ~8 s the centre of the arena is empty while the outer rings are drawn. The music carries the energy there.
- **The final split is very late.** It comes at step 164, about 0.3 s before the end, so "THE RULES SPLIT!" is not bannered. The rule labels under the riders carry the duel.
- **Bolt wins.** This matches BRIEF.md's balance preference.

## Owner review
- pending
- Owner review (2026-10-12): the song is better, the movement is not; give them DIFFERENT approaches and a real challenge over which approach is better -> neon_trails4.
