# rocket_boosters4 — the honest race, then a FLYING CARPET (gag) (batch70)

- Brief: docs/BRIEF_batch70.md §2 (owner: the rope pull "does not work" -> removed; Bolt falls way behind and runs out of fuel far below orbit; a public-domain pop-culture helper takes him up; the helper is a GAG, no fake numbers; Mochi's annoyed reaction is the payoff). New file `scenes/rocket_boosters4.py`, generated from rocket_boosters2.py (rb2/rb3 untouched). Opens on @<viewer>'s comment card as before. Caption: "Rematch: tank + ~2 BOOSTERS~ vs ~3 STAGES~" / "who reaches ~ORBIT~ first?".

## The race (honest, rb2 bit-for-bit)
- Mochi: rb2's core 200 t + 2 × 50 t boosters; boosters drop 1.92 (40 km), core dry 4.64 (144 km), coasts to ORBIT at sim 10.23.
- Bolt: ep. 1's 3 stages; drops 3.00 / 7.20 / 9.60; last stage dry at sim 9.60 at 194 km. "200 km BEHIND..." at sim 7.9 (honest gap). Without the carpet his coast reaches the line at sim 12.58 (2.35 s after her).

## The gag (not physics)
- Helper: a FLYING CARPET (1001 Nights folk tales; Galland's French edition 1704-1717; public domain). Picked as the most instantly recognisable PD magic ride; drawn as a plain red Persian-style rug (gold border, navy medallion, tassels, no face), nothing from any film.
- Flies in from the lower right at sim 8.35, waits beside him, slides under the capsule as stage 3 drops, ride sim 9.66 → line at 10.05 (log-height ease-in curve, `_apply_gag`). Mochi crosses 0.18 s later.
- From 9.66 the HUD shows "???" for his km and mass, status "CARPET?!" / "IN ORBIT?!" / "WINNER?!"; banners "A FLYING CARPET?!", "BOLT WINS?!", "BY FLYING CARPET", Mochi's "THAT'S NOT A ROCKET!" + honest "IN ORBIT 0.2 s LATER". Camera follows his honest flight (no zoom jump).

## Sound
- Mendelssohn, Italian Symphony I (PD; midiworld note source, as ol_blade_split): bar 4 → bar 19's A-major downbeat (score beats 12-57, quarter 0.236 s), cadence = Bolt's crossing; + harp glissando when the carpet arrives, celesta + a tonal rising glide on the ride. rb2's tonal SFX re-pitched to A major (ticks, clunks, puffs, sputters, bells, drones).

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 843 frames = 14.05 s. −14.00 LUFS, peak −2.7 dBFS, last 0.5 s digital silence. flash_check 0 = PASS. Seam 1.36 (space → blue-sky dissolve; rb2 1.13, rb3 1.41).
- RMS/s −17.7 −17.5 −16.4 −16.2 −17.6 −17.5 −18.9 −16.6 −17.4 −17.0 −15.4 −14.9 −16.2 −30.2 (hold).
- Frames read: 0.5, 3.4, 8.6, 9.9, 10.3, 10.65, 11.2, 13.9 (+ Fast stills 560-700).

## Doubts
- The ride is short (0.4 s from scoop to the line): Mochi's honest crossing fixes the deadline. The carpet is on screen ~1.7 s in total.
- No lead change in the race itself; Bolt is behind from liftoff to the carpet.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\rocket_boosters4.mp4`. Owner review: pending.

## v2 (coordinator, batch70): SLOW-MO gag + a readable carpet
- The clip clock runs at x0.25 from the pickup (sim 9.66) to just after Bolt's crossing (10.09): `clip_t` / `sim_t` warp, +1.17 s; the sim is untouched. A gold "SLOW-MO" pill (top right) during it. Music re-timed so the A-major cadence still lands on the crossing (clip 11.9); SFX events mapped through `clip_t`; the whoosh glide spans the slowed ride.
- Carpet 252 x 46 px (was 208 x 34), tassels 20-24 px waving, 3.4 px gold border, bigger medallion; the ripple runs on the clip clock (keeps waving in slow-mo).
- After the win: "THAT'S NOT A ROCKET!" + Mochi annoyed hold ~2.4 s before the loop.
- Checks (encoded Full HD, label b70s): h264 yuv420p 1080x1920 60 fps, 920 frames = 15.33 s. -13.98 LUFS, peak -2.0 dBFS, last 0.5 s silent. flash_check PASS. Seam 1.65. RMS/s -17.8 -17.4 -16.5 -16.4 -17.0 -17.8 -18.5 -17.1 -17.0 -17.0 -15.9 -17.6 -14.7 -16.1 -24.6. Frames read 10.5, 11.0, 11.6 (+ Fast stills 610-860).
- The delivered file (review/batch70/rocket_boosters4.mp4) is v2.
