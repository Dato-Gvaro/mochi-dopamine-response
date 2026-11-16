# murmuration5 — a peregrine falcon vs 15,000 starlings; Mochi and Bolt watch (batch29)

Owner review of murmuration4 (2026-10-12): "they look like slow motion. What if they are on the ground watching another predator, not an ugly bird, flying through the birds, and the birds avoid it." New file; imports murmuration2 (flock sim, stoop planner, escape waves, `Ink` look, Vivaldi bed) and murmuration3 (`Layer`, `front_alpha` depth occlusion), both unchanged on disk.

- **Real-time pacing:** m2's module constants are re-tuned at import, not on disk:
  - `V0` 190 -> 235 px/s;
  - 8 short, fast stoops: lead 0.85 -> 0.52 s, falcon peak ~2,700 px/s;
  - strike radius 110 -> 240 and flee force 1000 -> 2200, growing each stoop;
  - clearance 40 px, so nobody is caught (logged: the closest bird is always >= 40 px).
- **The falcon:** an elegant peregrine silhouette with slate wings, a pale body and a thin GOLD rim light from the sunset, plus a dark head with a yellow eye.
  - Wings are open while it glides and tuck back by speed (fully tucked at >= 950 px/s).
  - At stoop speed: a warm speed streak plus 4 motion-blur ghosts.
  - It waits high at the upper left between stoops, using m2's steep-stoop planner: climb over the densest patch, near-vertical stoop, out below, back up the left edge.
  - Birds nearer the camera occlude it (m3 `front_alpha`), so it reads as slicing THROUGH the fold.
- **Watchers:** Mochi and Bolt sit small (r 27) on the knoll at the lower left. They show awe (wow) during each stoop, flinch (squash) at the strike, then a happy hop/cheer when the flock gets away. Bolt reacts 0.07 s later.
- **HUD:** caption `A falcon vs 15,000 starlings | ~Can it catch even ONE?~`, and a counter `stoops: n · caught: 0`. The answer is no.
- **Hook / loop:** the 8th stoop strikes on the LAST frame, so frame 0 (= the sim's end state) is the falcon in the fold with the escape wave lit. m2's 0.75 s rewind loop makes it exact.
- **Music:** murmuration2's bed, unchanged. Vivaldi "Winter" RV 297 I (PD; Mutopia id 351 notes), full strings, timpani, stabs, choir, booms, quarter = 108.
  - Stoops 1-7 land on its stab beats: 2.22, 6.67, 10.0, 13.33, 15.56, 17.78, 20.0. The cadence is at 22.40.
  - The 8th (hook) stoop falls in the silent tail.
- **Render:** `NF_SCALE=1.0 python scenes/murmuration5.py`. Flags: `--still --frame a,b`, `--silent-only`, `--reuse`.
- **Checks (Full HD v1, 2026-10-12):**
  - h264 yuv420p 1080x1920 60 fps, 1518 frames = 25.30 s.
  - Audio: -14.01 LUFS, peak -5.0 dBFS, last 0.5 s -81 dBFS.
  - flash_check: 0 flashes = PASS (mean lum 0.17).
  - Loop seam: last -> first mean delta 1.35, one exact sim step at stoop speed; clip median 0.76, p90 1.13.
  - Closest bird to the falcon: >= 40 px.
- Weak spot: at frame 0 the tucked falcon sits just ABOVE the lit fold, entering it, not inside it. In full stoop it reads as a slim dart.
- **Delivered:** `<VIDEOS_DIR>\batch29\murmuration5.mp4` (Full HD). Owner review: pending.
- Owner review (2026-10-12): moved to Reserve.
