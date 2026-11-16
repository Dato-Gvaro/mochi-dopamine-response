# rocket_boosters2 — comment reply v2: the viewer's idea goes to MOCHI (batch68)

- Brief: docs/BRIEF_batch68.md §4 (owner: "you misunderstood: they were cheering for MOCHI"). New file `scenes/rocket_boosters2.py`, generated from rocket_boosters.py + rocket_stage.py's Bolt (generator script kept in the session scratchpad only; the scene file is self-contained). rocket_boosters (batch67) and rocket_stage untouched.
- Opens on @<viewer>'s comment card (verbatim "How About One Big tank + 2 boosters?", drawn; no likes/age). Caption after the card: "Mochi: tank + ~2 BOOSTERS~ vs Bolt: ~3 STAGES~" / "who reaches ~ORBIT~ first?".

## THE ONE CHANGE
- Mochi flies ONE BIG TANK + 2 SIDE BOOSTERS (batch67's booster rocket, in her colours): core 200 t + 2 × 50 t fuel (50 t = the best split for the apex under these rules, batch67 sweep), core engine = her ep. 1 engine (3 t), boosters = ep. 1's small engine (1.32 t), fuel rate per tonne of engine = her ep. 1 rate (from ep. 1's 7.8 s burnout, `T_MEMPTY1`). m0 442.4 t, T/W 2.68.
- Bolt = ep. 1's three stages, bit-for-bit: same `simulate()`, same `SPECS["bolt"]` (127.6 / 110.8 / 50.2 t fuel), same stack drawing (REF_PX 314, window 28/43). m0 424.6 t, T/W 1.28.

## Honest result (integrated)
- Mochi leads from liftoff to orbit (no lead change). Boosters dry at sim 1.92 (40 km, −45 t), core dry at 4.64 (144 km), she coasts into ORBIT at sim 10.23 (the cadence) = **MOCHI WINS**.
- Bolt: stage drops at 3.00 (13 km), 7.20 (80 km), 9.60 (194 km); at her orbit moment he is at 239 km; he reaches orbit at sim 12.58 (as in ep. 1), **2.4 s later** ("IN ORBIT 2.4 s LATER" in the hold).
- Why: the same 300 t of fuel, but three engines lift 2.68× her weight at liftoff and the boosters' empty shells drop at 40 km; Bolt's stages lift only 1.28× and lose time low down.

## Timeline (clip = sim + 0.6; 14.23 s = 854 frames)
- Card 0-2.9 s, caption from 3.05 s. BOOSTERS DROPPED 2.52 s · STAGE 1 DROPPED 3.60 · Mochi FUEL EMPTY 5.24 · STAGE 2 DROPPED 7.80 · STAGE 3 DROPPED 10.20 · **MOCHI WINS / IN ORBIT 10.83** · "239 km..." 11.13 · Bolt IN ORBIT 13.18 · dissolve 13.63-14.23.
- HOLD lengthened 1.9 → 2.8 s so Bolt's arrival is on screen.

## Sound
- Wagner, Ride of the Valkyries (PD; midiworld transcription, as batch67's rocket_boosters), bars 63 (pickup) - 70 re-timed so the B-major cadence = Mochi's ORBIT crossing. SFX as batch67: tonal altitude ticks, clunk + puff + tumble ticks for every drop (her boosters, his 3 stages), 3-note sputters at both burnouts, the orbit chime for Mochi, a smaller 3-note chime when Bolt arrives, engine drones (hers brighter with boosters, his per stage).

## Checks (encoded Full HD, label b68)
- h264 yuv420p 1080x1920 60 fps, 854 frames = 14.23 s. −13.98 LUFS, peak −2.20 dBFS, last 0.5 s digital silence.
- RMS/s −19.6 −17.4 −17.2 −17.7 −16.8 −17.1 −17.9 −15.8 −15.9 −16.9 −15.6 **−13.7** (cadence) −16.3 −25.7 (hold). SFX events/s 11 6 16 16 9 11 8 14 13 9 23 5 0 3.
- flash_check PASS (1 flash at 13.98 s: the loop dissolve space → blue sky, as ep. 1). Encoded seam 1.13 (codec drift through the dissolve; batch67's was 1.10).
- Frames read: 0.5, 2.55 (booster drop), 10.9 (win), 13.3 (Bolt arrives); Fast stills 0, 190, 230, 330, 500, 650, 690, 800.

## Doubts
- No lead change: Mochi is ahead the whole flight; the story is "the viewer's idea beats Bolt's stages", by 2.4 s.
- The hold is quiet (−25.7 dB in second 13): the cadence chord dies away while Bolt coasts in.
- "IN ORBIT 2.4 s LATER" sits on the orbit line near Mochi's solar wings.

## SSTO (viewer @mylantisfromfractalblockworld) — feasibility for a next episode
- In OUR rules (reach 400 km): Mochi's ep. 1 single tank tops out at 364 km; +3% exhaust speed → 397 km, +5% → 420 km, +8% → 455 km (sim sweep). An aerospike's real gain is altitude compensation (better thrust low down), roughly 5-10% average Isp during ascent over a fixed bell, so an honest "aerospike" episode would just make it.
- In the real world: LEO needs ~9.4 km/s with losses. Aerospike Isp ≈ 340 s at sea level, ≈ 430-455 s in vacuum (XRS-2200 / VentureStar's RS-2200, LOX/LH2). With ~400 s average: mass ratio e^(9.4/3.92) ≈ 11, i.e. ~91 % of liftoff mass must be propellant (tanks + engines + wings + payload ≤ 9 %). Wings add dry mass. X-33/VentureStar (aerospike SSTO) was cancelled in 2001; no SSTO has reached orbit.
- Verdict: buildable and honest IF the episode keeps our 400 km rule and states the aerospike gain as an assumption (+5 % exhaust speed); do NOT claim real orbit for a spaceplane.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch68\rocket_boosters2.mp4`. Owner review: pending.
