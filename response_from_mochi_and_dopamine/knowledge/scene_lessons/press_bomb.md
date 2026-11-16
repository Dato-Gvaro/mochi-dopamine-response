# press_bomb — press franchise episode: Bolt swaps his hammer for a BOMB (batch66, 2026-11-01)

- Brief: coordinator task 2026-11-01 (weekly press franchise; one nameable change per episode).
- New file `scenes/press_bomb.py`, copied from press_shaker (itself from press_split4). The older press scenes, longform_atom, lib/ and tools/ are untouched. The bomb look (draw_bomb, the ring/fireball/smoke FX, the "BOOM!" sticker) and the bomb SFX recipe (synth_fuse → synth_explosion + thunk; bounce + pok on landing) were copied from longform_atom's `--crushers`.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch66\press_bomb.mp4` (Full HD 9:16, label b66).
- Caption (baked): "Every ball hit ~HARD~ splits into 3" / "~Press~ or ~BOMB~:" / "whose jar ~OVERFLOWS~ first?".

## THE ONE CHANGE
- Bolt's hammer becomes a cartoon fuse bomb, dropped by a claw on a rail into an OPEN jar (no lid; the side walls stop at the rim). Mochi's hydraulic press is the franchise model and look.
- Same rule for both: a ball hit hard splits into 3 at 0.66 r (equal volume). Same jars, same MAX line (y 560).

## Bomb physics (`Chamber.boom`, `ring_hits`, `move_bomb`, `drop_lost`)
- Cycle: the claw lets go → the bomb falls (5000 px/s²) and lands on the floor-connected pile (it ignores balls in flight) → it digs in `--dive` 40 px while the fuse burns `--fuse` 0.45 s → BOOM → `--gap` 0.55 s → the next one. 1 BOOM every ~1.45 s.
- BOOM: a shockwave ring runs out at 1500 px/s. Each ball gets ONE outward kick K·exp(−d/L) when the ring reaches it (d = surface distance from the bomb; K `--kick` 2400 px/s, L `--kl` 120 px). It splits only if the kick beats V_BREAK(gen) = 0.62 m/s × 1.155^gen (press_shaker's rule: smaller pieces need harder hits; dust never splits). Children inherit the kick.
- A ball whose centre crosses the rim line outside the walls is LOST: removed from the jar's count, then drawn on its real launch velocity, fading as it falls.
- Pile physics changes in the bomb jar only (the press jar keeps the franchise values):
  - Kicked balls skip the speed caps for 0.4 s (cap 4200 px/s). Contact damping still applies to them. Skipping damping too (`--dampfree`) made a permanent snow globe.
  - An asymmetric cap: a blast-loosened pile can fall back at g (+y up to 1600 px/s), while sideways and upward speeds keep the franchise's 260 cap. With the 260 cap on falling, the blasted pile floated as foam for seconds. With no cap at all the dust pile boiled (median 374 px/s).
- Overflow for the bomb jar: the 3 % top of the FLOOR-CONNECTED balls (the spray doesn't count) must sit above MAX for 8 frames, measured ≥ 0.6 s after a BOOM. A momentarily puffed-up pile is not an overflow.
- Press tempo is quicker than the series (P_DOWN 300, P_LIFT 210, P_PER0 2.9, P_PER_MIN 2.0, P_PAUSE 0.20) so the race fits ~20 s. Waves are still exact ×3: 3 / 9 / … / 6,561; it overflows at sim 19.02 s.
- Look: airborne balls (not floor-connected) are drawn at 50 % opacity, so the pile's surface reads against the spray.

## Honest search (the race is near a knife edge)
- Bolt-only sims (~10 s each; the chambers are independent; the press overflows at sim 19.02 s). Grid K {1600, 2000, 2400} × L {120, 150, 190} × dive {40, 120, 220}, seed 1, final model: **the press wins 17 of 27, the bomb 10** (bomb overflows at 15.4–18.9 s).
- The earlier models flipped results (the 260-cap foam model: the press won 15/19, but Bolt's "overflow" there was floating foam). Every model change is logged above.
- Picked K 2400, L 120, dive 40: a press win where Bolt's settled pile never crosses MAX (closest 16 px under, at sim ~19 s). Several press-win settings show Bolt's pile poking above MAX for a few frames, which would read as fake. Seeds 0, 2, 3, 4 with this bomb: the press wins every time (Bolt lost 95–289).
- Counterfactual `--lid` (bomb jar closed, nothing lost): Bolt still has not overflowed by 22 s. **So the losses are real but NOT what decides it.** Each blast only splits the balls near the bomb, while the press splits every ball every stroke. Bolt lost 93 by the finish (~2 % of his balls).

## Seed 1 (clip time = sim − 0.6 s)
- 0.0 s: the bomb sits fizzing on Bolt's one ball; the press plate is coming down. First BOOM at 0.18 s (1 → 3); the press's first squeeze lands ~0.3 s.
- Bolt leads from 3.3 s (21 vs 9). BOOMs at 0.18, 1.73, 3.32, 4.87, 6.42, 7.92, 9.40, 10.83, 12.30, 13.75, 15.18, 16.58, 17.97 s.
- Biggest blast: +1,090 at 12.3 s (1,669 → 2,753). Worst throws: 47 lost (17.97 s), 29 (16.58 s), 20 (13.75 s).
- Counts M/B: 6 s 27/237 · 10 s 243/1,164 · 14 s 729/3,489 · 16 s 2,187/4,077 · 17.4 s 2,187/4,584.
- LEAD CHANGE at 17.53 s (the press's last wave, 2,187 → 6,561). OVERFLOW at 18.42 s: the press 6,561 vs Bolt 5,144, Bolt 93 lost so far. PRESS WINS at 18.82 s (the plate snaps, the pile erupts). Dissolve 19.63 → 20.23 s.
- Banners: "BOLT LOST N OVER THE TOP!" for up to the two biggest throws (≥ 10 lost) clear of the other banners and the finale. In seed 1 only one qualifies: "BOLT LOST 20" at 14.5 s. Per BOOM: "+N IN ONE BLAST!" (N = 2 × splits). A persistent "LOST OVER THE TOP: N" sits in Bolt's jar.

## Sound
- Für Elise note per split group (≤ 1 per 60 ms), franchise crunch per split, press thunk/clank/hiss, A-minor cadence on the overflow, glass + thunk on the snap, riser into the press's last stroke.
- Bomb: latch click on release, bounce + pok on landing, fuse sizzle over the fuse, explosion + thunk on BOOM.
- post_fade: the last 0.5 s is silent (loop seam).

## Args
- `--seed` 1, `--kick` 2400, `--kl` 120, `--dive` 40, `--fuse` 0.45, `--gap` 0.55, `--v0` 0.62, `--grow` 1.155, `--vdense` 1600; press `--pdown --per0 --permin --plift`; `--only bolt|mochi` (one chamber, tuning), `--lid` (counterfactual), `--dampfree`, `--resim`, `--report`, `--verbose`, `--still --frame 0s,12.3s,...`, `--reuse`, `--label`. The sim is cached in `output/press_bomb_sim_<params>.pkl`; the full sim takes about 1 min.

## Checks (encoded Full HD, b66; render ~25 min at 2 encoder threads)
- h264 yuv420p 1080x1920 @ 60 fps, 1214 frames = 20.23 s. Muxed −14.05 LUFS, peak −5.89 dBFS, last 0.5 s −90 dBFS (silent).
- flash_check PASS (0 flashes, mean luminance 0.028). Seam mean |delta| 0.74.
- Notes 60 (9 distinct, top 20 %); events per 5 s 9 / 10 / 20 / 21 (climbing). RMS per 5 s −16.2 / −16.7 / −15.5 / −15.1.
- Onsets: all 20 detected onsets sit on sim events: notes/BOOMs, the bomb landings (0.45 s before each BOOM), the press release hiss, and the explosion's debris tail (~0.95 s after each BOOM).
- Frames read from the mp4: 0, 0.2, 3.4, 12.45 (1:1 crop of Bolt's jar), 14.6, 18.45, 20.2, and the seam pair (first/last frame). Fast stills: 0.45, 12.65, 13.3, 17.6, 18.45, 18.95, 19.9.
- Side safe zone: the press_split4 stage transform (walls 110–905 px = 0.10–0.84 w); the claw rail and the tags are inside Bolt's jar. Lost balls and the spray fly wider (decoration).
- Nits: the bomb jar is always busy with spray; Bolt's last BOOM's sticker sits beside OVERFLOW! for ~0.3 s; the losses (93) are real but not decisive (see the `--lid` test).

## Outcome
- (fill after upload)

## v2 (2026-11-01, owner: "let bomb dive into balls deeper and then explode")
- `--v2` (v1 reproduces without it; sim cache tag `_v2f<frac>`). On landing `dive_to = land + min(--dive 330, --divefrac 0.6 × (FLOOR − BM_R − 2 − land))`; constant-speed dive arriving DIVE_REST 0.10 s before the BOOM (kinematic, scripted like longform_atom's BM_DIVE; the disc pushes balls out each PBD iteration, `apply_machine`). Drawn BEHIND the balls while buried (`bomb_buried`), with a faint rim + the fuse spark on top (`fuse_tip`, `draw_spark`, refactored out of `draw_bomb`, v1 pixels unchanged).
- Seed 1 result (`press_bomb_b66v2`): PRESS still wins at sim 19.02 (clip 18.42), 6,561 vs 5,190; Bolt led clip 3.35-17.57; lost 285 by the overflow (356 by the end) vs v1 93. Biggest blast +1,772 at clip 10.87. Loss banners 29 (11.62) / 27 (14.75).
- **Deep blasts lift the whole overburden**: more balls thrown out, airborne share 56 % of frames (v1 35 %). Bolt's floor-connected top flickers above MAX from sim 18.82 (runs of ≤ 4 frames) but never holds 8: photo finish, and at the OVERFLOW frame Bolt's jar LOOKS full too (main risk).
- Depth sweep, Bolt-only to 20.5 s (press fixed at 19.02): 0.6/330 no overflow · 0.6/240 none · 0.5/260 **bomb overflows 18.93** · 0.45/200 none. Knife edge, as v1.
- Checks (Full HD, `review\batch66\press_bomb_v2.mp4`): 1214 frames = 20.23 s, −13.99 LUFS, peak −6.18, last 0.5 s −81 dBFS, flash 0, seam 0.78, notes 53, events/5 s 9/10/16/18.

## v2 (2026-11-01, owner: "let bomb dive into balls deeper and then explode")
- `--v2` (v1 reproduces without it; sim cache tag `_v2f<frac>`). On landing `dive_to = land + min(--dive 330, --divefrac 0.6 × (FLOOR − BM_R − 2 − land))`; constant-speed dive arriving DIVE_REST 0.10 s before the BOOM (kinematic, scripted like longform_atom's BM_DIVE; the disc pushes balls out each PBD iteration, `apply_machine`). Drawn BEHIND the balls while buried (`bomb_buried`), with a faint rim + the fuse spark on top (`fuse_tip`, `draw_spark`, refactored out of `draw_bomb`; v1 pixels unchanged).
- Seed 1 result (label b66v2): PRESS still wins at sim 19.02 (clip 18.42), 6,561 vs 5,190; Bolt led clip 3.35-17.57; lost 285 by the overflow (356 by the end) vs v1 93. Biggest blast +1,772 at clip 10.87. Loss banners 29 (11.62) / 27 (14.75).
- **Deep blasts lift the whole overburden**: more balls thrown out, airborne share 56 % of frames (v1 35 %). Bolt's floor-connected top flickers above MAX from sim 18.82 (runs of ≤ 4 frames) but never holds 8: photo finish, and at the OVERFLOW frame Bolt's jar LOOKS full too (main risk).
- Depth sweep, Bolt-only to 20.5 s (press fixed at 19.02): 0.6/330 no overflow · 0.6/240 none · 0.5/260 **bomb overflows 18.93** · 0.45/200 none. Knife edge, as v1.
- Checks (Full HD, `review\batch66\press_bomb_v2.mp4`): 1214 frames = 20.23 s, −13.99 LUFS, peak −6.18, last 0.5 s −81 dBFS, flash 0, seam 0.78, notes 53, events/5 s 9/10/16/18.

## v3 (2026-11-01, coordinator: keep the honest photo finish, make it not look rigged)
- `--v3` (implies `--v2`; same sim cache, events json identical to v2). `finish_plan()`: per jar the rule's own top as fill % of MAX, HELD = min over the last HOLD_N 8 frames; Bolt "settling" = any of those frames inside T_CALM of a BOOM or a swing > 20 points. `draw_finish()` from sim 18.1 (clip 17.5): "SETTLED n%" at y 1342 under each jar (winner: "SETTLED 100% · FULL" from f_win), pulsing "STILL SETTLING…" in Bolt's jar at Y_MAX+60, and under the banner "PRESS HELD MAX FIRST" + the touch margin: Bolt's loose pile first crossed MAX at clip 18.22, the press's winning run started at 18.30 (held 8 frames at 18.42; Bolt's best run 3 frames). BOOM! stickers for blasts from 1.6 s before to 1 s after f_win: 0.35 s, ×0.7, at FLOOR−70 (clear of OVERFLOW! / LEAD CHANGE!).
- Deliverable `<VIDEOS_DIR>\MochiAndBolt\review\batch66\press_bomb_v3.mp4` (label b66v3): 1214 frames, −13.99 LUFS, peak −6.18, last 0.5 s −81 dBFS, flash 0, seam 0.80. v2 -> archive/press_bomb_v2.mp4.
- **STAGED 4K** (2026-11-02): `--v3 --label p4k` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-05\3_press_bomb.mp4` (events json byte-identical to b66v3). 2160x3840 h264 yuv420p 60 fps, 1214 frames, -13.99 LUFS, peak -6.18, flash 0, seam 0.68.
