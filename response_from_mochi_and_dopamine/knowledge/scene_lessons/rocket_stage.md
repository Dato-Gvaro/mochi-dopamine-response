# rocket_stage — One BIG tank vs 3 STAGES: who reaches ORBIT? (batch51, 2026-10-25)

- Brief: docs/BRIEF_batch51.md ("rocket_stage") + BRIEF_batch50 lessons. New scene file; lib/ and tools/ untouched. Not the rejected `rocket_stages` (batch37: no music, time-lapse clock, sea splash).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch51\rocket_stage.mp4` (**v1**, Full HD 9:16, 15.70 s, 942 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "One ~BIG~ tank vs ~3 STAGES~:" / "who reaches ~ORBIT~?"
- **Twist:** Bolt wins by being clever: he throws away his empty tanks. Mochi's one big engine launches harder and leads for 9 s, but she hauls a 130 t empty tank and her coast tops out 36 km under the line.

## Layout
- Rockets at x 362 (Mochi) and x 660 (Bolt), side by side. Altitude tags (km, big) at x 178 / 842 at window height, with a pill under each: "1 BIG TANK" → "NO FUEL"; "STAGE 1/3" → "2/3" → "3/3" → "CAPSULE" → "IN ORBIT".
- Rockets: rounded noses, the character in a gold-rimmed window (no military styling). Mochi: one coral tank with a big "1" and a gold fuel slot, one engine. Bolt: mint stack, stages numbered 1-2-3 bottom-up, each with its own fuel slot and engine, decoupler rings.
- World: log-scaled altitude (y = YL + S·(Λ(400) − Λ(h)), Λ = ln(1 + h/0.6 km)), so landmarks spread out: launch pads + towers + smoke (0 km), cloud deck "CLOUDS · 10 km" (fades out by ~100 km), "KÁRMÁN LINE · 100 km · SPACE" (dashed cyan), "ORBIT · 400 km" (dashed gold, a small ISS drifting on it) — in view from frame 0 at y 372.
- Camera: one smooth rise + zoom, no shake. The ORBIT line rides 372 → 600, the rockets' midpoint 880 → 665 (the zoom follows from those two); frozen after the cadence. A rocket's reference blends from its base (on the pad) to its nose (above 40 km). The sky darkens with altitude, stars fade in above ~35 km, Earth's blue curve rises in the bottom. Faint speed streaks slide past each rocket at a rate set by its speed.
- HUD (y 1352–1544): "FIRST TO ORBIT (400 km) WINS"; per side "MOCHI · 1 BIG TANK" / "BOLT · 3 STAGES", MASS (t, pops at each drop), a LEADING / FUEL EMPTY / WINNER / TOO SHORT pill, a FUEL bar.
- Key content inside x 0.10–0.84w; only the sea, clouds, Earth and tumbling spent stages go wider.

## The physics (integrated, not scripted)
- a = F/m − g; each burn empties its tank at a steady rate (thrust = vₑ·ṁ); a separation removes that stage's dry mass. One time-lapse scale folded into g (2.75 km/s² video), vₑ 54.9 km/s (video units). Only km and tonnes are shown.
- Same capsule (10 t), same tank build (shell = 42% of the fuel it holds), same exhaust speed.
- Mochi: 300 t fuel, 130 t empty tank + engine, 440 t at liftoff, T/W 1.44. Empty at sim 7.8 (118.6 km). Her ballistic max is 364 km (sim 21 s).
- Bolt: stages of 127.6 / 110.8 / 50.2 t fuel (289 t total, *less* than Mochi), dry 55.3 / 48.2 / 22.6 t, 424.7 t at liftoff, T/W 1.28. Acceleration jumps at the drops: ×1.42 (2.28 → 3.24) and ×1.36 (8.24 → 11.17).
- Parameters fitted (scipy differential evolution, scratch scripts) so that: separations sit on beats, Mochi's burnout on a beat, the lead change ≈ 9 s, Bolt crosses 400 km on the cadence, Mochi's max ≈ 350–365 km.
- Spent stages fall with 3× g (air-drag cheat) and drift outward while tumbling. At the line the capsule's climb is damped onto it (insertion), solar wings unfold.

## Timeline (clip s; clip = sim + 0.6)
- **0.0 s:** both just off the pads (0.8 / 0.5 km), launch smoke, flames, pickup note. Mochi LEADING.
- **0.5 / 1 / 2 s:** 1.7 vs 1.1 km → 3.0 vs 2.0 → 7.2 vs 4.9 km; ticks climb, the ground drops away, the rockets rise past the cloud deck.
- **3.6 s (bar 2 beat 3):** STAGE 1 DROPPED (13 km): clunk + puff, −55 t, "LIGHTER = FASTER", flame grows.
- **7.8 s (bar 5 downbeat):** STAGE 2 DROPPED (80 km), −48 t.
- **8.4 s:** Mochi: FUEL EMPTY (119 km), "...COASTING"; her drone sags and stops.
- **9.83 s:** BOLT TAKES THE LEAD (both ≈ 168 km).
- **10.2 s (bar 6 beat 2, the tune's high E-flat):** STAGE 3 DROPPED (194 km), −23 t; the 10 t capsule coasts on.
- **13.2 s (cadence, bar 8):** Bolt crosses ORBIT: "BOLT WINS!" / "IN ORBIT!", gold glow + sparkles, wings unfold; Mochi at 263 km, red dashed line "MAX 364 km: 36 km SHORT!", annoyed, drifting lean. HUD WINNER vs TOO SHORT (10 t vs 140 t).
- **15.1–15.7 s:** dissolve into the pre-roll (the liftoff); the HUD switches at the midpoint.

## Sound (music first)
- **Piece:** Gustav Holst, "Jupiter, the Bringer of Jollity" (The Planets, 1914–16; Holst d. 1934, PD), the big tune — epic, heroic, a big arrival. Not on any used/banned list; no other scene uses it (boss_fight uses "Mars").
- **Source:** Holst's own hymn setting "Thaxted" (1921), Mutopia-2005/01/18-527 (engraving placed in the **public domain**), `<SOUNDFONTS_DIR>\scores\holst_jupiter_thaxted\` (`Thaxted.ly`, `.mid`, `-let.pdf`, `SOURCE_mutopia_527.txt`). Tune, bass and chord symbols hand-copied from the .ly, transposed C → E-flat (Jupiter's key). Downloaded 2026-10-25.
- **Excerpt:** pickup + bars 1–8 (phrases 1–2), 3/4, one steady tempo, quarter = 100 (the source MIDI's tempo); cadence = bar-8 downbeat = Bolt at the line. Bar 7 beat 3 uses the Dm/F of the hymn's last phrase.
- **Arrangement** (lib/orchestra, MuseScore_General): violins on the tune, strings + horns an octave down; brass + flute join on phrase 2; strings pad + harp pulse on every beat; cello/contrabass bass (pizz from phrase 2); timpani on the separations and phrase-2 downbeats, a roll into the cadence; E-flat tutti cadence (strings, violins, brass, horns, contrabass, timpani, harp sweep). CC11 crescendo 0.66 → 1.0.
- **SFX** (all tonal; energy above 4 kHz 0.41%):
  - engine drones: a low tonal drone per rocket on the bass of the harmony (sine + 4 harmonics, 40 ms glides, a gentle 7 Hz throb), level = thrust; Mochi's an octave lower and sagging at burnout; Bolt's brighter per stage;
  - altitude milestones (0.5, 1, … 9, every 5 km to 100, every 10 km after): a soft tick climbing the E-flat scale, snapped to the 16th grid, chord-fitted; bells at 10 and 100 km;
  - each separation: a crisp tonal metal clunk + a tonal "fwomp" puff + three falling tumble ticks + a pop tick for the mass readout;
  - lead-change bell, Mochi's 3-note sputter, the orbit chime (rising E-flat arpeggio) + 4 wing ticks, a soft falling glide for Mochi in the hold.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS); the last 0.5 s zeroed; 0.25 s of silence padded so the muxer's -shortest keeps all 942 frames.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 942 frames = 15.70 s.
- −14.01 LUFS, peak −2.37 dBFS, last 0.5 s ≤ −80 dBFS.
- RMS/s: −17.9 −17.8 −17.8 −16.5 −17.2 −18.6 −15.9 −15.7 −15.6 −17.1 −15.7 −17.0 −16.9 −14.3 (cadence) −15.6 (hold), then the silent tail.
- SFX events/s: 5 8 8 10 7 5 8 16 15 10 16 9 9 12 0 (hold) 0.
- flash_check PASS (1 flash, at 15.48 s: the loop dissolve from space back to the blue launch sky; mean luminance 0.08).
- Seam: pre-encode last → first 0.37 vs adjacent 0.38 (continuous); encoded check_clip 0.909 (I/P drift through the dissolve; adjacent encoded frames there are 1.0–1.15).
- Frames read from the mp4: 0.5, 1, 2, 3.65, 7.85, 8.5, 9.95, 10.3, 13.3, 14.8; 1:1 crops of the stage-1 drop (3.65) and the end state (14.8).

## Doubts
- **Mochi does not fall back on screen.** With honest gravity a coast lasts about as long as the burn, so a rocket that runs dry "just short" keeps rising for many seconds. She runs out mid-race (119 km), coasts, and at the cadence a red dashed "MAX 364 km: 36 km SHORT!" line shows where she will top out; she only drifts (a slow lean) in the hold. The brief asked for empty just short + falling back.
- From 10.2 s nothing is burning (both coast); the streaks, counters and chime carry the motion.
- The lead change (9.8 s) comes from Mochi slowing on her coast + Bolt's stage 3, 2 s after his 2nd drop.
- Cartoon scale: on the log axis a rocket is ~20 km "tall" at liftoff, so the 10 km cloud deck sits at window height in the first 2 s. Heavy tanks (shell 42% of fuel) make the dead-weight point strong.
- "Thaxted" is also the tune of the patriotic hymn "I Vow to Thee, My Country"; we use it as Holst's Jupiter (instrumental, no title shown). Flagging in case the coordinator treats it like the 1812 anthem.
- Event rate dips to 5/s in seconds 0 and 5.

## Args and cost
- Physics: `--g --ve --eps --eng --tla --seps --fuels --mempty`; camera `--h0 --yl0 --yl1 --ym0 --ym1`; `--gfall`; sound `--sfx --drone --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim is instant; Full HD render ~2.5 min at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)
