# rocket_boosters — comment reply: "How About One Big tank + 2 boosters?" (batch67 wave B, 2026-11-03)

- Brief: docs/BRIEF_batch67.md clip 6 + the comment-video skill. Comment by @<viewer> on "Why rockets throw away their empty tanks" = **rocket_stage** (batch51, uploaded Oct 31; ledger `videos\MochiAndBolt\uploaded\2026-10-30\UPLOAD.md`), not the rejected rocket_stages. Text reproduced verbatim; no likes, age or heart drawn (unknown).
- New file `scenes/rocket_boosters.py` (copy of rocket_stage; the brief asks for new scene files, which also keeps rocket_stage bit-reproducible). Deliverable `<VIDEOS_DIR>\MochiAndBolt\review\batch67\rocket_boosters.mp4` (Full HD, label b67).
- Real screenshot: none on disk (`assets/comments/` does not exist); the card is drawn (comment_overflow's card). Owner: save it as `assets/comments/<viewer>.png` if the real one should ship.
- Caption (baked, after the card): "One ~BIG~ tank vs tank + ~2 BOOSTERS~:" / "who reaches ~ORBIT~?". Card holds 0-2.9 s, lifts off by 3.35 s; caption fades in 3.05-3.45 s; on the loop dissolve the caption fades out and the card fades back in (pure functions of the frame index).

## THE ONE CHANGE
- Bolt flies ONE BIG TANK + 2 SIDE BOOSTERS (the comment's idea) instead of 3 stages. Mochi is ep. 1's one big tank, same numbers (her flight is bit-for-bit ep. 1's).
- Rules (ep. 1's): 300 t fuel in total, 10 t capsule, tank shell = 42 % of its fuel, same exhaust speed, a = F/m − g. Engines: core = Mochi's (3 t); each booster = ep. 1's small engine (1.32 t); every engine burns at Mochi's rate per tonne of engine (10.55 t/s per t), so thrust ∝ engine mass. The boosters drop together when dry; the empty core stays on (no extra staging).
- Bolt: core 200 t + 2 × 50 t. m0 442.4 t vs Mochi 440 t. T/W 2.68 vs 1.44.

## Honest result
- Boosters dry at sim 1.92 (40 km): −45 t of shells + engines. Core dry at 4.64 (~150 km). Bolt crosses ORBIT (400 km) at sim 10.23 = the cadence; his coast would top out ~664 km. Mochi: empty at 7.8 (119 km), apex 364 km (36 km SHORT), as ep. 1.
- Bolt leads from liftoff (no lead change): with 3 engines he lifts 2.68× his weight. So the answer to the comment is "yes, it works, by a lot".
- Booster size sweep (apex km): 20 t → 512, 30 → 579, 40 → 634, **50 → 664**, 60 → 646, 75 → 515. 50 t is the best split under these rules, not a value tuned to a winner.

## Timeline (clip = sim + 0.6; 13.33 s, 800 frames)
- 0.0 s: both just off the pads (0.8 vs 2.9 km), the comment card on top. 2.52 s: BOOSTERS DROPPED! (−45 t), they tumble away left and right. 5.24 s: Bolt FUEL EMPTY, ...COASTING (Mochi still burning). 8.40 s: Mochi FUEL EMPTY. 10.83 s: Bolt at ORBIT: BOLT WINS! / IN ORBIT!, Mochi's red "MAX 364 km: 36 km SHORT!". 12.73-13.33 s: dissolve into frame 0.

## Sound
- Wagner, Ride of the Valkyries (PD), midiworld transcription (as ol_domino_giant): the last two beats of bar 63 + bars 64-70, re-timed (dotted quarter = T_CAD / 21 = 0.487 s) so our B-major chord (bar 71) lands on the ORBIT crossing. Ep. 1 used Holst's Jupiter.
- SFX as ep. 1 (tonal ticks per altitude milestone, chord-fitted from the score's brass/horn/bass notes; clunk + puff at the drop; sputters; orbit chime in B major; engine drones, Bolt's brighter while the boosters burn).

## Checks
- Pre-encode seam (stills, Fast): last → first 0.52 vs an interior step 0.71 (perfect loop). Encoded seam is higher (codec drift through the dissolve, as ep. 1: 1.54).
- Encoded Full HD: h264 yuv420p 1080x1920 60 fps, 800 frames = 13.33 s. −14.01 LUFS, peak −2.26 dBFS, last 0.5 s silent. RMS/s −19.4 −17.3 −17.1 −17.8 −16.7 −17.1 −18.0 −16.3 −16.1 −17.2 −15.8 −13.8 (cadence) −18.7. SFX events/s 12 8 15 9 10 11 9 11 12 7 10 5. flash_check 0 fails (1 flash at 13.07 s, the dissolve). Encoded seam 1.10.
- Frames read from the encoded file: 0, 1.0, 2.55, 3.3, 5.3, 8.5, 10.9, 13.0; 1:1 crop of the booster drop (2.6).
- First version had no music under the first 0.6 s (bar 64 started at sim 0): fixed by adding bar 63's last two beats as a pickup (first second −21.3 → −19.4 dB).

## Doubts
- No lead change: Bolt is ahead from the first frame (honest; the drama is the margin, "664 vs 364 km").
- From 5.2 s Bolt coasts (no flame); SFX events/s fall at the end (10 → 5).
- Thrust ∝ engine mass is our rule; with equal-thrust engines the boosters would add no thrust, which is not what boosters are for.
