# ol_marble_elimination (DopamineEXE, channel 2)

## v2 (batch60, 2026-10-30): obstacle course, PICK YOUR MARBLE, bigger, slower eliminations
Owner on v1: "needs something more satisfying than circles; more challenging; let the viewer choose a marble; they go out too fast". v2:
- **8 named marbles, r 38** (v1: 10, r 30): RUBY, BLAZE, AMBER, LIME, TEAL, AZURE, IRIS, ROSE. Names 22/19 px inside.
- **Course** (logical px, static camera): lift tube x 815-901 (y 455-901) -> ramp A (812,492)->(340,572) with a stop lip at the top -> **SPINNER** (red bar, hub (580,420), half-length 100, 2.4 rad/s, the lower arm sweeps WITH the flow but slower: it holds marbles back or bats them) -> **SPLIT** peg (250,660) r 18 + a pin (362,735): left = a long run-up on the bridge, right = a short one -> **BRIDGE** (planks on a truss) near side (130,800)->(430,856), a **GAP** of 103 px, far side (533,925)->(836,965) (a 69 px step down) -> **LAP** post x 620 + gold trapdoor x 640-770 -> the tube. A marble too slow for the gap (threshold ~680 px/s) drops into a cup of the **WHEEL LIFT** (centre (450,980), r 140, 6 cups, 3.0 rad/s, its top turns back) and rides it ~330 deg before it is tipped onto the far side (~2 s penalty). Eliminated marbles fall into the **OUT** bin (x 640-901, floor 1234) and pile there, greyed.
- g 4,000 (v1 6,500), lift 1,500 px/s: slower and readable. Same impulse physics as v1 + a kinematic spinner capsule (surface velocity in the contact).
- **PICK YOUR MARBLE**: 0-1.5 s the 8 marbles in a 2x4 lineup (r 54, names 30 px in their colour) over the dimmed course; 1.5-1.9 s they fly to the starting grid (5 on ramp A behind a gold gate, 3 in the tube); **GO!** at 1.9 s (the gate drops).
- Seed **10** (scan 1-30; kept: ~2 leader changes, no jams, final 21-25 s): out ROSE 8.13, RUBY 10.58, TEAL 13.72, AZURE 15.36, AMBER 18.32, BLAZE 21.05, **IRIS 22.53 -> LIME WINS**. Gaps 2.4-3.1 s (v1 1.1-2.5 s; ~19/min vs ~38/min). Leader TEAL -> BLAZE (9.5 s) -> LIME (18.7 s). Wheel catches: AZURE 4.0, ROSE 5.5, RUBY 7.9, TEAL 8.8 + 10.8, BLAZE 18.3 (the two early leaders both lost it at the gap). Hold 1.8 s, 0.6 s dissolve to the lineup. **24.93 s, 1,496 frames.**
- Caption unchanged: `Every lap the ^LAST^ marble is out…|until ~ONE~ wins` (`^x^` = the leader's colour; gold-white during the lineup).
- **Music:** the same Tchaikovsky "August: Harvest" (PD, Mutopia), new splice: score beats 0-21 (theme, bars 1-7) + 45-108 (the second ending, the development and the F# dominant run-up), so the B-minor return (score 108 = music beat 84) is our tutti at the last elimination. Quarter = 224 bpm (dotted quarter 149), set by T_WIN. String pad on the F# dominant from music beat 72.
- Delivered `<VIDEOS_DIR>\DopamineExe\review\ol_marble_elimination.mp4` (Full HD, label v2); v1 archived as `archive\ol_marble_elimination_v1.mp4`.
- Checks (encoded): h264 High yuv420p 1080x1920 60 fps, 1,496 frames; -14.00 LUFS, peak -6.55 dBFS, last 0.5 s digital silence; flash_check PASS; seam mean |delta| 0.240. Frames read at 0.5, 1.7, 2.0, 4, 5.9, 8.2, 10.7, 13.8, 18.4, 21.1, 22.6, 24 s; 1:1 crop at 8.2 s (ROSE OUT!, RUBY over the gap, AMBER at the line, names legible).
- Side safe zone: course x 122-901, lineup 169-847, HUD 166-884 (the tube's right wall at 901 = 0.834 w).
- Doubts: the first elimination comes at 8.1 s (lineup 1.9 s + the whole field must finish lap 1); the race is decided mostly at the gap (a catch costs ~a lap); 25 s is long for the format (owner asked for fewer eliminations per minute); the start is a grid (front of the grid starts ahead).
- Flags: `--seed (10) --pick (1.5) --hold (1.8) --g (4000) --r (38) --vlift (1500) --spinw (2.4) --wheelw (3.0) --gapx (533)`; `--scan a-b`; `--leadin` removed.
- Upload draft: "Every lap the LAST marble is out… until ONE wins 🏁 #satisfying #physics #shorts" · "Pick your marble: only ONE survives the gap 🏁 #satisfying #physics #shorts" · "Two leaders fell into the wheel… LIME didn't 😬 #satisfying #physics #shorts". Pinned: "who did you pick? two leaders fell into the wheel and lime just kept rolling…"

## v1 (batch59)
- Batch 59 (docs/BRIEF_batch59.md #5). The marble-race genre, side view: **10 named glass marbles** run a loop: a lift tube carries them up, they roll down a ramp with a bump, rain through a pin board, land on the gutter and roll over the LAP line. **The last marble to cross the line each lap drops through a trapdoor** into the OUT tray (they line up there in order, greyed). 10 → 1; the physics decides who goes and who wins.
- Caption (baked, `--cap`; `--cap ''` = base): `Every lap the ^LAST^ marble is out…|until ~ONE~ wins` (`^x^` = the current leader's colour).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_marble_elimination.mp4` (Full HD, seed 17, label fhd, **16.95 s, 1017 frames**). No 4K yet.
- Why 10, not ~12: one lap takes ~1.9 s (lift 0.25 s + ramp + pins + gutter), so 11 eliminations would need ~21 s + the finale; 10 marbles = 9 eliminations in 14.8 s, inside the brief's 15-20 s.

## World (logical 1080x1920, static camera)
- Marbles r 30 (60 px), glossy glass with a rotating swirl; names upright in the marble (17/15.5 px bold, outlined). Colours: RUBY red, BLAZE orange, AMBER yellow, LIME, JADE green, TEAL, AZURE blue, IRIS violet, ROSE pink, FROST ice.
- Track (one thin white line): lift tube x 830-894 (y 388-1124, chevrons running up), ramp (826,464)→(548,540) with a bump and a kicker, pin board walls x 186 / 822, 4 staggered rows of pins (y 612-822, 104 px apart; no pin closer than 1.6 D to a wall, so nothing wedges), gutter (188,925)→(836,1104), checkered LAP post x 598, gold trapdoor x 612-762 right after the line (hinged at its right end, swings down), OUT tray (790,1160)→(196,1208).
- Leader: gold crown on the marble furthest along the course (laps × lap length + distance since the line), a change must hold 0.35 s. "NAME OUT!" pop over the door per elimination. Winner: gold ring + pulses + big crown.
- HUD: meter y 1300 = LAP n/9, one coloured notch per eliminated marble, gold "1 WINNER" → "ROSE WINS!". Counter y 1500 = MARBLES LEFT + "LEADER <NAME>" pill (→ "WINNER ROSE"). Watermark 35%.

## Physics (`simulate`, seeded; ~10 s CPU, cached `output/_cache_ol_marble_elimination_<hash>.pkl`)
- Discs with impulse contacts against capsules (ramp, walls, pins, bump, gutter, door, tray) and each other: restitution walls 0.30, pins 0.38, marble-marble 0.50 (0 below ~120 px/s, so they settle), no sliding friction (rolling), spin = tangential speed / r. g 6,500 px/s², 10 substeps x 2 iterations.
- Lift: kinematic, 2,600 px/s, one marble per slot (gap 2r+8), order preserved; release at the top rolling left at 760-860 px/s.
- Lap rule: a marble crossing the line is the target if every other marble still racing has at least as many laps; the door is open for the target only (the door capsule is switched off for it), it falls into the tray.
- Seed choice: `--scan` over 1-40 (rejects jams: a racing marble that moves < 6 px in 1 s). Seed 17 = the early leader is the one eliminated LAST, a 0.2 s final duel.

## Timeline (clip s, seed 17)
- Out: IRIS 0.69, BLAZE 3.14, RUBY 5.07, TEAL 6.98, JADE 8.49, LIME 10.29, FROST 12.40, AMBER 13.65, **AZURE 14.76** (gaps 2.45 → 1.11 s: the eliminations come faster as the field thins).
- Leader: AZURE leads 1.1-7.0 s, ROSE takes over at 7.0 s. Final lap: ROSE crosses at 14.49, AZURE 0.2 s behind at 14.69 → the door → **ROSE WINS at 14.76**. Hold 1.6 s (ROSE rides the lift alone with the crown), 0.6 s dissolve to frame 0.

## Sound
- **Music:** P. I. Tchaikovsky, The Seasons Op. 37a No. 8 "August: Harvest" (1876; d. 1893, PD), the B-minor Allegro vivace in 6/8. Mutopia `Tschaikowsky-op37.8.mid` (Public Domain), `<SOUNDFONTS_DIR>\scores\tchaikovsky_seasons_aug\` + SOURCE.txt. Score beats 0-45 (bars 1-15: the theme and its repeat) + bar 8 again as the repeat's first ending (the F#7 dominant), landing on our B-minor tutti at beat 48 = the last elimination. Steady dotted quarter = 130 (set so beat 48 = 14.76 s). Not on any used list; not kid-coded; not banned. (January and February of the same set were used today on Mochi & Bolt: different pieces, same composer/set.)
- Arrangement: piano (both hands), violin on the top line, pizzicato bass per dotted quarter, a soft string pad from bar 9, timpani roll into the end; finale = B-minor strings, piano, horns, timpani B, harp sweep, falling celesta.
- SFX: glass tink per pin hit (G5-G6 on the score's sounding notes), crisp glassy clack per marble-marble hit, a round tock per landing on the track/tray; the trapdoor = a wooden clack + a low tone falling a major third (pleasant, no buzzer). Sampled ≥ 22 ms apart, gain / (rate/6)^0.4. `level_bed` (+4 dB crescendo, finale +5 dB), `audio.master(peak_db=None, reverb=0.40)`, last 0.6 s digital silence.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 1017 frames, 16.95 s. **flash_check PASS** (0 flashes).
- **-14.00 LUFS**, peak -6.59 dBFS, last 0.5 s digital silence. RMS/s (audio test) -17.6, -18.4, -17.5, -16.8, -17.6, -17.0, -16.7, -16.2, -16.0, -16.2, -15.8, -16.3, -15.7, -15.9, -15.5, -15.3, fade.
- Seam mean |delta| 0.218.
- Frames read from the mp4 at 0.5, 3.1, 7.0, 12.4, 14.5, 14.8, 15.6, 16.8 s; 1:1 crop at 14.70 s (AZURE on the open door, ROSE crowned in the lift, the OUT row with readable names).
- Side safe zone: track x 186-894, HUD 166-884: inside 0.10-0.84 w (the tube's right wall at 894).

## Doubts
- **The physical hit rate falls** as marbles are eliminated (88 → 13 contacts/s; SFX 25 → 12/s): fewer racers. What climbs is the elimination pace (2.45 → 1.11 s apart) and the music.
- Only 2 leader changes (AZURE → ROSE at 7 s); the drama is the early leader going out last, by 0.2 s.
- 10 marbles instead of ~12 (length, see above). Names inside a 60 px marble are small on a phone; the OUT pop and the leader pill carry them.
- The door opens only under the target (for the others it stays solid): no case in this seed where another marble is on it.

## Flags
`--seed (17) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0) --scan a-b --leadin (0.7) --hold (1.6)`. Physics `--g (6500) --sub (10) --vlift (2600) --r (30)`.

## Upload draft
- Titles: "Every lap the LAST marble is out… until ONE wins 🏁 #satisfying #physics #shorts" · "10 marbles, 9 laps, 1 trapdoor: who survives? 🏁 #satisfying #physics #shorts" · "AZURE led for 6 seconds… and still lost by 0.2 s 😬 #satisfying #physics #shorts".
- Pinned comment: "azure led half the race and still went out last by a hair… who were you rooting for?"

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/ol_marble_elimination.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 1496 frames 24.93 s; -14.00 LUFS, peak -6.55 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed v2. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-09\1_ol_marble_elimination.mp4`, 04:00 local Nov 10 (= 19:00 US East Nov 9). FHD review copy → `DopamineExe\archive\ol_marble_elimination_fhd.mp4`.
