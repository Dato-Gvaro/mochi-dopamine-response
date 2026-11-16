# ol_apollonian (DopamineEXE, channel 2)
- Batch 54 (docs/BRIEF_batch54.md). Sierpinski's fractal family (17.7K), but a new shape and a new rule: **filling, not removing**. An Apollonian gasket inside one big circle: 3 equal circles leave 4 curved-triangle gaps; every round, **every gap gets the biggest circle that fits** (exact: Descartes' circle theorem with complex centres; max tangency error 1e-12 px). Each new circle makes 3 new gaps: 4, 12, 36 ... 26,244 new circles per round.
- Caption (baked, `--cap`; `--cap ''` = base): `Every gap gets the ^BIGGEST^ circle that fits…|how close to ~ZERO~ space can it get?` (batch55; was `until there's ~NO SPACE~ left`, which overpromised: the honest end is 1.6%).
- **Shipped 4K (batch55):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-04\1_ol_apollonian.mp4` (label ship, 2160x3840, 13.10 s, 786 frames), 04:00 local Nov 5. FHD review copy archived as `archive\ol_apollonian_fhd.mp4` (it has the OLD purple colours + old caption).

## Batch 55 fix (2026-10-28)
- Owner: "try it, but the big purple circles don't look good: switch colour". **Recolour** (`--pal v2`, default; `--pal v1` = old): no purple anywhere. By generation: ocean blue (the 3 big, H 0.565 S 0.64 V 0.71) -> teal -> green -> lime -> gold -> amber -> coral -> rose -> pink (newer = brighter). The meter gradient and the caption highlight follow.
- **Caption line 2** -> `how close to ~ZERO~ space can it get?` (x 118-898 = 0.109-0.831 w, inside the side safe zone). The HUD goal stays "NO SPACE"; the meter honestly stops at SPACE LEFT 1.6%.
- Checks (encoded 4K): h264 yuv420p 2160x3840, 60 fps, 786 frames, 13.10 s; **flash_check PASS** (0 flashes); **-14.01 LUFS**, peak -3.17 dBFS, last 0.5 s digital silence; seam mean |delta| 0.148. Frames read at 0, 0.3, 2, 5, 10.45, 13.05 s + a 1:1 crop of the lower-right cusps at 9.5 s.

## World (logical 1080x1920, static camera)
- Big circle centre (508, 752), r 384 (x 124-892, inside 0.10-0.84 w), thin white line. The 3 starting circles r 178.2 (top, lower-left, lower-right).
- 9 rounds: **39,368 circles** in all (the counter counts the big one: 4 at frame 0).
- Colour by generation, newer = brighter so the action reads: indigo (the 3, V 0.62) -> blue -> teal -> green -> gold -> amber -> coral -> rose -> pink (S ~0.44-0.64). Glossy radial gradient for r >= 7, flat + highlight for 1.6-7, opacity-weighted dots below (rounds 7-9 are mostly sub-pixel).
- Pop: scale 0 -> 1.2 in 0.09 s -> 1.0 by 0.24 s; a white ring on big new circles, a brief white flash on small ones (the cusps sparkle as a round sweeps).
- Each round sweeps clockwise from the top (the centre gap first), over 92% of its window, slightly accelerating.
- HUD: meter y 1290 = space filled (honest area, 0 -> 98.4%), "SPACE LEFT 100%" -> "1.6%", "ROUND n / 9" above, gold NO SPACE goal from frame 0. Counter y 1488 "CIRCLES" + "×3" pill (pops at each round start). Watermark DOPAMINE.EXE 35%.
- `--zoom` (default 1 = off): a zoom into a cusp was tried (x2.4) and dropped: any close view is mostly one of the 3 big indigo circles.

## Timeline (clip s)
- Rounds start at 0.05, 0.62, 1.20, 2.06, 3.21, 4.65, 6.09, 7.52, 8.96 s (on the score's beats 0, 1, 2, 3.5, 5.5, 8, 10.5, 13, 15.5 after beat 18).
- Pops/s: 12, 40, 93, 191, 352, 768, 1,884, 3,655, 6,522, 19,328, 6,519 (climbing to the end).
- Circles at s: 4, 16, 56, 149, 340, 692, 1,460, 3,344, 6,999, 13,521, 32,849 -> 39,368. Space left: 100% -> 40% (1 s) -> 19% -> 12.9% -> 9.6% -> 7.0% -> 4.8% -> 3.9% -> 3.0% -> 2.2% -> 1.6%.
- **10.40 s cadence**: the last circle; outer ring turns gold, 2 gold shimmer sweeps across the gasket, 12 sparkles, twinkles in the cusps through the hold, counter 39,368 gold. Hold 2.1 s, 0.6 s dissolve into frame 0 (the 3 circles). 13.10 s.

## Sound
- **Music played as music:** J. S. Bach, "Jesu, Joy of Man's Desiring" (chorale movement of Cantata BWV 147, 1723; d. 1750, PD), score beats 18-36: the famous triplet motif (its 2nd statement, bar 5) to the ritornello's G-major cadence, where the choir enters with the chorale's first chord = the last circle. Steady **104.3 bpm** (quarter). Source: midiworld.com `jesu.mid`, saved at `<SOUNDFONTS_DIR>\scores\bach_jesu_joy_bwv147\` + SOURCE.txt. Not on any used list; not kid-coded; not banned.
- Arrangement: oboe + violin (+ soft strings) on the triplet line; strings_slow, cello, contrabass, harp on the continuo; a soft pizzicato on each dotted-quarter pulse; timpani roll into the cadence. Cadence: choir G-major chord + strings, oboe, harp roll, celesta, tubular bell, timpani G.
- SFX: per circle a soft felt-mallet "pop" (tiny downward blip, no noise) on a note the score sounds there, lower for bigger circles (G3 ... ~D7); sampled >= 12 ms apart (+0-16 ms jitter), gain / sqrt(rate/30), ramped in over the first 3 s (the first big pops are long and low). 12 tinks on the sparkles.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 786 frames, 13.10 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -3.17 dBFS, last 0.5 s digital silence. RMS/s (audio test): -18.2, -17.0, -17.9, -18.4, -18.8, -18.4, -18.5, -17.3, -17.6, -17.4, -14.0 (cadence), -12.7, -29.7. Pop SFX events/s ~33-48 (sampled).
- Seam (check_clip): mean |Δ| **0.221**.
- Frames read from the mp4 at 0, 0.3, 1, 2, 5, 8, 9.5, 10.45, 11.2, 13.05 s; 1:1 crop of the lower-right cusps at 9.5 s.

## Doubts
- **Honest end state is 1.6% space left, not 0%.** The caption says NO SPACE; the meter stops just short of the gold goal and reads "SPACE LEFT 1.6%". A gasket never reaches 0 (10 rounds = 1.1%).
- After ~4 s the 3 big indigo circles + the 4 next ones fill ~85% of the frame; the later rounds happen in the cusps and along the rim (readable at 1:1, small on a phone). The counter, flashes and pops carry it.
- The white flash on fresh tiny circles is drawn as small squares (2-3 px at 1:1).
- The outcome (it fills up) is fairly predictable; the open question is how many circles and how close to 0.

## Flags
`--seed (1) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0)`. Geometry `--rb (384) --rounds (9)`. Clock `--tcad (10.4) --hold (2.1)`. Camera `--zoom (1.0) --zt0 --zt1 --zang --zd`.

## Upload draft
- Titles: "Every gap gets the biggest circle… until there's NO space left ⭕ #satisfying #physics #shorts" · "3 circles became 39,368 and they all touch ⭕ #satisfying #physics #shorts" · "Can circles fill a circle with NO gaps? 🤯 #satisfying #physics #shorts".
- Pinned comment: "39,368 circles and there's still 1.6% empty space left… how many rounds would it take to hit zero?"
