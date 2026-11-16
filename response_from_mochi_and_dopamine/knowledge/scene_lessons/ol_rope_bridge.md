# ol_rope_bridge (DopamineEXE, channel 2)
- Batch 59 (docs/BRIEF_batch59.md #2). A rope-and-plank bridge over a gorge. Heavy glossy balls rain onto it, more every beat; **every ball that lands adds 20 kg** (LOAD counter, "+20 kg" pops on the first landings). The elastic rope sags deeper (its own catenary), the balls roll to the low point and pile up, the ROPE TENSION at the posts climbs to the ROPE LIMIT, the lashing frays, the planks creak, and on the cadence the rope **snaps at the post with the higher tension**: the deck drops out from under the pile, swings against the far cliff, and 147 balls pour into the gorge.
- Caption (baked, `--cap`; `--cap ''` = base): `Every ball that lands adds ^WEIGHT^…|until the bridge ~SNAPS~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_rope_bridge.mp4` (**v2: bigger, clearer stats**, Full HD, seed 2, label fhd3, **12.30 s, 738 frames**). v1 archived as `archive\ol_rope_bridge_v1.mp4` (`--stats 1` reproduces its HUD). No 4K yet.

## v2.1 (2026-10-30, batch61): the hand ropes TIED to the posts (owner's optional polish)
- Owner: "the hand ropes look like they float in mid-air, far from where they hang". The handrail was the deck offset 64 px along each node's normal, so at the steep ends it started ~30 px inside the gorge, in mid-air.
- Fix (drawing only; sim, events and sound unchanged): while an end of the deck is still on its anchor (its end link intact), the last 5 handrail points blend (weight (1 - q/5)^2) onto a tie point on the post top (`HR_TIE_Y` = AY - 66), with a 3-turn lashing there. After the snap the broken side's handrail swings free with the deck and a short stub hangs from that post top. The glitchy rope on the ground at the end is LEFT as is (owner).
- Pre-fix script: scratchpad `ol_rope_bridge_pre_b61.py` (builder S session).

## v2 (2026-10-30, batch60): the stats, big and readable
- Owner on v1: "ok, but the stats need to be more visible." Brief: a tension gauge on each rope, a load kg counter, a sag readout, a % to-limit bar.
- **Sim, timeline, sound unchanged** (audio wav bit-identical to v1). HUD only (`--stats 2`, default):
  - **A dial per rope** above each post ("LEFT ROPE" / "RIGHT ROPE", centre x 196 / 820, y 548, r 72): a 270° arc filled teal -> gold -> red with the rope's own tension, a needle, ticks every 25%, a red zone 90-100%, a gold mark at the limit; the value under the dial ("18.8 kN", 36 px; orange/red past 75%). Drawn BEHIND the balls (a ball flying past is never covered). At the snap the broken rope's title turns gold "SNAPPED!" and it reads 0.0; the other rope shows its real (falling) tension.
  - **Sag readout**: a dashed level line between the anchors, a gold double arrow down to the deck's lowest point (behind the balls), and "SAG 4.9 m" (36 px) in the gorge under the deck (3.8 m at frame 0 -> 5.5 m at the snap; 652 px = 18 m). Fades out 0.2 s after the snap.
  - **% to the limit**: the meter bar is now 20 px thick; under it "67%" (48 px, orange/red past 75%) + "OF ROPE LIMIT", and "LIMIT 28.1 kN" (gold) on the right -> "SNAPPED!". After the snap the bar stays full (100%: it reached the limit).
  - LOAD counter unchanged (128 px kg); its "LOAD · n BALLS" line brighter (alpha 0.62 -> 0.85).
- **Per-rope tension** = each end link's XPBD multiplier (as v1's), the same 0.25 s smoothing and running max before the snap. The HUD's limit = the BROKEN rope's value at the snap (**28.1 kN**; v1's single meter used the max of both before smoothing, 28.7). The other rope can read a hair higher at that frame only through the smoothing (the sim breaks the rope with the higher RAW tension), so its dial is capped at the limit: both read 28.1 kN / 100% at 9.6 s. The sound/creak/fray thresholds still use v1's `kn` / `kn_limit`.
- Proof-read on screen: "LEFT ROPE", "RIGHT ROPE", "18.8 kN", "SAG 4.9 m", "67% OF ROPE LIMIT", "LIMIT 28.1 kN", "SNAPPED!", "LOAD · 80 BALLS" (1,600 kg = 80 x 20 kg): all literally true.

### Checks v2 (encoded Full HD, fhd3)
- h264 High yuv420p 1080x1920, 60 fps, 738 frames, 12.30 s. **flash_check PASS** (0 flashes, mean lum 0.013).
- **-14.00 LUFS**, peak -6.08 dBFS, last 0.5 s digital silence (= v1). Seam mean |delta| 0.286.
- Frames read from the mp4 at 0.5, 3, 7, 9.6 (both dials 28.1 / 100%), 9.75 (SNAPPED!), 10.2 s; stills at 0, 5, 9.33, 9.68, 9.75, 10.0 s (the 9.33 still = the first layout, number inside the dial, where the needle crossed it: moved under the dial).
- Side safe zone: dials x 114-902, labels 130-896 (inside 108-907).

### Doubts v2
- Both ropes read the same within 0.1 kN all the way (the load is symmetric), so the two dials move together; the left one breaks because its raw tension was a hair higher at the snap.
- The arrow of the sag readout sits behind the pile once the balls fill the middle; the "SAG x.x m" label carries it.
- The dials sit in the sky over the cliffs; balls bouncing near a post fly in front of them.

### Flags v2
`--stats (2; 1 = v1 HUD)`.

## World (logical 1080x1920)
- Gorge: rock cliffs left of x 180 and right of x 836, tops y 780, floor y 1212; one thin white outline. Wooden posts at x 182 / 834 (rope anchors y 772) with rope lashings.
- Bridge: 24 planks (wood gradient, each link of the chain), a foot rope under them, a handrail rope drawn 64 px off the deck along its normal + suspender cords. Span 652 px = 18 m.
- Balls r 13, glossy (radial gradient + highlight), a white ring on landing. Hue by drop order (ordered sweep teal -> green -> gold -> orange -> coral -> magenta, S 0.70): the pile is layered by arrival.
- Stress: the snapping post's lashing frays (fibre ticks) above 75% of the limit. Snap: fibres burst from the post, a frayed end on the deck, a stub left on the post. No flash.
- HUD: meter y 1300 = ROPE TENSION (kN) toward a gold ROPE LIMIT -> "SNAPPED!". Counter y 1500 = LOAD in kg + "+20 kg" pill (pops per landing) + "LOAD · n BALLS". Watermark 35%.

## Physics (`simulate`, seeded; sim ~20 s, cached; `--resim`)
- XPBD chain: 25 nodes (planks 6 kg), rope length 1.09 x span, compliance 1.6e-5 px per force unit (the rope stretches under load: sag 139 -> 178 px), red/black Jacobi, 10 substeps x 10 iterations. Starts on the exact catenary for its length.
- Balls (20 kg): PBD discs, cKDTree contacts; ball-plank capsule contacts push the ball and both plank nodes by their inverse masses (the load really bends the chain). Before the snap the handrail netting keeps balls between the posts. Gorge floor restitution 0.35.
- Drops: round(2 x 1.105^k) balls released for beat k (2 -> 16 per beat), timed to land through the beat; x uniform 290-726.
- **Tension = the XPBD multiplier of the end links** (lambda / h^2), shown at real gravity (the sim runs a brisk g = 1,400 px/s^2 = 3.9 g, so kN are scaled by 9.81/38.7), smoothed 0.25 s, running max before the snap. **The limit = the tension at the snap beat** (28.7 kN for 2,940 kg: T = W / (2 sin theta) at the ~30° rope angle, consistent).

## Timeline (clip s, seed 2)
- 0.0: 4 balls on the deck, 3 in the air, 4.0 kN. Landings/s 5, 6, 8, 9, 12, 15, 21, 20, 29, 18 (the last second is 0.71 s). Landed 4, 9, 15, 23, 32, 44, 59, 80, 100, 129 -> 147.
- Tension/s 4.0, 5.7, 6.8, 8.1, 9.0, 12.2, 16.3, 20.3, 22.3, 26.1 kN; creaks from 55% (on the beat), every half beat past 80%.
- **9.71 s SNAP** (score beat 22, the cadence into C major) at the left post; the deck swings to the right cliff (21 plank knocks), the balls hit the gorge floor ~10.1-10.6 s. Hold to 11.71 s, 0.6 s dissolve to frame 0. 12.30 s.

## Sound
- **Music:** J. S. Bach, Invention No. 13 in A minor BWV 784 (1723; d. 1750, PD). Mutopia Project `bach-invention-13.mid` (Public Domain; Bach-Gesellschaft), saved at `<SOUNDFONTS_DIR>\scores\bach_invention13\` (+ .rdf). Score beats 0-22 (bars 1-6: the A-minor arpeggio theme, the falling sequence, the cadence into C major on bar 6 beat 3 = SNAP) at a steady 136 bpm; our C-major tutti held under the fall. Not on any used list; not kid-coded; not banned.
- Arrangement: piano both voices (velocity crescendo), pizzicato bass, harp doubling the top line, a string pad from bar 3, timpani roll into the snap; the snap = C major strings, piano, horns, boom, harp roll.
- SFX: a hollow tonal wooden knock per ball landing on a plank, a glassy clack per ball landing on the pile (>= 16 ms, pitched to the score's sounding notes), soft tonal plank creaks (no noise) from 55% stress, a low rope twang + crack at the snap, plank knocks on the cliff, thuds + clacks as the balls hit the gorge floor. Stems: bed -21.2 LUFS, SFX -20.1. `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 738 frames, 12.30 s. **flash_check PASS** (0 flashes).
- **-14.00 LUFS**, peak -6.08 dBFS, last 0.5 s digital silence. RMS/s (audio test) -18.3, -17.1, -16.9, -17.5, -17.0, -16.6, -15.9, -16.1, -15.0, -13.7 (snap), -14.0, fade, silence. SFX events/s 5, 6, 8, 9, 12, 12, 20, 19, 23, 20, 24.
- Seam mean |delta| 0.208.
- Frames read from the mp4 at 0, 0.5, 1.5, 3, 5, 7, 8.5, 9.6, 9.75, 9.9, 10.2, 10.6, 11.2, 12.2 s; 1:1 crops at 9.55 s (full pile, frayed post) and 9.82 s (the deck dropping out under the pile).
- Side safe zone: posts x 182 / 834, bridge between, HUD 166-856: inside 0.10-0.84 w.

## Doubts
- The caption promises the snap, so "will it hold?" is about WHEN; the meter creeping to the gold mark carries the tension.
- 0-3 s: 5-9 landings/s (2-3 balls per beat) is calm; the rate climbs to ~29/s.
- After the snap the pile falls mostly as one blob (it rests on the deck), then spreads on the gorge floor.
- The limit is a chosen strength (= the tension at the snap beat); the creak/fray thresholds follow the honest tension.
- The handrail is drawn (an offset of the deck), not simulated.

## Flags
`--seed (2) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0)`. Physics `--g (1400) --sub (10) --iters (10) --rb (13) --slack (1.09) --alpha (1.6e-5)`. Clock `--bpm (136) --fall (1.7) --hold (0.3)`.

## Upload draft
- Titles: "Every ball that lands adds WEIGHT… until the bridge SNAPS 🌉 #satisfying #physics #shorts" · "How much weight can a rope bridge hold? 🌉 #satisfying #physics #shorts" · "147 heavy balls vs one rope bridge 💥 #satisfying #physics #shorts".
- Pinned comment: "it held almost 3 tons before the left rope gave up… which side did you think would snap first?"

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/ol_rope_bridge.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 738 frames 12.30 s; -14.00 LUFS, peak -6.08 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed fhd3 (+ the batch61 hand-rope ties, drawing only). Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-09\2_ol_rope_bridge.mp4`, 16:00 local Nov 10 (= 07:00 US East Nov 10). FHD review copy → `DopamineExe\archive\ol_rope_bridge_fhd.mp4`.
