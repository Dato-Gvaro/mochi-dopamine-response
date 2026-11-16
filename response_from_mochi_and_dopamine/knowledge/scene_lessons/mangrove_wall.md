# mangrove_wall: sea wall or mangroves, whose village floods? (BRIEF_mochi_1113 clip 3, 2026-11-13)

- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\new_1113\mangrove_wall\mangrove_wall.mp4` (FHD, 12.50 s, label fhd). The README there has the rung table, physics sources, numbers, titles and pin.
- Built on the sandcastle_wave look (lanes, HUD, caption, tonal SFX, mastering). The water/flood model is new and analytic, so there is no sim cache.
- Mochi = 300 m mangrove belt (top), Bolt = vertical 1.2 m concrete wall (bottom). Rounds double the wave height (20/40/80/160 cm) and the wave count (2/2/4/8). Bar = 2.0 s.

## Model
- Waves are sech² humps at c = 520 px/s, crest 0.6 H.
- Mochi: H × 0.6 per 100 px of belt (McIvor et al. 2012: 13-66% / 100 m).
- Bolt: image-method reflection R = 0.9 → standing crest 1.14 H. It overtops only when 1.14 H > 1.2 m (round 4).
- Flood depth: EurOtop 2018 vertical wall q = 0.05·exp(−2.78 Rc/H)·√(gH³), × 1 h / 100 m → 1.42 m. It is spread over round 4's 8 waves.
- Homes are stilt houses; sills 0.30-1.28 m set the flood order.
- 70 px/m vertical. The village is 0.5 m above SWL.

## Lessons
- `toon.watcher_pose` squashes (laugh/cheer/wince). Force `p["sx"] = p["sy"] = 1.0` for the no-shape-change rule.
- No pulse/pop anim may start exactly at frame 0 when the loop dissolves from a pre-roll (the divider pulse broke the seam: 1.04 → fixed 0.64).
- epic_hits("boom") returns a wave_part without "notes": guard the OFFSET shift loop.
- Shared scratchpad between parallel builders: keep the lock wrapper in a per-builder path (`output/tmp/builderC/`) and wrap the script body in `{ }`.

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/mangrove_wall.py --still --frame 0,168,300,450,648`
- `NF_SCALE=1.0 python scenes/mangrove_wall.py --label fhd` (render ~3 min)
- `--report` prints the per-round EurOtop q, belt numbers and flood times.

## Outcome
- (fill after upload)
