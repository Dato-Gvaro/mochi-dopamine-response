# pizza_deal: ONE 18-inch or TWO 12-inch? whose jar FILLS to the top? (batch74, NEW)

- Brief: docs/BRIEF_batch74.md (IDEAS.md pick 1). New file `scenes/pizza_deal.py`; no lib changes.
- Fact (exact geometry): 18" = pi x 9^2 = 254.5 sq in; 2 x 12" = 2 x pi x 6^2 = 226.2 sq in (+12.5 %). The viral "one large beats two mediums" fact.
- Model: every pizza is cut on a 1-inch grid centred on it (sim areas 226.3 / 254.5, from 24x24 supersampling per cell; edge bites count only their real area). Crust first: outer cells leave first, so each pizza shrinks toward its centre. Every pizza is cut at the SAME speed: cut(t) = 5 + 2.5 t + 1.6 (TAU/ln2)(2^(t/TAU) - 1) sq in, TAU 2.0 s (the speed doubles every 2 s). Mochi's two pizzas cut at once, so she gets 2x the rate.
- Jars: 16 x 15 tiles = 240 sq in to the rim (the FULL line); 20 px per inch for pizzas, bites and jars alike. Bolt's last 14 bites spill over the rim into the gap between the jars.
- Result (sim, clip time): Mochi's boards empty at 9.03 s (226); LEAD CHANGE 11.28 s; Bolt FULL 11.47 s; Bolt done 11.65 s (254). Frame 0: 6 vs 3 already landed. Clip 14.6 s (dissolve 14.0-14.6).
- Landings per second: 22 20 19 25 28 37 46 65 87 42 55 48 (falls after Mochi stops at 9 s: only one pizza left cutting).
- Music: Denza, "Funiculi, Funicula" (1880, PD; scores/denza_funiculi/funiculi_melody.mid), one pizz note per landing (>= 85 ms apart), a soft thud per bite; celesta ping at the lead change; timpani + D-major brass/strings at FULL.
- FAST stills (b74): output/pizza_deal_b74_f0 / f560 / f680 (lead change) / f780.png.
- Doubts: LEAD and FULL are only 0.2 s apart (226 vs 240); Mochi's jar ends at 94 % (one row short) so the gap reads small, which is honest; clip 14.6 s is slightly under the 15-17 s band.
- Coordinator OK (2026-11-07) + tweaks: finale held to 15.5 s; "+12% MORE PIZZA" on Bolt's jar from Bolt done + 0.5 s; melody repeat runs collapsed to <= 2 (top pitch 33 % -> 24 %).
- Checks (encoded Full HD b74): 930 f = 15.50 s; -14.02 LUFS, true peak -5.4 dBTP; flash PASS; seam 0.63; events/5 s 41 51 16. Delivered <VIDEOS_DIR>/MochiAndBolt/review/batch74/pizza_deal.mp4.
- Owner review (2026-11-07): "loved it". 4K (b74k) verified: 2160x3840, -14.02 LUFS, TP -5.4, flash PASS, seam 0.38. Scheduled at videos/MochiAndBolt/schedule/2026-11-14/3_pizza_deal.mp4 (slot 3, 23:45 local Nov 15).
