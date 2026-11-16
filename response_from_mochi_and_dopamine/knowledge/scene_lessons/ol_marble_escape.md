# ol_marble_escape (DopamineEXE, channel 2)
- Batch 52 (docs/BRIEF_batch52.md). "1,000 marbles. Only ONE escapes." A pachinko board with trap cups, a felt floor with dead-end notches, and ONE tiny exit (clear width 1.10 marble diameters), marked EXIT in gold from frame 0. The physics decides which marble gets out and when. The seed was picked so that exactly one marble ever escapes.
- Different from ol_marble_funnel (×2 gates, jar burst) and ol_spiral_maze: there is no multiplication here. This is a clogging/jamming story (count DOWN to one).
- Caption (baked, `--cap`; `--cap ''` = base): `^1,000^ marbles, ONE tiny exit|only ~ONE~ escapes` (`^x^` = the newest marble's hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_marble_escape.mp4` (Full HD, seed 4, label fhd, 14.35 s, 861 frames). No 4K yet.

## World (logical 1080x1920, static camera)
- Board: a thin white frame from x 128 to 888, top at y 318, with a spout (x 348-668) that the marbles pour from.
- Peg field: 6 staggered rows (y 372-552, 54 px pitch, r 4.5).
- Cup row A (rim 600 → 716): 4 cups.
- Cup row B (rim 780 → 1000): 5 cups, the middle one directly over the exit (it shields the exit from straight drops). Faint glass fill.
- Four scatter pegs at y 1040-1052.
- Felt floor: a shallow V (7°, y 1124 → 1172) with 4 dead-end notches per side (u 0.35/0.55/0.74/0.90).
- Exit neck: x 508 ± 9.7 (clear 15.4 px = 1.10 d, gold walls), 31 px long. Below it is a small gold tray.
- Marbles: r 7, glossy. Hue follows pour order: cyan → blue → violet → magenta → rose (S 0.68, V 0.93). The winner turns gold only once it is out.
- HUD:
  - Meter at y 1300: "CLOSEST TO EXIT n%", the closest in-play marble's distance to the exit. A rose tick marks the best of the last 2 s (the "so close" high-water mark). A gold EXIT goal is shown from frame 0.
  - Counter at y 1494: "N / MARBLES LEFT IN PLAY". At the escape it becomes "1 of 1,000 / ESCAPED" in gold.
  - A thin white ring marks the current leader.
  - "SO CLOSE" tags (max 4, ≥1 s apart) appear where a leader got stuck by the exit.
  - "JAMMED" (rose) shows next to EXIT while a stuck marble sits in the mouth.
  - Watermark "DOPAMINE.EXE" at 35%.

## Physics (scenes/ol_marble_escape.py `simulate`, seeded, cached pkl)
- Position-based dynamics: dt 1/60, 4 substeps × 3 iterations, cKDTree pairs, G 1500 px/s².
- Coulomb friction between marbles: static 0.6, kinetic 0.4 (PBD, proportional to overlap).
- Friction on walls is proportional to the normal push (μ 0.3); pegs have none.
- Restitution: pegs 0.5, walls 0.2-0.4 (impacts > 100 px/s only).
- Felt rolling resistance on the floor: μr 0.22, which is above tan 7°, so a lone marble stops on the floor and only pile pressure pushes marbles on. Speed cap 760.
- Pour: 1,000 marbles over 14 s, from random spots across the spout.
- Escape = the marble's centre leaves the neck bottom.
- In play / stuck:
  - A marble that rests (moves < 2.5 px) for 0.5 s is stuck. Shoved more than 3.5 px, it is back in play.
  - Unpoured marbles count as in play.
  - So the counter can tick up by a few when the pile shifts. That is honest.
- Honesty fixes made while building:
  - v1 used 2 px thick walls, which made the clear gap SMALLER than a marble. The PBD squeezed marbles through it. Fixed: the clear width really is 1.10 d.
  - v1 also had wall friction without a normal force (a lone marble could hang in the neck). Fixed.
- Seed search (`--search a-b`): keep only runs with exactly ONE escape, at sim 11.6-16.0 s, and no second one within 6 s.
  - Typical runs give 2-10 escapes, all in bursts at 8-10 s when the overflow reaches the floor.
  - Seeds 1-62 → only seed 4 qualified.
  - Seed 4 was re-run to 30 s: still exactly 1 escape (15.75 s). That is 14 s after it and 12.5 s past the clip end.
- Frame 0 = sim 3.75 s. Frame 0 slides between 1.0 and 4.0 s so the escape lands about 12 s into the clip (`--tl`).

## Timeline (clip s, seed 4)
- 0: the flood is pouring (~270 in), cups A partly full, row B starting to fill. Peg clicks from the first frame. Counter 915, meter 78%.
- In play at each second: 915, 839, 783, 737, 696, 593, 573, 526, 471, 373, 343, 350, 232 → the escape.
- 4-6 s: cups overflow; the first leaders roll onto the felt.
- 6.3 s: the first SO CLOSE (a leader stops 84 px short).
- 6.3-11.5 s: 9 leaders get within 21-84 px of the exit and stick (notches, the felt, the arch). The exit jams (JAMMED from ~8.5 s) while the pile grows.
- The pour ends at 10.25 s and the pile settles.
- **12.00 s = cadence:** marble #575 (poured at 8.07 s) squeezes through the neck. It turns gold, a gold ring and 12 sparkles go off, "ESCAPED!" appears, the counter reads "1 of 1,000", the meter shows 100%, and the jam closes behind it (JAMMED again).
- Hold 1.75 s, then a 0.6 s dissolve into the pre-roll (= frame 0).

## Sound
- **Music played as music:** Franz Schubert, "Erlkönig" D. 328, Op. 1 (1815; Schubert d. 1828, PD), the galloping piano introduction.
  - Source: Mutopia Project (C.F. Peters edition, licence "Public Domain"), `<SOUNDFONTS_DIR>\scores\schubert_erlkoenig\Erlkoenig.mid` + `SOURCE.txt` (downloaded 2026-10-27).
  - First use: not on any used list or docs/scenes, not kid-coded, not banned. Suspenseful, driving and on topic (a chase/escape).
  - Bars 1-7 (G-minor octave triplets, the rising bass motif twice, C → C# → D7 dominant), 28 beats at one steady **140 bpm** (the file's tempo is 152). Then OUR G-major chord (Picardy third) on the bar-8 downbeat = the escape.
  - `SEG_OPTS` also allows bars 1-7 + bar 15 (32 beats) for a longer clip.
- Arrangement (lib/orchestra):
  - Schubert's two piano hands with a crescendo.
  - A strings_trem pad on the sounding chord per beat.
  - Cello + contrabass (8vb) on the bass motif.
  - Soft timpani G per bar; horns hold D through the last 2 bars; a timpani roll on D into the cadence.
  - Cadence: G major on strings, piano roll, horns, trumpet, flute, harp roll, celesta glints, tubular bell, timpani G.
- SFX (×0.55, tonal, no noise), all real contact events from the sim:
  - Peg hits = crisp glass clicks on a chord tone Schubert sounds there (G5-G6).
  - Cup / floor / marble-marble knocks = rounder clacks an octave lower.
  - Thinned to a cap that ramps 0.7× → 1.25× over the clip (52 → 90 events/s, falling to 41 in the settling second before the escape).
  - SO CLOSE = a soft two-note tink; the escape = a G6 chime + 12 sparkle tinks.
  - Breakdown: click 489, clack 367, tink 19.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence; own mux without `-shortest`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 861 frames, 14.35 s. **flash_check PASS** (0 flashes, mean lum 0.011).
- **-14.00 LUFS**, peak -3.01 dBFS, last 0.5 s digital silence, energy > 5 kHz 0.017%.
- RMS per second (muxed): -19.0, -18.5, -18.5, -17.9, -18.1, -17.5, -17.4, -17.1, -17.0, -16.8, -16.1, -16.9, -11.8 (cadence), -19.9, silence.
- Seam: mean |Δ| last → 0 is 1.337. That is an ordinary step in this file (median frame step 1.40, p10 0.78); check_clip's generic 1.1 line does not fit 1,000 moving marbles.
- Frames read from the mp4 at 0, 0.5, 1, 2, 6.3, 6.5, 7.8, 7.9, 9.0, 10.3, 10.4, 11.5, 11.92, 12.0, 12.15, 12.5 and the last frame.
- 1:1 crops of the exit at 7.8 (SO CLOSE + leader ring), 11.92 (the winner inside the neck, JAMMED) and 12.15 (gold marble in the tray, sparkles).

## Flags
`--seed (4) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0) --tl (12.0) --resim --search a-b --stats a-b --tend`.

Sim-changing flags (re-search after any change): `--n (1000) --r (7) --ew (1.10) --pour (14) --g (1500) --mus/--muk (0.6/0.4) --mur (0.22) --iters (3) --notch --cupa (716) --cupb (1000) --vtop (1124) --tent --escmin/--escmax (11.6/16.0) --verify (6)`.

Full sim ~75 s; FHD render + mux a few minutes.

## Doubts
- **"Only ONE" is honest for this seed only.** In most runs 2-10 marbles get out. The caption is true for this run: exactly 1 of 1,000 by 30 s of sim.
- **The event rate falls at the end.** The pour ends at 10.25 s, so in the last ~1.7 s before the escape the board settles (hits 90 → 41/s). This is the "jammed" tension beat; the music (D7 dominant + timpani roll) carries it.
- **The exit is small on a phone.** The neck is 15 px wide at the bottom of the board. The gold walls, glow, EXIT/JAMMED labels and the leader ring carry it, but the squeeze itself lasts only a few frames.
- **The counter falls 915 → 232, not to 1.** About 230 marbles are still creeping or pouring-tail when the winner gets out.
- **Frame 0 is sim 3.75 s,** so the cups are already partly filled (the busy-frame rule).
- **Is the outcome obvious from frame 0?** The count is promised (ONE), so the uncertainty is WHICH marble and WHEN.
  - The ring hops between 9 leaders that get "SO CLOSE" and stick.
  - The exit shows JAMMED for ~3.5 s.
  - The winner is a late marble (poured at 8 s, out of frame-0 view), not an early leader.
  - So the "who" is not guessable.
- **Marble size:** 1,000 at r 7 (the same size as ol_marble_funnel), kept at 1,000; readable as glossy beads, small.

## Upload draft
- Titles (≤95 chars incl. tags):
  - "1,000 marbles, ONE tiny exit… only one got out 😮 #satisfying #physics #shorts"
  - "999 marbles got stuck. Watch the ONE that escaped 🟡 #satisfying #physics #shorts"
  - "It was jammed for 3 seconds… then ONE marble squeezed through #satisfying #physics #shorts"
- Pinned comment: "9 marbles got right up to the exit and froze… did you spot the one that made it before it went gold?"

## Shipped (4K, 2026-10-28, batch53)
- Owner: "ok let's try" → 4K ship. `NF_SCALE=2.0 python scenes/ol_marble_escape.py --label ship` (seed 4, cached sim pkl: escape at sim 15.75 s = clip 12.00 s, winner #575, 9 near misses: identical to the FHD).
- Encoded: h264 yuv420p 2160x3840 @ 60 fps, 861 frames = 14.35 s. −14.00 LUFS, peak −3.01 dBFS, last 0.5 s silent. flash_check PASS (0 flashes, mean lum 0.011). Seam mean |Δ| 1.228 (an ordinary step for 1,000 moving marbles, FHD 1.337).
- Frames read from the 4K mp4: 0.5 s, 12.3 s (ESCAPED! 1 of 1,000) + a 1:1 crop of the exit at 12.1 s.
- Staged: `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-03\2_ol_marble_escape.mp4` (16:00 local Nov 4 = 07:00 US East Nov 4). FHD review copy → `DopamineExe\archive\ol_marble_escape_fhd.mp4`.
