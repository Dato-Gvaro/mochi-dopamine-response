# dune_deflate — Same car, same dune: only the TIRE PRESSURE differs (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 6, wave 2). New scene file; caption/sound chain copied from shred_race; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\dune_deflate.mp4` (**v1**, Full HD 9:16, 14.80 s, 888 frames).
- Caption (baked; `--nocap` = base): "Same car, same dune: only the ^TIRE PRESSURE^ differs" / "~15 psi~ or ~35 psi~: who reaches the ^TOP^ first?" (same engine, same throttle: both floored; the only other difference is Mochi's stop to let air out, which is part of the pressure choice).

## Story (clip times, sim values; clip 0 = sim 0.7 s)
- Split screen, one camera per car (Mochi top lane, Bolt bottom lane), a mini-map strip on top with the whole dune, the gold TOP flag and both cars ("TOP in n m"). Generic boxy open-top 4×4s (round lights, no grille slots, no logos), the characters in the driver's seat.
- Frame 0: Mochi stopped, valves puffing, needle at 26 psi ("LETTING AIR OUT (sped up)": an onboard deflation system, the 1.5 s stop is shown sped up); Bolt already 3.6 m off the line at 35 psi, sand spraying.
- 0.9-3.1 s "BOLT LEADS" (he is 10-18 m ahead on the packed flat: 28.4 vs 9.9 m at 3 s).
- 4.0 s Bolt reaches the soft face: sinkage 1 → 13 → 17 cm, slip 34 %, the car slows; **5.26 s STUCK** at 42.5 m (wheels spinning, rooster tail, sinks to 26 cm, sand piles on his bonnet).
- Mochi reaches the face at ~4.2 s: 15 psi, footprint 24.5 vs 12.1 cm, ground pressure 133 vs 271 kPa, sinkage 6 → 12 cm, slip 2-16 %, steady climb. **6.55 s LEAD CHANGE**.
- **10.50 s Mochi crests the TOP** (70 m) = the cadence: "MOCHI WINS"; she rolls onto the summit flat. Result card: "15 psi: 2× longer footprint, half the ground pressure" / "deepest rut: Mochi 12 cm · Bolt 26 cm".
- 11.4 s Bolt lets his air out too (hiss, needle 35 → 15), sheepish smile; he stays stuck: his wheels already sit in a 26 cm rut (the brief's "creeps free" is not what the model gives, so it is not shown).
- Dissolve 14.2-14.8 into the pre-roll.
- Brief deviations (truth over brief): lead change 6.55 s (brief 9.2), crest 10.5 s (12.8), Bolt does not get free.

## The physics (scenes/dune_deflate.py `run()`)
- Car 2,000 kg (4.9 kN per wheel), wheel R 0.38 m, wheelbase 2.7 m. Drive force 9 kN for both (floored) up to 90 kW, cruise limit 8 m/s.
- Tire: area A = W / (p_inflation + 30 kPa carcass), footprint L = A / 0.15 m; ground pressure p_g = p_inflation + 30 kPa (35 psi → 271 kPa, L 12.1 cm; 15 psi → 133 kPa, L 24.5 cm).
- Bekker sinkage z = (p_g / (k_c/b + k_φ))^(1/n) × (1 + 1.2 slip), n 1.1, k_c 0.99 kN/m^(n+1) (Wong, dry sand); k_φ 40 MN/m^(n+2) on the packed flat, 3.0 → 1.5 MN on the face (1.5 = Wong's dry sand; the brief's 0.5 would sink a 35 psi tire 57 cm). The rut deepens over ~3 m of travel.
- Resistance: compaction R_c = b k z^(n+1)/(n+1) + tire hysteresis (0.012 + 0.35/psi)·W per wheel; slope M g sin θ, face 10° → 20° over 40 m (flat 0-30 m).
- Janosi-Hanamoto traction (A c + W tan φ)(1 − K/(sL)(1 − e^(−sL/K))), c 1 kPa, φ 31°, K 1 cm; the slip is solved so traction = drive force; a longer footprint gives more traction at the same slip. Stuck (v = 0, drive on): slip 100 %, digs 5 cm/s to 26 cm.
- Note: with honest numbers the soft tire is NOT slower on the flat; Bolt's lead comes only from Mochi's deflation stop.

## Nerd stats
- Per lane (≤3): psi gauge, GROUND kPa, SINK cm (red above 15 cm). Mini-map: positions + "TOP in n m". Banners: LETTING AIR OUT (sped up), BOLT LEADS, STUCK!, LEAD CHANGE!, MOCHI WINS.

## Sound
- **Piece:** I. Albéniz, "Rumores de la Caleta (Malagueña)", Recuerdos de viaje Op. 71 No. 6 (1887; d. 1909, PD), from the original PIANO score (Mutopia-2006/12/29-898, Public Domain edition), `<SOUNDFONTS_DIR>\scores\albeniz_rumores_caleta\` + SOURCE.txt. Played as music at a steady tempo (dotted quarter = 100): the ostinato bars leading into bar 26's A, where our A-major tutti lands on the crest. Replaces the brief's "Asturias (Leyenda)" (no PD piano note data reachable). Not used elsewhere (grep 2026-10-31).
- Arrangement: harp + piano + pizz on the guitar-like chords, piano + cello on the bass line, contrabass octave on the downbeats; A-major cadence (timpani, strings, brass, harp, piano) + held strings.
- SFX: soft low sand "tik" on the eighth grid per moving car (16ths while a wheel spins), gain ∝ wheel speed; two quiet tonal engine hums (pitch ∝ wheel speed); a band-limited hiss only while a pressure is dropping; dings on STUCK and the lead change.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 888 frames = 14.80 s. Muxed −14.00 LUFS, peak −2.00 dBFS, last 0.5 s −240 dBFS.
- RMS/s: −18.5 −18.1 −18.0 −17.5 −16.7 −17.0 −16.3 −15.8 −15.5 −15.6 −13.6 (cadence) −14.1 −26.8 −33.9.
- flash_check PASS (0). Seam mean |delta| 0.63 (good band).
- Side safe zone: cars x ~330-600 (camera anchor 0.43w), lane HUDs 114-414, mini-map 110-905, banners and result card inside 0.10-0.84w; lane scenery runs edge to edge (decoration).
- Frames read from the mp4: 0.05, 2.0, 5.5, 10.6, 13.0, 13.5; stills at 0, 2.5, 5.5, 7.0, 10.5, 10.7, 11.0, 13.0.

## Args
- `--toff` (0.7), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## v2 (2026-11-01, owner review: "besides rotating tires it's hard to tell they are moving")
- `--v2`, same sim. Depth layers, each scrolling at a fixed fraction p of the camera travel: sunset horizon glow + low sun (p 0.02), clouds (0.06), a hazy far ridge (0.12) with a 5-camel caravan walking RIGHT along it (so when Bolt is stuck the camels overtake him; their walk can't read as the car moving), the existing dunes (0.25), date-palm groves (0.5), and ground pebbles + dry scrub tufts fixed to the ground (p 1). Tyre tracks: chevron tread marks (near + far wheel) pressed into the sand behind each car, depth-shaded from the logged sinkage, plus the trough lip line.
- Deliverable `<VIDEOS_DIR>\MochiAndBolt\review\fixes_1101\dune_deflate_v2.mp4`. 14.80 s, -14.00 LUFS, peak -2.00, silent tail, flash 0, seam 0.81. v1 -> archive/dune_deflate_v1.mp4.

## v3 (2026-11-01, owner review: "instead of split screen, let them be in the same screen and start together; main view is on whoever is first, and a small box in the corner shows who's out of screen")
- `--v3` (implies the v2 layers; v1 and v2 reproduce unchanged without it). ONE shared view (y 352-1328): two lanes on the same dune, Bolt the far lane (surface line), Mochi the near lane 88 px lower (drawn in front). `to_px` reads the view being drawn (`VW`).
- **Start together**: both launch at sim t = 0 from a painted START line across both lanes; Mochi's onboard system lets the air out WHILE she drives (35 -> 15 psi over T_DEF 1.5 s, still labelled "sped up"). v1/v2 had her stop 1.5 s while Bolt left at -0.6 s. Clip 0 = sim 0.25 (`--toff`).
- **Honest result of the new start**: no real lead change. They run level on the packed flat (Bolt is never more than 0.5 cm ahead; the soft tyre slips less, so Mochi creeps ahead). "MOCHI PULLS AHEAD!" + ding at 4.45 s = the first frame she is 1.0 m in front (`lead_time()`, PULL_M); "BOLT LEADS" / "LEAD CHANGE!" are not shown in v3 (they would be false).
- Clip times: Bolt STUCK 6.31 s at 42.4 m (6.6 m behind, still in frame: the STUCK! banner rides above his car); Mochi crests 9.43 s (= cadence, "MOCHI WINS" at the top), Bolt 27.5 m behind; he lets his air out at crest + 0.9 s and stays stuck (26 cm rut). D 13.73 s (824 frames), dissolve into the pre-roll.
- **Camera**: path distance of the LEADER (max of both; continuous because they swap only when level), leader anchored at 0.60 w. **Inset** (x 114-498, y 1046-1316, zoom 0.64): the trailing car's own live view, shown while his front bumper is left of x 100 (inside the tall-phone crop), 0.15 s fade/scale-in; frame and name tag in his colour, "n m behind", red "STUCK!" while he sits stuck. On from 6.92 s to the end.
- HUD: both psi/GROUND/SINK panels at the top of the view (Mochi left 114-414, Bolt right 601-901). Banners on one row (y 560). Mini-map, result card and caption unchanged.
- **STAGED 4K** (2026-11-02): `--v3 --label d4k` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-10\2_dune_deflate.mp4` (events json byte-identical to v3). 2160x3840 h264 yuv420p 60 fps, 824 frames, -14.00 LUFS, peak -2.00, flash 0, seam 0.41.
