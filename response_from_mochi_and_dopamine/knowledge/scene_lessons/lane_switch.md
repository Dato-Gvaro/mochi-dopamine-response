# lane_switch — Switch lanes or stay in one: who gets to the TEST TRACK first? (batch57 v1, batch58 v2, batch60 v3)

## v3 (batch60, 2026-10-30): the real road problem: lane hoppers make stop-and-go
- Owner on v2: "still not the actual road problem". Brief: docs/BRIEF_batch60.md. Edited in place (sim by the previous wave-B builder, drawing/banners/destination by M-B). Pre-v3-drawing copy: scratch `mbB/lane_switch_pre_v3draw.py`; v2 script `mb/lane_switch_v2.py`; v2 video → `MochiAndBolt\archive\lane_switch_v2.mp4`.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\lane_switch.mp4` (**v3**, Full HD, 15.63 s, 938 frames, label v3, seed 110).
- Caption: "~Switch~ lanes or ~stay~ in one?" / "Who gets to the ~TEST TRACK~ first?"
- **Story:** Mochi drives the RIGHT lane, Bolt the middle, level at 220 m. Frame 0: Bolt is already blinking into the left lane ("BOLT: THAT LANE IS MOVING!"). 1.0 s he hops back: "HIS CUT-IN MAKES THE CAR BEHIND BRAKE" (a red BRAKES pill on that car while it brakes; measured from the sim, < -1 m/s²). 2.4 s "NOBODY CUTS INTO MOCHI'S LANE". Lead changes 4.0 BOLT / 7.3 MOCHI / 8.6 BOLT / 11.6 MOCHI AHEAD; 6.5 s "STOP-AND-GO!" (Bolt down to 3 km/h, NO GAP pill, his STOPS 1). Right verge: OTHER DRIVERS n lane hops. Destination: a TEST TRACK pit lane (orange gate bar over a checkered line, numbered garage boxes on both verges, TEST TRACK painted across the road) and a POWER LAP board (loose homage, no show name/logo) that fills 1 MOCHI 0:47 / 2 BOLT 0:49 as they arrive. Cadence 12.63 s: "MOCHI ARRIVES FIRST!", "0 LANE CHANGES BEAT 5". The camera follows the pair into the pit lane (both stay on screen).
- Nerd stats: live km/h under each name tag, per-lane km/h pills, HUD per side: metres to the track (leader tinted + AHEAD), LANE CHANGES n · STOPS n (a stop = speed under 1.5 m/s), TIME with the x3.7 time-lapse.
- **Sim v3** (`V3` dict; honest IDM, dt 1/15, all cars, the same car model and random short brakings 0.04/s for everyone): lanes 0-1 = switchers (check the other lane 2x/s, hop if its next car is faster by 0.1 m/s; seeing hops nearby makes them hop sooner); a hop needs 1.0 m in front / 0.5 m behind and the new follower may need to brake up to 5 m/s² (Bolt 8: he squeezes in); Bolt waits 2.5 s between hops. Right lane: nobody changes in or out; Mochi keeps a 2.5 s headway (rides out the waves). The race stops counting at the line; v3 lets the sim run on to +60 m only so the camera can follow (the race is unchanged).
- **Honest odds (120 seeds, V3):** Mochi first in 61 %, mean +3.1 s. Seed 110: Mochi 46.5 s real, Bolt 48.6 s (+2.1 s); same mean speed (4.7 vs 4.6 m/s) but Bolt's swings more (std 2.1 vs 1.2 m/s); Mochi never stops (min 3.3 m/s), Bolt once (0.7 m/s). 5 Bolt lane changes, 5 lead flips, max separation 12.3 m. Only 16 of the 21 hops before the finish (others + Bolt) made the car behind brake (< -0.4 m/s²): no banner says "every".
- Proof-read: all banners are statements about this race and measured from the sim.
- **v3 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 938 frames = 15.63 s; muxed −14.00 LUFS, peak −1.99 dBFS; last 0.5 s −157 dBFS; flash PASS (0); seam last→first 0.49 (0→1 1.42: the x3.7 scroll). SFX/s 14 18 10 10 10 8 14 13 15 8 15 10 6. Frames read from the mp4: 0, 1.6, 3, 6.6, 7.0, 7.6, 12.7, 12.9, 14.5, 14.8, 15.3. Key content x 144-898 (board right edge 898 < 0.84w = 907).
- **v3 doubts:** the stop-and-go is honest but mild (Bolt's one stop at 6.5 s; most of the time both crawl at 10-25 km/h); the margin is 0.56 s of clip (2.1 s real). The pit lane garages are busy decoration at the end.

## v2 (batch58, 2026-10-29): the HERD effect (no truck, no return)
- Owner on v1: "not a real situation: the truck is slow, but why did Bolt go back behind the truck again? Maybe he changes lanes and the others change too, that lane gets busy, and Mochi going in one lane goes without problems." Brief: docs/BRIEF_batch58.md. Edited in place; v1 script at scratch `m58/lane_switch_v1.py`, prototype/search `m58/lane_v2.py` + `m58/lane_search.py`; v1 video → `MochiAndBolt\archive\lane_switch_v1.mp4`.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\lane_switch.mp4` (**v2**, Full HD, 15.63 s, 938 frames, label v2, seed 62).
- Caption: "Jump to the ~FASTER~ lane or ~stay~?" / "Who gets ~HOME~ first?"
- **Story:** both in the middle lane, Bolt one car (7.5 m) AHEAD of Mochi, 220 m to the exit. Frame 0: a gap has opened in the left lane, Bolt is already pulling into it ("BOLT: THAT LANE IS FASTER!"); 3 drivers around him jump in within 0.3 s ("EVERYONE ELSE SWITCHES TOO!", right-verge counter LEFT LANE +n cars followed Bolt, amber blinkers). Lane speed pills at the bottom of each lane (km/h; fastest green, slowest red): left 22-23 → 12-13 km/h, middle 18-25. 8.0 s "THE "FAST" LANE JAMS!"; Bolt keeps getting "NO GAP" (he wants back but the flowing middle lane closes too fast: MOBIL safety), soft horn. 9.76 s "MOCHI AHEAD!"; she crosses EXIT · HOME on the cadence (12.63 s): "MOCHI'S HOME FIRST!", "0:39 vs 0:43", "THE "FAST" LANE FILLED UP", "STAYING PUT WINS". Bolt: 1 lane change.
- **Sim v2** (IDM as v1; trucks only in the right lane, 15 %; lane change 2.0 s): every ordinary car checks a neighbour lane at 0.20/s and changes if it looks faster by 1 m/s; each recent change into that lane within 30 m multiplies the check rate (×(1+8n)) and lowers the edge needed (0.3 m/s for 1 seen, any lane not 0.5 m/s slower for ≥2 seen) = herd imitation. Safety: the new follower must not need to brake harder than 2 m/s² (3.5 for herd drivers and Bolt). Drivers wait 10 s between changes (Bolt too). Start (after a 30 s warm-up): lane-1 cars cleared around the pair; left-lane cars between −1 and 80 m removed (the gap that LOOKS faster). Camera: midpoint of the pair, PXM 24, Y_CAM 800 (both cars stay between the banners and the lane pills; max separation 24.8 m).
- **Honest odds (199 seeds, same start):** Mochi gets home first in 63 % (66 % of the 190 runs where Bolt takes the gap at once), mean +2.6 s for staying, although Bolt starts 7.5 m ahead. Seed 62 picked for a late lead change (77 % of the race), a jam and a 3.5 s real margin.
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 938 frames = 15.63 s; −14.01 LUFS, peak −1.99 dBFS, last 0.5 s digital silence (−240 dBFS); flash PASS (0, mean lum 0.042); seam 0.34 (good band). SFX/s 20 10 8 6 9 6 6 6 6 10 8 6 8. Frames read from the mp4: 0.3, 5.0, 8.3, 10.0, 12.8 + 1:1 crops at 8.3 and 9.9 s; stills 0-14 s. Key content x 144-892 (inside 0.10-0.84w).
- **v2 doubts:** the herd jumps in at the very start (0.2-0.3 s clip), then one more at 9.2 s; the "jam" is lane 0 at ~13 km/h vs ~18-25 in the middle, not a standstill. The start gap is staged (removed cars); the rest is the sim. 3-8 s has 6 SFX/s (the music carries it).

- Brief: docs/BRIEF_batch57.md (Mochi & Bolt 3). New scene file; lib/ and tools/ untouched. Caption/banner/HUD helpers and the sound/mastering chain copied from checkout_queue.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch57\lane_switch.mp4` (**v1**, Full HD 9:16, 15.63 s, 938 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Stay in your lane or ~keep switching~:" / "who gets ~HOME~ first?"
- **Story:** top-down 3-lane road in stop-and-go traffic, the camera following the pair. Frame 0: Mochi (middle lane) and Bolt (left lane) level, 220 m to the EXIT, traffic already moving, brake lights rippling. Bolt edges ahead (1.7 s, "AHEAD"), switches into a faster-looking lane at 4.9 s ("BOLT SWITCHES!", +1, blinkers), then switches back at 5.9 s, right behind a truck ("STUCK BEHIND A TRUCK!", SLOW TRUCK tag at 6.5 s). He is 13 m ahead, but Mochi's lane surges and the gap melts (progress strip at the left). "MOCHI AHEAD!" at 11.5 s; Mochi passes under the EXIT · HOME gantry on the cadence (12.6 s): "MOCHI'S HOME FIRST!", "0:46 vs 0:47", "2 LANE CHANGES: 1 s SLOWER", "SWITCHING DOESN'T PAY". Bolt annoyed, Mochi grinning through their sunroofs.

## Layout
- Road x 339-675 (lanes 112 px, 30 px/m), verges with scrolling trees; cars 56 × 135 px with the driver's face through the sunroof (r 23); trucks 76 × 330 px. Name pills above Mochi's and Bolt's cars.
- Progress strip x 144-248 (START → EXIT, two dots). HUD y 1366-1544: "TIME m:ss (time-lapse x3.7)", per side metres to the exit (leader tinted + "AHEAD"), LANE CHANGES.
- Camera = critically damped follow of the pair's midpoint (+3 m), no zoom; key content x 144-675 (inside 0.10-0.84w).

## The physics (seeded, honest; real seconds, dt 1/15)
- Intelligent Driver Model per vehicle: cars v0 14 m/s, T 1.3 s, s0 2 m, a 1.4, b 2.0; trucks (7 % of traffic + 2 placed) v0 10, T 1.6, s0 3, a 0.40, b 1.5. Spacing 5-11 m × a per-lane density factor 0.95-1.12. Ordinary drivers brake briefly at random (0.035/s, -2.5 m/s² for 0.6-1.4 s), which starts brake waves. They also move to a clearly faster lane now and then (0.25 checks/s, threshold +1.0 m/s, gaps 5 m / 3 m), so the lanes even out.
- Bolt: every 1.5 s he glances at the next 3 cars within 40 m in each lane; if a neighbouring lane beats his by 0.5 m/s and the gaps are ≥ 4 m ahead / 2 m behind, he changes (2.2 s, cautious ≤ 0.5 m/s², blocks both lanes). Mochi never changes.
- 35 s warm-up, then both are inserted level at x = 0 (cars in the way removed before frame 0). Exit 220 m ahead. Time-lapse one constant x3.67 so Mochi reaches the exit on the cadence.
- **Honest odds (340 seeds):** staying gets home first in 166 (49 %); switching gains on average 1.3 s on a ~52 s drive (2.4 %). So the result is "about the same", the real finding. Seed 168 was picked (search scored on a close finish, lead changes, and the last change before the finish landing behind a truck): Mochi 46.3 s, Bolt 47.5 s. After the truck change Bolt's 13 m lead melts to 3 m in 6 s real (truck a = 0.4 m/s²; Mochi's lane surges to 8 m/s), and she passes at 42 s.

## Sound (music first)
- **Piece:** Antonín Dvořák, String Quartet No. 12 in F "American" Op. 96, IV. Finale (1893; d. 1904, PD). Driving, motoric. Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD (N. Simrock 1894), `dvorak-o96-mids.zip` (`dvorak-o96-3.mid` = Mvt 4) + rdf + SOURCE.txt at `<SOUNDFONTS_DIR>\scores\dvorak_american_quartet\`. All 4 parts read at runtime.
- **Excerpt:** 2/4, quarter = 152 (bar 0.79 s): MIDI bars 8-23 (the finale theme over its rhythm, then the C pedal), cadence = the F-major arrival of bar 24 (12.63 s).
- **Arrangement** (lib/orchestra): the quartet's own scoring (violin I, violin II, viola, cello + contrabass 8vb); cadence = timpani + F-major strings/horns, held chord.
- **SFX** (tonal): a distance tick every 5 m per car (8th grid, pitched to the harmony; the rate follows the speed), soft low bumps for brake-light onsets near the pair (16th grid), blinker relay ticks on Bolt's lane changes, a soft two-note truck horn at the twist, dings on lead changes and the cadence.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 938 frames = 15.63 s. -14.00 LUFS, peak -1.99 dBFS, last 0.5 s digital silence.
- RMS/s: -19.2 -17.9 -17.7 -18.8 -16.8 -17.8 -16.9 -17.1 -16.4 -16.7 -16.1 -15.8 -15.2 -16.1 (cadence) -28.1, then silence.
- SFX events/s: 6 9 9 8 10 13 12 9 8 4 7 11 10 0.
- flash_check PASS (0 flashes, mean lum 0.04). Seam last → first 0.19 (check_clip 0.34, good band).
- Frames read from the mp4: 0.5, 5.3, 11.6, 13.4 + a 1:1 crop at 6.8 s; stills at 0, 0.5, 5.5, 6.5, 8.3, 11.5, 12.8, 14.7.

## Doubts
- Bolt changes lanes only **2×** before the finish (honest for this rule in dense traffic; a 3rd change comes after he crosses and is not counted). "Keep switching" may read as overstated; a more aggressive Bolt (lower threshold, tighter gaps) is a new search (~10 min / 170 seeds).
- The truck twist is gradual: Bolt is still 13 m ahead when the "STUCK" banner appears, and Mochi only passes at 11.5 s. The progress strip shows the gap closing.
- The race is real-sim, not staged: the seed is chosen; the odds over 340 seeds are a coin flip with a ~1 s mean edge for switching.
- 9.0-10.5 s has fewer SFX (4-7/s): both crawl behind slow traffic.

## Args and cost
- `--seed` (168), `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~4 s (pure Python IDM, ~110 vehicles); Full HD render ~70 s at 2 encoder threads. Seed search scripts: scratchpad only (lane_proto4.py / lane_search4.py logic is identical to `run()` here).

## Outcome
- (fill after upload)

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/lane_switch.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 938 frames 15.63 s; -14.00 LUFS, peak -1.99 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v3. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-06\2_lane_switch.mp4`, 16:00 local Nov 7 (= 07:00 US East Nov 7). FHD review copy → `MochiAndBolt\archive\lane_switch_fhd.mp4`.
