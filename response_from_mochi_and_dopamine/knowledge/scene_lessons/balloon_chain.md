# balloon_chain — "Every balloon that pops POPS 2 more" / "Spread out or packed? First to CLEAR the ceiling"

- **v5 (owner 2026-10-23: "the two next ones are kind of TICKING to explode"; pins kept, they show the cause). Approved to ship once the owner sees the ticking.**
  - Every triggered balloon TICKS before it pops: from the moment its pin arrives, a pulse on every 8th of the music (every other 16th): swell +12 % and back over 0.15 s, slightly brighter each pulse (+0.10, +0.18, +0.26 toward white), a gentle residual swell between pulses; then it pops on its 16th and releases its 2 pins. Bolt's balloons tick 2-3 times (73 x2, 54 x3, 17 x1 where a second pin shortened the fuse). Mochi's rare pin-hit balloons tick the same way. No flashing (flash_check 0).
  - Sound: one soft tonal tick per room per 8th that has ticking balloons (sine + a little 2nd harmonic, 12 ms decay, a chord tone C6-B6 of the current harmony, gain 0.045 x (1 + log2 n), max 0.11, panned to their mean x). No noise.
  - Same sim, seeds (Bolt 100 / Mochi 0), music, timings as v4.
  - v5 checks (encoded `output/balloon_chain_v5_9x16.mp4`): h264 yuv420p 1080x1920 60 fps 17.20 s; -13.98 LUFS, peak -5.9 dBFS, last 0.5 s -240 dB; RMS/s -22.4 -21.2 -18.5 -19.0 -19.1 -16.7 -15.1 -17.0 -16.1 -16.4 -16.1 -15.7 -15.5 -15.1 -14.1 (cadence) -16.1 -42.5 (tail); flash_check PASS (0); seam post-encode 1.20 (codec floor 0.91, see v4).
  - Frames read at 1.3 s (the tip row's 2-pin bursts, targets ticking), 4 s (ticking front at 17), 8 s (the yellow front ticking under LEAD CHANGE), plus a 2x zoom of one tick cycle (1.47-1.73 s).
  - Full HD delivered over `<VIDEOS_DIR>\MochiAndBolt\review\batch48\balloon_chain.mp4`. 4K ship render: `output/balloon_chain_ship_9x16.mp4` (NF_SCALE=2.0).

- **v4 (coordinator 2026-10-23: pins too small at phone size; same sim, seeds Bolt 100 / Mochi 0).**
  - Every new pin ~2.2x bigger: k = 1.15 (~36 px long in Full HD), Bolt's first bursts (gen <= 2) k = 1.45 (~45 px); brighter gold head, steel shaft, a soft glow along the pin (11k px wide, 22 % alpha) and a longer trail along the flown arc (8 x 16 ms). Drawn flight 0.20 s (sim hit time stays 0.12 s; the strain quiver starts when the drawn pin arrives). Hit spark a bit bigger.
  - First ~2 s: Bolt's thrown pin k = 2.0 with a glow; balloons targeted by his first bursts (gen <= 2) get a soft pulsing gold ring from the pin's arrival until they pop.
  - Loop seam: clip frame f now shows sim time (f + 1)/60 and the last frame dissolves fully into sim t = 0, so last -> first is one ordinary 1/60 s step; the soundtrack is shifted by the same frame (4 ms fade-in at sample 0). Post-encode seam 1.20 (v3 1.33). Measured codec floor: the SAME frame coded twice (I vs P) already reads 0.91 on this detailed picture, so ~1.2 is codec noise, not a cut. (Forcing a keyframe on the last frame did not help: 1.375.)
  - v4 checks (encoded `output/balloon_chain_v4_9x16.mp4`): h264 yuv420p 1080x1920 60 fps 17.20 s; -13.98 LUFS, peak -5.7 dBFS, last 0.5 s -240 dB; RMS/s -22.4 -21.3 -18.5 -19.0 -19.0 -16.7 -15.1 -17.0 -16.1 -16.4 -16.1 -15.7 -15.4 -15.1 -14.1 (cadence) -16.1 -42.5 (tail); flash_check PASS (0).
  - Frames read 1:1 (Bolt's room) at 0.3 s (big thrown pin on its arc into the tip), 1.3 s (the first 2-pin bursts flying out, targets ringed), 4 s (17 popped, two 2-pin bursts on the front), 10 s, plus 14.08 s (Mochi's misses falling through empty air, clearly visible).
  - Delivered over `<VIDEOS_DIR>\MochiAndBolt\review\batch48\balloon_chain.mp4`.

- **v3 (owner review of v2, 2026-10-23): pins spawn pins.** Kept: music, counters, lead change, CLEAR finale, colours, mastering, loop.
  - Bolt: no arms. A simple throw of his ONE pin from the top of his head (small squash/hop at -0.10 s, dotted gold arc, pops the bouquet tip at 0.25 s), then he just stands with a smug face; "1 PIN" tag stays.
  - **New chain rule (both rooms):** a popping balloon releases exactly 2 new pins. Each flies to a neighbour within PIN_REACH = 12 px of its skin (one not hit yet if there is one, else one already straining), along a short circular arc (0.12 s), with a tiny spark on the hit; with no neighbour in reach the pin flies off into the air and drops (0.9 s). The hit balloon quivers/swells for the fuse (0.70-0.95 s), then pops on the next 16th. A second hit keeps half the remaining fuse. **No jolts any more** (P_JOLT unused); every Bolt pop is a pin pop (149 of 149).
  - Mochi's lattice gaps (~16-20 px) are mostly beyond 12 px, so her 2 pins per pop usually fly into empty air and fall; 24 of her pops all clip come from a pin that did reach a neighbour (chains of 1-2, then dead).
  - Clean look: removed the rubber shards and "+n" labels; pop = a small soft ring (0.22 s) and the balloon is gone; rubber bits 2 per pop at 45 % alpha (floor 30 %). Pins are small gold-head steel pins with a short trail along the path; pins are clipped to their room.
  - Seed Bolt **100** (from 1,500, fuse 0.70-0.95; filter: all 150, last pop exactly 14.000 s, one lead change), Mochi 0. Same music cut as v2 (bars 11-13 + 16-19, CLEAR = F-major arrival at 14.0 s). Clip 17.20 s.
  - Timeline: 0.25 tip pops, its 2 pins hit the 2 tip neighbours, they pop at ~1.25 s (then 4 pins …). Counts M/B: 0 s 21/0, 1 s 25/1, 2 s 29/3, 3 s 35/10, 5 s 46/26. **LEAD CHANGE 7.88 s**; Mochi on 16ths from 8.5 s; CLEAR 14.0; Mochi ends 123/150 (27 LEFT). Pops/s (B+M) 5 6 12 13 13 16 19 19 24 29 30 35.
  - v3 checks (encoded `output/balloon_chain_v3_9x16.mp4`): h264 yuv420p 1080x1920 60 fps 17.20 s; -14.01 LUFS, peak -5.8 dBFS, last 0.5 s -240 dB; RMS/s -22.4 -21.4 -18.6 -18.9 -19.1 -16.7 -15.1 -17.0 -16.0 -16.4 -16.1 -15.7 -15.4 -15.1 -14.0 (cadence) -16.0 -41.4 (tail); flash_check PASS (0); seam pre-encode 0.73 (post-encode 1.33, GOP quality as before); check_clip notes 368 / 23 distinct.
  - Frames read 1:1 on Bolt's side at 0.3, 1, 3, 6 s from the encoded file, 2x zooms of the first pins (0.27-0.32 s, 1.27-1.37 s), Mochi at 3.2 s (pins falling into air), 14.08 s.
  - Delivered over `<VIDEOS_DIR>\MochiAndBolt\review\batch48\balloon_chain.mp4`. v2/v1 notes below are history.

- **v2 (owner review 2026-10-23: "the first character is ok shooting something, but I don't get how the second character is popping?")**. Bolt's side made instantly readable; everything else kept.
  - Bolt THROWS his one pin on screen: wind-up in the pre-roll, release at -0.10 s, a dotted gold arc from his hand to the bouquet tip, which pops at 0.25 s (on the 8th grid). Then he crosses his arms (stubby arms drawn over the toon) and smug-waits; a gold "1 PIN" tag sits over him the whole clip. Before the lead change he looks smug, not worried.
  - Every pop: a soft ripple ring (1 → 4 r over 0.35 s); its 2 rubber shards fly as thick blobs with a motion-blur trail along a slight arc to the balloon they hit (0.08 s), a small spark on the hit; jolted neighbours shake (3.4 px, 19 Hz, 0.4 s); a hit balloon quivers from the moment it is hit and swells until it bursts; "+n" floats up from every pop that sets off n more (n = shard hits + jolts, gold if ≥ 2), until 1 s after the lead change. The old small "x2" marks are gone; the big x2 doubling badges stay.
  - Because the pin now lands at 0.25 s (not -1.25 s), the chain runs 1.5 s later: new Bolt seed **4893** (from 8,000; filter: all 150, last pop exactly 14.000 s, the pin pop's 2 shards BOTH hit, one lead change 6-8.5 s). Shards now reach their target at +0.08 s in the sim.
  - Music cut one bar longer: bars 11-13 (0-6 s) + bars **16-19** (6-14 s, bar 16 = the tutti C-minor 8ths), F-major arrival = **CLEAR at 14.0 s**. Clip **17.20 s** (1032 f).
  - Timeline: 0.0 Mochi 26 / Bolt 0 (pin in the air); 0.25 tip pops "+3"; 0.88/1.0 its two hits pop; counts 1 s 31/3, 2 s 36/8, 3 s 41/13, 6 s 56/41; **LEAD CHANGE 7.88 s** (64 v 66); Mochi on 16ths from 8.5 s; CLEAR 14.0; Mochi ends 124/150 (**26 LEFT**). Pops/s (B+M) 7 8 13 12 15 14 18 18 20 24 25 33.
  - v2 checks (encoded `output/balloon_chain_v2_9x16.mp4`): h264 yuv420p 1080x1920 60 fps 17.20 s; -14.01 LUFS, peak -5.6 dBFS, last 0.5 s -240 dB; RMS/s -21.9 -20.5 -18.8 -19.3 -19.0 -16.9 -15.0 -17.0 -16.1 -16.5 -16.2 -15.7 -15.4 -15.1 -14.1 (cadence) -16.0 -41.4 (tail); flash_check PASS (0); seam pre-encode 0.53 (post-encode 1.14, GOP quality, as v1); check_clip events/5 s 121/177/68.
  - Frames read 1:1 on Bolt's side at 0.2, 1, 3, 6 s (throw arc, first "+3"/"+1", "+2"s on the front, the 41-count front), plus 2x zooms of 0.25-0.37 s and 1.0-1.07 s, 7.88 s, 14.08 s, last frame.
  - Delivered over `<VIDEOS_DIR>\MochiAndBolt\review\batch48\balloon_chain.mp4`. The v1 notes below describe the first cut (seed 354, CLEAR 12.0, 15.2 s).

- New scene (batch48). Same critical-mass idea as mousetrap_chain (owner favourite), new look and mechanic: balloons and pins instead of traps and balls.
- Two rooms with the SAME 150 balloons each, against the ceiling, on strings. Ordered rainbow by row (ceiling row red → bottom row violet), same rule in both rooms.
  - Mochi (coral) ties hers OUT on tethers: a 10 x 15 lattice (37.6 x 42 px pitch, jitter ±5, gaps ~16-20 px). Strings run straight down to the floor.
  - Bolt (mint) lets his float into ONE tight bouquet: an inverted triangle of touching balloons (rows of 17 → 3, hex), every string tied to one knot over a weight.
- Caption baked in-scene (`--cap`): `Every balloon that pops ~POPS 2~ more|Spread out or packed? First to ~CLEAR~ the ceiling` (POPS 2 gold, CLEAR red). Line 2 was shortened from the coordinator's "Spread out or packed tight? First to clear the CEILING" so it fits the safe width at a readable size.
- New file `scenes/balloon_chain.py`; no lib/ or tools/ changes.

## Chain model (seeded, event-driven, same rules in both rooms)
- A popping balloon flings 2 rubber shards in random directions. A shard pops the first balloon it meets within REACH = 20 px of the popped balloon's skin (it flies through balloons that are already gone). Balloon radius 11 px.
- A balloon TOUCHING a popping one (centre distance ≤ 2r) is jolted and pops with p = 0.5. Only Bolt's balloons touch.
- A hit balloon strains (swells ×1.17, quivers, bright rim) for a fuse of 0.6-0.9 s, then pops on the next 16th of the music. A second hit while straining keeps half the remaining fuse (more nicks burst it sooner).
- Mochi throws a pin on every 8th (her sweep: columns left to right, each column bottom up): +1 manual pops. A quarter after Bolt overtakes her (from 6.0 s) she panics and throws on every 16th. Her pins stop at CLEAR.
- Result: Mochi's shards rarely reach a neighbour (25 chain pops in the whole clip): subcritical. Bolt's one pin goes critical: 84 shard pops + 65 jolt pops, the front climbs the widening bouquet so his pop rate rises to the end.
- Seeds Bolt 354, Mochi 0. Bolt picked from 2,500 for: all 150 pop, the last one exactly on 12.000 s (bar-20 downbeat), one lead change at 5-7 s, a Bolt pop in the first 0.13 s, pops/s still high in the last second.

## Layout (side safe zone)
- Rooms x 118-494 (Mochi) and 526-902 (Bolt); ceiling y 372, floor 1196. Labels SPACED OUT / PACKED TIGHT above. Caption 108-907.
- HUD under the floor: rainbow fill bar with a CLEAR tick at the end, "POPPED", "n/150" (gold = leader) at y 1342.
- Until the lead change: giant counts (132 px) in both rooms, a "+1" pop on every Mochi pin, a big "×2" each time Bolt's count doubles (2, 4 … 64), small "×2" marks on his first-generation pops.
- Pop look (no white): the 2 shard streaks, a thin coloured ring, 7 snap ticks; 8 rubber bits per pop flutter down (drag, terminal ~225 px/s) and settle as a rainbow carpet on the floor. Popped strings fall (Mochi) or hang from the knot (Bolt's tassel).

## Sound (music first)
- **Vivaldi, "L'Inverno" (Winter), Op. 8 No. 4, I. Allegro non molto** (1725; d. 1741, PD). Not on the used/banned lists; not kid-coded.
- Notes from Mutopia #351 (`<SOUNDFONTS_DIR>\scores\vivaldi_winter\winter-mids\winter-score.mid`, Mutopia-2010/02/08-351; SOURCE_mutopia_351.txt there). The engraving is CC BY-SA 3.0; only the PD composition's pitches and rhythms are read, into our own arrangement.
- One steady tempo: quarter = 0.5 s, bar = 2 s. Cut: bars 11-13 at 0-6 s (the build, then the solo violin's arpeggios take off at 2 s), bars 17-19 at 6-12 s (the arpeggios an octave up, then the C7(b9) bar), our F-major (Picardy) arrival on the bar-20 downbeat = 12.0 s = CLEAR.
- Visual sync: Mochi's pins pop on the 8ths (16ths after 6.0 s), every chain pop lands on a 16th.
- Arrangement (lib/orchestra): solo violin; violin I/II on strings, viola, cello + contrabass an octave down (all from the score); a C pedal on pizz + contrabass 8ths where the tutti rests (bars 12-19); timpani on the downbeats from 2 s; horn C pedal; choir from 6 s; string tremolo + timpani roll into 12 s; a timpani hit on the lead change; F-major cadence (strings, brass, tuba, choir, harp run, timpani, boom, soft crash).
- SFX (tonal, no noise): a soft balloon "pok" per pop: sine body with a quick downward glide (decay 30 ms), 2nd harmonic, 150 Hz thump, a small rubbery snap (3.1/4.7 kHz, 2.5/1.5 ms). Pitched to the current harmony (C5-D6, higher rows higher), density-scaled 0.27/(dens/1.5)^0.42. Two soft glass bells on the lead change.
- `master(peak_db=None)`; last 0.5 s digital silence.

## Timeline (seeds M 0 / B 354, clip 15.20 s = 912 frames)
- Sim starts at -5 s (Mochi has been pinning); Bolt's single pin pops his bottom-tip balloon at -1.25 s.
- 0.0: Mochi 26 vs Bolt 5, a Mochi pin pop on frame 0, Bolt's next pop at 0.125. Counts M/B: 0.5 s 29/9, 1 s 31/10, 2 s 36/17, 4 s 46/36, 5 s 53/46.
- **LEAD CHANGE 5.75 s** (57 vs 59); Mochi pins on 16ths from 6.0 s. 8 s 78/89, 10 s 98/122, 11 s 108/141.
- **CLEAR 12.000 s** = Bolt's last pop = bar-20 downbeat = the F-major cadence. Mochi stops at 118/150 (**32 LEFT**, her two right columns).
- PACKED TIGHT WINS! 12.35, 32 LEFT 12.9, faces to 14.6, dissolve 14.6-15.2 into frame 0.
- Pops per second (B+M, s 0-11): 10 10 15 15 17 20 23 24 27 27 27 23.

## Checks (encoded `output/balloon_chain_v1_9x16.mp4`)
- h264 yuv420p 1080x1920 60 fps, 15.20 s. -14.01 LUFS, peak -5.7 dBFS, last 0.5 s -240 dB.
- RMS/s: -21.2 -20.4 -18.3 -18.8 -18.8 -16.2 -16.3 -16.8 -16.3 -15.8 -15.6 -15.2 -14.0 -15.8 -41.1 (last = the silent loop tail). Cadence quarter-seconds -13.8 vs body ~-16.3 (+2.5 dB).
- flash_check PASS (0 flashes, mean lum 0.017).
- Loop seam: pre-encode (PNG frame 911 vs 0) mean delta 0.53, same as adjacent frames (0.5-0.7). check_clip's post-encode figure reads 1.12: the first frame is a fresh keyframe, the last one sits at the end of a GOP, and the 300 detailed balloons make that compression difference large. Not a visible cut.
- check_clip: events/5 s 126 / 177 / 51 (finale); 352 note events, 22 distinct.
- Frames read from the encoded file at 0, 0.5, 1, 2, 5.77, 10, 12.02, 13.5, 15.18 s, plus 1:1 crops at 0.5 s (Mochi's pins) and 11.5 s (Bolt's last balloons).

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/balloon_chain.py --still --frame 0,30,60,120 --label x`
- `NF_SCALE=1.0 python scenes/balloon_chain.py --label v1` (one process, x264 `-threads 2`)
- `python scenes/balloon_chain.py --report` / `--audio-only` / `--search A B` (Bolt seeds that clear)
- Sim knobs via env (BC_PJ, BC_F0/BC_F1, BC_HK, BC_REACH, BC_MJ, BC_T0) only for exploration; the defaults are the shipped values.

## Doubts
- Honest geometry: in a flat pack the chain grows with its front (about t², +1 row per fuse), not a clean ×2 per ring. "POPS 2" is literal per pop (2 shards, drawn as streaks); the big ×2 badges only fire when Bolt's count really doubles (2 … 64), so they get rarer.
- The 0.6-0.9 s fuse (a hit balloon swells and quivers before bursting) is stylised; it is what makes visible chain fronts and lands every pop on the music grid.
- Bolt's last second has fewer pops (12) than the peak (17); Mochi's 16th-note panic keeps the total near the peak (23 vs 27).
- Winter's opening build is tense (dim/dominant harmony) until the F-major arrival. If the owner hears it as too dark, the next try is the same cut with a brighter piece.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch48\balloon_chain.mp4` (Full HD). Owner review: pending.

Owner review (2026-10-23): "the first character ok shooting, but I do not get how the second character is popping" -> v2: make Bolt's single pin and the chain spread obvious.

Owner review (2026-10-23): "remove the hand gesture; when his one pin pops the balloon, two pins pop out in short circular arcs and hit two more, etc., not heavy, no mess" -> v3.

Owner review (2026-10-23): v4 "ok I guess; or the triggered balloons tick (swell/shrink) before exploding" -> v5 adds ticking pulses, then 4K.
