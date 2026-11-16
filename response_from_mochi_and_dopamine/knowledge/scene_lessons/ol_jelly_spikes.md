# ol_jelly_spikes (DopamineEXE, batch62 #1)

## v2 (2026-10-31, owner review of v1)
- Owner: (1) different PD music, our own synthesis; (2) "viewers must SEE the difference between the 5 balls at a glance": a visibly distinct inside per ball, labelled.
- **Materials** (look only; the physics is unchanged: same skin, the fill packed firmer or softer = SOFT %): HARD GEL 0% (opaque deep red, hard specular) · SILICONE 25% (opaque milky peach, satin) · HONEY GEL 50% (translucent amber, 5 air bubbles, caustic) · WATER GEL 75% (clear, fresnel rim, 8 bubbles, caustic) · GLITTER GEL 100% (translucent violet, 30 twinkling flecks). Bubbles/flecks sit in each ball's polar frame and follow the skin as it deforms. Lane labels: material name (lane colour) + "SOFT n%"; strain bars moved 20 px down. Finale: "SURVIVOR: GLITTER GEL" / "100% soft · its skin peaked at 57% (tears at 60%)". No "jelly/slime" on screen.
- **Music:** Tchaikovsky, Swan Lake, "Danse napolitaine" tarantella (PD; Mutopia PD edition read at runtime, `<SOUNDFONTS_DIR>\scores\tchaikovsky_danse_napolitaine\SOURCE.txt`), quarter = 140; impacts on score beats 88/92/96/100 (+ timpani), the piece's own E♭ cadence (beat 104) = the survivor (B♭7 → rich E♭ chord + harp). Trumpet lead + strings an octave down + pizzicato chords + horns + contrabass/tuba. SFX unchanged (pitched to E♭ chord tones). Aida (v1) is free again.
- Sim, timeline, caption unchanged. v1 archived as `DopamineExe\archive\ol_jelly_spikes_v1.mp4`.
- Checks (encoded): h264 yuv420p 1080x1920 60 fps, 9.53 s; **-14.01 LUFS**, peak -6.04 dBFS, last 0.5 s silent; flash PASS; seam 0.277. Stills at 0, 0.08, 1.83, 5.5, 7.8 s; 1:1 crop of the five balls at frame 2 (encoded).
- Titles: `Hard gel vs glitter gel: which ball survives the spike? 💥 #satisfying #physics #shorts` · `Every drop 3 m higher… until only ONE ball survives 💥 #satisfying #physics #shorts` · `0% vs 100% soft: which ball survives the spike? 💥 #satisfying #physics #shorts`. Pinned: `the hard one didn't even last a second. which one did you pick?`

## v1 (2026-10-31)
Five gel balls, SOFT 0% (rock hard) → 100% (squishy), dropped onto five steel spikes. Every round a fresh ball of each surviving softness falls from 3 m higher (3, 6, 9, 12 m); a ball whose skin tears is OUT. Shown at SLOW-MO ×8 (labelled), ramping to real time after the last round.

- Caption (baked; `--cap ''` = base): `Every drop is ^3 m HIGHER^…|until only ~ONE~ survives the spike`. True: +3 m each round, exactly one survivor.
- **Brief deviation (truth over brief):** the brief asked for 2× heights (0.5 → 16 m). With a lossy gel fill, the tear heights come out roughly LINEAR in softness (0% ≈ any drop, 25% ≈ 4.0 m, 50% ≈ 7.5 m, 75% ≈ 10.2 m, 100% ≈ 12.9 m; probe at P_HARD 17600, visc 300). A doubling ladder can't give one pop per round: 0.5-8 m gave pops only in R2 + R5 (three at once), and 16 m pops everyone. The +3 m ladder gives exactly one pop per round. Music changed from the brief's Lohengrin to Verdi's Aida Triumphal March (earlier builder's choice; Lohengrin had no usable source).
- Result (sim decides): R1 3 m 7.7 m/s: **0% pops** at 0.08 s (pre-stretched to 57%; the tip adds the last 3%). R2 6 m 10.9 m/s: 25% pops (65%). R3 9 m 13.3 m/s: 50% pops (65%). R4 12 m 15.3 m/s: 75% pops (60.4%, barely); **100% survives, peak 57.3%** (near miss). Order is monotonic: harder = pops first.

## Model (`simulate`, deterministic, ~105 s CPU)
- Pressure soft body per ball: 128-node skin ring, edge springs (tension K 1.6e6 × strain, no compression), edge damping 0.15 critical, isothermal gas P = P0·A0/A, gravity, DT 4e-5 s.
- Softness s sets inflation P0 = P_HARD·(1 − 0.9 s) (P_HARD 17600) → skin pre-stretch e0 = P0·R/K: 0.572, 0.443, 0.315, 0.186, 0.057.
- **Gel fill viscosity** (new in this build, `--visc` 300 1/s): momentum-conserving internal drag on node motion relative to the ball's CoM. Without it the restitution was 0.85-0.94 (unreal for gel) and the survivor bounced off-screen at the finale; with it e ≈ 0.7 (hard) → 0.2 (soft) and the survivor settles on its tip.
- Spike: rounded cone, tip radius 3 px, half-angle 12°, Coulomb μ 0.2; base plate. 1 m = 1040 px (ball 10 cm, r 52 px).
- Tear: any skin edge strained past 60% → the edge is cut, the gas vents in ~2 ms, the skin recoils; 46 droplets spray from the tear (seeded rng 62), land on the plate and stay put; torn skins fade ~1 s after the pop.

## Timeline (140 bpm, a round per bar)
- Impacts 0.08 / 1.79 / 3.51 / 5.22 s (pops at the same frames); survivor + cadence 6.94 s; hold 2.0 s; 0.6 s dissolve into frame 0. **9.53 s, 572 frames.**
- Frame 0: all five balls 0.08 s above the tips, roster + ladder meter + 60% red ticks on screen.

## Screen
- Caption 0.12h; roster of 5 dots (red X per pop, gold ring on the survivor) y 356; SLOW-MO ×8 tag; "DROP n m / IMPACT v m/s" readout y 500-544 (fades at the cadence; the finale "SURVIVOR: 100% SOFT" + "its skin peaked at 57% (tears at 60%)" takes that space).
- Spikes tips y 930, plate 1080; lane tags SOFT 0% / 25% / 50% / 75% / 100%; per lane a SKIN STRAIN bar with the red 60% tick + live %, OUT in red.
- Ladder meter y 1300 (3 / 6 / 9 / 12 m); counter y 1500 SURVIVORS 5 → 1 (gold at the end) + "ROUND n/4" pill; watermark 35%.
- Side safe zone: lanes x 188-828 ± 52 → 0.13-0.82w.

## Sound
- Verdi, Aida, Triumphal March theme (PD), Verdi's notes hand-encoded in the scene (LEAD / FAN_HI / FAN_LO / BASS), our own orchestra synthesis; impacts on the bar downbeats (+ timpani); the score's own V → I lands on the survivor (E♭7 → rich A♭ chord + harp). Source notes: `<SOUNDFONTS_DIR>\scores\verdi_aida_triumphal\SOURCE.txt` (the MIDI there is reference only, © sequencer).
- SFX: tonal wet "blup" per impact (A♭ chord tones, +12 ms off the beat), a crisp pitched "pok" per tear, quiet droplet plips.

## Checks (encoded mp4)
- h264 yuv420p 1080x1920 60 fps, 9.53 s; **-14.01 LUFS**, peak -5.85 dBFS, last 0.5 s digital silence; flash_check PASS (0 flashes); seam mean |Δ| 0.252.
- Frames read at 0, 0.08, 0.33, 0.67, 1.8, 2.5, 5.3, 5.5, 7.0, 7.8, 9.3 s; 1:1 crops of the spike row at 0.08, 5.27 and 7.8 s.

## Flags
`--visc` (300), `--k`, `--phard`, `--hold` (2.0), `--resim`, `--dry`, `--audio`, `--still --frame a,b`, `--cap`.

## Upload draft
- `0% vs 100% soft: which ball survives the spike? 💥 #satisfying #physics #shorts`
- `Every drop 3 m higher… until only ONE ball survives 💥 #satisfying #physics #shorts`
- `The hardest ball popped first. The softest one? 💥 #satisfying #physics #shorts`
- Pinned: `the rock hard one didn't even last a second. which one did you pick?`

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/ol_jelly_spikes.py --label k4ship` (defaults) → `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-12\1_ol_jelly_spikes.mp4`. v2. h264 yuv420p 2160x3840 @60, 572 frames 9.53 s; -14.01 LUFS, peak -6.04 dBFS, last 0.5 s silent; flash PASS (0); seam 0.17; events json bit-identical to v2. Frames read at 0.1 / 7.8 s. FHD review file → `archive\ol_jelly_spikes_fhd.mp4`.
