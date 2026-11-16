# collapse_floors2
- Episode 2 of collapse_floors (the channel's best Short: 3,338 views, the only one pushed for 3+ days; reports/2026-10-15_channel_analysis.md). New file; v1 untouched.
- **The ONE nameable change: "this time the LAVA RISES."** The lava creeps up and SURGES every ~3 s (the gaps shrink: 1.6, 5.2, 8.6, 11.7, 14.5, 17.0 s ...). When it reaches a floor, that floor MELTS from the rim inward, tile by tile. The floors run out from below while Mochi and Bolt burn them from above.
  - Why this change and not "4 players" or "glass floors": v1's tension is "who falls first". The rising lava adds a clock without changing the rule, and it turns the last floor into the climax (both on it while it melts).
- Kept from v1:
  - The look: oblique hex floors (sapphire / emerald / amethyst), the stage, crack lines, shatters, plops.
  - The rule, "Every tile they touch DROPS", and the survival race.
  - The HUD, "FLOORS LEFT".
  - The end gag: SPLOOSH, smoke launch, soot, annoyed stare, HA.
  - The sound: Pachelbel-canon marimba on landings and glass-harp clinks.
- Caption: `Every tile they touch DROPS | ~...and the LAVA is RISING~` (y_f 0.10).
- **Title idea:** "Every tile they touch DROPS… and the lava is RISING 🔥"

## Mechanic
- **Lava level:** `L(g) = -900 + 8g + 0.2g² + 26 px per surge` (each surge takes 0.5 s).
  - Bottom floor: melts 16.1-18.7 s. Middle floor: 25.0-26.8 s (never reached).
  - Melt order: rim to centre, set by each tile's melt level (`melt_level`).
  - A tile melts by sinking glowing into the lava. Tiles glow hotter as the lava nears (`lava_heat`), plus a 0.9 s pre-melt glow.
- **Sim (v1 sim plus four changes):**
  - The game starts 1.15 s before frame 0 (F0 = -69).
  - The lava is a moving target. A plunge is the moment z crosses L(t).
  - Melts are pre-set drop times. Cracks use `td = min(melt, crack + delay)`.
  - "Smart" aim: they never pick a tile that drops before they would land (SMART 0.8). Without it, the falls came too fast (median end 10 s).
- **Escalation (p = t/22):**
  - Crack delay goes 0.55 -> 0.30 s.
  - Hop height goes 88 -> 132 (CHR 58, so the head stays under the floor above).
  - Hop distance goes 100 -> 195.
  - Aim error goes 12 -> 36.
  - From 9 s a landing cracks 1 neighbour, and 2 from 15 s, strummed 0.05 s apart.
- **Banners:**
  - LAVA RISING! (1.7 s), then lead banners.
  - FLOOR N MELTS! outranks LAST FLOOR! when they collide.
  - Up to 3 SAVED! pops for near-misses.
  - Banners pop at 0.8x scale or more.
- **HUD pips:** a pip goes dark when that character falls through the floor, or when the floor melts (it fades over the melt window). Pips relight with the reform.
- **End:**
  - The lava holds 0.45 s, then drains to L0 over 1.15 s.
  - Each floor re-forms once the draining lava has cleared it.
  - The last 1.15 s replays the game's own pre-roll, so the loop is EXACT. It is not a rewind and needs no dissolve.

## Sound
Three buses, then `audio.master()`, then a 30 ms fade at the seam.
- **Marimba:** the canon, one note per landing, in clip order.
- **Glass harp:** v1's shatter chords and fall glides.
- **In-scene SFX:**
  - A glass CRACK tick on every crack (`sfx_crack`).
  - A pitch-rising lava BLOOP on every visible bubble pop (`sfx_blub`).
  - A deep double glug plus a soft hiss on each surge.
  - Sizzle (steam) plus a bloop per 0.12 s bucket of melting tiles.
  - Plop: splash plus steam plus a bloop.
  - A soft sine riser for 1.3 s into the plunge, then three falling glugs as the lava drains.
- The tail is NOT silent: the last 1.15 s is the pre-roll (landings and cracks), so the audio continues straight into frame 0.

## s576 (default)
- **Falls:**
  - Bolt 5.37: Mochi leads.
  - Mochi 7.93: tied.
  - Mochi 14.48: LEAD CHANGE.
  - Bolt 15.30: both on the last floor.
  - Floor 3 starts melting at 16.1 (banner).
  - Bolt is eaten at 17.34 and plunges at 17.40.
- SAVED! at 9.85 and 13.31.
- Tile drops per ~5.8 s: 22, 24, 54 (climbing). Landings: 22, 20, 18 (hops get longer).
- Clip is 21.40 s (1284 frames).
- Other seeds (--search):
  - 533: Mochi falls into the lava through holes at 16.0. Two lead changes, first fall at 3.0.
  - 77, 720, 468, 782.
- Pre-encode seam (mean |Δ|): 1282->1283 is 0.678, the seam 1283->0 is 0.672 and 0->1 is 0.729, so the seam is exact.
- Checks (encoded Full HD, NF_CRF=14):
  - h264 yuv420p 1080x1920, 60 fps, 1284 frames.
  - -13.93 LUFS, peak -6.2 dBFS. The first sound is at 0.07 s. The last 0.5 s peaks at -8.5 dBFS (the pre-roll, on purpose).
  - flash_check PASS (0 flashes, mean luminance 0.11).
  - Events per 5 s: 84, 91, 113, 121 (climbing).
- The encoded seam is 1.109 at crf 14 (1.294 at crf 18). An encoded normal step is 0.66-0.90.
  - That excess is H.264 noise and not a state jump. Full-res PNG against encoded frame: 1.84 at frame 0 and 1.82 at frame 1283, while the PNG seam is 0.693.
  - The lava texture is costly to encode, so render this scene at NF_CRF=14.
- Args:
  - --seed, --label, --cap ('a|~b~'), --melody, --still --frame.
  - --search N: sim only. Filter: plunge 16-21.5 s, at least 1 lead change, first fall at 2 s or later, at least 3 falls.
  - --audio-only: sidecars and wav, no video.
- Delivered <VIDEOS_DIR>\batch33\collapse_floors2.mp4 (2026-10-14). Owner review: pending.

Owner review (2026-10-15): DROPPED — "duplicating the old one and changing jumps won't work on YouTube". Sequels must be a genuinely new game, not the winner with one tweak.
