# egg_drop — Mochi goes +1 floor a drop, Bolt DOUBLES his: whose egg survives the HIGHEST drop? (batch50, 2026-10-25)

- Brief: docs/BRIEF_batch50.md ("egg_drop"). New scene file; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch50\egg_drop.mp4` (**v2**, Full HD 9:16, 14.00 s).
- Caption (baked; `--nocap` gives the base): "Mochi goes ~+1~ floor, Bolt ~DOUBLES~:" / "whose egg survives the ~HIGHEST~ drop?"
- **Twist:** doubling LOSES. Bolt leads 16 vs 12 from 6.65 s, goes for 32 and his egg goes SPLAT. Mochi's steady padded egg survives 17, one floor above his best.

## Layout
- Two identical 32-floor lattice drop towers. Mochi's is at x 262 (coral-tinted steel) and Bolt's at x 758 (mint-tinted). The ground is at y 1300 and the floor pitch is 26.5 px.
  - Each floor has a numbered plate. A plate LIGHTS in the side colour when an egg survives from that floor; the splat floor gets a red X.
  - So the towers are the height meter: Mochi's fills a solid ladder (1-5 are pre-lit), while Bolt's lights 1, 2, 4, 8, 16 and then shows an X at 32.
- Each character rides a lift platform on the inner face of their tower (r 40). The rig hangs from a hook arm at the deck tip.
  - The fall lines are x 448 (Mochi) and x 574 (Bolt), each over a landing pad in the middle of the frame.
- A big floor tag ("13 / FLOOR") rides next to each platform on the outer side: x 150 and x 866, both inside 0.10-0.84w.
- HUD panel (y 1352-1542): "HIGHEST SURVIVED DROP" over each side's name + rule ("MOCHI +1" / "BOLT ×2") and the best survived floor (56 px).
  - It also shows a LEADING / TIED / WINNER pill. After the splat, Bolt's rule line reads "32 FLOORS = SPLAT!".
- Stamps sit on the ground strip under the pads, off the fall paths:
  - Mochi: "SURVIVED ✓" on every landing.
  - Bolt: "OK!", "OK...", "CRACK!", "PHEW!".
- Calm camera: static, no zoom or shake. Dusk sky (navy to plum to a warm horizon), with ordered colours and no white flash.

## The rule (the readable cause)
- **Mochi:** a quilted cushion box plus a parachute. The fall is drag-limited (terminal 600 px/s), so every landing is a soft bounce.
  - She lands one drop a bar (6 at 0.15 s ... 17 at 11.15 s) and rises +1 floor right after each safe landing.
- **Bolt:** a bare egg with three straws and a strip of tape. It falls freely (g 2100 px/s², 32 floors = 0.90 s), so the impact speed grows with √height.
  - 1 and 2 floors: OK. 4: small crack. 8: "CRACK!". 16: a big crack and a yolk drip ("PHEW!"). 32: SPLAT.
  - His climbs speed up (8ths, then 16ths, one floor per tick). The tag counts every floor, and a lift "ding" plays on arrival.
- Growth: Bolt ×2 per drop (1 → 32, 5 doublings). Mochi +1 per drop (6 → 17, 12 drops).

## Timeline (clip seconds; clip = sim + 0.15)
- **0.0 s:** Mochi's 6-floor parachute rig is about to land. Bolt is on floor 1, bobbing smugly, with his rig on the hook.
- **0.15 s:** Mochi lands (soft bounce, SURVIVED, plate 6 lights) and her lift rises to 7.
- **0.5 s:** Bolt releases his 1-floor drop. It lands at 0.65 s ("OK!").
- **1.0 s:** Mochi's 7-floor rig is mid-fall and Bolt's egg wobbles on the pad. HUD 6 vs 1.
- **2.0 s:** Bolt has just ridden 2 → 4 (ding) and Mochi's 8-floor rig is falling.
- **4.15 s:** Bolt's 8 lands on the tutti entrance (bar 9) with a crack.
- **6.65 s, LEAD CHANGE:** Bolt's 16 survives ("PHEW!"). The banner "BOLT TAKES THE LEAD!" appears (16 vs 12). Bolt cheers; Mochi goes "wow".
- **7.3-9.07 s:** Bolt climbs 16 → 32 (8 ticks on 8ths, then 8 on 16ths). Then "32 FLOORS?!": Mochi is worried and Bolt laughs.
- **9.75 s:** Bolt releases from 32. The whistle and floor flashes run down the tower.
- **10.15 s:** Mochi's 16 lands. The HUD reads TIED.
- **10.65 s, SPLAT:** on the dominant (bar 15 beat 2). A clean fried-egg splat: yolk, egg white, shell bits, the straws fly off. "SPLAT!"
- **11.15 s, CADENCE:** Mochi's 17 lands softly. "MOCHI WINS!" / "HIGHEST SURVIVED: 17". The HUD shows 17 WINNER vs 16.
- **11.6-12.15 s:** Bolt's lift rides down into his own yolk (descending ticks, then a squelch). Yolk ends up on his feet.
- **12.4 s:** "again?", with Bolt deadpan and annoyed. Mochi laughs ("HA HA") until the dissolve.
- **13.4-14.0 s:** dissolve into the pre-roll (sim −0.75 → −0.15). The HUD switches at the midpoint.

## Sound (music first)
- **Piece:** W. A. Mozart, Horn Concerto No. 4 in E-flat, K. 495, 3rd mvt Rondo, Allegro vivace (1786; Mozart d. 1791, PD).
  - It is famous, cheerful, steady 6/8 and not kid-coded. It is on no used or banned list, and no other scene uses it.
  - Source: Mutopia-2010/01/10-1736 at `<SOUNDFONTS_DIR>\scores\mozart_horn4\MozartHornConcerto4.mid` (+ `info.html`, `SOURCE_mutopia_1736.txt`). The engraving/MIDI is CC BY-SA 3.0; only the PD composition's pitches and rhythms are read.
- **Excerpt:** rondo bars 5-16: the theme's second solo half, then the tutti repeat from bar 9 (4.15 s).
  - It ends on the **bar-16 E-flat cadence = 11.15 s**. Steady tempo, dotted quarter = 120.
  - The bar-4 pickup starts at clip 0, 17 ms late.
- **Arrangement** (lib/orchestra, MuseScore_General):
  - solo horn; ripieno horns; oboes; strings split at D3 (upper parts on strings, bass on cello + contrabass); soft pizzicato in the tutti;
  - CC11 dynamics: the solo phrase soft, the tutti forte;
  - **cadence:** a held E-flat chord (strings_slow, horns, contrabass, a rolled harp, timpani).
- **SFX** (all tonal; energy above 4 kHz 0.14%):
  - lift ticks: marimba-like, climbing the E-flat scale with the floor, on the 8th/16th grid;
  - lift "ding" when Bolt arrives;
  - release click;
  - soft falling whistle: a sine glide into a chord tone, louder and longer for higher Bolt drops; very soft for Mochi;
  - Mochi's landings: a cushion thump plus a padded "bwoomp" bounce, on the downbeat;
  - Bolt's landings: an egg "tok" plus a wobble tone, and a tonal crack (3 pitched snaps) from 4 floors up;
  - the 32 fall: a soft descending tick every 2nd floor;
  - **splat:** tonal crack, wet pitched "splap" plus bloop, low thump, and droplet bloops on the 16th grid;
  - the descent: descending ticks, then a squelch.
- Mastering: `level_bed` (+2.5 dB crescendo, `--findb 1.5`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS). The last 0.5 s is zeroed.

## Checks (v2, encoded Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 840 frames = 14.00 s.
- Audio (muxed): −14.00 LUFS, peak −2.11 dBFS, last 0.5 s silent.
- RMS/s: −20.5 −19.0 −18.7 −19.2 −16.6 −16.4 −16.1 −16.0 −16.0 −15.6 −15.5 −14.2 −15.5 (−25.3, the tail).
  - Body (1-11 s) −16.7; the cadence (11.15-11.65 s) −14.0, about 2.7 dB up.
- SFX events/s: 9 13 13 13 11 12 10 10 15 11 24 17 9.
- flash_check: PASS (0 flashes, mean luminance 0.028).
- **Loop seam:**
  - Pre-encode, last → first frame is 0.29 mean delta, the same as adjacent frames (0.29 / 0.34). It is motion-continuous (Mochi's rig falling).
  - Encoded: check_clip 0.75; the frame pair is 0.97 against 0.30-0.34 for adjacent encoded frames. That is I/P-frame drift on the towers (spread evenly at 1-3 per pixel), not a jump.
- Encoded frames read at 0.5, 1, 2, 6.75, 10.68, 13.3 s. 1:1 crops read: the splat at 10.70 s, and Bolt in the yolk with "again?" at 13.0 s.

## Doubts
- The event rate is flat (10-13/s) through the body and peaks only at the 32 climb, the splat and the win (15, 24, 17). Bolt has a 3 s gap between his 16 landing and the 32 release; his long climb fills it.
- Cartoon scale: the characters are ~3 floors tall, and the plate numbers are small (15 px). The big floor tags and the HUD carry the numbers.
- Cartoon cheats:
  - a new rig pops onto the hook after each climb;
  - Mochi's high drops are released 0.2 s after the previous landing;
  - the splat bits are biased away from Mochi's pad.
- Mochi starts at floor 6 with 1-5 pre-lit. She "has been at it" before frame 0, so frame 0 is mid-action.
- The Horn Concerto score was newly downloaded for this scene. The parallel batch50 builders were not checked for the same pick.

## Args and cost
- Args: `--sfx 0.30`, `--findb 1.5`, `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Cost: sim is closed-form (instant). Full HD render ~1 min at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)
