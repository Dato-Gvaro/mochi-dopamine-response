# phantom_jam — Same 22 cars, one tap on the BRAKES: keep a gap or tailgate, whose ring hits 70 LAPS first? (batch64, 2026-11-01)

- Brief: docs/BRIEF_batch64.md (Mochi & Bolt 3). New scene file; caption/render/master chain copied from string_fan; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch64\phantom_jam.mp4` (**v1**, Full HD 9:16, output label v1). 15.75 s.
- Caption (baked; `--nocap` = base): "Same 22 cars, one tap on the ^BRAKES^" / "~Keep a gap~ or ~tailgate~: whose ring hits ^70 LAPS^ first?" (Mochi coral first, Bolt mint).

## Story (clip times)
- Two ring roads stacked (Mochi top, Bolt bottom), 230 m, 22 rainbow cars each; each character drives car #1, right behind the car that taps. Big faces in the ring centres ("KEEPS A GAP" / "TAILGATES"); right column: LAPS (distance of all 22 cars, in laps, one decimal), AVG km/h, STOPPED n, a 14 s speed sparkline (avg + slowest car). HUD: the race bars to the 70-lap flag from frame 0.
- 0.1 s TAP! in both rings (−10 km/h over 1 s). 0.9 s "BOLT BRAKES 13 km/h · MOCHI ONLY 3" (sim: his car dips 31→18 km/h, hers 29.5→26.5).
- 2.9-6.1 s "BOLT LEADS by 0.1 laps" (drawn only while true). 6.16 s LEAD CHANGE (real 18.2 s). TIME-LAPSE ×3 to real 20 s, rising to ×14 by real 40 s (chip shows the live factor).
- ~9.5 s "BOLT'S RING: FIRST FULL STOP" (real 37.4 s). The jam drifts backwards (red glows under stopped cars, brake lights).
- 13.15 s Mochi's ring reaches 70 laps: "MOCHI WINS", cadence; Bolt 52.2. "a jam with NO crash". Bolt's ring keeps stopping (6-7 stopped). Dissolve 15.15-15.75 into the pre-roll.

## The physics (`run_ring()`)
- OVM (Bando 1995) dv/dt = a[V(h) − v] + noise (σ 0.2 m/s², seed 1), a = 3.9 /s, V(h) = max(0, 8.4(1 + tanh((h − 10.15)/3)) − 0.6) m/s, h = centre distance, cars 4.5 m. Humans accelerate ≤ 1.0 m/s² (brake as hard as asked) — this is what makes the jam lose flow (capacity drop); without the cap the stop-and-go ring kept ~the same average speed (tested).
- No-overlap guard (≥ 1 m gap, never contact). dt 10 ms.
- Mochi = FollowerStopper (Stern 2018): command = her 30 s running-average speed (starts 8.2 m/s), cut by the 3 gap bands (4.5/5.25/6 m + Δv²/2d); accel −1.5/+1.0. Her gap 9.3 m vs Bolt's 5.9 m at the start.
- Results: Bolt's ring 31.7 → 26 (20 s) → 21 (40 s) → 18 km/h, 5-7 stopped from 37 s; Mochi's ring 29.5 km/h steady, 0 stopped ever (slowest car 19.5 km/h). First-pass brake depths on Bolt's ring 13 km/h for cars 1-7 then 14-19 (≈×1.07/car): the brief's "×1.3 per car" chip and "STOP by car 9 in 2 s" are NOT true here and were left out.
- Tested a = 4.4 / 4.9: no full stops at all; a = 3.3-3.6: lead change even earlier. Bolt's early lead is honestly small (0.1 lap) because the tap slows his ring within seconds.

## Sound
- **Piece:** N. Paganini, Moto perpetuo Op. 11 (PD). The brief's Strauss II Perpetuum mobile Op. 257 (and Tritsch-Tratsch) had no PD MIDI/score reachable. Note source: midiworld gp_moto.mid (theme track 4 from beat 14, chords track 6, bass track 9; `<SOUNDFONTS_DIR>\scores\paganini_moto_perpetuo\`, SOURCE.txt).
- Every lap-line crossing on Mochi's ring plays the next theme note (violin + pizz double; bass + afterbeat chord when the half-beat changes) — it accelerates with the time-lapse (2-3 → 11 notes/s). Bolt's crossings: a low wooden tonal tick in the current harmony (stutters in the jam). Hard brakes (onset < −2.5 m/s²): short low tonal "dmm", merged ≤1/0.18 s per ring. Own C major cadence at the finish.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 945 frames = 15.75 s. Muxed −14.00 LUFS, peak −2.01 dBFS, last 0.5 s −240 dBFS.
- flash_check PASS (0). Seam mean |delta| 0.60 (good band).
- Events/5 s 35 / 46 / 48; theme notes/s 3 2 2 2 3 2 2 4 6 10 11 11 11 then cadence.
- Side safe zone: cars x ≥ 115 (0.106w), road edge 0.093w, grass ring = decoration; stats column x 615-855; text inside 0.10-0.84w. Rings ≤ 0.68h, HUD 0.72-0.79h.
- Frames read from the mp4: 0.03, 1.0, 1.8, 4.5, 6.3, 9.8, 12.0, 13.3, 15.7.

## Args
- `--a` (3.9), `--seed` (1), `--target` (70), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/phantom_jam.py --label k4ship` (defaults) → `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-08\3_phantom_jam.mp4`. h264 yuv420p 2160x3840 @60, 945 frames 15.75 s; -14.00 LUFS, peak -2.01 dBFS, last 0.5 s silent; flash PASS (0); seam 0.48; events json bit-identical to v1. Frames read at 0.5 / 13.3 s. FHD review file → `archive\phantom_jam_fhd.mp4`.
