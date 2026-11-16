# quake_damper — Every quake is 2× STRONGER: weight at the BOTTOM or TOP, which tower SURVIVES? (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 5, wave 2) + Coordinator note: lab shake-table model only, the tower tips sideways onto a crash mat, no building-collapse imagery (no windows, people, city, dust, no straight-down pancake). New scene file; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\quake_damper.mp4` (**v1**, Full HD 9:16, 15.02 s, 901 frames).
- Caption (baked; `--nocap` = base): "Every quake is ^2× STRONGER^" / "Weight at the ~BOTTOM~ or ~TOP~: which tower ^SURVIVES^?".

## Story (clip times, sim values)
- A blue shake table in a dark test lab, two identical 12-floor steel-frame models (open frames with X bracing, no windows), a crash mat on the floor to the left. Both add +5 % of the tower's mass: Mochi a grey block bolted to the ground floor, Bolt a gold ball on cables hung inside the top 2 floors. They sit on their roofs.
- Frame 0: the table has been shaking for 4 s (pre-roll), R1 sway visible; "SAME TABLE · SAME +5% WEIGHT". Rounds = one music bar (2.67 s); QUAKE ×2 at 2.72 s, ×4 at 5.38 s, ×8 at 8.05 s (badge in the seismograph strip + banner).
- Peak inter-storey drift per round, Mochi / Bolt: 0.57 / 0.12 %, 0.99 / 0.23 %, 1.88 (amber) / 0.45 %, R4: Mochi cracks storeys 4 (9.01 s), 3 and 5 (9.06 s) / Bolt 0.91 %. Roof sway R3 1.81 vs 0.45 cm. During R3 "base weight: 0 cm less sway".
- 9.18 s Mochi's tower hinges at storey 4 and the 9 floors above tip SIDEWAYS (rigid tip about the hinge, then off the hinge onto the mat, flat), landing 10.44 s in 3 slab chunks with clangs; Mochi slides off her roof onto the fallen frame, wow → annoyed stare. "TOPPLED!".
- Table winds down 10.17-10.67 s; 10.72 s (bar 5's B-flat) "BOLT WINS"; the ball settles; side text: "the gold ball swings against the sway and does 85% of the tower's damping · Bolt's peak drift: 0.9% (limit 2.5%)". Dissolve 14.42-15.02 into the pre-roll.
- The white/gold arrows on Bolt's roof and ball show their true velocities: opposite directions.

## The physics (scenes/quake_damper.py `simulate()`)
- Shear-building model: 12 floor masses (1 kg), storey stiffness tapering linearly to 50 % at the top (thinner upper columns), scaled so f1 = 1.50 Hz (f2 4.17, f3 6.84 Hz). Rayleigh damping 2 % in modes 1-2. Base = table displacement A sin(2π·1.5 t), A = 0.24 mm × 2^round (0.24 / 0.48 / 0.96 / 1.92 mm), ramp-in 0.5 s, 4 s pre-roll. dt 1/1200 s, semi-implicit Euler.
- Mochi's base block rides the table, so her tower's equations are exactly the bare tower's (that is the honest "0 cm less sway").
- Bolt's TMD: pendulum m_d = 5 % of the tower (0.6 kg) on the roof, Den Hartog with the modal mass (mode 1 normalised at the roof, M1 = 5.56 kg → μ = 0.108): f_d = 1.354 Hz (L = 13.6 cm, drawn true), ζ_d = 0.173. Max ball offset 2.4 cm.
- Failure: storey drift > 2.5 % cracks it (stiffness × 0.4, red joints); 2+ cracked storeys = failure, hinge at the cracked storey with the largest drift. Topple: thin-rod tip about the hinge to 0.95 rad, then off the hinge to flat on the mat (gravity-timed), 3 slab chunks slide apart; scripted after the sim's failure, direction toward the mat.
- Drawing: sideways motion ×6 (labelled "motion drawn ×6 sideways · lab model, 12 floors, 1.2 m"); every number is the model's true value. Damper share = ∫c_d v_rel² / (that + ∫ vᵀCv) up to the cadence = 85 %.

## Sound
- **Piece:** S. Rachmaninoff, Prelude in B-flat major Op. 23 No. 2 (1903; US PD, EU PD since 2014), bars 1-4 at quarter = 90 (one beat = one 1.5 Hz shake cycle, one bar = one round), our B-flat tutti on bar 5's downbeat. Source: Mutopia-2014/08/15-1960, `<SOUNDFONTS_DIR>\scores\rachmaninoff_prelude_op23_2\` + SOURCE.txt. Replaces the brief's Piano Concerto No. 2 (no PD note data reachable). Not used elsewhere (grep 2026-10-31; Op. 3 No. 2 and Op. 23 No. 5 are different works).
- Arrangement: the left-hand surge on piano (lowest notes up an octave) + cello on the beats, right-hand chords on piano + horns + strings (folded ≤ F5), B-flat octave pedal (cello + contrabass), timpani on each round start, a growing velocity ramp; tutti cadence + harp + held strings.
- SFX: a steel-frame tick at every roof sway peak (gain ∝ sway, harmony-locked), bolt pings when the quake doubles, a clang per cracked storey, 3 clangs on the mat landing, a soft thump when Mochi lands. No rumble bed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 901 frames = 15.02 s. Muxed −14.00 LUFS, peak −2.00 dBFS, last 0.5 s −240 dBFS.
- RMS/s: −18.6 −18.8 −17.7 −17.4 −17.5 −17.1 −16.6 −15.9 −15.8 −15.2 −14.5 −13.0 (cadence) −23.3 −31.7 −41.2.
- flash_check PASS (0). Seam mean |delta| 0.67 (good band).
- Side safe zone: towers x 492-870, table 476-890, mat 104-462, fallen frame 120-480, characters, HUD and text inside 0.10-0.84w.
- Frames read from the mp4: 0.05, 6.5, 9.3, 9.7, 12.5; stills at 0, 6.2, 8.9, 9.3, 9.6, 10.0, 10.7, 13.0.

## Args
- `--a1` (0.00024 m), `--taper` (0.5), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/quake_damper.py --label k4ship` (defaults) → `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-08\2_quake_damper.mp4`. h264 yuv420p 2160x3840 @60, 901 frames 15.02 s; -14.00 LUFS, peak -2.00 dBFS, last 0.5 s silent; flash PASS (0); seam 0.51; events json bit-identical to v1. Frames read at 0.5 / 12.5 s. FHD review file → `archive\quake_damper_fhd.mp4`.
