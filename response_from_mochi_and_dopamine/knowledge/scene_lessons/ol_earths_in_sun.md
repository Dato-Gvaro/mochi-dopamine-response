# ol_earths_in_sun (DopamineEXE, BRIEF_dopa_1113 #4)
- FILL + ×N: Earths pour into a hollow Sun in doubling batches until 1,304,000 (NASA NSSDC Sun/Earth volume ratio), then the Sun ignites. Jupiter tag at 1,321 (NSSDC), "1 MILLION… ONLY 80%" at 2^20.
- Review copy + README (facts, sources, rung table, titles): `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_earths_in_sun\`. FHD only (label fhd).

## Model
- Units = Earth radii. FCC lattice, hex layers horizontal, spacing d = (√2·4π/3)^(1/3) = 1.8094 → ONE site per Earth volume, so the level of N sites = the true volume fraction. Cut = the 1,304,000 sites nearest the centre (radius 109.24 vs the Sun's 109.2); drawn shell = cut + 1. Lattice shifted so the lowest layer rests on the shell.
- Fill order: height + 0.55·layer·(1−e^(−r²/60)) (centre of a layer first) + jitter.
- Drawn per frame: the visible wall (outer 1.25 d shell facing the viewer, 42k sites) ∪ the top 1.5 layers ∪ ≤700 falling Earths; depth-sorted sprites. ~42 s FAST, Earth sprites LOD (detailed ≥4 px, else lit dots).
- Camera: px/radius = softmax(250 / pile size, S_F = 362/R_draw); target slides from Earth #1 to the centre with weight (S_F/s)^1.5 (^0.8 threw Earth #1 700 px off at macro: the distance is 108 radii).
- Batch k completes on Thaxted onset B[k] (B = 0,1,2.5,3,…,21), beat 22 = FULL; beat length 0.56 → 0.36 s, the last partial batch 0.19 s (keeps the Earths/s rate climbing).

## Gotchas
- A skewed lattice index grid (x = i·d + j·d/2) needs i over ±2·nx and j over ±R/(d·√3/2), or whole regions are missing (showed as black holes in the pile).
- With a view from above, the bowl's lowest point is NOT the silhouette bottom: draw latitude rings + a floor glow so Earth #1 does not float.

## Sound
- Holst "Thaxted" (Jupiter's big tune), Mutopia 527 (PD): melody strings+horns+celesta, chords strings_slow, bass contrabass/cello, timpani on bar downbeats; B-flat tutti + choir + boom + cymbal swell (no noise) at FULL. Soft tonal knocks per sampled landing.
