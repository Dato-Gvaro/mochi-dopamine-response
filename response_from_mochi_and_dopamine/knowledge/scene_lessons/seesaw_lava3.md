# seesaw_lava3
- Episode of seesaw_lava2 (2026-10-14, batch33). Why: seesaw_lava2 was #3 in the 2026-10-15 report (1,582 views); characters in peril over lava do best. seesaw_lava2.py stays untouched; lava3 imports its look (cave, lava, vent, magma rocks, smoke, dunk path) and seesaw.py's geometry.
- NAMEABLE CHANGE: "every rock is BIGGER than the last". kg table = 14 x 1.055^k, and each rock is always at least 1 kg heavier than the one before. Radius = sqrt(13 kg), so a disc's mass ~ r^2 (pebbles 14 kg r 13.5; final 96 kg r 35). A "+NN kg" label shows on every landing. "41 / 63 / 82 kg ROCK!" banners appear as milestone rocks leave the vent.
- Physics: the peg field is physics2d with 5 ember studs + a wedge (gaps sized for r<=40). The tilt is real TORQUE: tau = sum of kg x lever arm / BK_X, where the arm is where the rock actually rests (greedy lowest-spot packing in a taller basket, BK_H 190, mound up to +110). The tip is at |tau| >= TAU_D = 220. Pivot response: tilt = 0.88*THMAX*|u|^0.75 (gives easily, stiffens near the lava). Landing kick = 0.10 + 0.0105*kg rad/s, so each bigger rock lurches harder. Kg totals must agree in sign with the torque whenever |u| > 0.15 (search filter), so the counters never contradict the board.
- Hook: the sim runs from an empty machine; the clip starts at a searched pre-roll frame (`--pre`). That frame has: baskets loaded, Mochi's end already down (u0 = -0.54, sweating), and a 23 kg rock in flight that lands on Mochi's side at 0.25 s. The pre-roll is silent; the first fall whooshes into its thud from t = 0.
- Loop: the last 0.5 s dissolves into the pre-roll frames -30..-1, so the last frame = sim frame -1 (seam mean 0.469). After the reset, the board eases to the pre-roll angle (no ghost board).
- s3550 / pre 580: 37 rocks (9 pre-roll), lead changes 5. Mochi has near-tips at 3.7 and 5.3 s, then recovers. Bolt has a near-tip at 14.8 s. The 96 kg final boulder tips Bolt at 21.18 s (Mochi wins, 645 vs 951 kg; the counters freeze at the tip). Pattern breaks: 0.25 lurch, 3.7, 5.3 SO CLOSE, 8.0 (41 kg), 13.8 (63 kg), 14.8 SO CLOSE, 17.1 (82 kg), 21.2 tip, dunk. Clip 25.93 s.
- Sound: the material layer is synthesised in-scene as the `bed`:
  - a stone thud into the iron basket, deeper and longer with kg, plus grit and a faint cage clank;
  - a wood creak/groan on every landing (a stick-slip pulse train through plank resonances, longer and lower for heavy rocks);
  - a stone tok on studs and walls;
  - a vent puff on release;
  - a riser into the final boulder.
  The blue_danube note per landing and the seesaw_lava2 accents go through events: slam, sploosh, whoosh, cheer, sizzle, bloops, plus steam hiss on near-tips. NOTE: tools/regen_audio.py from `_events.json` does NOT rebuild the bed; re-run the scene instead.
- Checks (Full HD): h264 yuv420p 1080x1920 60 fps, 25.93 s; -14.02 LUFS, peak -5.2 dBFS, last 0.5 s -73 dBFS; flash_check PASS (0); seam 0.469; audible from 0 s.
- Doubts: the landing rate is ~1.4/s, flat (events/5s 7,6,8,7; studs/creaks fill the gaps), because big rocks fill the baskets fast. Mid-clip rocks still read small next to the tall cages. The winner's "HA HA" is partly hidden behind the drop field when the winner's end is high.
- Title idea: "Every rock is BIGGER than the last… who touches the LAVA first? 🌋"
- Args: --seed (3550), --pre (frames; auto via best_start for other seeds), --label, --cap, --search N --from S, --still --frame a,b,c.

Owner review (2026-10-15): DROPPED — a duplicate of seesaw_lava2, "won't work".
