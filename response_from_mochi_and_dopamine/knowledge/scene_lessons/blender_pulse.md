# blender_pulse — Same ice, same blender: MAX or PULSE, who gets all SNOW first? (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 1). Started by a builder that died at 00:19 (file untested, defaults never reached SNOW); finished 2026-10-31 afternoon. lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\blender_pulse.mp4` (**v2** label, Full HD 9:16, 13.74 s, 824 frames).
- Caption (baked; `--nocap` = base): "Every blade ~HIT~ splits ice in 2, down to SNOW" / "~MAX~ or ~PULSE~: who gets all SNOW first?". Rewritten from the brief's "Every ice piece the blade HITS splits in 2": SNOW pieces are hit and do NOT split, so that line was false.

## Story (clip times, seed 0)
- Frame 0 = sim 1.2 s: both motors already running, cubes cracked (28 / 18 pieces), "SAME ICE · SAME BLENDER". Mochi sits on MAX (20,000 rpm steady); Bolt hops on PULSE (0.40 s ON / 0.25 s OFF, period tightening 0.65 → 0.50 s).
- 1 s 143 / 50, 3 s 879 / 384: "MOCHI LEADS", then a live "MAX ×n" banner (×2.3 at 3 s, up to ×3.2).
- ~4.0 s her slush is flung up the walls; 5.33 s AIR POCKET reaches 80 % (dashed dome, "9 cm", ICE AT BLADE 0 %): "AIR POCKET! THE BLADE SPINS IN AIR". Her count freezes at 1,619.
- Bolt: a slump every OFF, a crunch burst every ON: 1,077 at 5.5 s, 1,516 at 7 s. 7.42 s "LEAD CHANGE!".
- 8.32 s → 10.84 s: labelled "FAST-FORWARD ×2" through Bolt's last pieces (honest exponential tail: the last chunks are diluted in snow and only reach the blade now and then; 6 s of sim shown in 2.5 s).
- 10.84 s Bolt hits SNOW 2,048: "SNOW! 2,048", cadence. Mochi lets go of MAX, her bridge drops into the blade and she presses again: a late crunch to 1,911 (too late). 11.6 s "BOLT WINS" + "pulsing drops the ice back onto the blade". Dissolve 13.14-13.74 into the pre-roll.
- MAX leads 54 % of the clip; lead change 3.4 s before SNOW (brief targets ≥55 % and ≥2 s; the 54 % is the sim's truth).

## The physics (honest model, scenes/blender_pulse.py)
- 2D PBD discs (cKDTree contacts, 6 substeps × 8 iterations, shock propagation 0.2), gravity, tapered jug walls (wall restitution 0.3), velocity caps 3,200 px/s free / 1,800 px/s in dense slush.
- 8 cubes r 36 px (3 cm). Split = 2 equal-area halves (r/√2); gen 8 (r 2.25 px, 1.9 mm across) = SNOW, immune. All-snow = 2,048 exactly.
- Blade: 4.5 cm, 20,000 rpm → 94 m/s tip; swept band half-height 28 px above the floor; hit rate 4.0/s × w² × max(1, (22 px / r))² for pieces in the band (a whole cube often bounces off); non-hits get washed out at 10/s × w²; children kicked at 0.15 × tip speed capped at 1.5 m/s and immune for 60 ms. Needs ≥40 % speed to break ice. Spin-up 95 % in 0.08 s.
- Vortex (toroidal: out along the floor, up the walls, in at the top, down the centre) 2.0 m/s × w², 0.35 s spin-up lag; drag on pieces ∝ 1/r.
- Air pocket: target radius 4.6 cm × spin × fine term, spin = (vortex/full − 0.8)/0.2 (only a fully developed vortex), fine = (share of mass in gen ≥ 6 − 0.6)/0.3; builds with τ 0.9 s, collapses with τ 0.04 s; pieces are pushed out of the bubble. Pulsing caps the vortex near 60-80 %, so Bolt's pocket never forms.
- Tuning log: the 00:19 defaults (r0 45, vortex 1.3 m/s, pocket on w², fine = gen ≥ 4) never reached SNOW in 17 s; 12 runs swept λ, R_ref, wash, band, vortex, velocity cap, cube size and the fine threshold. Every run shows the same honest tail (the last ~5 % of pieces take ~5 s); the FAST-FORWARD ×2 label is the fix instead of a fudged hit rate.
- Nerd stats (per jug): MOTOR rpm + bar (steady vs pulses), BLADE TIP m/s, ICE AT BLADE % (red when ≤25 %), the pocket's dashed outline + "9 cm", big PIECES counter with ×2 pops, SNOW meter with the 2,048 goal mark from frame 0, footnote "SNOW = every piece under 2 mm · ×2 = pieces doubled".

## Sound
- **Piece:** L. v. Beethoven, Violin Concerto in D Op. 61, III. Rondo (1806, PD), Mutopia PD edition `<SOUNDFONTS_DIR>\scores\beethoven_violin_concerto3\violin_concerto_3.mid` (+ .rdf, SOURCE.txt). The brief's Rossini "La gazza ladra" overture had no PD score/MIDI reachable (Mutopia, Commons, midiworld; IMSLP behind a bot check).
- One note per split (merged to ≤1 per 60 ms) walking the rondo's solo line folded into the low/mid register, strings + piano, cello/contrabass octave bass on the dotted-quarter beats, pizzicato on Bolt's pulse starts; D major cadence on SNOW (timpani, strings, harp, piano, held strings).
- SFX: a crisp pitched ice crunch per split (+13 ms), button clicks on each pulse, dings on the pocket and the lead change, a quiet tonal motor hum per jug (pitch follows the blade; +3 semitones in the air pocket). No hiss/whoosh beds.

## Checks (v2 encoded, Full HD)
- h264 High yuv420p 1080x1920 @ 60 fps, 824 frames = 13.74 s. Muxed -14.00 LUFS, peak -2.01 dBFS, last 0.5 s -90 dBFS (silent).
- RMS/s: -18.3 -16.5 -15.5 -16.6 -17.3 -16.5 -17.9 -15.8 -16.3 -16.2 -17.3 -13.6 (cadence) -25.3 -54.3. Notes/s: 15 15 15 15 13 11 12 12 13 11 5 0 (the split notes are capped at 1 per 60 ms; the 10-11 s bucket is the end of Bolt's tail + the cadence).
- flash_check PASS (0, mean lum 0.046). Seam mean |delta| 2.64 vs 2.16 (frames 0→1) and 3.77 (100→101): this scene is full of fast small pieces, the seam is as continuous as any frame pair (dissolve into the pre-roll).
- Side safe zone: jugs x 122-897 (the right jug wall at 0.83w), characters, counters and text inside 0.10-0.84w.
- Frames read from the mp4: 0.05, 1.0, 5.5, 7.5, 9.0, 10.9, 11.8, 13.7; stills at 0, 1, 3, 5.5, 7.5, 9.33, 10.92, 12.67.

## Args
- `--seed`, `--lam`, `--rref`, `--lamp`, `--wash`, `--fine`, `--fgen`, `--band`, `--avon`, `--amax`, `--vdense`, `--rpmax`, `--taup`, `--r0`, `--sub`, `--iters`, `--shock`, `--ff` (2; 1 = no fast-forward), `--sfx`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--resim`, `--nocap`, `--label`.
- Sim ~5 min (cached to output/blender_pulse_sim_<hash>.pkl); Full HD render a few minutes at 2 encoder threads.

## Outcome
- (fill after upload)

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/blender_pulse.py --label k4ship` (defaults) → `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-08\1_blender_pulse.mp4`. h264 yuv420p 2160x3840 @60, 824 frames 13.73 s; -14.00 LUFS, peak -2.01 dBFS, last 0.5 s -90 dBFS; flash PASS (0); seam 2.46 (scene norm); events json bit-identical to v2. Frames read at 0.5 / 11.8 s. FHD review file → `archive\blender_pulse_fhd.mp4`.
