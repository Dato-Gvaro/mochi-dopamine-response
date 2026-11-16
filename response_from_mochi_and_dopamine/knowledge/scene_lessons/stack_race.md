# stack_race

- Rule: bolt_stack for two. Mochi's lane on the left, Bolt's on the right, the same rule in both: a block slides in, drops, the overhang is sliced off. Slider speed rises EVERY level, uncapped: 360 + 1600*((k-1)/75)^1.3 px/s (2214 at level 85). First to MISS loses: a drop with < 16 px of overlap tips off.
- Error model per drop (seeded, one RNG per lane): perfect 55% -> 35% with speed; bad 5% -> 13% (18-60 px); else 3-17 px. 2 perfects in a row regrow the block +14 px. Re-aim pause 0.07-0.19 s, which also breaks lane sync, so the two lanes alternate and the height lead keeps swapping.
- Opening is forced: Mochi's first drop slices 34 px, Bolt's is perfect, so Bolt laughs at 0.6 s (hook). Both sliders are already moving at frame 0 and both characters are mid-hop.
- Reactions (notable events only): slice >= 20 px -> the other laughs (HA HA), the dropper winces; the other looks worried on the dropper's 3rd perfect in a row while it's narrower. 1.6 s gap between reactions per character. Perfect drop = 0.4 s grin. Otherwise determined, sweating when the top is < 150 px.
- Miss: the block tumbles, "MISS!", the loser goes wow then dizzy with stars; the winner laughs (1.35 s), then cheers + confetti + "<NAME> WINS!" banner. Hold 2.6 s.
- Layout: lanes at x 302 / 778, 460 wide (0.88 w total), each tinted toward its character, white divider + VS badge. One camera follows the HIGHER top (CAM_KEEP 470), so the heights compare honestly. Counters per lane at 0.75h/0.80h; haze below 0.70h.
- Seed search: `--search N` (sim only) keeps 25-35 s races with loser width <= 75, scores width-lead changes + height-lead changes - winner/loser width gap.
- Sound: ode_to_joy note per drop (both lanes share one walker, panned by lane), quiet pok; perfect = octave + small pop; slice = soft snap; miss = falling major run 79-76-72-67 + soft bounce; cheer = rising arpeggio + pop; hiss on reset. Lane onsets < 12 ms apart get nudged (the mixer drops onsets < 10 ms apart).
- Loop: towers sink into the plinths, counters count back to 0, camera returns, characters glide to their frame-0 mid-hop pose, sliders ghost back in. Seam pre-encode max 27/255 on 29 px (shadow fringe); post-encode mean 0.26.
- s498: Bolt wins 85 vs 83. Mochi misses at 33.98 s on a 24 px top (Bolt's top is 40 px). 38.08 s clip. Drops/5 s (both lanes): 14, 20, 23, 29, 37, 45. Height lead changed 25 times, width lead 20. -14.0 LUFS, peak -7.2 dBFS, last 0.5 s -71 dBFS. flash_check: 3 flashes, worst 1 per s = PASS. h264 yuv420p 60 fps, 1080x1920.
- tools/check_clip.py crashed on this PC: frame extraction got a non-zero ffmpeg exit (`-vsync 0`). Its audio_stats + seam were run by hand.
- Args: --seed, --label, --cap, --melody, --search, --still --frame.
- Owner review 2026-10-03 (batch 2): GOOD - approved to ship (Schedule 2026-10-05).
- Owner review 2026-10-04: Unsynced drop sounds aren't satisfying; add 3-5 drops where both lanes hit identically (synced sound) -> stack_race_sync.
