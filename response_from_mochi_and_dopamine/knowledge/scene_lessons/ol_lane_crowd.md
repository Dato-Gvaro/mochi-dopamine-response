# ol_lane_crowd (DopamineEXE, batch64 #3: swap-in for the dropped ol_brazil_nut)

## v1 (2026-11-01)
A corridor (thin white walls, open periodic ends: who walks out at the top comes back in at the bottom). 100 walkers, 50 heading UP (warm red → orange by position across the corridor) and 50 heading DOWN (cool cyan → blue), all mixed at random, each with a white heading chevron. Nobody is told where to walk; under "TIME-LAPSE ×1.5" lanes form by themselves (soft column glow under each formed lane, "+1 LANE" pill and a bell per lane). At 8.11 s everyone is in a lane: 8 LANES, IN A LANE 100%, gold, "8 lanes, nobody coming at anyone" + "nobody planned it: lane formation (self-organisation)", Arabesque cadence, eases to REAL TIME and the lanes stream on. Dissolve into frame 0. **10.72 s, 643 frames.**

- Caption (baked; `--cap ''` = base): `Two crowds walk ^THROUGH^ each other…|until everyone is in a ~LANE~`. True: from the lock on, 100% of walkers have no oncoming walker on their line in every remaining frame (checked: 100.0% of frames).
- 28 px dots, 100 walkers on 756 × 760 px (~10% of the floor): the owner's "not crowded".

## Model (`simulate`, dt 1/120 s, ~3 s CPU)
- Social force (Helbing & Molnár 1995) with explicit collision prediction (Zanlungo, Ikeda & Kanda 2011): drive to v0 = 75 px/s (1.34 m/s at 56 px/m) with τ 0.5 s; repulsion A 300 px/s² · exp((2R − d*)/B), B 12 px, where d* is the distance at predicted closest approach (horizon 0.8 s); anisotropy λ 0.2 (walkers behind count 20%); body contact force; wall repulsion; noise 10 px/s². Speed cap 1.3 v0. Periodic corridor length 760 px.
- First try (plain distance-based social force, no prediction) clogged (counterflow stand-offs, speed 10-45% of v0, no lanes): rejected as unreadable. With prediction, lanes formed in 5/5 seeds: lock (screen) seed 1 11.4 s, 2 7.6 s, 3 10.4 s, **4 8.1 s**, 5 6.3 s; all stayed 100% after locking. Seed **4** chosen (lanes climb 1 → 8 spread over the clip).
- IN A LANE = no walker of the other direction within 1.8 radii sideways anywhere in the corridor. LANES = runs of same-direction walkers side by side (sorted across the corridor) that are all IN A LANE (live: it can drop). A lane "locks" when the count reaches a new maximum held ≥ 0.2 s. Lock = the first moment after which 100% stay in a lane: real 12.47 s.

## Timeline (screen, ×1.5 until the lock)
- 0 s: in a lane 4%, 0 lanes, walkers already dodging (brush at 0.01 s) · 0.16 s lane 1 (it breaks again) · 1.5 / 1.54 s lanes 2, 3 · 2.29 s lane 4 · 2 s 40% · 4 s 59% · 5.3 s 72% · 6.76 s lane 5 · 7.23 s lane 6 · 8.0 s 98% · **8.11 s lanes 7 + 8, 100%** · ease to real time · 10.12-10.72 dissolve.

## Sound
- Debussy, Arabesque No. 2 in G (1891, PD), Mutopia MIDI (`<SOUNDFONTS_DIR>\scores\debussy_arabesque2\SOURCE.txt`; unused elsewhere: ol_mirror_split uses Arabesque No. 1). Score beats 16-32 (the G-major theme to its V → I), tempo set by the sim (119 bpm) so beat 32 = the lock: rich G chord + harp + soft timpani. Theme an octave down (owner's low/mid rule).
- SFX: a bell per lane that locks (G-major pentatonic, rising; two at once ring 60 ms apart), a soft low pok when two walkers brush within 4 px (density-capped). 11 events.

## Checks (encoded, output/ol_lane_crowd_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 10.72 s; **-14.00 LUFS**, peak -6.41 dBFS, last 0.5 s digital silence; flash_check PASS (0); seam mean |Δ| 0.26 (check_clip; natural motion ~0.7).
- Side safe zone: corridor x 127-889 (0.12-0.82w), content ≤ 1240 px (0.65h).
- Stills read at 0, 0.2, 2.5, 5, 7, 8.13, 10 s; 1:1 crop at 8.7 s (lanes, chevrons).

## Flags
`--seed` (4), `--n` (100), `--A`, `--B`, `--lapse` (1.5), `--label`, `--cap`, `--still --frame`, `--dry`, `--audio`, `--sfx`, `--sound 0`.

## Upload draft
- `Two crowds walk through each other… until everyone is in a lane 🚶 #satisfying #physics #shorts`
- `100 people, nobody in charge: 8 lanes appear by themselves 🚶 #satisfying #physics #shorts`
- `Walk straight at each other long enough and lanes form 🚶 #satisfying #physics #shorts`
- Pinned: `nobody told them where to walk and they still made 8 lanes. do you keep right in a crowd?`

## v2 (2026-11-01, owner review: "needs more engagement… how many times they become line")
- `--v2`, same sim. A falling **DODGES / SEC** counter beside LANES (LANES moved to x JX-190, DODGES at JX+170, 116 px). Honest substitute for the owner's "BUMPS / SEC": real body brushes stop by 1.3 s real (the model predicts and sidesteps), so they can't carry a race. A dodge = a walker's sideways speed rising past 0.25 v0 (0.34 m/s; hysteresis 0.12), counted in a centred 1 s window of REAL time, excluding the first 0.2 s off the spawn. Runs 19-27 -> 14 -> 8 -> 5 -> 3 -> 0 (0 at real 12.0 s, the lock is 12.47). Each counted dodge draws a small white sidestep mark beside the walker for 0.35 s.
- Bigger "+1 LANE": the new lane's column flares (lane colour + gold outline, decay 0.35 s) with a 46 px "+1 LANE" tag inside it (rows stack so tags never overlap); the counter pill is 38 px and the LANES number pops harder.
- Deliverable `<VIDEOS_DIR>\DopamineExe\review\fixes_1101\ol_lane_crowd_v2.mp4`. 10.72 s, -14.00 LUFS, peak -6.41, silent tail, flash 0, seam 0.30. v1 -> archive/ol_lane_crowd_v1.mp4.

- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-13\2_ol_lane_crowd.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 643 frames, -14.00 LUFS, peak -6.41, flash 0, seam 0.18. Full HD -> archive/ol_lane_crowd_v2.mp4.
