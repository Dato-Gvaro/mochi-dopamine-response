# neon_trails2 — light-trail duel, rework (batch27, 2026-10-11)

Built from the owner's review of neon_trails: "remove those two bikes starting from the middle, they are too many for that scene; if the board is left too empty, reduce its size. Also change the music — something 80s and MIAMI style." v1 is untouched.

## What changed vs v1
- **Bikes:** the two mid-board neutral spawns are removed. 4 neutral bikes remain, all spawned on the rims.
- **Board:** 18x22, down from 20x24. Cells are bigger and the payoff labyrinth is denser (parallel spirals).
- **Music:** "Neon Mile", an original 80s Miami track (see Music). The whole game clock is locked to its groove.
- **Banners:** they now pop DOWN (118 % → 100 %) at full alpha, so they are readable from their first frame.
- **Kept from v1:** the look, the hook (payoff-first de-rez), the loop, the AI, the HUD and the flash safety.

## Engagement (seed 696, AI params look 5 / box 100 / straight 2)
- Neutrals are out at 3.21 / 4.82 / 5.09 / 6.70 s, then "1 vs 1!".
- "BOXED IN?!" at 14.49 s: her 16-cell box glows red.
- **"1-CELL SQUEEZE!" at 15.54 s:** Mochi slips through a true 1-cell gap with Bolt 1 cell away, near the camera. This lands on the big stab.
- "MOCHI TAKES THE LEAD!" at 16.61 s.
- The two race in parallel spirals up the right side. **Bolt crashes at 19.55 s**, on the final A minor, with Mochi at 0 cells left: "MOCHI WINS! by ONE STEP!"
- 5 lead changes in the last 12 steps.
- Search: 18x22 hit rate ~1/60 with the composed clock.
  - Alternatives: 821 (16x20, 1-cell gap, Mochi by 15) and 208 (20x24, Bolt wins by 1, wider gap).

## Clock (one groove, 112 bpm)
- Frame 0 = the hook's first note.
- Launch on beat 2 (1.07 s). Bikes step on 8ths (3.73 cells/s).
- The drop at bar 5 (10.71 s) moves them to 16ths (7.47 cells/s).
- The squeeze lands on beat 2 of its bar (15.54 s): the stab plus a stop-time break of 1.88 s. The bikes keep riding at 16ths through the break.
- Re-entry on E at 17.41 s for one bar.
- The final A minor at 19.55 s, which is the loser's crash.
- Ring 2.45 s, then a 1.3 s silent tail. T = 23.30 s.

## Music: "Neon Mile" (ORIGINAL, written in the scene, owned)
- **Harmony:** A minor, i–VI–III–VII (Am F C G), one chord per bar.
- **Hook:** an 8-bar sax hook in 3+3+2-eighth syncopation, range D4–D5, played on GM tenor sax plus a polysynth an octave below.
- **Bass:** octave-bouncing 8ths.
- **Pads:** warm pad + synth strings.
- **From the drop:** bright synth-brass stabs on beat 1 and the and-of-2, and a 16th square arp.
- **Squeeze:** big stab, held chord, a gated tom fill and a reverse-cymbal swell into the E bar, which climbs to the A.
- **Drums:** our own numpy LinnDrum-style synthesis:
  - pitch-drop kick;
  - gated-reverb snare and toms (dense room chopped at 0.32-0.38 s);
  - 3-burst clap;
  - closed and open hats.
  - Crash and splash cymbals come from the soundfont kit.
- **Every neutral crash** = gated low and mid toms + splash, on the step grid.
- Instruments: lib/orchestra.py (MuseScore_General, MIT). "tenor_sax" is added to orc.INSTRUMENTS at runtime, scene-local; no lib file was edited.
- **Sync:** onsets were measured within 16 ms of every anchor:

  | anchor | time (s) |
  |---|---|
  | launch | 1.07 |
  | crashes | 3.21 / 4.82 / 5.09 / 6.70 |
  | drop | 10.71 |
  | squeeze | 15.54 |
  | re-entry | 17.41 |
  | final | 19.55 |

## Checks (<VIDEOS_DIR>\batch27\neon_trails2.mp4, Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1398 frames = **23.30 s**.
- LUFS -14.02, peak -2.07 dBFS (the synthesized drums are punchy), last 0.5 s -84.3 dBFS.
- flash_check: 0 flashes.
- Seam:
  - Post-encode 0.590 (good band).
  - Pre-encode, frame 1397 → 0: 0.0461, equal to the normal frame delta (0.0457), so the loop is exact.
- Encoded frames read at 0, 0.25, 0.5, 1.1, 2, 3.25, 10.75, 14.5, 15.56, 16.65, 19.57 and 20.6 s.

## Args
- `--seed 696 --cols 18 --rows 22` (defaults).
- `--still --frame ...`, `--silent`, `--audio-only`, `--report`, `--search a n`.

## Doubts
- **Mochi wins again.** The closest Bolt win (208) has no true 1-cell gap.
- **The final crash is at the far-right corner,** small on screen.
- **The sax is the soundfont's GM tenor sax.** It is measured only, not heard; if it sounds cheesy, the lead can go to saw_lead or synth_brass with a one-line change.

## Owner review
- pending
- Owner review (2026-10-11): music too boring and slow; other movement: let them finish in beautiful drawn lines -> neon_trails3.
