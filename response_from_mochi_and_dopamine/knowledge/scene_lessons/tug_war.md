# tug_war — "Every second Bolt's team DOUBLES" / "Mochi adds 3. Who pulls it over the LINE?"

- New scene (batch48). A tug of war where the teams GROW: Mochi (coral, left) 20 at frame 0, **+3 every second** (linear); Bolt (mint, right) starts ALONE and **doubles every second** (1 → 2,048). Mochi's head start drags the flag toward her LINE; Bolt's x2 overtakes; the last x2 yanks the flag over his LINE and Mochi's whole team flies into a pile (Mochi on top, annoyed; Bolt smug).
- Caption baked in-scene (`--cap`): `Every second Bolt's team ~DOUBLES~|Mochi adds 3. Who pulls it over the ~LINE~?` (DOUBLES gold, LINE red).
- New file `scenes/tug_war.py`; no lib/ or tools/ changes.

## Layout (side safe zone x 108-907)
- Arena mat y 430-1372. Rope y 900. Centre line (dashed) x 458, LINES at ±80 px (coral left = Mochi's, mint right = Bolt's), "LINE" labels from frame 0. Centre sits left of the screen centre so Bolt's crowd gets 204 px of width.
- Leaders R 46, 42 px behind their LINE. Crowds are grids behind them (column-major from the front, rows centre-out), cell ≤ 56 px (Mochi) / ≤ 80 px (Bolt), shrinking so N fits (Bolt's 2,047 helpers at ~9.5 px). Each row holds a branch rope tied to the main rope at the leader (a fan). Colour = ordered gradient by distance from the leader: coral → gold, mint → teal → indigo.
- Crowds shuffle 0.45 × the rope travel (Mochi's back edge reaches x 107.5 at the near miss; Bolt's 906 at the yank).
- HUD: team counts (gold = bigger team) with "+3"/"x2" badges on the beat, a FLAG meter between the two LINE ticks. Giant counts (165 px) over both sides with big "+3"/"x2" until ~6 s.

## Physics (1-D, honest)
- `x'' = K(B − M) − G v − BQ v|v|`, K 4, G 1.0, BQ 0.5 (count units). Each helper pulls one unit; the counts in the force are the counts on screen (step changes on the beat). Linear + quadratic skid drag on the feet; that caps the speed, so the race back takes ~2 s instead of a 0.3 s snap.
- Sim starts at −2.5 s from rest (the flag is already moving left at frame 0). The LINES are where the flag is at 11.20 s (L_sim 143.3), so the LAST doubling carries it over.
- Lines tried with plain linear damping: the flag crossed Bolt's line at ~9 s (B = 256). With force / total mass it never came back. Quadratic drag gave the timing.

## Timeline (clip 14.50 s = 870 frames)
- 0.0: 20 vs 1, flag at −0.16 L moving left, giant counts. First downbeat (theme) + heave at 0.1; Mochi +3 at 0.6, 1.6 …; Bolt x2 at 1.1, 2.1 … 11.1.
- Counts: 0.5 s 20/1, 1 s 23/1, 2 s 26/2, 4 s 32/8, 6 s 38/32, 6.1 s 38/64 (Bolt's team bigger), 9 s 47/256, 10 s 50/512, 11.1 s 53/2,048.
- Flag nearest Mochi's LINE: −0.63 L at 6.15 s. **LEAD CHANGE (flag over the centre) 9.37 s.** **Over Bolt's LINE 11.20 s** (BOLT WINS!).
- Flights 11.23-12.1; pile lands on the final stab 12.1 (Mochi last, on top). Faces until 13.9, dissolve 13.9-14.5 into the pre-roll.

## Sound (music first)
- **v3 (coordinator 2026-10-23): music swapped to Johann Strauss I, "Radetzky-Marsch" Op. 228** (1848; d. 1849, PD). "Entry of the Gladiators" (v1/v2) was dropped as the circus/clown tune (made-for-kids risk). Audio-only change: the v1 picture was re-muxed with `-t 14.5`.
- **Notes:** no MIDI/MusicXML exists on Mutopia, IMSLP or Commons, so they were transcribed from the PD first edition (Haslinger, Vienna 1848, plate 10,996, IMSLP #322630, native 3800x5000 scan; note-head finder + visual reading). Cross-checked against IMSLP #78169 (PD piano edition), IMSLP #30496 (piano-conductor) and the Wikipedia incipit. The PDFs and SOURCE.txt are in `<SOUNDFONTS_DIR>\scores\strauss1_radetzky\`. The notes live in the scene as `RZ_MEL` / `RZ_ACC`.
- **Cut, one steady tempo** (half note 0.5 s, so a 2/2 bar = 1 s, matching the picture's 1 s grid):
  - intro bars 1-4 at 0.1-4.1 (the hammered D chords at 0.1);
  - first strain bars 5-10 at 4.1-10.1 (the grace-note "f# e# f#" theme);
  - closing bar 19, the A7 run, at 10.1-11.1 = the race back;
  - closing bar 20, three tutti D chords, at 11.1 = the last x2 and the yank;
  - our final D stab at 12.1 = the pile, with the tonic ringing to ~13.5.
  - Bar 10 has the same notes as bar 18, so bar 10 → 19 is the score's own approach to the cadence.
- Every x2 lands on a downbeat and every +3 on beat 2. Measured onset-flux peaks sit within ±5 ms of the downbeats (0.1, 1.1 ... 11.1).
- **Arrangement** (lib/orchestra):
  - Melody an octave down (F#4-C#5) on strings + clarinet, trumpet from bar 5, flute at pitch quietly, grace notes kept.
  - The score's oom-pah: bass on tuba + pizz (contrabass from bar 5), off-beat chords on horns + pizz. Bar 1's chords also on brass.
  - Bass drum on downbeats, snare on off-beat quarters, timpani from bar 5.
  - Race back: timpani roll on A, snare roll, A7 string tremolo on bar 19.
  - Cadence chords at gain ×1.5. No reverse cymbal / noise riser.
- **SFX unchanged** (tonal, no noise), re-pitched to D major:
  - a low rope pluck on every heave beat (the score's bass note);
  - 3 bups per +3;
  - a glass ping + rising ripple of bups per x2 (3 + 2k pops);
  - the dragged team's feet ticks (8th → 16th as the flag speeds up);
  - LEAD CHANGE glass pair, yank pluck, landing bups, Mochi's thump.
- `master(peak_db=None)`, last 0.5 s digital silence.

## Checks (encoded `output/tug_war_v3_9x16.mp4` = v1 video + v3 audio, muxed with `-t`)
- h264 yuv420p 1080x1920 60 fps, 14.50 s (video and audio both 14.500 s).
- Loudness: −14.00 LUFS, peak −5.0 dBFS, last 0.5 s −240 dB.
- RMS/s: −18.6 −18.1 −18.1 −19.1 −17.7 −16.9 −16.5 −16.5 −17.8 −15.8 −16.3 −13.2 −13.3 −25.9. The last second is the loop-tail hold/fade.
- Cadence (11.0-12.0 s) quarter-seconds −13 vs bar 19's run −15…−18 (mean −16.3): **≈ +3 dB**.
- check_clip events/5 s 149/164; 29 distinct notes, top note share 13.7 %.
- flash_check PASS (0 flashes). Seam mean delta 0.356 (picture unchanged).
- v1/v2 (Gladiators) frames were read from the encoded file at 0, 0.5, 1 (1:1), 2, 9.4, 11.15 (1:1), 11.6, 12.3 and 14.48; the picture is identical in v3.

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/tug_war.py --still --frame 0,30,60,120 --label x`
- `NF_SCALE=1.0 python scenes/tug_war.py --label v1` (one process, x264 `-threads 2`)
- `python scenes/tug_war.py --report` / `--audio-only`

## Doubts
- Bolt's side is nearly empty for ~3 s (1, 2, 4 helpers): the honest exponential. The giant "20 vs 1" counts carry it.
- At 2,048 the helpers are ~9.5 px dots: a gradient swarm, not faces (only for ~0.1 s before the yank and in the finale).
- 14.5 s, just under the 15-20 s target; the cut is the honest ladder (11 doublings + finale).
- The Radetzky notes are a hand transcription from a scan (no PD MIDI exists). The bars used are simple and were cross-checked against three editions; the intro voicings (bars 1-4 LH) are simplified.
- Tiny helpers pull as hard as big ones (the brief's equal per-helper pull); a pedant may comment.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch48\tug_war.mp4` (Full HD, v3 with Radetzky; overwrote v2). Owner review: pending.

Owner review (2026-10-23): "might work" -> SHIP (4K).

Owner review (2026-10-23): "might work" -> SHIP. 4K: `output/tug_war_ship_9x16.mp4` (2160x3840, h264 yuv420p 60 fps, 870 frames, 14.50 s; v3 Radetzky wav re-muxed with `-t 14.5`, bit-identical to v3). -14.00 LUFS, peak -4.96 dBFS, last 0.5 s -240 dB, flash_check PASS (0), seam 0.245. The first 4K try lost ffmpeg at ~9.4 s with 0.1 GB RAM free (another job held ~12 GB); x264 now runs with `-rc-lookahead 12`.

Ship (2026-10-23): 4K staged at MochiAndBolt/schedule/2026-10-30 slot 1 (03:00 local Oct 31).
