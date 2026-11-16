# lantern_chain — Mochi's TORCH (1 lantern at a time) vs Bolt's FUSE (every lit lantern lights 2 more): who lights all 168 first?

- Brief: coordinator task 2026-10-24 (batch49, docs/BRIEF_overnight_1023.md). New mechanic, new file. It borrows domino_branch's HUD, faces, banners, captions and dissolve loop, and pinball_split's `master_keep_lift`.
- **Breaks the batch pattern** (4 batch49 videos end with "the doubler wins late, the loser says again?!"). Bolt lights his half first, but **his chain doesn't stop at the middle pole**. The last generation's sparks race across into Mochi's half and light every lantern she hasn't reached yet. The very last one catches next to her torch on the cadence, so the **whole night sky is lit at once**.
  - Ending: no "X WINS" banner. It reads "WHOLE SKY LIT!", Bolt goes smug with a "you're welcome" sticker, and Mochi gives him a flat stare.
- Caption: "Every lit lantern's fuse lights ~2~ more" / "~Torch~ or ~Fuse~:" / "who lights all ~168~ first?". The answer is Bolt, at 12.27 s. Then he lights hers too.
- Layout: one night-street panel (violet neon frame, x 118-898, y 404-1292) split by a middle pole at x 508.
  - Each half has 14 wires × 12 paper lanterns = 168, so 336 in all, **all hanging dim from frame 0**.
  - Mochi and Bolt stand on the street at y 1246.
  - HUD per half: a meter (y 1322), the rule label (y 1398) and "n / 168" (y 1474, gold for the leader / full).
  - **Mochi's meter fills coral for her own lanterns and mint for the ones Bolt lit in her half.**
- Colours, all warm: Mochi's lanterns go crimson-coral → coral → orange-coral by column; Bolt's go deep orange → amber → gold by generation (sat ~0.65-0.8).
  - The lanterns Bolt lights in her half are gold among her coral, so you can see who lit them.
  - The glow is a radial gradient (r 31) that ramps in over 0.15 s. Lit lanterns sway gently about their hook, with a kick on catching.
  - A faint warm wash grows over each half with its lit fraction. Finale: a +35% glow swell, eased (no flash, no white, no fireworks).
- Calm camera: static, no zoom.

## The rule (each side readable at a glance)

- **TORCH (Mochi):** a long telescopic pole with a small flame. The tip glides to the next lantern and lights it on **every 16th of the music** (3.75/s, steady). She works column by column from the outer edge toward the pole, snaking down and up.
  - 24 lit before frame 0; 81 her own by the cadence.
- **FUSE (Bolt):** one lantern. Every lantern that catches sends **two sparks** along glowing fuses to two more: a complete binary tree, 1 + 2 + 4 + ... + 128 = 255 lanterns.
  - A gold "×2" pops on generations 0-3.
  - The fuse lines stay as faint warm threads, so the tree is visible.
  - The layout is a k-d split of his half (each subtree gets its own region, the node at the region's centre).
  - 41 of generation 7 land in his half and complete it. The other **87 sparks cross the pole**. Their parents are mostly the inner gen-6 lanterns; the pairing was solved as an assignment for the shortest, flattest fuses.
- **Timing (scripted):** one rank order (generation by generation; in generation 7 his own lanterns first, then the crossing wave from the pole inward) mapped onto a cumulative curve N(t) ~ t^2.5. Every light is quantised to the 16th grid.
  - A spark leaves its parent so that it races at ~210 px/s (crossing sparks 150 px/s, 0.8-2.6 s in the air), never before the parent has caught (0.2 s).
  - The constraint 2 × 168 − 81 = 255 makes his tree fill exactly his half plus the rest of hers.

## Timeline (seed 5; clip s)

- **0 s:** 25 / 3. Mochi's torch lights lantern 25 on the downbeat (col 2), and Bolt's 2nd gen-1 lantern catches on frame 0 (its "×2" fades in). One spark is racing. Every lantern of both halves hangs dim.
- **0.5 s:** 26 / 4. **1 s:** 28 / 5, with the gen-2 lanterns catching and ×2 pops. **2 s:** 32 / 9, three sparks in the air.
- **LEAD CHANGE at 6.40 s** (47 / 43 at 6 s, then 51 / 58 at 7 s). Bolt cheers; Mochi goes "wow", then worried.
- **11.9 s:** the first crossing spark passes the middle pole. Mochi: "wow" (she looks at the sparks coming).
- **12.27 s:** Bolt's half is full ("ALL LIT!" over his half). 63 sparks are in the air at 12.5 s, racing into her half.
- **CADENCE at 14.93 s** (bar 8 downbeat): Mochi's last torch lantern (her 81st) and Bolt's last spark land side by side on col 6. 168 / 168 each, with the banner "WHOLE SKY LIT!".
  - Bolt goes smug with "you're welcome" from 15.68 s. Mochi goes wow, then an annoyed flat stare from 15.63 s.
- Clip **16.63 s** (998 frames). The last 0.6 s cross-fades (sky, characters, banner) into the pre-roll, and the counters switch at the midpoint.
- **Growth:** Bolt's lanterns 3 at frame 0 → 255 (**×85**); his half's counter 3 → 168 (×56). Sparks in flight: 1 at 0 s, 3 at 2 s, 14 at 11 s, 63 at 12.5 s.
- Lanterns lit per second:

  | s | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 (0.93 s) |
  |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
  | Mochi | 4 | 4 | 4 | 3 | 4 | 4 | 4 | 3 | 4 | 4 | 4 | 3 | 4 | 4 | 4 |
  | Bolt | 3 | 4 | 7 | 5 | 10 | 12 | 15 | 12 | 20 | 22 | 25 | 21 | 30 | 34 | 33 |
  | all | 7 | 8 | 11 | 8 | 14 | 16 | 19 | 15 | 24 | 26 | 29 | 24 | 34 | 38 | 37 |

  The dips in seconds 3, 7 and 11 are the grid, not the chain: those seconds hold only 3 sixteenths (3.75 per second). Per 16th, Bolt's rate climbs steadily: 0.9 → 1.6 → 2.7 → 3.8 → 5.1 → 6.5 → 7.9 per 2-s bin.

## Sound (music first)

- **Beethoven, Piano Sonata No. 8 "Pathétique" Op. 13, II. Adagio cantabile** (1798; Beethoven d. 1827, PD).
  - Source: Mutopia-2011/10/25-295 (piano; Berners 1908 / Peters 1910, **Public Domain**), saved at `<SOUNDFONTS_DIR>\scores\beethoven_pathetique2\pathetique-2.mid` (+ `.ly`, `SOURCE_mutopia_295.txt`).
  - No other scene uses it. It is not on the used or banned lists, not Chopin, not kid-coded and not seasonal.
- **Excerpt:** the opening theme, bars 1-7, at one steady tempo (quarter = 56.25: a quarter is 64 frames, a 16th 16). Frame 0 = the first downbeat.
  - The cadence is bar 8's downbeat (V → I in A-flat) = 14.93 s.
  - The score's bar-8 appoggiatura is replaced by the resolved A-flat chord.
  - Flag: 56 is about 1.6× the usual Adagio pace (a flowing "cantabile" feel, not a slow one).
- **Arrangement** (lib/orchestra, MuseScore_General): piano plays all three lines from the score (melody, the 16th accompaniment, bass).
  - Strings_slow and a soft violin an octave up double the melody, and cello plus contrabass double the bass. A CC11 crescendo runs through the clip.
  - **Cadence:** a held A-flat chord on piano, strings_slow, cello, bass and a rolled harp. No boom, no cymbal.
- **SFX:** a soft tonal "fwip" chime per light: a sine gliding up into its note over ~10 ms, octave and twelfth partials, a 4 ms soft attack. Nothing above ~5 kHz, no noise.
  - Mochi: one chime per 16th, at the accompaniment note of that 16th an octave up (Eb4-Ab4).
  - Bolt: one chime per 16th on which his lanterns catch, near the melody note (G5-C6), layered with chord tones, 1 + log2(n) voices (1 → 6). It gets louder with log2(n).
  - `--sfx 0.20` keeps the SFX ~3-7 dB under the music.
- Mastering: domino_branch's `level_bed` (+2.5 dB crescendo, `fin_db` 1.8), then pinball_split's `master_keep_lift` (room reverb 0.5, -14 LUFS, a 5 ms lookahead limiter at -2 dBFS). The last 0.6 s is zeroed.

## Checks (encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch49\lantern_chain.mp4)

- Video: h264 yuv420p 1080x1920, 60 fps, 998 frames = 16.63 s.
- Loudness: −14.00 LUFS, peak −2.00 dBFS. The last 0.5 s is silent (−240 dB).
- **RMS per second (muxed):** −18.7, −18.0, −17.1, −18.4, −17.1, −17.2, −16.7, −17.4, −15.6, −16.9, −15.8, −16.4, −16.0, −15.5, −15.9, −15.3, (tail). No second below −18.7.
- **Finale:** 0.4 s RMS +4.8 dB over the body median. Energy above 4 kHz: 0.05%.
- SFX events per second: 7-8 (6 in the 3-sixteenth seconds). Bolt's chime voices per second climb 3 → 16 and hold at ~16 from 10 s (capped at 6 layers per 16th).
- flash_check: 0 flashes = PASS (mean luminance 0.011). Lighting is monotonic (no opposing luminance pairs). Each glow is r 31 and ramps over 0.15 s.
- **Mean luminance** (relative, linear): the finale at 15.4 s (whole sky lit) is 0.053 (sRGB luma 0.112); frame 0 and the last frame are both ~0.052 mean gray /255.
- **Loop seam:** check_clip mean delta 0.865 (just above the 0.72 good band).
  - Rendered (PNG) the seam is 0.146 whole-frame and 0.032 in the sky: only the two counters tick (24 → 25, 2 → 3).
  - The rest is codec noise. The encoded last frame sits 0.68 from its own PNG (frame 0, an I-frame, sits 0.35), and normal consecutive encoded steps are 0.12-0.33.
  - The last frame is clip time −1/60, fully dissolved.
- Side safe zone: caption, panel, lanterns, labels, counters, characters and stickers all sit inside 0.10-0.84w. "you're welcome" spans ~0.58-0.81w; Mochi's left edge is at 0.116w.
- Frames read from the encoded file at 0, 0.5, 1, 2, 6.4, 12.3, 12.6, 14.95, 15.9 and 16.6 s, plus 1:1 crops at 1.0 s (a spark pair leaving a lantern, ×2 pops) and 12.6 s (the crossing sparks at the pole). Fast stills at 0, 1, 2, 7, 11.7, 12.3, 12.7, 13.7, 15.1, 16.0, 16.3 and 16.6 s.

## Nits / doubts

- **Lanterns are small** (22 × 31 px each on a 32 × 52 grid). The sky reads as a field of lights more than as individual lanterns. Sparks are 2-3 px heads with a 10-13 px glow.
- **Frame 0 is darker than a typical batch opener**: Mochi has 25 lit along the left edge, Bolt 3, and the 336 dim outlines show the goal. The big visual (the sky filling) comes from ~8 s on.
- **The crossing is scripted:** the k-d layout, the solved parent pairing and the rank → time curve. Fuse speeds vary (45-238 px/s for the crossing ones). Each spark is cause-and-effect correct (parent lit → spark → child), but the timing is aimed so the last two lanterns meet on the cadence.
- **The tempo is brisk for an Adagio** (see Sound).
- **Bolt still technically "wins"** (his half is full at 12.27 s). The twist is that he then finishes hers and steals her finish. If the owner wants a pure "together" or a Mochi win, the alternative is a wet-fuse stall.

## Args and cost

- Defaults are the shipped values:
  - Chain: `--seed 5 --troot -2.60 --p 2.5 --v 210 --vx 150`.
  - Ending and sound: `--tend 1.70 --fin 1.6 --sfx 0.20`.
- Other args: `--report`, `--still --frame a,b`, `--audition` (wav + LUFS, RMS/s, events/s), `--reuse`, `--sound 0`, `--label`, `--cap`.
- The sim is analytic, so there is no cache. Cost: ~1.5 min Full HD at 2 encoder threads.
- Owner review: pending.
