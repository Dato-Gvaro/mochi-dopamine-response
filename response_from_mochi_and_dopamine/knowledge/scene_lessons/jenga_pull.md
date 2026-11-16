# jenga_pull — Mochi slides 1, Bolt yanks 2: whose tower falls first LOSES (batch51, 2026-10-25)

- Brief: docs/BRIEF_batch51.md ("jenga_pull") + BRIEF_batch50 lessons (the win must look like winning; the music must fit the mood). New scene file; lib/ and tools/ untouched. Style, HUD, banners, reactions and the rigid-body solver are copied from box_tower.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch51\jenga_pull.mp4` (**v1**, Full HD 9:16, 13.08 s, 785 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "Pull blocks until the tower ~FALLS~:" / "whose tower falls first ~LOSES~".
- **Twist:** the faster puller loses. Bolt leads the count from frame 0 to the end (20 vs 15). His drag leans his tower more with every yank; his 20th yank topples it onto him. Mochi's last careful slide lands on the cadence, and her hole-y tower is still standing.
- This is a two-character duel. The DopamineEXE ol_jenga_giant (one giant tower + robot arm) must stay visibly different.

## Layout
- A den: a slate-plum wall, wainscot panels, warm lamp pools and a walnut floor at y 1250.
- Two identical 18-level towers in a light oblique view, so both layer types read. Depth recedes up-right at 0.212 px per px, which shows the top and right faces.
  - End layers (even levels) show 3 end faces of 58 × 34. Bar layers (odd levels) show the long face of the front bar, 174 × 34.
  - Natural maple, a touch darker low in the tower (ordered).
  - The accents are painted: coral (Mochi) and mint (Bolt). End faces get a centre dot; bars get painted tips.
- Towers stand at x 345 (Mochi) and x 625 (Bolt). Mochi (r 46) is at x 156 with her crate at x 14–104. Bolt is at x 850.
- Key content sits inside x 0.10–0.84w. The crate and the right end of the debris pile go wider.
- A tag above each tower shows the count + "PULLED", and a LEAN pill under it:
  - the pill colour goes green → amber → red with the tip risk;
  - at the end Mochi's pill reads "STILL STANDING" (gold) and Bolt's "FELL FIRST!" (red).
- Dashed plumb lines rise from both bases. Bolt also gets a coloured lean line once his lean passes 0.8°.
- HUD (y 1362–1544) has the header "TOWER FALLS FIRST = LOSES", which becomes "BOLT'S TOWER FELL FIRST". Each side shows:
  - its count, "PULLED" and a WOBBLE meter (a green → amber → red track);
  - its rule ("SLIDES 1 PER BEAT" / "YANKS 2 PER BEAT");
  - a pill: AHEAD (Bolt), then WINNER for Mochi and LOST for Bolt.
- **Win state:**
  - Mochi: a gold glow behind her standing tower, a gold frame around it, sparkles, "MOCHI WINS!" and a WINNER pill.
  - Bolt: a pile on the floor around him, a red "OUT!" stamp over it, FELL FIRST! and LOST; he is annoyed, with dazed stars and "rematch?".
- Calm static camera, no white flash.

## Rule and physics (honest statics + rigid-block crash)
- Players never touch the top two levels, and every bar layer keeps its middle bar.
  - **Mochi** slides the LEFT end block of end layers, or the front/back bar of bar layers, toward herself with a smooth ease, then tosses it into her crate. One per bar (2/4) until bar 28, then one per beat; the last one lands on the cadence.
  - **Bolt** yanks the RIGHT end blocks and front/back bars toward himself, one per beat (two per bar). The block shoots out and flies off over his shoulder.
- **Drag:** each yank drags every level above it toward him by (1.0 + 0.25·k) × 58/54 px, and the 20th by 15 px (the hardest yank). Mochi's careful slide nudges by −0.3 px.
- **Static check (`statics`):** for the floor and every level interface, the centre of mass (x AND depth) of everything above must lie over the contact patch's hull.
  - The hull is the overlap of the end blocks' x extents with the bars' depth extents. It is a rectangle, because the patches form a product grid.
  - Bolt's end layers miss their right block, so their support ends 29 px right of centre, and his drag moves the weight right.
  - His min margin falls 29 → 3.7 px (19 pulled, top drift 66 px, lean 6.2°). It reaches **−8.6 px at pull 20**, the right block of level 2. The scene asserts that 20 is the first unstable count.
  - Mochi's min margin stays ≥ 18.5 px (depth, level 7); her lean is ≤ 0.4°.
- **Rocking (cosmetic):** each yank rocks Bolt's tower about its base corner, 0.15° → 1.85° and growing. It fades out before the 20th yank so the crash starts from the static pose. Mochi's rock is 0.1°.
- **Crash = 2D rigid-block sim** (box_tower's sequential-impulse solver, generalised):
  - per-body sizes; depth masks (end blocks collide with everything; bars only with bars in the same depth slot);
  - dt 1/480, 16 iterations, gravity 2400, block friction 0.22, floor 0.55, restitution 0.40;
  - colliders: the floor, Bolt's body (a circle), Mochi's tower face (x 435) and a wall just past the frame edge (x 1095).
  - It starts 0.08 s after the 20th yank, with the yank's momentum on the levels above (`--kick` 200 px/s).
  - Result: the upper tower shears, tips right and falls across Bolt, then scatters into a pile up to the frame edge. An 8-block stub stays.
  - The first floor hit is at sim 9.01; blocks bonk Bolt from 9.01 on.
  - The sim is cached as `output/jenga_pull_crash_<params>.pkl`; `--resim` forces a new one.
- Growth: Bolt +2 per bar (3 → 20), Mochi +1 per bar, then +2 per bar from bar 28 (2 → 15). Bolt is ahead in the count the whole time.

## Timeline (clip s; clip = sim + 0.18)
- **0.0 s:** Mochi 2 vs Bolt 3 pulled, holes in both towers. Mochi's bar is mid-slide; Bolt's arm is reaching. Both pulls clear at 0.18 s, and Bolt's block flies off by 0.2 s.
- **0.5 / 1 / 2 s:** 3 v 4, then 3 v 5 ("2× FASTER!" next to Bolt, who laughs), then 4 v 7 (Bolt's lean 1.0°). Something is moving on both sides in every frame.
- **5.2 s:** "IT'S WOBBLING..." (Bolt 14, lean 3.1°). Bolt is worried from 6.2 s; Mochi glances over at 6.7 s.
- **8.18 s (bar 28):** the 20th yank, then "UH-OH...", a long tonal creak, and the tower shears and tips.
- **9.2 s:** "CRASH!" The column comes down across Bolt and blocks bonk him (wince → annoyed + dazed stars). Mochi's sprint runs at one per beat.
- **10.18 s (cadence, bar 30 downbeat, ff):** Mochi slides out level 2's left block, the same spot that killed Bolt's tower, and hers stands.
  - "MOCHI WINS!", gold glow + frame + sparkles, STILL STANDING, the OUT! stamp, WINNER 15 vs LOST 20.
  - Mochi cheers, laughs, then gives a smug smile at the pile. Bolt shows "rematch?" at 11.2 s.
- **12.48–13.08 s:** dissolve into the pre-roll (the last frame is pure pre-roll). The HUD switches at the midpoint.

## Sound (music first)
- **Piece:** Edvard Grieg, *Troldtog* ("March of the Dwarfs"), Lyric Pieces Op. 54 No. 3 (1891; Grieg d. 1907, PD).
  - It fits "when will it fall": a creeping pp staccato that becomes a long chromatic crescendo and lands on a fortissimo D.
  - Not on any used/banned list and not used by any other scene (Troldhaugen is a different Grieg piece). Not kid-coded. The title is not shown anywhere.
- **Source:** Mutopia-2015/06/14-2014 (MIDI + LilyPond placed in the **public domain** by the typesetter; C.F. Peters edition ca. 1891). Saved at `<SOUNDFONTS_DIR>\scores\grieg_troldtog\Troldtog.mid` (+ `.ly`, `SOURCE_mutopia_2014.txt`). Downloaded 2026-10-25.
  - A first pick, Gounod's *Funeral March of a Marionette*, was dropped: no PD MIDI was found and IMSLP downloads are bot-gated.
- **Excerpt:** from the end of bar 19 to the **bar-30 downbeat** (MIDI quarter 58), at one steady tempo, quarter = 0.50 s (120 bpm).
  - Bars 20–21 are the scurrying pp figure; bars 22–29 the chromatic crescendo over the A pedal.
  - The bar-30 ff arrival is voiced D major (the trio's key) for the win, over Grieg's own ff D-A octave stomps.
- **Arrangement** (lib/orchestra, MuseScore_General):
  - the original texture on soft piano; pizzicato + staccato bassoon on the bass; staccato clarinet on the chords; flute on the 32nd-note scurries;
  - from bar 22: oboe, tremolo strings and contrabass; from bar 26: horns; timpani A on the downbeats and a roll through bar 29;
  - an expression ramp of 0.56 → 1.0;
  - **cadence:** a D-major tutti (strings_slow, brass, horns, contrabass, timpani D) + octave stomps + a celesta arpeggio.
- **SFX** (all tonal):
  - **wood clack** = a pitched body with free-bar partials 1 : 2.76 : 5.40 and a 4 ms attack glide, pitched to the chord sounding;
  - Mochi: soft stick-slip ticks on the 16ths during each slide, a round "tok" on the clear, and a soft tok as the block lands in the crate; three D-major dings at the last pull;
  - Bolt: a bright clack per yank, plus a tonal creak (box_tower's bowed-wood groan) per yank once the rock passes 0.45°, getting louder;
  - a 1 s bending creak at the topple;
  - the **avalanche:** every simulated impact over 130 px/s, gathered on a 32nd grid and pitched to the harmony (lower for harder hits, doubled a fifth up for clusters), plus a "bonk" when blocks hit Bolt.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS). The last 0.5 s is zeroed. The WAV is padded 0.25 s so the mux's `-shortest` keeps all 785 video frames.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 785 frames = 13.08 s.
- −14.01 LUFS, peak −1.93 dBFS (muxed), last 0.5 s digital silence.
- RMS/s: −19.9 −19.0 −19.5 −18.6 −18.7 −18.8 −17.7 −18.2 −15.0 (topple) −13.4 (crash) −12.1 (cadence) −13.8 (hold) −22.3 (fade), then the silent tail.
- SFX events/s: 7 8 9 9 9 9 9 8 11 32 20 0 (the hold carries only music).
- Pulls/s: 3 3 3 3 3 3 3 3 3 2 1.
- flash_check PASS (0 flashes, mean luminance 0.047).
- Seam: pre-encode mean delta 0.155 (the same as one frame of motion, 0.164). Encoded (check_clip) it is 0.692, inside 0.12–0.72 but near the top: the encoder's last P-frame against the I-frame.
- Frames read from the mp4: 0, 0.5, 1, 2, 5.5, 8.3, 8.5, 8.85, 9.2, 9.6, 10.25, 10.3, 12.0, 12.3, 12.5 and 13.06.
- 1:1 crops: the falling column across Bolt (9.2) and the win state (12.0).

## Doubts
- The upper tower shears level by level before it tips (low block friction 0.22). It reads as "it's going", but it is less of a clean single topple than a real jenga tower.
- About a third of the falling column lands past the frame edge (x > 1080). The visible pile is around Bolt (x 530–1080), and its right end is outside the side safe zone.
- One of Bolt's blocks (level 2 left) recoils and ends upright against the base of Mochi's tower. This is physics (her tower is a collider), but a viewer might think it touches her tower.
- Bar-layer pulls only change the shade of the bar you see (the middle bar shows, recessed). The holes that read best are the end-layer ones.
- Cartoon cheats:
  - rubber-hose arms;
  - Bolt's yanked blocks fly off-screen;
  - Mochi's bars turn end-on in the air into the crate;
  - the drag is a scripted per-yank shift, with only its consequences computed (statics, crash).
- The second after the cadence has no SFX (music only).
- Troldtog was newly downloaded; the parallel builders were not checked for the same pick.

## Args and cost
- Args: `--kick 200`, `--mub 0.22`, `--rest 0.40`, `--wall 1095`, `--sfx 0.36`, `--findb 2.0`, `--still --frame a,b`, `--audition`, `--report` (prints per-pull margins/lean + crash timings), `--resim`, `--reuse`, `--nocap`, `--label`.
- Cost: crash sim ~4 s (then cached); Full HD render ~35 s at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)
