# island_ch9_raft (STRANDED ch9 THE RAFT HOME): 9:16 Short notes

General chapter notes: docs/scenes/island_long.md.

## 9:16 4K fix (owner review 2026-11-08: "the city enlarging and getting small")
- Cause: the hero skyline scale = 260/(260 + DIST - LEADER's distance).
  - It pulses down at tacks.
  - It peaks at 1.00 when Mochi reaches the harbour mouth, then drops to 0.42 as she runs back for Bolt.
  - The Short's time cuts (5.0 / 10.0 s) made it jump, and the lit windows switch on in batches.
  - **The 16:9 (live) has the same pulse** (246 shrinking frames). Reported, not changed.
- Fix (9:16 only; the 16:9 is bit-identical): `city_v(c)`, ONE silhouette (SKYLINE).
  - The scale grows log-linearly in the Short's own time, from the true size seen from the BACK raft (monotone) at the first hero frame (0.131) to the last (0.415).
  - Window-light dusk is linear 0 -> 0.65.
  - Never shrinks: per-frame steps 0.0001-0.0004.
- Picture only: 37.79 s / 2268 f, approved FHD sound copied.
- Not changed (not in the owner's note):
  - The Short's own cuts at 10.0 s (0.067) and 30.3 s (0.039).
  - The hero -> harbour shot change at 22.4 s (0.24). The harbour shot draws its own close-up city.
- Owner 2026-11-09: the 2 remaining 9:16 hard jumps (10.0 s, 30.3 s) are ACCEPTED as is; no smoothing.
