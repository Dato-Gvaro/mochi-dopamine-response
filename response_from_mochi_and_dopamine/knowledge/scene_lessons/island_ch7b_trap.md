# island_ch7b_trap (STRANDED ch7b TRAP FLOOR): 9:16 Short notes

General chapter notes: docs/scenes/island_long.md.

## 9:16 4K fix (owner review 2026-11-08)
- Jumps found: 1 hard time cut at 6.1 s (clock 6.1 -> 10.44; the tile counters jumped 5 -> 13). Then Bolt (straight, so ahead) walked out of the Mochi-following crop for good.
- Fix (9:16 only; the 16:9 is bit-identical):
  - `RampEdit` window (1.0, 1.0): peak x5 at 5.1-7.1 s, with motion blur and a "▶▶ x5" tag at (118, 640). The counters run up continuously.
  - Bolt follow-cam inset, owner's option:
    - Box (600, 585, 300x250): inside x 0.10-0.84w and far above 0.71h, clear of Mochi's shield / THUNK line (~850+).
    - Labelled "BOLT →". It renders the same floor with the camera pushed onto Bolt (`_CAM`), zoom 0.63.
    - It fades in on his main-view x (continuous) and holds on the exit arch as he leaves. It fades out at C_DOOR + 0.5-1.0.
  - `--check`: 2 frames (6.91-6.99 s) where Bolt straddles the right safe edge while walking out. The inset is already up there; accepted.
- Length unchanged: 15.82 s / 949 f. The sound was rebuilt from events (the skipped steps / arrows now sound).
- Scene-score max: 0.012 (was 0.068).

## 9:16 v3: normal speed (owner 2026-11-09)
- Owner: no fast-forward. The RampEdit is gone; the 9:16 EDL is one span, clock 0 -> C_WIN + 2.2, at 1x.
- No "▶▶ x5" tag. The Bolt follow-cam inset is unchanged (fades in near the edge, holds, fades out), now at real speed.
- Length 20.17 s / 1210 f (v2: 15.82 s / 949 f). Sound rebuilt from events: 38 steps, 12 arrows, 12 thunks.
- 16:9 bit-identical: 6 stills + the 16:9 wav/events hashed before/after.
- v2 kept: scenes/_versions/island_ch7b_trap_v2.py; its 4K is archive/stranded_shorts/ch7b_9x16_4k_v2_ramp.mp4.
- `--check`: 6 frames (6.90-6.98 s), Bolt straddling the right safe edge as he walks out. Same accepted case.
- FAST scene-score max 0.011 (none > 0.04).
- 4K (label s4k3, review/island_shorts_4k/run_4k_fix3.py): 2160x3840 h264 yuv420p 60/1, 1210 f, -14.0 LUFS, TP -4.3, flash PASS, scene max 0.0112.
