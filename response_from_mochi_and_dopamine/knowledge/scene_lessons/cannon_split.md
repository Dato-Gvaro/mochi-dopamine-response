# cannon_split — Mochi's BIG BALL vs Bolt's SPLIT shell (every piece that hits splits ×3): whose castle is GONE first?

- Brief: coordinator task 2026-10-24 (batch49, docs/BRIEF_overnight_1023.md). New mechanic, new file. It borrows pinball_split's HUD style, faces, banners, captions, dissolve loop and master.
- Not a cannon_duel repeat: that one was sail ships at sea (broadside vs mortar, sinking hulks), and siege_duel was catapult vs trebuchet on a stone wall. This one has brick castles, an exponential cluster split and a rubble pile.
- Caption: "Every piece that hits splits ~×3~" / "~Big ball~ or ~Split shell~:" / "whose castle is ~GONE~ first?".
- Two stacked lanes (side view), each with violet neon panels at x 112-904 (0.10-0.84w): Mochi at y 400-860, Bolt at y 880-1340 (≤ 0.70h).
  - Each lane has a cannon plus its character (left) and an identical running-bond brick castle wall (right).
  - Each wall is 15 × 30 bricks (18 × 10 px) plus 2 merlon rows = 487 bricks, on a ground line with faint far hills.
- HUD inside each lane (sky, top-left): the rule label ("BIG BALL: 18-brick crater" / "SPLIT ×3: N pieces" live), "n / 487 bricks" (gold for the leader), and a meter to GONE.
- Bricks: one calm gradient by row for both castles: deep berry → brick red → terracotta → ochre (sat ~0.68-0.78). Settled rubble is dimmed (×0.58) and lies BEHIND what still stands, so the remaining wall reads. Mochi's balls are coral. Bolt's pieces are coloured by generation (blue → cyan → mint). There is no white flash and no confetti.

## History

- **v1** (2026-10-24): Mochi had 3 bricks per ball, one ball a beat. The lead changed at 8.0 s, and Mochi finished at 28%.
- Owner review: "ok, but the big ball does little damage — let's make it destroy more." The coordinator then asked for:
  - a heavy, destructive crater per hit (10-20 bricks);
  - Mochi clearly leading for most of the clip;
  - a late lead change at ~10-12 s;
  - a close finish, with Mochi at 5-15% left.
- **v2 = the current file and the review file.**

## The rule (each side readable at a glance)

- One gravity (1200 px/s²) for everything. Every flight is a true parabola, and every hit lands on the music grid (180 bpm: beat 20 frames, 8th 10 frames).
- **BIG BALL (Mochi, coral):** a heavy ball (r 15) lands **every 2 beats** on a 2-beat arc. It is aimed at the next brick of a fixed bite order (top-left first).
  - Each impact punches a **crater**: the **18 bricks** nearest the impact point blast outward (120-260 px/s radial, plus her ball's push, spinning up to 15 rad/s). They tumble and pile up.
  - Any brick left with nothing under it falls too (support). Two hits took 19.
  - A thin coral shock ring expands to 76 px over 0.35 s (no flash), and the spent ball fades into the rubble.
  - Rate: 18 bricks per hit, 1.5 hits/s, ≈ 25 bricks/s. Her wall visibly crumbles fast.
- **SPLIT (Bolt, mint):** one shell per bar (downbeat), on a 2-beat lob that **bursts into 3 in the air** above the wall, with a big gold "×3".
  - Every piece that hits a brick knocks it out and splits into 3 on that 8th (small gold "×3", up to 3 shown per 8th).
  - Each new piece is a HIT (an exposed brick reached by a clean arc, 2-5 8ths later), a MISS (it flies off into the rubble) or a DUD (it lands without breaking and fizzles).
  - The hit chance ramps 0.36 → 0.56 over 20 s of sim; hops get quicker over 16 s.
  - It is a scripted branching process: outcomes are chosen, and the arcs are solved to the chosen bricks.
- **Why it turns:** Mochi is linear; Bolt multiplies. He is weak for ~3 s (2-9 bricks/s), then climbs to 48-58 bricks/s from 7 s and passes her at 11.0 s.
- **Collapse:** once ≤ 10% of his wall is left, it comes down on the next downbeat (the cadence). In v2 he had eaten 485 of 487 himself, so only the last 2 bricks crumble.
- Mochi's head start (j0, the impacts before frame 0) is chosen by `pick_j0` so her line crosses his once, at ~`--tlead` 11.0 s. Her last impact lands before the cadence; no ball is fired that never lands.
- Calm camera: static.

## Timeline (seed 3, phase 0; clip s)

- The clip starts at Bolt-sim frame 320. Mochi's j0 is 1.
- **0 s:** Mochi's crater blows out on the downbeat (18 → 36 bricks), with debris flying and the ring. Bolt has 17 pieces in the air, a mid-air "×3", and his next shell fires.
- **0.5 s:** 36 / 20. **1 s:** 54 / 20. **2 s:** 90 / 22. **7 s:** 217 / 115.
- **LEAD CHANGE at 11.0 s** (326 vs 328, with 103 pieces in the air).
- **CADENCE at 14.67 s:** Bolt is GONE (487/487), with "CASTLE GONE! SPLIT WINS!". **Mochi has 416 = 85%**: 71 bricks (15%) still stand as a stump on her rubble.
  - Mochi goes wow, then annoyed, with "again?!". Bolt cheers, then laughs.
- Clip **16.37 s** (982 frames). The last 0.6 s dissolves into the pre-roll.
- **Growth: Bolt 17 → 487 bricks (×29); pieces in the air ~7 → 107.**
- Bricks per second:

  | s | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 (0.67 s) |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Mochi | 36 | 18 | 36 | 18 | 37 | 18 | 36 | 18 | 36 | 19 | 36 | 18 | 36 | 18 | 36 |
  | Bolt | 3 | 2 | 3 | 9 | 16 | 27 | 34 | 48 | 48 | 54 | 54 | 58 | 49 | 41 | 24 |

  Mochi's per-second count alternates because 1.5 hits fall in each second.

## Sound (music first)

- **L. v. Beethoven, Overture to Egmont, Op. 84** (1810; Beethoven d. 1827, PD). The coda, the "victory symphony" (Allegro con brio, F major).
  - Source: Mutopia (full-score MIDI, Breitkopf & Härtel, **Public Domain**), saved at `<SOUNDFONTS_DIR>\scores\beethoven_egmont\Egmont.mid` with `SOURCE_mutopia_egmont.txt`.
  - No other scene uses it. It is not on the used or banned lists, not Chopin, not kid-coded and not circus.
- **Excerpt:** score beats 966-1010 (coda bars 9-19) to the bar-20 F-major arrival on the finale. One steady tempo, quarter = 180.
- **Arrangement** (lib/orchestra): every part is read from the score.
  - Violin I is an octave down, plus a quiet layer at pitch. Then violin II, viola, cello, contrabass (8vb), two horn parts, trumpet, flute, piccolo, oboe, clarinet, bassoon and timpani, with a CC11 crescendo.
  - **Cadence:** a held F-major block, rolled harp, timpani F and a soft boom.
- **SFX** (tonal, nothing above ~5 kHz, no noise):
  - **Thump:** a tonal cannon thump per shot.
  - **Mochi's impact (v2):** a big marimba clack (s 0.85) pitched to the strings' chord near C5, plus a **deep tonal thud** 3 octaves below (sine body gliding onto the note, ~0.25 s decay).
  - **Bolt's knocks:** a crisp clack per 8th on which he knocks bricks, layered 1-6 voices by log2(count).
  - **Burst:** a tonal "tink" at each mid-air burst.
- Mastering: pinball_split's `level_bed` plus `master_keep_lift()` (-14 LUFS, 5 ms lookahead limiter at -2 dBFS). The last 0.6 s is zeroed.

## Checks (v2, encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\cannon_split.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 982 frames = 16.37 s.
- Loudness: -14.01 LUFS, peak -1.99 dBFS. The last 0.5 s is silent (-240 dB).
- **RMS per second (muxed):** -18.0, -18.1, -17.3, -17.8, -17.2, -16.9, -17.0, -17.0, -16.2, -16.6, -16.0, -16.2, -15.8, -15.7, -14.6, -19.4 (tail).
- **Finale:** +4.7 dB over the body. Energy above 4 kHz: 0.45%.
- flash_check: 0 flashes = PASS (mean luminance 0.011). The shock ring is thin and low-alpha.
- **Loop seam:** check_clip mean delta 1.215 (over its 1.1 "broken" mark).
  - Measured at 270x480 gray: 0.914, against plain steps of ~0.56 and other crater/beat steps of 0.52-0.88.
  - Frame 0 is a crater impact plus Bolt's shot, so the step is genuine and is not a cut. The difference is all inside the lanes (HUD and caption ≈ 0).
  - The last frame is clip frame -1 (Mochi 18), fully dissolved.
- Frames read from the encoded file at 0, 0.5, 1, 2, 7, 11.0 (the lead change), 14.7 (the finale) and 16.35 s (the last frame).
- Fast stills read at 0, 0.5, 6.7, 11.0 and 14.73 s, before and after the rubble-behind / dim fix.

## Nits / doubts

- The **seam step is larger** than a plain frame step, because the crater on frame 0 is the event.
- **Bolt's rate peaks at 58/s (11 s), then eases** to 49, 41 and 24 in the last 1.7 s as his wall runs out. The climb to the end was traded for the late lead change plus close finish the owner asked for. Linear vs ×3 can't have a late crossing, a 5-15% margin and a rate rising to the last frame all at once.
- Bolt's process is scripted (chosen outcomes, true parabolas). The 10% collapse rule barely acts in v2 (2 bricks).
- Bolt's counter growth is ×29 (17 → 487), lower than v1's ×240, because his wall must be ~2/3 gone by 11 s.
- About 5% of splits show only 2 new pieces, and arcs may graze brick corners (0.6 r clearance test).
- Mochi's rubble heap is tall (~130 px) but lies behind the standing bricks and is dimmed.

## Args and cost

- Defaults are the shipped values: `--seed 3 --phase 0 --p0 0.36 --p1 0.56 --pramp 20 --dramp 16 --rfin 0.10 --reach 46 --pshell 0.67 --clipk 0.6 --clipend 0.90 --tlead 11.0 --mper 18 --mint 2 --tend 1.70 --fin 2.0 --findb 1.5 --sfx 0.22 --timp 0.40 --boom 0.22`.
- Other args: `--search --seeds a,b` (Bolt lane only), `--report`, `--cache` (pickles the sim in output/; the key includes every sim arg), `--still --frame a,b`, `--audition`, `--reuse`, `--sound 0`, `--label`, `--cap`.
  - Any change to the Bolt sim code reshuffles its RNG, so re-search seeds after one.
  - `--mper 19` gives a 90% finish but a 3-way neck-and-neck at 11.8-12.2 s.
- Cost: sim ~5 s; Full HD render ~8 min at 2 encoder threads.
- Owner review: v1 reviewed ("big ball does little damage"); v2 pending.

## Ship render (2026-10-24)

- The owner approved v2 ("good").
- 4K ship render: `output/cannon_split_ship_9x16.mp4` (`NF_SCALE=2.0 --cache --label ship`, the v2 defaults, encoder 2 threads plus `-rc-lookahead 12`).
- Checks:
  - h264 yuv420p 2160x3840, 60 fps, 982 frames = 16.37 s.
  - -14.01 LUFS, peak -1.99 dBFS; the last 0.5 s is silent.
  - flash_check 0 = PASS; seam 1.074.
- Frames read at 0, 11.0 and 14.7 s.
- Not staged.
