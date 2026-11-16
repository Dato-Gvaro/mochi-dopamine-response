# treasure_capsize: gold stacked HIGH vs stowed LOW, survive the storm (batch30)

- **Brief:** age of sail. Two identical galleons each take 12 gold chests. Mochi stacks the gold HIGH (6 on deck, 4 lashed under the main yard, 2 in the crow's nest). Bolt stows it LOW in the hold. The same storm hits both. Mochi capsizes on the climax; Bolt rights herself on every roll.
- **World:** wooden galleons seen from astern as a cut-away section (planked hull, lit hold, wale with coral or mint stripe, cannon muzzles), canvas course and topsail, shrouds, fighting top, pennants, stern lanterns, iron-banded gold chests, a water barrel. Dusk sky, storm clouds, rain streaks, foam and whitecaps. Lightning is thin bolts with a small local glow, never a full-frame flash. Nothing modern.

## Physics (`scenes/treasure_capsize.py`, one model for both ships)
- **Hull:** a real section polygon (beam 10 m, deck 6 m, draft 3.4 m, tumblehome). For each heel angle the waterline is solved by bisection so the displaced area stays constant. That gives B(phi), and GZ = G_x - B_x (cross curves). KB 1.91, BM 2.97, KM 4.88 m.
- **Mass:** ship 100 t (KG 3.2 m, k 3.8 m) + 12 chests x 2.5 t at their real positions. That gives KG, the lateral G and the roll inertia.
  - Bolt: KG 2.88 m, GM 2.00 m, tipping point (angle of vanishing stability) 102 deg.
  - Mochi: KG 4.45 m, GM 0.43 m, tipping point 47.6 deg (46.2 deg after the cargo shift).
- **Roll:** `phi'' = -(g/k^2) GZ(phi - alpha) + (g/k^2) h_wind cos^2(phi) - 2 zeta w0 phi' - 0.25 phi'|phi'|`. Integrated at 8 substeps per frame.
  - Time is compressed x4.5 (model scale), so the roll periods fit a Short.
  - Effective wave slope alpha = 0.35 x the visual slope. The wavelength (520 px) equals the ship spacing, so both ships always meet the same wave phase.
- **Storm:** a gust plus a wave on every music bar.
  - Gust arms per bar (m): 0.053, 0.058, 0.085, 0.108, 0.112, 0.218, **0.30 (bar 7, the climax)**, then 0.05 and 0.03 as the storm passes.
  - Wave slope rises from 0.05 to 0.15 rad.
  - The gusts were tuned sequentially so Mochi's peaks climb 15 / 21 / 27 / 32 / 37 deg.
  - **Knife-edge:** a bar-6 gust of 0.23 instead of 0.218 already capsizes her in bar 6. Retune with the bisection recipe (sequential per-bar targets), never by hand.
- **Cargo shift:** when Mochi first passes 28 deg (11.42 s), the two top deck chests slide 1.9 m to the port rail. G moves sideways and down.
- **Capsize:** Mochi passes her tipping point at 17.67 s (bar 7 downbeat 17.52).
  - Then bullet-time: the world runs at 0.09 x from 17.57. Music and characters stay at 1x.
  - She ends at 80 deg heel at the seam, still going over.
  - Past 65 deg, sails and masts in the water damp the roll (zeta += 25 x ramp). A floating-rig support (6.0 m/rad past 80 deg) never engages in this clip.
- **Bolt:** peaks 8-24 deg and always comes back.
- **Gold:**
  - Releases are angle-triggered: the 2 crow's-nest chests at 51/53 deg, the 4 yard chests at 55-63 deg, the 2 shifted deck chests at 68/71 deg.
  - Each released chest flies ballistically from its last ship velocity, with a coin trail, then splashes and sinks.
  - The 4 attached deck chests pour coins over the rail from 49 deg to the seam, so frame 0 has gold pouring.
- **Mochi** is thrown at 56 deg (20.4 s) onto her barrel between the ships and gives an annoyed stare at Bolt from ~21.5 s. Bolt cheers on deck from 19.9 s, every 1.05 s.

## On screen
- 2-line caption baked in: `Gold stacked HIGH vs stowed LOW` / `~Which ship survives the storm?~`.
- Labels: GOLD UP HIGH / GM 0.4 m (coral), GOLD DOWN LOW / GM 2.0 m (mint).
- Each hull shows a G dot (CG symbol) and an M dot (metacentre) joined by a line. Mochi's two dots nearly touch.
- Gauges per ship: a +-120 deg arc with the needle, red wedges past the TIPPING POINT (with its value), and `HEEL n deg`, which turns red once past the tipping point.
- Banners read from their first frame (1.15 -> 1.0 scale, 72-100 px):
  - 12 CHESTS EACH (1.17 s)
  - STORM! (2.54)
  - 26 deg / 21 deg FROM TIPPING! (6.05 / 8.62)
  - CARGO SHIFTS! (11.42)
  - 9 deg FROM TIPPING! (14.05)
  - CAPSIZE! (17.67)
  - LOW GOLD WINS! (20.05 to the seam, so it is on frame 0)

## Hook and loop
- **Frame 0** = sim frame NS-1, the frame after the last one. It shows Mochi's ship at 80 deg with gold pouring, Mochi on the barrel, Bolt upright and cheering, LOW GOLD WINS!, and a lightning bolt.
- 0-0.8 s: smooth rewind (icon top-right) through the whole storm to the empty ships. At 0.8-2.2 s, 4 volleys of 3 chests land on beats 2, 2.5, 3, 3.5 of the hook bar. Sky, rain and waves build from ~1 s. The first gust lands at 2.52 s.
- The loop is exact: the seam pre-encode is 0.314 against the 0.313 neighbouring step. Post-encode the seam reads 0.82 mean, because of the keyframe at frame 0; the end steps read 0.35 and the rewind steps 0.7-1.7.

## Music
- **Piece:** Mendelssohn, *The Hebrides* (Fingal's Cave) overture, Op. 26 (1830, rev. 1833; composer d. 1847: PD). The opening motif, bars 1-6 and 9-10.
- **Notes:** read by eye from the Breitkopf & Haertel first-edition full score [1834], plate 5543 (Royal College of Music C785/2, archive.org `c-785-images`, pages n84-n86, PD). The motif was cross-checked with the PD Commons theme example.
  - Motif (viola octave): r8 r16 F#4(16) | D4(8) C#4(16) D4(16) | B3(q) | F#3(q).
  - It is sequenced in Bm (bars 1-2), D (3-4) and F#m (5-6) as printed.
  - Bass: B2 / D2 / F#2. Harmony is the triads under it (violins hold F#5 / D5 in the score).
  - Source notes, checksums and the downloaded pages: `<SOUNDFONTS_DIR>\scores\mendelssohn_hebrides\SOURCE.txt`.
  - No MIDI of Op. 26 exists on IMSLP, Mutopia or Commons (checked 2026-10-12).
- **Arrangement** (lib/orchestra, 96 bpm, bar = 2.5 s):
  - Bar 0 (hook) = score bar 9: tutti, boom at 0.02 s.
  - Bars 1-2 = score bars 1-2: violas + cellos + tremolo strings + bass, thin.
  - Bars 3-4 = score bars 3-4: + horns, choir, timpani.
  - Bars 5-6 = score bars 5-6: + trombones, oohs, booms.
  - Bars 7-8 = score bars 9-10: full tutti, violins an octave up (top F#5), trumpets. Cymbal swell + boom into bar 7 = the capsize.
  - Bar 8 beats 3-4: an F# major half cadence. **This is our addition, not in the score.**
  - 22.52: B minor cadence chord. Silent from 24.5.
  - Timpani rolls into bars 2, 5 and 7. A taiko hit on the cargo shift.
- **SFX** (own synthesis, under the music): a wave swoosh before each downbeat, wood creaks at Mochi's big rolls and the shift, soft thunder on the strikes, chest splashes, the rig splash, a quiet coin shimmer and a reverse whoosh on the rewind.
- **Sync:** every gust or surge is a bar downbeat. The loading volleys are on beats. The cargo shift has a taiko hit. The capsize is the bar-7 climax. The lightning strikes fall on the booms (bars 5, 6, 7 and the cadence).

## Checks (Full HD, encoded)
- h264 yuv420p 1080x1920, 60 fps, 1560 frames = 26.00 s.
- -14.01 LUFS, peak -5.1 dBFS, last 0.5 s -80.8 dBFS.
- RMS per 5 s: -14.5 / -20.8 / -18.0 / -14.2 / -15.1. That is the hook, the thin start, the build, and the climax as the loudest window.
- flash_check: 0 flashes, PASS (mean lum 0.044).
- Frames read: 0, 0.5, 1, 2, 3, 13, 17.8 and 21.5 s, and the barrel close-up at 21.7 s.

## Doubts / next
- The near-miss is a creep: bar 6 never recovers (37 deg -> over). Escalation reads through the FROM TIPPING countdown instead.
- In bullet-time the falling chests take ~5 s of clip time to reach the water, which reads as slow motion.
- Mochi's ship capsizes to port, so part of the rig leaves the frame on the left.
- Delivered: `<VIDEOS_DIR>\batch30\treasure_capsize.mp4` (Full HD).
- **Owner review (2026-10-12):** "let's try it" -> APPROVED.
  - 4K `--label ship`: 2160x3840 h264 yuv420p 60 fps, 26.00 s.
  - -14.01 LUFS, peak -5.1 dBFS, last 0.5 s -80.8 dBFS. Seam 0.59. flash_check PASS.
  - Scheduled: `<VIDEOS_DIR>\Schedule\2026-10-16\1_treasure_capsize.mp4`.
- Owner review (2026-10-12): let's try it -> APPROVED, 4K (Oct 16 slot 1).
