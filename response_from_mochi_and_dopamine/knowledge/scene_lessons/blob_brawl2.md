# blob_brawl2 — Mochi's WHIP vs Bolt's 8 kg BALL on a chain (v2 of blob_brawl, 2026-11-15)

- Owner verdict on v1 (2026-11-15): "try it, but include more physics: one has a WHIP that acts like real physics, the other something that also shows physics". New file; `scenes/blob_brawl.py` untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\blob_brawl2.mp4` (Full HD 9:16, label v1) + `blob_brawl2_files\`. v1 archived to `archive\reviewed_2026-11-15\`.
- Caption (baked; `--nocap` = base): "Light fast ~WHIP~ vs heavy slow ~BALL~" / "Who breaks the other's ~SHIELD~ first?". HUD under the K.O. mark: "hit = ½mv²".

## The physics argument (one rule for both)
- Damage = real impact energy: every prop piece that strikes the other's shield deals ½ m v_n² (v_n = speed into the shield, relative to it). 1 HP = J_HP 300 J. Same rule, same constant, both sides.
- Knockback = real momentum: m (1+e) v_n / M_BLOB (40 kg). The ball shoves the shield visibly; the whip barely moves it.
- Units: 100 px = 1 m, real time, top view (no gravity).
- Escalation = the music: tempo B0 132 bpm → ×2 linearly over 12.5 s; both drives are locked to the beat, so swing speed ×2 and KE ×4 by the end. Hit rate keeps climbing (ball 1 → 1.5 hits/s; whip one hit per stroke, strokes every 2 beats).

## Whip (Mochi)
- PBD rope: 40 segments, 200 px, mass tapering geometrically ×1/40 handle → tip, total M_WHIP 2.2 kg (set by `--calib`). Verlet integration, distance constraints solved handle → tip, 2 iterations, SUB 32 substeps/frame, linear drag 0.6/s + QUADRATIC air drag QD/width·v² (QD 0.005; thin tip loses most).
- Handle = a floating grip on a circle r 100 around Mochi (shield r 70: gap ≥ 8 px with the grip; never touches). Stroke = 2 beats: back-cast 0-0.30 (−25° → −160° rel. to the aim, quintic ease), pause, forward cast 0.50-0.64, dead stop. Aim re-read only during back-cast + pause. Phase offset W_OFF 1.22 puts the forward tip peak (s ≈ 0.61) on an even beat.
- Tip/handle speed ≈ 5-7×: handle peak ~3.5k px/s (78 mph) → tip 400-650 mph (the taper does it; the drive is the same every stroke).
- CRACK = a tip-speed local peak ≥ 350 mph (back-cast peaks 160-300 mph stay below until the tempo climbs). Shock ring (2 rings, 0.24 s) + tip streak (substep path) + N-wave click SFX.
- One whip hit per stroke (contacts merged by stroke id).
- **Not converged in absolute mph:** SUB 16 → 32 → 64 raises peaks ~15-25 % each doubling even with quadratic drag (inextensible tapered string → tip speed singular in theory). The HUD number is the sim's value at SUB 32; we never claim "sound barrier" on screen. (Peaks occasionally pass 767 mph late in the fight.)

## Ball (Bolt)
- PBD chain: 14 links × 14 px (0.12 kg) + 8 kg ball r 34. Handle = a floating ring grip circling Bolt at r 96, once per BALL_BEATS 3 beats. The ball swings wide, lags, rebounds on a hit (e 0.45) and the chain goes slack, then re-tensions.

## Fighters
- Steering (not billiards): each keeps its prop's range (Mochi 290, Bolt 220 px centre-to-centre), circles the other at 160 px/s (direction flips at seeded 1.0-2.6 s), both steer their midpoint to the arena centre (K_CEN 1.5/s), wall avoid, V_MAX 250. Knockback decays τ 0.35 s.
- Without centring the fight hugged the wall and the whip/ball smacked the ring all the time; with it Bolt holds the middle (r ~90), Mochi circles at r ~210.
- Arena r 372 at (508, 852): x 136-880 (safe box 0.10-0.84 w), y 480-1224. Props collide with the ring, both shields; no damage from walls / own shield.

## Calibration (`--calib`, seeds 1-120, HP infinite, t ≤ 6 s)
- M_WHIP 2.0 → whip/ball 0.894; **2.2 → 1.003** (9014 J vs 8988 J). Chaotic: ±10 % run to run.
- Outcome (seeds 1-199, J_HP 300): K.O. in all 199, median 11.4 s; **Bolt wins 161 / Mochi 38**. Equal at 6 s, but the ball's v² + faster revolutions pull ahead late — the "speed alone isn't enough, mass × v²" story. Seed chosen for timing only, inside the majority outcome.

## Bugs fixed on the way (keep)
- RNG stream depended on `--tmax` (flip schedule generated up to T_MAX) → fixed 40 s horizon.
- PBD push-outs injected velocity: a ball squeezed between shield and wall was flung (one 253 HP hit). Collision corrections now move prev too; contact velocity set explicitly (restitution).
- Hit sparks/pops anchored to the struck shield (knockback moved it away from the stored point).

## Seed 114 (default)
- First whip hit 0.02 s with a crack at 0.006 s (frame 0 mid-cast); ball first hit 0.49 s.
- LEAD: Mochi 0.03 s → **Bolt 5.83 s**; **K.O. 11.97 s, Mochi's shield** (ball hit 16 HP).
- Whip 20 hits (88 HP), ball 14 hits (105 HP), 24 cracks; tip peaks 406 → 630 mph (one 802), ball 26 → 85 mph.
- HP/s: 2s M90/B91 · 4s M84/B82 · 6s M73/B74 · 8s M49/B61 · 10s M34/B42 · 11s M21/B33.
- Hits/s 3 2 2 2 2 3 3 4 3 3 3 4 (last full second = the max).
- Clip 14.28 s = K.O. + 1.7 s finale (ball keeps swinging, slack whip trails the ejected loser, K.O. / WINS / recap) + 0.6 s dissolve to frame 0.

## Sound
- Grieg, In the Hall of the Mountain King (PD, Mutopia #1888, read at runtime like v1) on the fight's OWN beat map (`beats()` / `beat_time()`): theme from score beat 4 for floor(beats(KO)) − 16 beats, then the last 16 presto beats (324-340), final B-minor chord ON the K.O. (seed 114: KO at beat 38.95, theme 4-26). v1's orchestration.
- SFX (own synth, no beds): whip CRACK = N-wave click + snap ring on a chord tone (~midi 93), gain ∝ (v/V_CRACK)^0.7; glass-shield crack per hit (+12 ms, gain ∝ damage); ball = steel clang on a low chord tone + body thump; K.O. shatter (14 tinks) + thud at +0.55 s.
- Master: −14 LUFS / −2 dBFS lift (v1 chain); music silent from T − 1.25; last 0.5 s digital silence.
- Sound events/s 6 4 4 4 4 6 6 9 6 6 7 10 14 (climbs into the K.O.).

## Checks (encoded Full HD, label v1)
- h264 yuv420p 1080x1920 @ 60, 857 f = 14.28 s; −14.01 LUFS (muxed, stereo), peak −1.94 dBFS, last 0.5 s −240 dB; flash_check PASS (0 flashes, mean lum 0.006); seam pre-encode max 2/255, post-encode mean 0.30.
- Onsets: 66 / 71 crack/shield/clang events (93 %) within 40 ms (own HP-1.5 kHz flux detector, `output/tmp/bb2/onset.py`).
- `tools/check_loop.py` does not fit this scene (its probe expects `_9x16` still names and a failing out-of-range frame; this scene clamps) — seam measured with two stills (frame 0 vs frame 99999 → last).
- Contact sheet + 1:1 crops of the crack (f686-690) and a ball hit (f612-619) from the encoded mp4.

## Doubts
- Absolute mph not converged (see Whip). Never claim "sound barrier" in captions/titles.
- "slow BALL": the ball reaches ~85 mph late (slow only next to the tip).
- Shield crack webs get dense by the K.O.; the K.O. stamp hides the ejected loser ~1 s.

## Args
- `--seed` (114) `--calib` `--mw` `--jhp` `--b0` `--tramp` `--lw` `--qd` `--vcrack` `--nc` `--lc` `--bbeats` `--rm` `--rb` `--kcen` `--vmax` `--sub`, `--still --frame a,b`, `--report`, `--nocap`, `--reuse`, `--label`.
- Sim ≈ 0.75 s per clip second at SUB 32 (pure Python); calib (120 seeds × 6 s) ~2.5 min on 11 workers; seed search `output/tmp/bb2/search.py --from a --to b` (~8 min / 200 seeds).
