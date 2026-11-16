# domino_branch — Mochi's straight LINE vs Bolt's forking TREE: who knocks down 1,000 first?

- Brief: coordinator task 2026-10-24 (batch49, docs/BRIEF_overnight_1023.md). New mechanic, new file. It borrows press_drill's layout, HUD, faces, banners and dissolve loop, and ol_domino_giant's tonal wood clack.
- Caption: "Every domino knocks ~1~ or ~2~" / "~Line~ or ~Tree~:" / "who knocks down ~1,000~ first?".
- Top view of two tables (violet neon panels, x 118-492 and 524-898, y 412-1292). **Each rival set up exactly 1,000 dominoes, and the whole setup is visible from frame 0** (standing dominoes are drawn dim in their final colour), so the end state is on screen all clip.
- HUD per side: a progress meter to 1,000 (y 1312), the rule label ("LINE: knocks 1" / "TREE: knocks 2", y 1398) and "Down: N" (y 1482, gold for the leader). The faces sit between the labels.

## The rule (each side readable at a glance)

- **LINE (Mochi, coral):** one 16-row snake from the bottom left, 6.0 px spacing, 19 px wide. Every domino knocks one, **one per 16th = 15 a second, steady**.
- **TREE (Bolt, mint):** a binary tree from the bottom centre up, 6 generations: 1 / 2 / 4 / 8 / 16 / 32 branches of 32 / 28 / 28 / 20 / 16 / 12 dominoes (= exactly 1,000).
  - A branch drops one domino per 8th (the tree's dominoes have gaps, so the forks have room).
  - The fork domino at the end of every branch knocks the first domino of BOTH child branches, so his front doubles each generation.
  - Each fork of generations 1-4 pops a small gold "×2" as it fires (cause and effect).
  - Generation heights are fixed shares of the panel (`--hshare 0.19,0.16,0.16,0.17,0.17,0.15`), so the late generations fill the top half. Spacing by generation: 5.1, 6.1, 5.1, 7.2, 8.8, 10.8 px.
- **Why it turns:** the trunk is long and slow (1 per 8th, half Mochi's rate), so the line leads ~2:1 early. The 4th branch generation (4 fronts = 30/s) overtakes, and the 32 twigs (240/s) flood to 1,000 on the cadence.
- Colours: gradient by row (Mochi, crimson → orange → gold) and by generation (Bolt, blue → cyan → mint), sat ~0.7-0.8. Standing dominoes are at 38% of their colour. A fallen domino leans on the next one (a light top face plus a dark gap line). Fresh falls get a small hugging glow.
- **Finale:** at the cadence a soft light ripple runs up the tree from root to twigs (0.42 max lift, no white flash), with the banner "1,000! TREE WINS!". Bolt cheers, then laughs. Mochi goes wow, then annoyed, with "again?!" from +0.45 s.
- Calm camera: static, no zoom.

## Timeline (clip s; frame 0 = bar 94's downbeat, 24 8ths after the first push)

- **0 s:** both runs going. Mochi has 49 down (the bottom row, about to U-turn); Bolt has 24 (the trunk). Both clack on frame 0.
- **0.5 s:** 56 / 27. **1 s:** 64 / 31. **1.2 s:** the first fork (×2 pop). **2 s:** 79 / 46. Mochi is happy and Bolt is worried.
- Forks at 1.20, 4.93, 8.67, 11.33 and 13.47 s.
- **LEAD CHANGE at 7.07 s** (154 vs 152 at 7 s).
- **CADENCE at 14.93 s** (bar 122): the last 32 twig dominoes are knocked on the downbeat, so Bolt has 1,000 and Mochi has 273 (27%).
- Clip **16.63 s** (998 frames). The last 0.6 s dissolves into the pre-roll, and the HUD switches at the midpoint.
- Hits per second (clip):

  | Side | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Mochi | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 | 15 |
  | Bolt | 8 | 13 | 16 | 14 | 18 | 28 | 32 | 28 | 44 | 56 | 64 | 96 | 128 | 176 | 256 |

  The small dips (16 → 14, 32 → 28) are the 8th grid against whole seconds: 7.5 8ths per second.

## Sound (music first)

- **Beethoven, Symphony No. 5 in C minor, Op. 67, 1st movement** (1808; Beethoven d. 1827, PD).
  - Source: Mutopia piece 941 (full orchestral score MIDI, Breitkopf & Härtel 1862-65, **Public Domain**), saved at `<SOUNDFONTS_DIR>\scores\beethoven_symphony5_1\Symphony5_1.mid` with `SOURCE_mutopia_941.txt`.
  - No other scene uses it. It is not on the used or banned lists, not Chopin, and not kid-coded.
  - Flag: BRIEF_batch25 lists "Beethoven 5 on solo piano" as a rejected ARRANGEMENT. This one is the full orchestral score.
- **Excerpt:** score bars 94-121 (the exposition's E-flat closing theme, tutti 8ths, then the fate motif "da-da-da-DUM" in E-flat), and the bar-122 cadence on the finale.
  - One steady tempo: quarter 225 (half = 112.5; Beethoven marks 108). A quarter is 16 frames, an 8th 8 and a 16th 4.
- **Arrangement** (lib/orchestra, MuseScore_General): every part is read from the score.
  - Strings: violin I on strings + solo violin, violin II, viola, cello, bass.
  - Winds: flute, oboe, clarinet, bassoon. Brass and percussion: horns, trumpet, timpani.
  - A CC11 crescendo through the clip.
  - **Cadence:** a held E-flat chord on strings, horns, a short trumpet chord, cello and bass E-flat, a rolled harp run, timpani E-flat and a soft boom.
- **SFX:** ol_domino_giant's tonal wood clack (marimba-like partials plus a 2 ms low-passed tap, nothing above ~5 kHz, no noise). Its pitch class is the bass note sounding at the hit, so it is always consonant.
  - Mochi: one crisp clack per 16th near G5.
  - Bolt: one clack per 8th near G4. It layers 1 + log2(fronts) octave-doubled voices 3.5 ms apart, so it grows from one clack to a six-voice rattle as the branches double. Its gain also grows with log2(fronts).
  - `--sfx 0.20`: the SFX bed sits 5 dB under the music early and 3 dB under it late.
- Mastering: press_drill's `level_bed` (+2.5 dB crescendo, finale `fin_db` 3.8), `audio.master(peak_db=None, reverb=0.5)`, and the last 0.6 s zeroed.

## Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\domino_branch.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 998 frames = 16.63 s.
- Loudness: −14.01 LUFS, peak −5.85 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second (muxed):** −17.8, −18.2, −17.5, −17.7, −17.1, −17.2, −17.0, −16.6, −16.9, −16.2, −16.8, −16.0, −16.0, −16.6, −17.0, −16.6. No second below −18.2.
- **Finale:** 0.4 s RMS +2.8 dB over the body median.
- Clacks: 23 audible per second all clip (15 Mochi + 7.5 Bolt). Bolt's layer count climbs 1 → 6.
- flash_check: 0 flashes = PASS (mean luminance 0.009).
- **Loop seam:** check_clip mean delta 0.755. At 270x480 gray it measures 0.44, against normal steps of 0.002-0.15.
  - The difference is almost all the two counters ticking (48 → 49, 23 → 24) on frame 0, which is a genuine consecutive step.
  - The last frame is sim frame start−1, fully dissolved.
- Side safe zone: caption, panels, labels, counters and characters all sit inside 0.10-0.84w.
- Frames read from the encoded file at 0, 0.5, 1, 2, 7.07, 14.95 and 16.6 s, plus 1:1 crops of the first fork (1.25 s) and the twigs (14 s). Fast stills at 0, 0.5, 1.2, 2, 5.3, 7.07, 11.7, 13.5, 14.3, 14.95, 16.0 and 16.3 s.

## Nits / doubts

- **The standing twigs (gen 5) read as a grid of small horizontal dashes** at the top of Bolt's panel until they fall. Once fallen they become 32 clean mint lanes.
- The lower corners of Bolt's panel are empty (it is a tree silhouette). At the finale the tree fills the top ~55% densely.
- The line and the tree run on different speeds per domino (16ths vs 8ths). The visible reason is "the tree's dominoes have gaps / a long trunk". A sharp viewer may call the setup unfair.
- The audible clack density is constant (23/s). The climb is in Bolt's layering and gain, and in the hit counts (23 → 271 per second).

## Args and cost

- Defaults are the shipped values:
  - Race: `--e0 24 --segs 32,28,28,20,16,12 --beatf 16`.
  - Layout: `--rows 16 --hshare 0.19,0.16,0.16,0.17,0.17,0.15`.
  - Finale and sound: `--tend 1.70 --fin 2.0 --sfx 0.20`.
- Other args: `--label`, `--cap`, `--still --frame a,b`, `--report`, `--audition` (wav + LUFS, RMS/s, events/s), `--reuse`, `--sound 0`.
- The sim is analytic (hit schedule on the music grid), so there is no cache.
- Cost: about 4 min Full HD at 2 encoder threads (it is mostly the audio render).
- Owner review: pending.
