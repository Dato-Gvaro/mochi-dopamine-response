# melon_bands — Mochi adds +1 rubber band a beat, Bolt DOUBLES his every round: which melon SURVIVES? (batch50, 2026-10-24/25)

## v3 = owner review fix (2026-10-25) — CURRENT
- Owner on v2: "I don't get who won — Bolt's melon burst but he got more bands, so?" and "that classical music, I don't know how it fits."
- **Goal flipped:** caption "Mochi adds ~+1~ band, Bolt ~DOUBLES~ his:" / "which melon ~SURVIVES~?". Bolt pulls ahead in bands at 8.85 s ("BOLT PULLS AHEAD!", he cheers), the burst on the 13.1 s accent = he LOSES: "MOCHI WINS!", HUD Mochi WINNER / SURVIVED!, Bolt OUT / BURST!. Splatter, slice hat, deadpan kept; his sticker is now "oops.". Mochi: smug laugh at 11.3 s, cheer on the burst, laughs to the end. "IT'S CRACKING..." -> "NEAR THE LIMIT...".
- **Danger readable:** each SQUEEZE meter has a red zone (80-100%) and a red **BURST LIMIT** line (same limit for both); a red "DANGER!" pill over 70%.
- **Music swapped** to Offenbach's **Can-can** (Orphée aux Enfers, 1858, No. 15 Galop; PD). Owner's example William Tell is on the banned list (BRIEF_formula) and was disliked in ellipse_rays5, so the Can-can was used. No other scene uses it; not circus/nursery.
  - Notes read BY EYE from the 1860 Heugel piano score (BnF bpt6k1187743z, Commons pages 82-83 = printed pp. 80-81, PD): `<SOUNDFONTS_DIR>\scores\offenbach_cancan\` (+ SOURCE.txt). No PD MIDI exists on Mutopia/Commons; IMSLP's file host is behind a bot check.
  - Excerpt: the Galop's first strain (D major, 2/4) from bar 4 of the first pass, through the repeat and 2nd ending (13 bars at quarter = 120), to the **ff tutti downbeat = the burst** (clip 13.1 s), then a held D-major chord. Harmony simplified to triads (I-I-IV-I-V7-I, V/V-V | V7-I).
  - Arrangement: violins on the tune (+ clarinet/oboe an octave down), pizzicato + basses on the bass 8th, staccato strings/pizz + soft horns on the off-beat chords, light timpani every 2 bars; ff accent = D-major tutti + brass + timpani.
- Checks (v3 encoded): 1080x1920 h264 yuv420p 60 fps, 954 frames = 15.90 s; -14.01 LUFS, peak -2.00 dBFS, last 0.5 s silent; RMS/s -18.1 -18.2 -17.6 -17.6 -17.3 -17.3 -16.7 -16.7 -16.3 -16.3 -15.8 -15.6 -15.2 -13.7 -17.3 (tail -29.3); finale -11.9 vs body -15.5; energy > 4 kHz 0.33%; SFX events/s unchanged (4 2 3 4 5 4 8 7 11 13 19 21 21 26 6 0); flash_check PASS (0); seam 1.24 encoded (motion-continuous, see v2 note). Encoded frames read at 0, 2, 8.95, 13.12, 14.6, 15.88 s + HUD crop at 14.6 s.
- Doubt: the transcription is from a piano reduction read by eye (pitches checked against staff positions; graces dropped, left-hand voicings simplified).

## v2 (superseded): Vivaldi Autumn, "whose melon BURSTS first?", "BOLT WINS!" — notes below describe v2 unless v3 changed them.


- Brief: docs/BRIEF_batch50.md ("melon_bands"). New scene file; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch50\melon_bands.mp4` (**v2**, Full HD 9:16, 15.90 s).
- Caption (baked; `--nocap` gives the base): "Mochi adds ~+1~ band, Bolt ~DOUBLES~ his:" / "whose melon ~BURSTS~ first?"
- **Twist:** doubling wins, and the win punishes him. Bolt's melon bursts and rains down on him: a slice lands on his head like a hat, pink juice and seeds drip off him, and he says a deadpan "yay." while Mochi laughs.

## Layout
- Two identical round watermelons (R 162, half-height 170) sit on a wooden table: Mochi's at x 300, Bolt's at x 716. The edges are at 138 and 878, inside 0.10–0.84w.
- Big band counters sit above each melon (112 px, y 556). There is a "+1" pop on every Mochi snap and a gold "×2!" at the start of each Bolt round.
- The characters (r 78) stand on the floor in front of the table (Mochi x 200, Bolt x 820), each with a bucket of bands.
- HUD panel (y 1352–1538) for each side:
  - name + rule ("MOCHI +1" / "BOLT ×2");
  - live line ("ONE BAND EVERY BEAT" / "ROUND 5: +16 BANDS");
  - a SQUEEZE meter to the burst line, with a percentage;
  - a LEADING / WINNER pill.
- Calm camera: no zoom, no shake. The only motion that is not part of the story is a tremble of Bolt's melon (±1.8 px) above 72% squeeze.
- Colours:
  - Melon greens at saturation ~0.6.
  - Band hue follows its index (coral → orange → gold → sky → blue → violet → rose, sat ~0.6–0.7). This means the belt colour is a second counter.
  - Background: a dark plum wall, wood and two warm lamp pools. No white flash anywhere.

## The rule (the readable cause)
- **One squeeze law for both melons:** pinch P = 0.46·(n/96)^0.6, plus a small pulse on each snap.
  - The waist pinches into an hourglass and the lobes bulge.
  - The band belt grows (14 + 5.2√n px).
  - 12 cracks plus branches open at fixed squeeze thresholds (5%…88%) and grow from the belt toward the poles. They are drawn as dark zig-zags with a pink flesh core.
  - Above 70%, juice beads at the cracks. The melon bursts at 96 bands.
- **Mochi:** one band per beat (quarter = 120). She has 4 at frame 0, snaps band 5 at 0.1 s, and reaches 30 at the burst, which is 31% squeeze with 4–6 cracks visible.
- **Bolt:** band 1 is on at frame 0. Round r (one bar = 2 s) adds 2^r bands spread evenly across the bar, so the counter reads 2, 4, 8, 16, 32, 64. Round 7 adds 64 bands at 32/s, and the melon bursts after 32 of them, at 96.
- **Band flight:**
  - Each band is lobbed from the bucket UP THE GAP between the melons (Mochi 0.75 s; Bolt's first rounds use a 1.0 s lob).
  - It arcs over its own melon's top, is pulled down (0.12 s) and snaps tight with a damped overshoot.
  - In Bolt's last rounds the gap becomes a spiral stream of rings. Because the rings travel up the gap, they never cover the melon face.

## Timeline (clip seconds; the clip opens 0.1 s before the downbeat)
- **0.0 s:** both melons have their next band being pulled down over the top. Mochi's following band is rising up the gap. Bolt bobs to the beat.
- **0.1 s:** first snaps on the music's downbeat (Mochi band 5, Bolt band 2).
- **0.5 s:** 5 / 2. Mochi's band 6 is mid-lob in the gap and her belt still wobbles from the snap.
- **1.0 s:** 6 / 2. Mochi's band 6 snaps on and her first crack is already visible.
- **2.0 s:** 8 / 2. Bolt's 3rd band is in its high lob; it snaps at 2.1 s with "×2!".
- **6.1 s:** Mochi leads 17 / 8 (she cheers).
- **LEAD CHANGE at 8.85 s:** "BOLT TAKES THE LEAD!". Mochi goes "wow" and from then on watches his counter.
- **11.1 s:** "IT'S CRACKING..." (Bolt at 49+; the hourglass is deep and the cracks run to the poles). Both get worried.
- **BURST at 13.10 s, on the cadence:**
  - All 96 bands spring off.
  - The top half blows into 6 big slices, 18 flesh bits, 26 seeds and 46 juice drops.
  - The bottom half stays as a ragged bowl full of seeds.
  - "BOLT WINS!" (96 vs 30).
- **≈13.95–14.1 s:** the aimed pieces land on Bolt: 8 splats, 8 drops, 4 seeds, and the slice hat at 14.08 s. Bolt winces.
- **From 14.2 s:** Bolt is deadpan (annoyed lids, eyes on the viewer), dripping. A drip falls off him every 0.52 s and a pink puddle grows.
  - "yay." appears at 14.55 s. Mochi laughs ("HA HA") until the dissolve.
- **15.30–15.90 s:** dissolve into the pre-roll (sim −0.6 → 0). The HUD switches at the midpoint.
- **Growth:** Mochi 4 → 30 (+1 a beat). Bolt 1 → 96: ×2 a round, 6 doublings plus half a round.
  - Bands snapped per second: 3 2 3 3 4 4 6 6 10 10 17 18 33.

## Sound (music first)
- **Piece:** A. Vivaldi, *The Four Seasons*, Autumn (L'autunno) RV 293, 1st mvt Allegro (1725; Vivaldi d. 1741, PD). It is famous, festive, not kid-coded, and not on any used or banned list. No other scene uses it.
  - Source: Mutopia-2010/02/08-350, `<SOUNDFONTS_DIR>\scores\vivaldi_autumn\mids\autumn-score.mid` (+ `info.html`, `SOURCE_mutopia_350.txt`).
  - The engraving/MIDI is CC BY-SA 3.0. Only the PD composition's pitches and rhythms are read, as with vivaldi_winter.
- **Excerpt:** the opening ritornello from the bar-2 downbeat (score beat 4) to the **bar-8 beat-3 F-major cadence (beat 30) = the burst at 13.10 s clip**. One steady tempo, quarter = 120.
- **Arrangement** (lib/orchestra, MuseScore_General):
  - solo violin, tutti violins I/II, viola, cello, contrabass an octave down, and a soft harp doubling violin II;
  - a CC11 crescendo;
  - **cadence:** a held F-major chord (strings_slow, horns, a contrabass F1, a rolled harp, timpani F).
- **SFX** (all tonal; energy above 4 kHz 0.41%):
  - **band snap ("thwip"):** a pitched twang dropping onto a chord tone in 10 ms, plus a soft rind "thup".
    - Mochi: one per beat, climbing slowly with her count.
    - Bolt: gathered on the 32nd grid, each round sweeping up through the chord (a layered voice when 2 bands share a slot).
  - **rind creak:** a low bowed tone with a slow stick-slip ratchet, on the beat when a crack opens, louder with the squeeze. A 1.1 s rising groan through the last bar.
  - **burst:** a deep tonal thump, a rumble, 5 descending twangs (bands flying off) and 14 juicy "bloop" droplets on F-major tones.
  - **landings:** tonal plops gathered on the 8th grid; splats on Bolt; quiet drip plips.
- Mastering: `level_bed` (+2.5 dB crescendo, `--findb 1.5`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS). The last 0.5 s is zeroed.

## Checks (v2, encoded Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 954 frames = 15.90 s.
- −14.01 LUFS, peak −2.00 dBFS, last 0.5 s silent (−240 dB).
- RMS/s: −18.7 −18.4 −18.3 −18.4 −17.7 −17.8 −17.3 −17.3 −17.0 −17.0 −16.2 −16.4 −15.7 −14.0 −17.0 (tail −29.4).
- The finale (13.1–13.5 s) is −12.7 dB against −16.1 for the body.
- SFX events/s: 4 2 3 4 5 4 8 7 11 13 19 21 21 26 6 0. They climb to the burst.
- flash_check PASS (0 flashes, mean luminance 0.033).
- **Loop seam:**
  - Pre-encode, last → first frame is 0.84 mean delta. The frame pair before it is 1.03, so it is one frame of real motion (bands dropping).
  - Encoded check_clip reads 1.25, against adjacent encoded frames at 1.04–1.08 and busy mid-clip frames at 1.3–2.8.
  - The tool's 0.72 band was calibrated on low-motion neon clips. The seam is motion-continuous.
  - v1 (frame 0 exactly on the snap) read 1.45. Hence the 0.1 s offset.
- Encoded frames read at 0, 0.5, 1, 2, 8.95, 12.1, 13.05, 13.2, 13.7, 14.4, 15.2 and 15.88 s.
- 1:1 crops read: Bolt's melon at 12.7 s (hourglass, cracks, the ring spiral) and Bolt at 14.6 s (slice hat, splats, drips, deadpan eyes clear).

## Doubts
- Doubling's win is expected; the hook is the 9 s of Mochi leading and the splatter punchline. Mochi ends at 31% squeeze, which is a real but distant threat.
- Bolt adds just one band in the first 2 s. His side carries the downbeat bob, the 0.1 s snap and a slow high lob from 1.1 s.
- Pink juice on a character: we kept it clearly watermelon (seeds, a slice hat, rounded pink drips, no red streaks). It is worth a glance for the "no blood look" rule.
- Cartoon cheats:
  - the gap-lob flight path;
  - the aimed pieces (solved ballistic arcs onto chosen points on Bolt);
  - a squeeze law that is a curve, not FEM.
- Some burst slices fly off-frame right (decoration).

## Args and cost
- Args: `--seed 7` (burst particles), `--sfx 0.30`, `--findb 1.5`, `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Cost: sim < 1 s; Full HD render ~40 s at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)
