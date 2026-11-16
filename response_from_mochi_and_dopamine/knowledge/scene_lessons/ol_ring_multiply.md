# ol_ring_multiply (DopamineEXE, channel 2)
- Batch 54 (docs/BRIEF_batch54.md). The viral "ball escapes the spinning ring" format, new for this channel. Rule: **every ball that escapes through the gap = 2 new balls in the centre**, so the balls in play grow by 1 per escape and the escapes come faster and faster. Each escape also shrinks the ring a little and spins it a little faster. On the **1,000th escape the ring BREAKS** (cadence).
- Caption (baked, `--cap`; `--cap ''` = base): `Every ball that ^ESCAPES^ = 2 new balls…|until ~1,000~ escape`.
- **Shipped 4K (batch55, unchanged):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-04\2_ol_ring_multiply.mp4` (seed 5, label ship, 2160x3840, 14.48 s, 869 frames), 16:00 local Nov 5. FHD review copy archived as `archive\ol_ring_multiply_fhd.mp4`.
- 4K checks: h264 yuv420p 2160x3840, 60 fps, 869 frames; **flash_check PASS** (0 flashes); **-14.01 LUFS**, peak -4.15 dBFS, last 0.5 s digital silence; seam mean |delta| 0.260. Frames read at 0, 1, 6, 11.5, 12.3, 14.45 s (same timeline as the FHD).

## World (logical 1080x1920, static camera)
- Ring centre (508, 770), radius 360 -> 306 (x 148-868 at the start, inside 0.10-0.84 w): white 5 px line over a dark under-stroke, round lips at the gap. The gap is 70°. It warms toward gold over the last 25% of the goal.
- Balls r 8, flat fill + highlight, colour by generation (escapes back up its family line, 0-18) on one calm sweep coral -> amber -> gold -> green -> teal -> sky -> blue -> violet (S ~0.6). New balls grow in over 0.08 s. Motion streaks (last 6 frames, fading; drawn while <= 400 balls are in play).
- Escaped balls fly out, fall and fade over 0.8 s (75% opacity, decoration only, may pass the side safe band). A spark marks each exit; a soft pulse at the centre for the first 60 spawns.
- Finale: the ring splits into 12 gold arcs that fly out under gravity and spin, a gold ring runs out, all balls burst free; meter label RING BROKEN, counter 1,000 gold.
- HUD: meter y 1290 = escaped / 1,000 with the gold 1,000 goal from frame 0, "BALLS IN PLAY n" under it; counter y 1488 "ESCAPED" + "+2" pill (pops on every escape). Watermark DOPAMINE.EXE 35%.

## Physics (scenes/ol_ring_multiply.py `simulate`, seeded, exact)
- Gravity 400 px/s², dt 1/60 with 4 substeps. Perfectly elastic ball-ring reflection and equal-mass ball-ball collisions (cKDTree pairs, impulses accumulated per substep), speed cap 2,600 px/s.
- A ball whose centre reaches the ring inside the gap with room for its radius passes; it counts as escaped once fully outside. Each escape: 2 new balls at the centre (±4 px), seeded direction, 1,100 px/s.
- Ring radius 360 x max(0.85, 1 - 0.00015 x escapes); spin 2.0 rad/s x (1 + 0.0012 x escapes).
- One ball starts it all; frame 0 = sim 3.13 s (4 already escaped, 5 in play), the next escape at 0.12 s.
- Seed choice: seeds 1-6 at these settings (all reach 1,000 in 12.4-15.1 s of clip); seed 5 = the only one whose escapes climb every single second.

## Timeline (clip s, seed 5)
- Escapes/s: 3, 4, 5, 9, 18, 20, 33, 48, 65, 109, 193, 489. Escaped at s: 4, 7, 11, 16, 25, 43, 63, 96, 144, 209, 318, 511 -> 1,000.
- ~1,000 balls in play just before the end (the ring ~half full).
- **11.98 s**: the 1,000th escape = the cadence: the ring breaks. Hold 1.9 s (the burst flies out, the ring area empties), 0.6 s dissolve into the pre-roll = frame 0. 14.48 s.

## Sound
- **Music played as music:** J. S. Bach, Brandenburg Concerto No. 3 in G major BWV 1048, 1st mvt (c. 1718-21; d. 1750, PD), score beats 3.5-28: the famous opening (G-F#-G D-C-D ...) to the V7-I cadence on G at beat 28 = the 1,000th escape. Steady **123.2 bpm**. Source: midiworld.com `brand3.mid`, saved at `<SOUNDFONTS_DIR>\scores\bach_brandenburg3\` + SOURCE.txt. Not on any used list (Brandenburg 2 was used, not 3); not kid-coded; not banned.
- Arrangement: 3 violins, 3 violas, 2 cellos, contrabass (violone), a quiet harp doubling of the bass, timpani roll into the cadence; cadence = G-major tutti held 2 s + horns, trumpet, harp roll, falling celesta, timpani G.
- SFX: per escape a bright glassy ding (bell partials < 5.5 kHz) on a note the score sounds there, its register rising with log(escapes); sampled >= 12 ms apart (+0-16 ms jitter), gain / sqrt(rate/5). Soft wooden toks for ring hits while <= 60 balls are in play (>= 45 ms apart). The break: a big ding + a falling G-major cascade of 8 dings.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 869 frames, 14.48 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -4.15 dBFS, last 0.5 s digital silence. RMS/s (audio test): -18.7, -18.1, -17.9, -18.4, -17.5, -17.0, -17.0, -16.9, -16.5, -16.8, -16.5, -17.5, -12.5 (break), -17.2. SFX events/s 10, 13, 14, 21, 30, 33, 19, 27, 29, 35, 42, 40.
- Seam (check_clip): mean |Δ| **0.316**.
- Frames read from the mp4 at 0, 0.5, 1, 2, 5, 8, 10, 11.5, 12.0, 12.3, 13.2, 14.45 s; 1:1 crop of the packed ring at 11.5 s (the gap pouring balls out top-right, newborns at the centre).

## Doubts
- The first ~2 s are 5-12 streaking balls in a big ring (busy motion, but not a full frame).
- The ring breaking at exactly 1,000 is the goal's payoff, not a physical failure (the brief allowed it).
- Newborn balls cluster at the centre late on (a small radial pattern while ~400 spawn per second).
- Escaped balls spray past the side safe band (decoration; they fade in 0.8 s).

## Flags
`--seed (5) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0)`. Physics `--R0 (360) --shr (0.00015) --rmin (0.85) --rb (8) --gap (70) --w0 (2.0) --spd (0.0012) --g (400) --vs (1100) --goal (1000)`. Clip `--e0 (5) --hold (1.9)`.

## Upload draft
- Titles: "Every ball that escapes = 2 new balls… until 1,000 escape 🔴 #satisfying #physics #shorts" · "The ring kept shrinking… until the 1,000th escape broke it 💥 #satisfying #physics #shorts" · "Can 1 ball turn into 1,000 escapes? ⭕ #satisfying #physics #shorts".
- Pinned comment: "it took like 7 seconds to get the first 100 out and then 500 in the last second… where would you put the gap?"
