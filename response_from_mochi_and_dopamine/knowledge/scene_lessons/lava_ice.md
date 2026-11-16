# lava_ice — "LAVA spreads, ICE freezes — who takes the whole board?"

Batch31 formula test (research/reference_satisfying2dsims.md): pure black, one neon circle
arena, glowing cells, one counter per side, tension-first opening, ~45 s. NOT a copy of
their "Fire SPREADS, water SPLITS": different rules (Eden growth vs branching crystal
chains, melt/water + obsidian walls/breakthroughs), territory race, not "runs out first".

## Rules (sim, 60x60 grid clipped to a circle = 2,748 cells, one tick per frame)
- LAVA SPREADS: each lava cell flows into each empty/water 4-neighbour at 1.2 %/tick
  (steady Eden blob). Fresh lava (< 26 ticks) is HOT: melts any ice at 8 %/tick per hot nbr.
- ICE FREEZES IN CHAINS: a fresh ice cell is an active tip for 40 ticks; a tip freezes
  empty cells touching <= 2 ice (thin dendrites). Every new cell's chain link =
  neighbour max + 1; tip power = 1 + link/95, so chains ACCELERATE. Old ice fills gaps.
- Contact: lava melts thin ice -> WATER (thick ice 12 % rate); lava then flows into the
  water, ice tips refreeze it. Thick ice / tips freeze lava -> OBSIDIAN (blocks lava).
  Lava heats a wall by its lava-nbr count per tick; heat 45 -> BREAKTHROUGH (hot lava).
  Ice entombs obsidian it touches (new active tip -> chain reaction through lava).
- Race ends when one side owns all 2,748 cells.
- Balance: with these numbers ice wins ~95 % of seeds (accelerating beats steady); the
  seed picks the story. Seed search: `scratch search2` over 200 seeds, scored by
  contact 2.6-5 s, finish 37-46 s, lava ahead at 3 s, last lead change > 62 % of T,
  smallest mean count gap.

## Seed 122 (default)
- Contact 3.7 s. Lava leads early (steady) -> ICE TAKES THE LEAD 9.1 s (chains
  branch around) -> LAVA TAKES THE LEAD 21.8 s (breakthroughs) -> ICE TAKES THE LEAD
  32.6 s (chain avalanche cuts the lava into islands) -> full board 41.2 s.
- Counts: 10 s 393/487 · 20 s 1237/1360 · 30 s 1474/1088 · 35 s 865/1700 · 40 s 49/2657.
- Clip: race 41.23 s + finale 2.2 s (sweep band + "ICE TAKES THE WHOLE BOARD!") +
  rewind 1.3 s (whole battle backwards to frame 0, silent) = 44.73 s.

## Sound
- Bed (scene-local synth): lava = soft rising-pitch bubble bloops 150-270 Hz (cap ~14/s);
  ice = glassy 3-7 kHz crackle ticks (cap ~22/s); finale = filtered noise whoosh.
- Melody: Bizet "Habanera" (Carmen, 1875; PD) from audio.MELODIES, marimba, one note per
  spread/freeze before 3 s, then per new obsidian wall / breakthrough, gap 0.40 s -> 0.18 s (rate climbs); lead change adds
  the low octave (+13 ms, past the mixer's 10 ms rule). Finale = D-major arpeggio
  62-66-69-74-78 + D3. Rewind = silence (last 1.3 s).

## Checks (Full HD, <VIDEOS_DIR>\batch31\lava_ice.mp4, 2026-10-13)
- h264 yuv420p 1080x1920 60 fps, 2684 f = 44.73 s. LUFS -14.01, peak -7.6 dBFS,
  last 1.3 s audio peak -118 dB (silent). RMS/s flat -17..-16 from the first second.
- flash_check ok: 1 flash total (the 41.9 s finale sweep), worst 1 s = 1.
- Loop: pre-encode frame 0 vs last frame mean 0.006/255; post-encode mean 0.40 (good band).
- Melody notes 147, 12 distinct, top pitch 18 %; events/5 s 12-15-16-19-20-24-26 (climbing).
- Encoded frames at 0/1/2/3/10/25/33/38/42/44.2 s and a 1:1 crop at 38 s read correctly
  (water blue, obsidian near-black, fresh walls violet, fresh tips white).
- Render time ~21 min Full HD on a loaded PC (numpy cell image + cairo per frame).
- Opening melody: before 3 s the tune walks on growth events (first note 0.05 s); the
  first build started notes only at contact (3.7 s) and the first second measured -30 dB RMS.

## Lessons
- Two-step conversions with intermediates (water / obsidian) + surface-tension rules
  STALL into a frozen front. Decisive fronts need momentum: fresh cells (hot lava,
  active tips) attack hard, and conversions spawn fresh cells.
- The scratchpad is SHARED with sibling agents: use unique file names there.
- Owner review (2026-10-13): good but too long and slow; shorter and faster -> lava_ice2.
