# log_gauntlet
- New scene (batch36). Rule: "Every log swings FASTER than the last". Choice: Mochi DASHES straight through; Bolt WAITS and times each swing. Caption (baked, `--cap`): `Every log swings ^FASTER^ than the last|~Dash or wait?~`.
- World: two narrow wooden beams (Mochi x 390, Bolt x 690) over a dark river at dusk. There are 6 stations 430 apart, and the far platform (gold line, lanterns) sits at S_FIN = 2480.
- Projection: 3/4 view, `y = 1070 - 0.92 (s - cam) - 0.60 z`. The world layer is zoomed 1.25 about y = 1000 and pulls back to 0.95 after the fall, so Bolt's finish and Mochi in the river both fit.
- Logs: each log (radius 34, half-length 76) hangs on two parallel ropes from a timber crossbar.
  - A parallelogram hang means the log translates without turning, so it is an EXACT simple pendulum.
  - Each log sweeps across BOTH beams, so the same log judges both characters.
  - Each log shows its period on its bark ("1.45 s"). A ladder under the caption, `SWING: 2.0 s -> 1.7 -> 1.45 -> 1.25 -> 1.1 -> 1.0`, highlights the leader's log.
  - Dashed arc ghosts show each log's path, and speed ghosts trail fast logs.

## Physics
- Scale: 1 m = 900 px, g = 9.81 m/s^2.
- Periods 2.0 / 1.7 / 1.45 / 1.25 / 1.1 / 1.0 s, amplitudes 30 / 40 / 50 / 60 / 70 / 80 deg.
- Rope lengths are solved from `T = 4 sqrt(L/g) K(sin(th0/2))` (AGM): 864 / 608 / 427 / 303 / 223 / 173 px. theta'' = -(g/L) sin(theta) is tabulated by RK4; the period closes to 1e-14.
- A hit is a 3D sphere (character, r 64) against a capsule (log) contact.
- Mochi on a hit:
  - She is put just outside the log's band, spun (stun 0.62 s x U(0.8, 1.4)) and pushed sideways by `40 px * |v_log|/1000 * centrality`.
  - |dx| > 17 means a teeter (0.5 s). |dx| > 50 (beam edge + 12) means an edge wobble (0.34 s), then a real-g fall of 330 px into the river.
  - She drifts back to centre at 20 px/s, so a quick second hit stacks. That is why the faster logs finally get her: she gets no recovery time.
- Bolt:
  - He walks at 215 px/s and stops 16 px outside each band (the log sweeps a hair past his face).
  - He watches for at least 0.45 s, then goes when a full scoot (480 px/s) across the band is predicted clean by 6 px with the same contact test, plus a 0.03-0.08 s reaction delay.
- Escalation is honest:
  - The middle logs push hardest (log speed at the lane: about 1300 / 1400 / 1000 px/s for 2.0 / 1.25 / 1.0 s).
  - The short logs give the fewest clear windows (Bolt's waits grow from about 0.55 to 1.2 s), so Mochi is hit more often and recovers less between hits.
- Hook: log 0's phase is set so that it crosses Bolt's lane at t = 0.03 s (frame 0 shows the log at his face, a whomp at 0.08). Bolt goes at 0.37 s, and Mochi dashes in and gets a CLOSE! at 0.95 s.
- Seed search (`--search N --from S`). Filter:
  - Mochi falls at station 3 or later while leading by more than 40.
  - Bolt wins within 4.2 s of the fall.
  - 3-6 bonks and at least 3 lead changes.
  - Gap between them never over 560 (both stay in frame).
  - Hook near-pass by 0.22 s, clip 15-19.5 s.
  - Good seeds (of 6000): 10, 110, 656, 1175, 2183, 2251, 3956, 4238, 4320, 5737.

## s1175 (default)
- Bonks: 1.57 (1.7 s log), 2.57 (1.7, teeter), 4.85 (1.45), 6.43 (1.25), 8.08 (1.1, teeter), 9.95 (1.0, swatted, dx -68).
- Lead changes at 1.3, 3.17, 4.5, 5.13, 6.22, and 10.68 (the edge).
- Mochi falls at 11.03 and splashes at about 11.3. She floats up with the annoyed stare.
- Bolt times the last log, goes at 11.95 and wins at 13.62 (cheer hops, confetti, chime).
- Clip 15.20 s (912 frames), with a 36-frame dissolve into the pre-roll.

## Sound
No music, no beds, no whoosh, hiss or creak. Everything is synthesized in the scene:
- tock: a wood block at each swing end of the log a character is at, pitched up per station (720-1220 Hz). The tick-tock speeds up with the logs.
- whomp: a soft low tonal wooden pass sound (150 Hz bend, no noise) when a log passes within 30 px of a face.
- step ticks: Mochi every 0.13 s while dashing; Bolt every 0.22 s walking and every 0.12 s scooting.
- bonk: a hollow wooden BONK with a pitch drop.
- teeter: alternating taps.
- splash: a short body, plus a plip.
- chime: a rising major bell triad for the win.
- Onsets are kept at least 12 ms apart. Mastered with `audio.master()`. `--resound` rebuilds the audio onto the existing render.

## Flags
`--seed --label --cap --vote 1` (Team Mochi or Team Bolt? with a drawn arrow, after the win until the dissolve; default OFF; `--vote-y` 960) `--search N --from S --still --frame N --resound`. Tuning flags: `--push --vmlo --vmhi --vb --vgo --watch --stun --teeter --recenter --zoom --zend --hookleft`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 912 frames.
- -14.00 LUFS, peak -2.2 dBFS, last 0.5 s at -51.0 dBFS.
- flash_check PASS (0 flashes).
- Seam: pre-encode 3.62 against a normal step of 3.76, and the last frame is closer to frame 0 than to frame 1, so the loop is perfect. Encoded seam 4.12 against steps of 3.5-4.7. These are high-motion steps: logs, ripples and the camera all move. check_loop reports "MISMATCH" because the last frame is the pre-roll frame one step before frame 0, as in coin_bridge2.
- Events per 5 s: 79 / 77 / 29 (185 sound events).

Delivered <VIDEOS_DIR>\batch36\log_gauntlet.mp4. Owner review: pending.

Owner review (2026-10-16): good -> 4K.

Owner review: APPROVED. Shipped in 4K with the vote banner ON (A/B arm) to <VIDEOS_DIR>\Schedule\2026-10-20\2_log_gauntlet.mp4.
- Render: `NF_SCALE=2.0 --seed 1175 --label ship --vote 1`.
- Vote banner narrowed to fit the safe zone: max width 760, centred at x 500. It spans x 95-905 and y about 905-985, between Bolt on the deck and Mochi in the river, so no face is covered.
- Encoded 4K: h264 yuv420p 2160x3840, 60 fps, 912 frames = 15.200 s; -14.0 LUFS, peak -2.2 dBFS, last 0.5 s at -51 dBFS; flash_check PASS.
