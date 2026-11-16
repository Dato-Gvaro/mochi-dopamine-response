# press_tools3 — the CORNER ITCH: the reach widens until it hits the wall balls (batch71)

- Brief: docs/BRIEF_batch71.md §2. New file `scenes/press_tools3.py` (from press_tools2; untouched). Same comment card, ×3 split, deep trident at 1/3 speed in the pile, MAX + overflow snap.
- THE CHANGE: REACH = the outermost tip's distance from the chamber centre, the same for both tools: D0 90 px at sim 0 → the walls (218 px) at T_FULL 12 s, ACCELERATING (quadratic; "it widens faster every second"). Stops = press_tools2's unit patterns × (REACH − prong offset). Dashed guides + gold arrows show it; "REACH xx%" in the HUD.
- The wall balls: 4 big balls (gen 2, r 43.6) stacked against EACH wall at the start; inner edge 141 px from centre → out of reach until ~7 s.
- MAX y 560 (press_tools2 660): a higher overflow. T_PAYOFF 2.3.
- Seed 0 result: wall balls first crushed — trident 8.95 s, spike 7.77 s (sim); TRIDENT OVERFLOWS at clip 11.80 s, 3,603 vs 2,663 balls; no lead change. No single burst in the crush rate (trident 100-117/s, spike 121-170/s after 7 s): the wall columns get crushed over ~3 s.
- Tuning notes: linear reach 50→100 % by 11 s: overflow 25 s at MAX 560 (no wall balls); wall balls added: 9 s at rate 5 px/s; quadratic T_FULL 13: 11.1 s.
- Checks (encoded Full HD, label b71): h264 yuv420p 1080x1920 60 fps, 847 f = 14.12 s; −13.99 LUFS, peak −9.1; flash PASS; seam 1.90 (tools mid-strike at frame 0, press_tools2 1.74). Frames read 0.5, 3.0, 6.5, 9.0, 10.3, 11.85, 12.6, 13.8.
- Delivered review/batch71/press_tools3.mp4. Owner review: pending.

## v2 (batch71b, owner: "you don't get me": no visible limiter)
- Removed: the dashed reach guides + arrows, the "REACH xx %" line, the "tools reach WIDER" caption line and the wall-ball banners. Caption: "Every ball HIT splits into 3" / "which OVERFLOWS first?".
- Movement: until T_SWITCH (sim 5.5 = clip 4.9 s, ~45 % of the race) press_tools2's stop patterns, kept to the middle (outer tip 128 px from the centre, short of the wall balls' inner edge at 141); from T_SWITCH both tools work along the walls (KW stops ±1.0/±0.86/±0.72 alternating sides, the outer tip 8 px from the wall). MAX y 420 (press_tools2 660).
- Result (seed 0): TRIDENT OVERFLOWS at clip 11.00 s, 3,793 vs 2,025 balls, no lead change. Big wall balls at the overflow: 0 of the original size (gen 2), 0 gen 3; Mochi 2 / Bolt 4 at gen 4 (r 19, the size of ordinary fragments). Bolt's spike crushed one wall ball at sim 1.57 (it had rolled inward).
- Checks (label b71bv2): 799 f = 13.32 s; −13.99 LUFS, peak −8.9; flash PASS; seam 1.88. Frames read 1.0, 4.0, 5.5, 7.0, 9.0, 11.05, 12.5.
- Delivered review/batch71b/press_tools3.mp4.
