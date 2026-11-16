# ol_country_marbles2 (DopamineEXE, BRIEF_1113b B1) — CODE ONLY, no seed chosen, not rendered
- v2 of `ol_country_marbles` (v1 untouched; flags, text helpers, Csárdás bed, SFX waves and the writer are imported from it read-only).
- Owner (REVIEW_1113): balls drop into a circle; a bottom row of EMPTY circles; each ball that leaves lands in the next slot; can the USA win (no Asian-country pull)?
- File: `scenes/ol_country_marbles2.py`. Review folder (later): `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_country_marbles2\`.

## What changed vs v1
- **Pour entry, mid-action at frame 0.**
  - A hopper (3 lanes, 0.08 s per row) pours the 48 marbles through a door at the top of the ring.
  - The sim pre-roll is 0.5 s, so at frame 0: 16 inside, 5 falling, 27 still to pour. The pour ends at 0.71 s, the door slides shut 0.93-1.11 s, then the hopper lifts away.
  - Pouring marbles are kinematic: they push inside marbles aside, they don't collide with the wall, and they become normal once fully inside. The door is a one-way flap: inside marbles always see a wall there.
  - The thermostat target ramps 450 → 1200 px/s by 1.0 s.
- **Bigger ring**: R 355 (v1 338), centre (508, 740): x 153-863, y 385-1095.
- **Slots replace the roster**:
  - 4 × 12 EMPTY circles at y 1180-1330 (bottom 1350 < 0.71h).
  - Every OUT marble keeps its real exit velocity for 0.30 s, then arcs into the NEXT empty slot (0.48 s), in elimination order: a live ranking. The next free slot is outlined brighter.
  - The last slot is gold with a crown from frame 0 (the end state at frame 0). The winner's flag drops into it at the finale.
- **Close final**: while exactly 2 are left, a "FINAL:  A  vs  B" line shows at y 1134 (from the sim, nothing scripted).
- **HUD moved up**: "N COUNTRIES LEFT" top-left (116, 362); the exits pill top-right (812, 342), with "×2" popping under it.
- **Exit start angle**: `--th0 0` (right side; it reaches the bottom at ~2 s). v1 used -π/2.
- **Physics speed-up (same model)**: the wall collisions are vectorised. A full sim takes ~1 s CPU (seed 1: 0.8 s).
- Unchanged from v1: exits double every 2 s (1→16, Csárdás 3 bars), elastic marbles + gravity 900, spin 0.8 rad/s, exits 1.8 marbles wide, name tags, the big flag reveal + confetti, the Csárdás bed (beat 32 = the last OUT), the SFX set (+ a soft low clack when a marble lands in its slot), the caption, and the 0.6 s dissolve loop.

## The winner: real physics, seed chosen by `find_seed()` (NOT run yet)
- No force favours any marble. Marble i = country i. The seed sets the starting jitter and the drop order (which lane and row each flag pours in).
- `--find lo-hi` simulates each seed with pruning: it aborts the moment the USA is out, or when the last two are not USA + Canada/UK. Pruning only stops the scan early; it never changes a trajectory.
- A seed PASSES when, from the unmodified sim:
  1. winner = USA, runner-up (last OUT) = CANADA or UK;
  2. a visible 1v1: "2 left" (2nd-last OUT) → last OUT is 0.6-3.0 s;
  3. first OUT ≤ 1.6 s, and no OUT during the pre-roll;
  4. OUTs per second never fall period to period (10% tolerance, v1 rule);
  5. last OUT in 10.07-10.97 s (music cadence beat 32 = 10.67 s; the stringendo stays ×0.70-×1.15).
- Odds: USA 1/48 × rival 2/47 ≈ 1/1100, × timing → expect roughly 1 pass per 5,000-15,000 seeds. At ~0.5-1 s CPU per seed with 3 jobs, that is **~20-60 min per hit**. Run it when the laptop is free.
- 2026-11-13: rules 4 and 5 RELAXED (strict rule 4 passed 1/40 seeds). Checked 1-14001, no pass yet; resume `--find 14002-120000 --jobs 2 --want 2` (state in the review PROGRESS.md).
- Smoke (seed 1 only, not a search): first OUT 1.07 s, last 10.87 s, winner AUSTRIA. Left per second: 48 48 42 37 34 27 21 15 14 9 5 1. The USA was the runner-up at 10.68 s.

## Rung table (expected shape; exact numbers come from the chosen seed's `--dry` report)
| clip s | on screen | counter / milestone |
|---|---|---|
| 0.0 | Marbles POURING from the hopper into the big ring (16 in, 5 falling); ONE gold EXIT (labelled, at 3 o'clock); 48 empty slots, gold crown slot; "48 COUNTRIES LEFT", "1 EXIT" | 48 |
| 0.7-1.1 | pour ends, door slides shut, hopper lifts away | 48 |
| ~1.0-1.6 | **first OUT**: name tag, the marble arcs into slot 1 | 47 |
| 2.0 | ×2 → 2 exits (gold flash on the wall, ting, timpani downbeat) | ~42 |
| 4.0 / 6.0 / 8.0 | ×2 → 4 / 8 / 16 exits; the slot grid fills row by row | ~35 / ~25 / ~15 |
| last ~0.6-3 s | **FINAL: USA vs CANADA/UK**: the 1v1 | 2 |
| ~10.1-11.0 | the runner-up goes out into slot 47; exits seal gold; USA flies to the centre → big flag, **USA WINS!**, confetti in its colours; the flag drops into the gold slot; Csárdás D-major return | WINNER |
| +2.6 s | 0.6 s dissolve to frame 0 (loop) | |

- Expected length: last OUT + 3.2 s ≈ **13.3-14.2 s**.

## READY TO RENDER (later pass; TEMP/TMP on D:; lock only for clips)
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
# 1. seed search (CPU-heavy, run when the laptop is free; prints every pass)
python scenes/ol_country_marbles2.py --find 1-60000 --jobs 3 --want 3
# 2. pick the pass with the longest duel inside 0.6-3 s and the steadiest climb; then
python scenes/ol_country_marbles2.py --seed N --dry          # caches output/_cache_ol_country_marbles2_*.pkl; report says "find criteria PASS"
$env:NF_SCALE='1.0'; $env:NF_FAST='1'
python scenes/ol_country_marbles2.py --seed N --still --frame 0,30,70,300,<2-left frame>,<T_WIN frame + 60>,<last frame>
# 3. clips (mkdir output/render.lock ... rmdir)
python scenes/ol_country_marbles2.py --seed N --label fast
Remove-Item Env:NF_FAST
python scenes/ol_country_marbles2.py --seed N --label fhd
python tools/flash_check.py output/ol_country_marbles2_fhd_9x16.mp4
```
- **Stills, what to check:**
  - **f0**: marbles visibly mid-pour in the 3 lanes through the door. The hopper top (y 280) must clear the caption's 2nd line (baseline 258). The door posts sit outside the lanes, so no marble overlaps a post.
  - **f30-70**: no marble pops or overlaps where pouring marbles meet the heap (kinematic push). The door closes cleanly.
  - **f300**: slots filling in reading order; tags don't collide with the counter or pill; flags readable at r 20.
  - **2-left frame**: the "FINAL: USA vs …" line fits between the ring bottom (1095) and the slots (1160).
  - **Finale**: the "USA" name + WINS! sit inside the ring (y ~1000-1060); the gold slot has the USA flag + crown.
  - **Sides**: everything key inside x 108-907. Out-flying marbles may briefly cross it (motion only).
- **Clip checks:** OUT notes on OUT frames; -14 LUFS / tail silent on the muxed mp4; flash_check (the doubling flash is the gold wall, as v1: PASS there); loop seam (frame 0 = mid-pour).
- Then write the review README: the seed, the measured rung table, the titles (US pull, e.g. "48 countries, ONE winner… USA vs CANADA final 🇺🇸 #satisfying #physics #shorts". A flag emoji is fine; nothing political) and the pinned comment.

## Open risks
- **Nothing drawn yet.** The pour visuals (hopper, door, kinematic push) are untested on screen. The first stills may need tweaks to the hopper/door size.
- **The seed search may be slow or sparse.** It is ~1/1100 on the country pair alone. The duel and cadence windows cut it further; budget an hour of CPU.
- **Honesty:** the result is real physics, but the seed is SELECTED for a USA win, like v1's seed was selected for timing. If asked "is it rigged?", the true answer is "the sim isn't steered; we picked a run where the USA won". Keep any pinned comment from claiming randomness.
- **Event rate at the end:** fewer marbles → fewer clacks, as v1. The duel line and the slot fills carry the end; the music stringendo does the climb.
- The Csárdás timing assumes the last OUT is near 10.67 s. The window keeps it there; a seed outside it would need V1.tb's re-timing to stretch more.

## Rendered 2026-11-13
- Runner-up pool widened to high-RPM countries (Canada, UK, Australia, Germany, France, Netherlands, Sweden, Norway, Denmark, Switzerland, Ireland, New Zealand, Japan).
- Seed **16242**: USA vs FRANCE, duel 0.61 s. Seeds 1-16602 checked.
- FHD 14.20 s: -14.0 LUFS, -6.5 dBFS, flash PASS, seam 0.287.
- Delivered to `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_country_marbles2\`.
- Lessons:
  - The strict never-falling rate rule passes ~1/40 seeds; use the relaxed rule 4.
  - The pour had to be staggered and jittered: a rigid 3-column block looked fake. This is sim VERSION 2.
