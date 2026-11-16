# demolition_duel2 — comment reply: the BOTTOM-floor shortcut vs Bolt's SECRET weapon, a giant ANVIL (batch49, 2026-10-24)

Sequel to demolition_duel. It replies to @MinhNguyen-text on the original Short: "shortcut: just hit the bottom floor using the wrecking ball".
- Our reply: "ok mochi is literally writing this down rn. bolt pretended not to read it but he's cooking something too 😂"
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch49\demolition_duel2.mp4` (**v6**, Full HD, 9:16, 13.20 s).
- New scene file. demolition_duel.py is untouched.

## Versions
- **v1-v3 (superseded):** Bolt used a middle-floor "hammer" cut, the shortcut won, and the music was Mozart's Dies irae.
- **v4-v5 (superseded):** one giant bomb with a beat-ticking fuse, Bolt won, Magic Flute music.
- **v6 = owner rework:** Bolt is gone for several seconds, then comes back with something dramatic that goes through the building top to bottom.
  - The owner first suggested a fighter jet dropping a bomb. We agreed NOT to: a military jet striking a tower reads as war / 9-11 imagery, an ad-suitability and removal risk.
  - **Agreed: a giant cartoon ANVIL.**

## The one nameable change
- **"Mochi uses YOUR shortcut (she hits the BOTTOM floor). Bolt disappears... and drops a 10,000-ton anvil."**

## Opening / caption
- Frame 0 shows the real comment on a drawn card (x 178-838, y 92-300). Handle and text only: no like count, age or heart, because we don't know them.
  - If the owner wants the real screenshot, save it as `assets/comments/MinhNguyen-text.png`.
- The card holds 0-3.0 s and cross-fades to the caption by 3.4 s. The loop dissolve brings it back.
- At the end a small copy of the card returns above Mochi's crane (11.45 s →); she stares at it (shock, then annoyed).
- Caption (baked; `--nocap` gives the base): "Your ~shortcut~ vs Bolt's ~SECRET~ weapon:" / "which building hits the ~GROUND~ first?"
  - The anvil is kept a surprise.
- Frame 0 = Mochi's first bottom-floor hit on the bar-66 downbeat. Bolt, up on his lift, is reading the comment (he looks up at the card).

## Mechanics (music grid: half note = 120, quarter 0.25 s, 8th 0.125 s)
- **Mochi, BOTTOM FLOOR** (unchanged from v4/v5):
  - One hit every 1.5 s: 0, 1.5, 3.0, 4.5, 6.0. Cable 251 px = an honest pendulum.
  - Pillars 0 and 1 take 2 hits each (out at 1.5 s and 4.5 s). With 2 pillars gone the centre of mass is over the edge: "IT'S LEANING...".
  - Hit 5 (6.0 s) takes pillar 2, and the last pillar bursts at 6.05 s.
  - The tower comes down one floor every 3 quarters, from 6.5 s ("SHORTCUT WORKS!").
  - **Mochi leads from 1.5 s to 10.5 s.**
- **Bolt, the vanishing act:**
  - He reads the comment (0-1.0 s), the lift lowers (1.0-1.8 s), then drives off right, out of frame (1.8-2.6 s), with two soft blips.
  - His tower stands untouched and his spot is empty: "...WHERE DID BOLT GO?" (2.95 s). Mochi glances over with a smug "HA HA". The HUD reads "BOLT: GONE?!".
- **The return:**
  - **8.625 s:** a tonal falling whistle (a sine gliding down onto chord tones) and a dark shadow growing on Bolt's roof. "WHAT'S THAT SOUND?", HUD "INCOMING!".
  - **9.625 s (an 8th after bar 75 beat 2):** a giant cartoon anvil, 280 px wide with "10,000 T" on it, drops in at 2600 px/s with **Bolt riding on top**. It punches through the roof with a thump + a clang: "AN ANVIL?!".
  - **It then smashes down through ONE FLOOR PER 8TH** (frags spray out, calm dust).
  - **Floor 0 goes on the bar-77 B-flat cadence (11.00 s).**
  - The lead changes to Bolt at 10.5 s. Mochi has 4 floors left at 11.0 s.
- **Ending:** "BOLT WINS AGAIN!".
  - Bolt sits smug on the anvil (cheer, then a long laugh) with "NICE TRY.".
  - Mochi is shocked, then annoyed, staring at the comment card. Her tower keeps crumbling.
  - A 1.6 s hold, then a 0.6 s dissolve to frame 0.
- No fire, explosion, flash or military imagery.

## Sound (music first)
- **Piece:** W. A. Mozart, Die Zauberflöte K. 620, Overture (1791, Public Domain).
  - Source: Mutopia-2013/03/24-248, at `<SOUNDFONTS_DIR>\scores\mozart_magic_flute_overture\mids\allegroIscore.mid` (+ `SOURCE_mutopia_248.txt`, `info.html`).
- **Excerpt:** Allegro bars 66-78 (quarter beats 260-310): the exposition's closing build, with its repeated-note crescendo, to the **B-flat cadence at bar 77 = 11.0 s**. One steady tempo, half note = 120.
- **Arrangement** (lib/orchestra, MuseScore_General): every part is read from the score. The timpani are transposed -1 (the MIDI has them a semitone high). Plus a held B-flat chord on the cadence.
- **SFX:** tonal only, at gain 0.26, each snapped to the score's chord or bass.
  - Ball hit: a thump + a clack. Mochi's crush: a thump + a clack.
  - Lift leaving: 2 blips.
  - Whistle: a sine glide, 1.0 s, into the impact.
  - Anvil impact: a deep thump + a long bell "clang".
  - Each anvil floor: a descending clack, with a thump every 3rd.
  - Cadence: a thump + a tonal rumble.
  - Landings are gathered on the quarter grid. No hiss or noise burst.
- **Master:** -14 LUFS, a lookahead limiter at -2 dBFS, and the last 0.5 s is silent.

## Checks (v6, Full HD, 2026-10-24)
- h264 yuv420p 1080x1920 @ 60 fps, 792 frames = 13.20 s.
- Audio: -13.98 LUFS, peak -2.01 dBFS, last 0.5 s silent.
- RMS/s: -19.3 -18.0 -18.4 -18.6 -17.9 -18.0 -17.1 -17.1 -17.1 -16.2 -16.1 -14.7 -20.3 (the tail). No dip.
- SFX events/s: 4 6 1 4 4 0 9 2 5 6 15 10 3. Second 5 has no SFX: the music, the lean and the ball's backswing carry it.
- flash_check: PASS, 0 flashes (mean luminance 0.066).
- Loop seam: 0.0014 mean before encoding; 0.82 after (P-frame drift, the same as the original's 0.80).
- Encoded frames read at 0, 0.5, 1, 2 (Bolt leaving), 3.2, 6, 9.2 (whistle + shadow), 9.65 (impact), 10.2 (mid-penetration), 11.0 (finish), 12.0 and 13.18 s.

## Lessons / doubts
- The anvil's crush rate (one floor per 8th) is cartoon physics, chosen so its last floor lands on the cadence. Mochi's stepwise grind is the honest slow part.
- Cartoon cheat: the ball's cable hangs in front of the facade, so it reaches pillar 1 behind pillar 0.
- Bolt's lift briefly crosses x 0.84w as it drives out of frame (1.9-2.6 s), which is intended.
- The sim is cached by a file hash (`output/demolition_duel2_sim_*.pkl`).

## Outcome
- (fill after upload)
