# clones_battle3 — clones_battle2, but the video starts when the drops start

- Owner review of clones_battle2: "starts kinda in the middle — can we start the video when the drops start?". clones_battle2.py is untouched (s41 is reproducible).
- Only change: frame 0 is an EMPTY board with 4 clones per side at the pipe mouth (y=512, evenly spread with ±20% jitter), already moving down at vy=650. Counters start at 4:4, waiting +0:+0. First landing at 0.93 s.
- The loop ends on that state: the crowd pops away, the counters count down to 4:4, the waiting pills count down to +0, and the 4+4 start clones fade in at the pipe mouth.
- With fewer clones at the start the race ran about 1 s longer, so the target is 340 (was 380). Everything else is as clones_battle2: MR 32, 6 big peg rows, live cap min(76, 16 + 1.8t), steal pop + "HA!", "x2/x3/x5" landing pops, "+N waiting" pills, fair-share feed.
- Pick s53: Mochi wins 340:322 at 33.8 s; the clip is 37.2 s. 6 lead changes (6.1, 8.8, 19.5, 24.4, 29.4, 32.2). Landings per 5 s: [14, 45, 70, 91, 111, 122]. Steals per 5 s: [4, 20, 40, 53, 57, 76]. Max live 75. Sounded landings per second climb from 1 to about 20.
- Alternatives: s111 (Bolt 340:321, changes at 27.8 and 32.2), s63, s20.
- Measured (s53): -14.0 LUFS, peak -6.9 dB, last 0.5 s at -66.2 dBFS. flash_check: 12 flashes, worst second 2 = PASS. h264 yuv420p 60 fps 1080x1920, 2232 frames. Pre-encode seam: max delta 0. Encoded seam mean delta 0.417.
- Owner review: pending.
- Owner review 2026-10-05: Normal, could be better (posting Oct 6 as is).
