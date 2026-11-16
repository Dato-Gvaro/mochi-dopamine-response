# freefall_cargo — head-down dive vs flat tracking, a race to a falling supply crate (Wagner, Ride of the Valkyries)

## World (one era: modern)
- A four-engine turboprop cargo plane (generic, grey, no markings) over the sea and islands.
- Skydivers: Mochi and Bolt in jumpsuits with rig packs, harness straps and goggles. They land under ram-air canopies (cells in their own colours).
- Cargo: olive ammo and supply boxes, oil drums, wooden pallets, cargo nets and a military jeep. The SUPPLY crate glows gold.
- No IP. Never call it "Uncharted" in any text.

## The choice duel (same physics for every body)
- `dv/dt = g (1 − (v/vt)²)`, which comes from `m dv/dt = mg − ½ρC_dA v²` (so vt ∝ 1/√(C_dA)). Fixed dt 1/60, from rest at the ramp.

| | Posture | vt | sideways | swerve cost |
|---|---|---|---|---|
| Mochi | HEAD-DOWN | 80 m/s (spinning flat: 38) | max 5 m/s, 3.5 m/s² | tilting adds drag: vt − 22·|a|/a_max |
| Bolt | TRACKING (a glide) | 55 m/s | max 22 m/s, 14 m/s² | vt − 3·|a|/a_max |
| Crate | stable, then TUMBLING in the cloud bank | 68.2 → 40 m/s | glides 7.1 m/s sideways once it tumbles | |
| Debris | net 7, pallets 23-34, boxes 46-53, drums 76, jeep 92 m/s | | | |

- Both divers look down. They swerve from what is BELOW them (Bolt starts 0.75 s early, Mochi 0.55 s early). They cannot see what comes from ABOVE (the jeep, the drums).
- Choreography: each event's debris is placed on the diver's real path, so it crosses their depth at its beat with a chosen miss. Its release time or vt is solved from the same fall law.

## Race (story s = clip t − 0.8; bar = 1.85 s, bar 60 = s 0)

| bar | s | what happens |
|---|---|---|
| 60 | 0 | The ramp blows open (boom); cargo bursts out and both jump at 0.15 s. They are level for about 6 s (drag is tiny while slow). |
| 61 / 63 | 1.85 / 5.55 | Bolt swerves around a net and a pallet |
| 62 / 64 | 3.7 / 7.4 | Mochi near-misses (1.9 m, 2.0 m). Tilting costs her speed ("TILTING = DRAG!"). She leads by 19 m at s 8. |
| 65 | 9.25 | A tumbling box flutters into her path: CLIPPED, she spins flat for 3.32 s (vt 38). Bolt takes the lead. |
| 66 pos 3 | 11.72 | The jeep (vt 92) tumbles past her at −33 m/s relative, 3.0 m away |
| 67 | 12.95 | CLOUD BANK (fog, depth 481-531 m). The crate entered it at s 11.2, started to tumble and glide sideways. |
| 68 | 14.8 | TWIST banner: the crate glides sideways (toward Mochi's side, then past her) |
| 69 pos 3 | 17.2 | Mochi surges back (65-71 m/s; Bolt holds 54.6) while the crate slides away from her: "HEAD-DOWN CAN'T STEER!". She overtakes Bolt at s 19.13. |
| 70 pos 6 | 19.73 | Mochi reaches the crate's depth FIRST but **8.0 m wide**; she shoots past (bracket "8 m") |
| 71 | 20.35 | Bolt glides onto it (1.05 m) on the B-major climax chord: BOLT GRABS IT, canopy at +0.30 s |
| end | 21.70 | Slow motion (rate → 0.25). Mochi's canopy opens 0.75 s after her miss; the annoyed stare up at Bolt. TRACKING WINS! |

- **Why Bolt wins:** Mochi is faster (she arrives 0.62 s earlier), but the crate glides sideways at 7.1 m/s and head-down can slide only 5 m/s. Every tilt also slows her. Tracking glides at up to 22 m/s. The top panels show this live: speed (m/s down) and a SIDEWAYS bar against each posture's limit (5 vs 22).
- The physics is solved to land on the score: `--tune` solves the crate's vt (Bolt's arrival = the bar-71 downbeat), Mochi's spin time (her pass = bar 70's long F#), the cloud depth (divers in the bank on bar 67) and the glide (miss = 8 m). Results are in `TUNE`.

## Hook / loop
- Frame 0 = the payoff, at a 1.30× zoom: Bolt with the crate under his mint canopy, Mochi below under hers, annoyed, "TRACKING WINS!".
- A 0.8 s eased rewind (◀◀ badge) runs back to the plane. The ramp blows open on the bar-60 downbeat at 0.80 s, and they dive at 0.95 s.
- Rewind flicker fix: replaying 21 s of fall in 0.8 s raced clouds, debris and speed lines through ~25% of the flash grid. The first build FAILED flash_check (4 flashes at 0.3 s). The fix:
  - clouds, debris, speed lines and the far layer fade to 0 at the rewind's midpoint (`ka`);
  - a soft sky-coloured motion veil (≤ 0.6) covers the world;
  - no fog during the rewind.
- Everything is a function of story time tau. The last frame is one step before frame 0, so the seam is exact.

## Music
- Wagner, "Ride of the Valkyries" (Die Walküre, Act III prelude, 1856). **PD: Wagner died 1883.**
- Notes parsed with mido from `rvalkyri.mid` (midiworld.com, "Rearranged L. Roberts", a MIDI transcription of the orchestral score). The excerpt is bars 59 (last third) to 71, 9/8, re-timed to bar = 1.85 s. Tracks used: Strings I/II, French Horns, Trombones, Contrabass. The excerpt is embedded as `SCORE` in the scene.
  - Bar 59's tail is the string swirl crescendo, the rewind.
  - Bars 60-71 are the brass statement of the theme in B, a rising sequence that cadences F#→B on bar 71.
- Arrangement (lib/orchestra, MuseScore_General MIT):
  - Horns play the theme in both source octaves. Trombones join at bar 64 and trumpets (≤ D#5) at 68.
  - Strings play the mid figures; the high swirls are an octave down and soft.
  - Contrabass with a sub octave and a synth sub; tuba from 64.
  - Choir aah pads on each bar's harmony from 64 (the horn line's pitch classes), swelling into 71.
  - Timpani on every downbeat (the bass root), with rolls into bar 60 and into 71.
  - Booms on 60 (ramp), 65 (clip), 68 (twist) and 71 (grab). Cymbal swells into 68 and 71.
  - Final B-major chord held, then 1.5 s of silence.
- SFX (our own synthesis): a soft wind rush following the fall speed (-18 LU under the music), whooshes on the near-misses, a bigger jeep whoosh, a wooden thud on the clip, two canopy "fwumps", a rewind whoosh.
- Sync: ramp = bar 60, near-misses / swerves = bar downbeats, clip = 65, cloud = 67, twist = 68, miss = 70 pos 6, grab = 71.

## Checks (v1, Full HD, <VIDEOS_DIR>\batch30\freefall_cargo.mp4)
- Video: h264, yuv420p, 1080x1920, 60 fps, 1503 frames = 25.05 s.
- Audio: -14.01 LUFS. Peak -5.71 dBFS. The last 0.5 s peaks at -80.8 dBFS (silent tail).
- flash_check: PASS (worst 1 s = 2 flashes, at 5.4 s).
  - v1 first failed twice: 4 flashes in the rewind, then 3 at the cloud bank (13.1 s).
  - Fix: the calm rewind (see above), and fog that is softer (0.30 max) and slower (in and out over ~0.8 s), with bank puffs at 0.8 alpha.
- Loop seam:
  - Pre-encode, frame 1502 → frame 0 has a mean delta of 0.363, which equals a normal step (1502 vs 1501: 0.359), so the seam is exact.
  - Post-encode, check_clip reads 1.04. That is the frame-0 I-frame against a P-frame: the moving scene's slow-motion end measures 1.36 between frame-0 and frame-1502 encodes, against 0.46 for normal steps.
- Physics landing (`--report`):
  - Bolt grabs at s 20.350 (bar 71, 0.00 off), 1.05 m from the crate's centre.
  - Mochi passes at s 19.733 (bar 70 pos 6), 7.99 m wide.
  - Clip at s 9.25 (bar 65); the box is 0.17 m from her centre.
  - Near misses are 1.85-3.1 m. Ambient cargo stays ≥ 3.5 m from both divers after s 0.4.
- Music sync: the strongest bed onsets are at 11.9, 15.6 and 19.3 s, which are the bar 66, 68 and 70 downbeats.
- Encoded frames read at 0, 0.5, 1, 2, 3, 10.06, 12.5, 13.9, 14.6, 15.7, 20.53 and 21.25 s.

## Lessons
- A 27× rewind of a camera fall makes every cloud and debris piece flicker: fade the world content and veil it during the rewind.
- Fog for a cloud punch-through must ramp over ≥ 0.6 s each way, or it counts as a large-area flash.
- The lateral screen scale must be wider than the vertical one (18 vs 11 px/m), or an 8 m miss reads as a touch.
- Scheduled dodges + debris placed on the final path = deterministic choreography. Reactive dodging fed by debris that was placed on the previous pass's path oscillated and never converged.

## Doubts
- The divers are level for the first ~6 s. That is honest (drag barely matters while slow), but Mochi's speed lead only shows from ~s 6.
- The choreographed debris is placed on the divers' paths (a script, physically consistent), not emergent.
- The crate's glide while tumbling is honest physics in kind (autorotating boxes glide), but the 7.1 m/s value is tuned.
- Mochi's 3.3 s spin after the clip is tuned so that she arrives on bar 70.
- Owner review (2026-10-12): good visuals but no visible challenge; no arms/legs; objects fall with them and they hop object to object downward; whoever reaches the parachute backpack puts it on, grabs the other and opens the chute (grabber happy, grabbed annoyed) -> freefall_cargo2.
