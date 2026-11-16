# race2 — Mochi vs Bolt kart race (redo of mochi_bolt_race)

## Why mochi_bolt_race stalled (stills s54 f30 / f700 / f1480)
- Slow open: both racers sit behind a gate for 0.35 s, then creep down a shallow first ramp. Nothing happens in the first 2 s.
- Small faces: R53 in a 470 px half-lane. The bottom ~1/3 of the frame is an empty yellow band.
- The lead is unreadable. Mirrored zig-zag lanes mean "ahead" = further along a path that runs left in one lane and right in the other. The only lead cue is a 16 px head on a thin bar.
- Lead changes have no visible cause. Bumps are 13 px pink dots, and the swaps come from seeded bump/peg noise.
- Weak finish: a small "BOLT WINS!" counter, the loser looks mildly sad, no photo-finish moment and no laugh.

## The new rule
- Two STACKED horizontal lanes (Mochi top, Bolt bottom) share ONE camera and ONE x-scale, so further right = ahead. Both lanes have the same hills. Each 5-slot pack holds the same obstacles in both lanes {boost, boost, bonk, mud, spring}, shuffled and jittered per lane. That is why the caption can say "Same boosts, same bonks".
- Visible causes: BOOST pad +380 px/s (flames, "ZOOM!"). BONK block knocks the racer back at -0.15v, capped at 80 (block shatters, dizzy X-eyes + stars, "BONK!"). MUD = 0.6x top speed (sweat, "SPLAT!"). SPRING launches at 820 px/s. A racer that is in the air skips any pad or bonk under its arc ("JUMPED IT!").
- Speed model: v' = 1.8(vt - v) + 900*sin(slope). vt = 600 + 24t climbs every second, and slot spacing shrinks from 820 to 350 px, so hits/s climb.
- Rolling start: frame 0 is already at 620 px/s with the START line just behind. Forced opening: Bolt boosts at 0.37 s, Mochi bonks at 0.55 s, Bolt laughs at 0.63 s.
- Lead indicator: a crown on the leader (pops on each change), two progress rails with heads at 1392/1440, and "Lead changes: N" at 0.79h (pops). Lead change = the other kart is ahead by more than 35 px (hysteresis).
- Reactions: the new leader laughs (HA), the overtaken alternates worried/annoyed, and a bonk makes the other one laugh. Each character waits at least 1.0 s between reactions. Priority: bonk-dizzy > reaction > air (wow) > mud (annoyed + sweat) > boost (open grin) > idle (leader grin / trailer flat).
- Finish: 0.3x slow-mo from 0.45 s before the first crossing. Then a 0.9 s PHOTO FINISH freeze on the winner's crossing (zoom 1.18 on the line, white photo border, red line, "-0.05s" at the loser's nose; no white flash). Then slow-mo until the loser crosses. Then normal speed: the winner laughs (1.25 s), then cheers twice. The loser is annoyed for 2.7 s. Confetti, and a "<NAME> WINS! / by X s" banner on the lane divider.
- Loop: 1.0 s dissolve into frame 0. The last frame is 0.998 of frame 0; still diff mean 0.0008, max 75.
- Sound: william_tell (Rossini 1829, PD), one walker note per obstacle hit. Foley: boost = short sweep; bonk = bounce + squash; mud = squash + quiet splash ticks; landing = pok; lead change = octave note + small pop. A rising drum roll (accelerating poks) plays through the slow-mo. The crossing = latch + snap (shutter). Celebration pops accelerate until the dissolve, which is silent.
- Search: `--search N` (add `--all` to list everything) keeps first finish at 22-31 s, margin 0.03-0.25 s, at least 6 lead changes, max gap < 0.70W (both karts on screen), and at least one lead change in the last 5 s. About 1 in 60 seeds passes.
- Pick s1782: Mochi wins by 0.048 s. 9 lead changes at 4.5, 6.2, 8.9, 14.2, 17.1, 21.1, 21.8, 26.0 and 26.9 s. The last one is a boost past a freshly bonked Bolt 0.05 s before the line. Max gap 649 px. Alternatives: s1943 (Mochi, 0.046 s, 7 lead changes, last at the line) and s405 (Mochi, 0.108 s, 9 lead changes).
- Args: --seed, --label, --cap, --melody, --search [--from, --all], --still --frame.
- Measured on the Full HD encode (s1782): 33.05 s, h264 yuv420p 60 fps, 1080x1920. -14.0 LUFS, peak -6.0 dBFS, last 0.5 s at -40 dBFS (the celebration pops stop 0.45 s before the dissolve). Sound events per 5 s: 17, 24, 22, 31, 50, 31 (the last bin holds the silent 1 s dissolve). flash_check: 2 flashes, worst 1 per s = PASS. Post-encode seam mean 0.46 (good band).
- Delivered to <VIDEOS_DIR>\batch4\race2.mp4 (owner review pending).
- Owner review 2026-10-03 (batch 4/5): Not bad, but too heavy (too many effects/labels) for a simple satisfying video. Shelved.
