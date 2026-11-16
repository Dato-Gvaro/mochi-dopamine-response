# mb_iceberg_long1: "Mochi & Bolt vs The Iceberg", long video part 1 (16:9, plan 8:36)

- Plan: `docs/PLAN_iceberg_long1.md`. Review files: `<VIDEOS_DIR>\MochiAndBolt\review\mb_iceberg_long1_*` + `_files\` (README, PROGRESS).
- Step 1 (2026-11-14): drawing sheets, `python scenes/mb_iceberg_long1.py --sheet [--out dir]`.
  - `lib/frozen_objects.py`: 49 slot items + 4 trophies + hail gem; `draw(ctx, kind, x, y, s, rot, alpha)`, unit coords; `draw_slot(..., rim)`.
  - `lib/ice_tools.py`: 27 tools; `draw_tool` = sample3's call; working end up; Mochi tool +x, Bolt tool -x.
- Rarity by points: <500 common, <1500 rare, <5000 epic, <50000 legendary, >=50000 mythic.

## Lessons (drawing)
- At slot size (66 px), outlines of L*0.8 swallow thin parts (chain links, arrow shafts): use L*0.4-0.5 on small parts.
- Symmetric crevice arcs and pit highlights read as FACES/SMILES (nugget, meteorite): use angular cracks and irregular pits (MFK risk).
- A closed-eye arc reads cute/sleepy; a realistic shut eye is a small dark slit with no lid arc.
- Glow halos over the sky grey out (CLAUDE.md gotcha): keep them narrow and higher alpha.
- Check the tool's near edge against the owner's body (pile driver touched Bolt at DX 98).

## Step 2 (2026-11-14): the real scene, chapters 1-5 (test 0:00-2:25.8)
- **Structure.** `WAVES` (a tool pair each) grouped into `CHAPTERS` (an ice form each). Ch 1 = sample3 L1-L3 numbers verbatim (car -> headphones, chest -> sneakers; same seeds, same ch-1 timing 0:00-0:18.6). The file imports sample3's frozen PURE helpers (`s3.voronoi`, `s3.sfx_*`, `s3.draw_frost` ...); sample3 stays untouched.
- **Forms.** `cube` (sample3), `block` (Voronoi, several items), `icicles` (Voronoi ledge + 10 sliced icicles; ledge bottom edges split at the root spans so roots attach by TAGS), `shell` (the car mound: CAR_TOP profile + toothed bottom fringe, 108 cells, `carcell` = centroid inside the car body), `slab` (`grid_cells`: brick partition with split, tagged top/bottom edges, then rotated by `tilt`; reusable for the igloo bricks).
- **Items.** `Ice.items` [kind, lx, ly, s, core]. Freed when all core cells are gone; locked while >2 live non-core cells border the core. Any disconnected piece falls as ONE group body; an item inside it is `carried` and pops out where the piece lands (`shatter` reveal). `final` items (ledge pearls + ring) are freed only by the ledge split.
- **Phases.** `ice.phases` (generalised `boss["split"]`): `roof` (car, at 60% HP: crack climbs 2 s, the roof group drops as one slab) and `ledge_split` (icicles gone + ledge <= 90%: crack 1.6 s, two halves fall). The characters keep working during the crack and DODGE out from under 0.8 s before the drop (`sim.dodges`).
- **Trophy.** Car freed when car-cell HP <= 22% after the roof phase: the rest bursts, the car sits 1.25 s with "+10,000", then flies to HUD trophy slot 1. Points split by each one's share of the boss HP removed.
- **Score fairness.** A leftover that falls off on its own (tipped slab, burst block, ledge halves, roof slab) is credited by share of the work on that ice (`remove(..., split=True)`), not finisher-takes-all. Without it the race swung 30-40% on small damage changes.
- **Inventory.** 2x2 -> 2x3 at ch 2 (BAG +2) -> 2x4 at ch 3 (the grid moves up to y 330) -> full page flips to a new page (slides out, tab squares under the grid). Rarity rim from `fo.RARITY`. HP bar x 360-1060, trophy row x 1080-1328.
- **Sky.** Act 2 (ch 5) dissolves day -> sunset over 1.6 s, one direction, with a low sun disc.
- **Audio.** One hit grid G = 0.180 s for the whole video: every bed's beat = 4G (`PIECE_TEMPO`: prelude x1.30, canon x1.434, gymnopedie x1.188). Beds: prelude (ch 1-3), canon (boss), gymnopedie (lake), 1.5 s crossfades on beat lines. Cracks are pitched to the arpeggio (prelude) or a chord tone sounding at that tick. New SFX: `tunk` (hot ball sinking), `shave` (chainsaw, granular, no motor drone), `trophy` (glass-harp chord + low swell).
- **Chains (owner rule 2026-11-14).** `Chain`: Verlet points, anchor pinned and interpolated per substep (4 x 14 constraint passes), heavy load (mass 30), load-vs-polygon collision with restitution 0.12. `draw_chain_rig` draws the SAME parts as `ice_tools._wreckingball` along the simulated points (links alternate oval/bar along their own segment; the hook and the ball turn with their end segments). `--chaintest`: Bolt pulls the floating block back (ball lags, chain trails), then swings it forward with the ball: strike 615 px/s, chain bows 29 px and goes 5% slack after the hit. Ch 8 will store link positions per frame in simulate() the same way.

## Lessons (step 2)
- Tune damage against the MEASURED ch-1 pace (sample3: 3.5 cells/s). My first damage numbers ran the chapters at 7 cells/s (ch 2 in 12 s).
- Poisson seeding silently under-fills big forms (the car got 57 of 115 cells): print the cell count; raise `tries`, lower `dmin`.
- Peeks: mark one when ANY cell over the item's footprint goes (what the viewer sees), not when a core cell goes. The core rule left 11-16 s "nothing new" stretches that weren't real.
- Tools wander away from items: the "dig toward what shows" targeting pull (stronger once a peek happened) fixed the boss and lake openings.
- Group bodies: ink only their OUTER edges (an edge shared by two pieces is a seam) or they read as a wire mesh; on landing they break into their own cells, not into triangles (triangles made a "barbed-wire" band).
- A wrecking-ball test driven by a fast jerk whips the ball over its own pulley. Drive it like a crane operator: pull back, then swing with it (release time found by a numeric search).
- 4K: nothing here calls `identity_matrix()` except `fo.draw` with alpha < 1 (paint only, safe). Check the ol_light_race3 paint_parts trap if a parts painter is ever added.

## Numbers: FHD test (2026-11-14), `review\mb_iceberg_long1_test.mp4`
- 145.80 s, 8748 frames, h264 High yuv420p 1920x1080 60 fps, AAC 48k. -14.05 LUFS, TP -4.66 dBTP. Event->onset lag 0 ms (660 hit/snap/click events). flash_check PASS (23 flashes, worst 2/s at 48.7 s = the icicle ledge sliding in). freezedetect: none >= 0.5 s.
- Audio gap: SFX -14.4 / music -23.4 LUFS (9.0 dB integrated, 10.9 dB P90 vs median). 2364 SFX events.
- Chapters: 0:00 cubes 18.6 s | 0:19 big block 28.6 s | 0:48 icicles 19.6 s | 1:08 boss car 37.3 s (108 cells) | 1:47 lake 35.2 s. Hits/s climb in every chapter (boss 6.6 -> 24.4). Longest gap between NEW events 7.9 s. 13 lead changes; Mochi +17.6% at 2:25.8.
- Times: `--plan` ~2 s, FAST still ~2 s each, FHD render ~15 min (~6x real time; heavier than the plan's 3.5x estimate, so the full 8 min FHD is ~50-60 min; render in chunks).

## Open (for step 3)
- Pace: honest chapters run shorter than the plan (test 2:26 vs 2:48), so the full video projects to ~7:30. It needs >= 8:00 for mid-rolls: add honest rungs (more icicles, a 5th slab, more igloo bricks), never more HP.
- The race: heat-favoured act 2 (igloo, waterfall) would widen Mochi's lead. Re-balance so the plan's ~4:40 Bolt lead (wrecking ball) and the < 5% finish hold.
- The wrecking ball in ch 8: the wall is full-width and above the tools, so the pendulum strikes protrusions or lower wall bands from the side (`--chaintest` geometry). The pile driver drawing has no cable; if one is added, it uses `Chain` too.


## Step 3 (2026-11-14): the full video, chapters 1-13 (owner: "make more length")
- **Length = honest rungs only.** Ch 3 got 13 icicles on a 1440 ledge (was 10 / 1120); ch 2 a third block (C, the laptop); ch 5 a fifth slab (the snowmobile). New chapters' tools were calibrated to the established pace (ch 1-5 run ~3-3.5 cells/s; the first draft of ch 6-12 ran 4.2-5.2). No HP was raised anywhere.
- **New forms.** `make_igloo` (`brick_cells`: per-row extents, staggered bricks, tagged split edges; bricks pop out whole; the dome group drops), `make_falls` (Voronoi in a y-squashed space, then unsquashed: vertical columns; melted gaps pour water `draw_flows` + a droplet trickle), `make_wall` (body + 3 hanging drapes; thirds + centre drape drop), `make_hail` (4-5 cells, cube logic, onion rings; coin/gem POPS = points only, never a slot), the cave = `make_icicles` with spec data (16 stalactites, 210 ledge, meteorite in the split), `make_glacier` (5 bands, deeper = older, year tags, front + side calve), `make_berg2` (1560 x 690, ~294 cells, calving 1 + 2, the crown, the ship lower in the hull band).
- **Generic phases / trophies.** `_drop_phase(grp, at, dur, label, dodge, switch)`; `_set_trophy(kind, s, tx, ty, poly)` (+ `_set_parts` for honest "pk" peeks of trophy parts). `switch=True` hands the SAME ice to the next wave (the SUN DRILL combo).
- **The wrecking ball (ch 8)** is a simulated `Chain` stepped every frame in `simulate()`; the points are stored per frame (`fr["chain"]`) and drawn with `draw_chain_rig`. Geometry the pendulum can honestly reach: the wall hangs ABOVE the tools, and a pendulum cannot rise above its pivot (search: 2 marginal hits of 132), so the wall has 3 drapes with 350 px gaps; the block floats at the top of a gap and the ball swings sideways into a drape's face. Controller = a crane operator's pump: approach the pulled-back spot, wait for the ball's far swing, swing forward WITH it. Hits are whatever the physics says (6 per boss, 400-660 px/s); damage radius grows with impact speed. Mochi's heat avoids the drapes (they are the ball's).
- **Chain fixes found on the way:** (1) the impact speed must be read BEFORE the push-out, or impacts are silently absorbed (hits went 4 -> 10); (2) link constraints must be ONE-SIDED (only pull): two-sided links act like rods, and a slack chain pushed the ball up and jammed it under the wall for 0.3 s.
- **Score race.** Leftovers split by share (step 2); the SUN DRILL's break counts 50/50 (it is both tools locked together); material bias by chapter (snow + waterfall favour heat, the wall favours the ball). Tuned greedily in chapter order with `output/tmp/iceberg_long1/tune_race*.py` (a later chapter cannot change an earlier one). Measure the finish AFTER the last trophy lands (my first tuner read it at the finale start, before the ship's 100,000, and looked insensitive).
- **Finale (ch 13, 22 s).** `draw_collection`: every item ticks into a 10-column grid by rarity (0.105 s each, rising clicks), the 4 trophies, running totals, then FINAL SCORE + winner; `draw_panorama`: zoom out to the TIP (90% under water, a dark shape inside), the berg starts to turn over, "PART 2".
- **Chunked render.** `--chunks 1,2,..` writes `output/long1_chunks/<label>/chNN.mp4` (+ a frame-range json); `--assemble [--deliver path]` concats them (re-checks every range against the current sim: a changed timeline refuses to assemble) and muxes the soundtrack built once for the whole timeline. Re-render one chapter = re-run its chunk + assemble.

## Lessons (step 3)
- A pendulum cannot hit anything above its pivot; design the target geometry for the physics, don't script the hit.
- Read collision impact speed before position correction; rope/chain links must only pull.
- The sim is chaotic: any upstream change re-rolls everything downstream (items, race). Tune in chapter order and freeze earlier chapters.
- Peek detection must be geometric (cell polygon vs item circle); centroid distance missed edge exposures.
- New visible beats that ARE new should be marked (block bursts, the water runs again, a new glacier layer reached, trophy parts); repeated strikes are not.

## Numbers: full FHD (2026-11-14), `review\mb_iceberg_long1_full.mp4`
- 516.72 s, 31,003 frames, h264 High, yuv420p, 60 fps. -14.05 LUFS, true peak -3.53 dBTP. Onset lag 0 ms (2,256 events). flash PASS (51 flashes, worst 2/s). freezedetect: finale holds only (longest 2.07 s).
- Chapters: 0:00 / 0:19 / 0:56 / 1:21 / 2:02 / 2:40 / 3:10 / 3:46 / 4:42 / 5:16 / 5:56 / 6:51 / 8:14 (collection).
- Race: 17 lead changes; Bolt leads 4:07-4:43; final Mochi 192,849 vs Bolt 192,406 (0.2%), decided by the ship at 8:15.
- Wrecking ball: 6 physics strikes, 400-660 px/s. Chain test: strikes at 709 / 673 px/s; bow up to 35 px; slack up to 7.5%.
- Render: 4 chunk processes, 16 min of chunks + 3 min of assembly (audio + concat + mux); the berg chunk is the bottleneck.
- **Open:** 11 stretches of 9-13.5 s without a NEW mark (mostly mid-boss); finale static holds of up to 2 s; Korobeiniki and Greensleeves beds not built (the existing bgm pieces are reused).

## Step 4 (2026-11-15): owner's easy fixes (finds, real chain, round melt)
- **Finds** (`post_finds`, pure post pass: the sim is untouched). Small points-only pops trapped in plain ice: silver coin 100, brass gear 150, gold coin 150 (the hail coin, now drawn as ONE coin so it can't be mistaken for the 500-pt coin stack), old key 200, sapphire gem 250, trilobite 300, ruby 400 (`POP_PTS`, one table for hail + finds: same find = same points). Drawn in `lib/frozen_objects.py` (`FINDS`).
  - Every snapped icicle with nothing else inside holds one (its widest slice; pops where the icicle shatters). Elsewhere a find goes in a cell that breaks at the right time so no stretch runs > `FIND_GAP` 4.2 s without a NEW event. Whoever breaks the cell gets it. Never in split / burst / phase-drop cells or item cores.
  - Shown faintly THROUGH the ice (alpha 0.34 + a soft hint) so there is something to dig for; pops with "+N", ding + tinkle.
  - Race neutrality: the trailing side's cells are preferred, then the kind (from the chapter's pool) is picked to keep the running find-points difference near 0; where it runs > 400 the trailing side gets an extra find. Result: 73 finds, M 8,850 / B 8,800.
- **Chain** (`Chain`): exact, mass-weighted, ONE-SIDED link solve (tridiagonal direct solve of the taut links, 3 Newton passes, a link that would push drops out), alternating with the ball's push-out from the ice, then a follow-the-leader clean-up from the pinned anchor. Max link stretch 0.000% in the sim and in `--chaintest` (was 103% in ch 8: the ball jammed in the centre drape while the block flew off, then teleported out).
  - Rig controller: anti-sway "settle" before each strike (the block follows the ball until the swing dies), then a route AROUND the ice (down under the drapes, across, up into the gap) with legs limited to 0.5 g; free moves/dodges speed- and accel-limited (420 px/s, 0.45 g); in a dodge the rig LEADS Bolt; Bolt keeps clear of the ball.
  - Numbers: 7 strikes 240-770 px/s; swing <= 47 deg; slack <= 10%; ball-to-body clearance >= 4 px. Ch 8 runs 64.6 s (was 54.7).
  - Pile driver has no cable (rails + ram); the plasma/lance/hydraulic hose stubs are short rigid curves on floating tools (left as drawn).
- **Round melt** (lake slabs, `lake_field`): the ice is drawn from a field = base cells (alive + heat-melted) minus a metaball "melt cavity" that grows round from where the heat touched each cell (radius ~ mf^0.6), blurred (sigma 6 px) so no hair-thin slivers survive; marching squares -> loops -> the usual fill/texture/ink. Wet rim (blue film + gloss) on the melted edges; per melting cell one stable column grows a thin icicle from the hole's ceiling (or the slab's lower edge) with a drop that swells, falls and fades.

## Lessons (step 4)
- Mass-weighted Gauss-Seidel + a follow-the-leader pass injects energy (the FTL correction turns into velocity): the ball flew up and the chain went 47% slack. A direct tridiagonal solve of the taut links leaves no residual for FTL to fix.
- A chain sim is only as calm as its driver: a smoothstep move over a short leg is > 1 g at the ends and flings the ball over the pulley. Limit leg acceleration (<= 0.5 g) and settle the swing before the next move.
- Never drag the ball THROUGH ice: plan the anchor route so the hanging ball's straight path is clear (`wb_clear`), else go under.
- An arch of identical icicles reads as a mouth with fangs (face risk): one thin icicle per melting cell, varied lengths, >= 30 px apart.
- Additions that should not re-roll a chaotic sim go in a post pass that only READS the sim (finds); record extra facts (`c.who`, `b["cells"]`) without touching any sim decision or RNG.

## Numbers: full FHD v2 (2026-11-15)
- Plan: 524.65 s (8:44.6). Chapters: 0:00 / 0:19 / 0:56 / 1:21 / 2:02 / 2:40 / 3:10 / 3:46 / 4:51 / 5:24 / 6:04 / 6:59 / 8:23 (collection).
- Longest gap between NEW events 5.4 s (finale); none > 8 s (was 11 stretches of 9-13.5 s).
- Race: 29 lead changes; Bolt leads 7:47-8:23; the ship flips it: Mochi 203,448 vs Bolt 199,457 (2.0%).

## 4K ship (2026-11-15, approved v2)
- `NF_SCALE=2.0 ... --label 4k --chunks` (3 processes, 50 min; ch12 the bottleneck) + `--assemble` (3 min) -> `reserve\iceberg_long1_4k\` (mp4, UPLOAD.md, CHAPTERS.txt, thumbs A ship / B car / C mammoth).
- 3840x2160, 31,479 f, 524.65 s, -14.05 LUFS, peak -5.97 dBFS, flash PASS (worst 2/s). 4K vs FHD still 0.42-0.55: no scale trap. Chapters (floor): 0:00 0:19 0:55 1:21 2:01 2:39 3:09 3:45 4:50 5:24 6:04 6:59 8:22.

## Audio fix (2026-11-16): heat hiss too loud/harsh (owner)
- v2 (superseded): `sizzle_bed` (the continuous hiss under all 13 heat tools) was made soft (bandpass 1.4-4.2 kHz + lowpass 4.2 kHz, crackle lowpass 4.5 kHz, attack 0.12 s) and -6.5 dB: the stem goes -23.6 -> -35.4 LUFS (-11.9 dB), its 2-8 kHz energy -11.4 dB. The music bed stays referenced to the LEGACY sizzle, so music vs the other SFX is unchanged. 
- Re-muxed only (`-c:v copy`): `uploaded\2026-11-16\iceberg_long1_4k\iceberg_long1_4k_v2audio.mp4` + `archive\reviewed_2026-11-15\mb_iceberg_long1_full_v2audio.mp4` (FHD); video md5 identical. -14.02 LUFS, true peak -5.1 dBTP. Old wav kept as `output\mb_iceberg_long1_4k_16x9_audio_v1hiss.wav`.
- Lesson: a continuous noise bed reads far louder than its share of band energy (it was only ~-5 dB of the mix's 2-8 kHz in heat passages, yet the owner singled it out). Keep noise beds low-passed (< ~4.5 kHz) and >= 12 dB under the hits; measure the bed as its own stem, not in the mix.
- v3 (owner after the A/B: "too much hiss, much lower, less rough"): `HEAT_NOISE` = v1 | v2 | v3 picks the version (v1 and v2 rebuild bit-for-bit, max diff 1.2e-7). In v3 the sizzle is noise at 0.6-2.5 kHz with a 4th-order low-pass at 2.7 kHz, no crackle, a 0.25 s attack and `V3_SIZZLE_DB` -14.1, so the stem is -23.6 -> -45.6 LUFS (-22 dB). The `tss` voice is 1.2-3.5 kHz at -10 dB, and the `tunk` noise click is -8 dB with a 2 kHz low-pass. -> `iceberg_long1_4k_v3audio.mp4` (+ FHD `_full_v3audio`), video md5 identical, -14.02 LUFS, true peak -5.1 dBTP.
- What made the hiss: in 2-8 kHz the sizzle hiss was the loudest NOISE source (heat gun window -30.0 dB vs tss -44, crackle -47, slush -47). Ice cracks (-30 to -33) are bright too, but they are the hits. Rank noise sources by rendering each stem separately before touching anything.
