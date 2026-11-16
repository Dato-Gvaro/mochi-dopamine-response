# press_meteor — press franchise: Bolt swaps his bomb for METEOR STRIKES (batch67 wave B, 2026-11-03)

- Brief: docs/BRIEF_batch67.md clip 5. New file `scenes/press_meteor.py` (copy of press_bomb; press_bomb and longform_atom untouched). Meteor look (flame trail, glow, rock; fireball ×1.3, ring/smoke colours, "IMPACT!") copied from longform_atom's crusher tools.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch67\press_meteor.mp4` (Full HD 9:16, 20.23 s, 1214 frames; label b67).
- Caption (baked): "Every ball hit ~HARD~ splits into 3" / "~Press~ or ~METEOR~:" / "whose jar ~OVERFLOWS~ first?".

## THE ONE CHANGE
- No claw, no fuse, no dive: every 1.45 s a meteor streaks in from the sky (0.70 s, slanted from the jar's middle side, accelerating) and hits the pile's SURFACE at the next stop column (`land_y`). At contact the bomb's ring rule fires with a 1.25× harder kick (K 3000 vs 2400 px/s, L 120; longform_atom's meteor/blast kick ratio). The meteor vanishes in the fireball.
- Everything else is press_bomb: the same press tempo, open jar (balls over the rim are LOST), split rule (V_BREAK = 0.62 m/s × 1.155^gen), overflow test (settled top above MAX 8 frames), v3 SETTLED readouts (always on).
- Readout fix vs press_bomb v3: while Bolt's pile is settling the SETTLED % holds its last calm value (press_bomb showed the raw held value, which drops to ~40 % right after a hit while the jar looks 80 % full). "Who touched MAX" is searched only up to the overflow.

## Honest result
- Bolt-only sims to 21 s (press overflows at sim 19.02): seeds 0/1/2/3 at K 3000: Bolt's settled top 645-734 px at 18-20 s (MAX 560) → the press wins every seed. K 4000 / 5000 (seed 1): still no overflow before 19.02. Not a knife edge (press_bomb's bomb was).
- Why: surface hits split only the top layer; the press splits every ball every stroke. Lost over the top: 15 in total (surface hits mostly go sideways/down into the pile).
- Seed 1 (clip = sim − 0.6): first IMPACT 0.20 s; Bolt leads from ~3.3 s (9 vs 3 → 27 vs 9); biggest hit +872 (clip 11.9). LEAD CHANGE 17.48 s (the press's last wave); OVERFLOW 18.42 s: press 6,561 vs Bolt 4,538; PRESS WINS 18.82 s (plate snaps).

## Sound
- Bach, Toccata in D minor BWV 565 (`audio.MELODIES` "bach_toccata", PD), a note per split group (press_bomb: Für Elise). william_tell was tried first: 3 pitches, 78 % one note (monotone) → rejected.
- Meteor: a tonal riser over its 0.7 s streak (no noise whoosh), explosion + thunk on IMPACT. Press sounds, cadence, riser and glass as press_bomb.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 1214 frames = 20.23 s. −14.04 LUFS, peak −5.68 dBFS, last 0.5 s −90 dBFS.
- Notes 60, 10 distinct, top 16.7 %. Events per 5 s 10 / 10 / 20 / 20. flash_check 0. Seam 0.92 (press_bomb 0.74-0.80).
- Frames read (Fast encode): 0.1, 0.25, 2.0, 7.6, 12.5, 17.6, 18.45, 19.3; 1:1 crop of an impact (Full HD 11.85 / 11.97).

## Doubts
- The meteor's streak crosses the caption for ~0.3 s each time (it enters from above the stage).
- Few losses (15): the "LOST OVER THE TOP" banner never fires.
- The kick ratio 1.25 is a choice (documented above); the outcome holds up to 5000.

## Commands
- `python scenes/press_meteor.py --only bolt --report --tlimit 21 [--seed N --kick K]` (~9 s each)
- `NF_SCALE=1.0 python scenes/press_meteor.py --label b67` (sim ~1 min, render ~20 min at 2 threads)
