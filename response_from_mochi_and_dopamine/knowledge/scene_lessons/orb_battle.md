# orb_battle — Mochi vs Bolt, glass orbs that shatter

- Redo of bubble_battle after owner review 2026-10-04: soap bubbles + trampolines may read as kids' play (MFK risk). bubble_battle.py untouched (only draw_crown imported).
- Changes: soap bubbles -> GLASS ORBS (tinted rim gradient, caustic crescent low inside, window highlight + hot dot) fired by two gunmetal LAUNCHERS (floor corners, barrel 64 deg, recoil + muzzle glow per shot) in ballistic arcs (G_ORB 650, vy -760..-960 so apex stays below the caption). A hit SHATTERS the orb: 7+3*sz deterministic triangle shards (gravity 2100, spin, fade 0.5-0.7 s) + a ring in the hitter's colour. A missed orb smashes on the bed/floor (shards only, counts for nobody). No split rule (glass doesn't split). Dark "night" theme, steel trampoline frames. Caption "Every orb SHATTERS|~Most smashed WINS~".
- Rate 6 + 24*u^1.2 /s (440 fired, ~420 hit, ~9-36 on the floor). At 3.6 + 11 only ~214 hits: players catch almost everything, so the launch rate IS the escalation.
- Equal sizes work here (r 86 both; 30-seed mean diff +3, sd 15, ~3.3 lead changes) — the bubble version needed 92/78 because splits favoured Bolt's many quick jumps.
- Combos "xN!" from 15. Crown hysteresis 0.25 s (bubble_battle 0.4).
- Loop: launcher recoil eases to frame 0's (a shot fires at t=0 — the first seam diff was only the muzzle glow); frame 0's orbs are drawn back-extrapolated on their arcs and fade in over the last 0.45 s. Pre-encode last frame == frame 0.
- Sound: PD "habanera" (Bizet) walker on hits (+12 small), glass layer per hit 0.08 + 0.1*sz at glass_gain 0.45 (scene-local deliver(): kit.deliver has no glass_gain — tools/regen_audio would use 0.9), hit gate 0.045 s, floor smashes glass-only 0.05 gated 0.16 s, fanfare 74-78-81, bonk = glass 0.25 + pok, no note.
- s9: 29.42 s, MOCHI 219 vs BOLT 218, 7 lead changes (4.9, 7.9, 21.3, 21.6, 22.6, 24.05, 26.6 — Mochi retakes it on the last landing jump after the launchers stop). Hits per 5 s Mochi [23, 27, 37, 58, 66], Bolt [21, 30, 44, 50, 69]. Other close seeds: 6 (204-202), 101 (212-213, 10 changes), 91, 113.
- Measured (encoded): h264 yuv420p 1080x1920 60 fps, -14.0 LUFS, peak -5.5 dBFS, last 0.5 s -67.4 dBFS, flash_check 0 PASS (mean lum 0.06), seam mean 0.31.
- Args: --seed (9), --dur (26), --label, --cap, --sim, --search N, --still --frame.
- Delivered <VIDEOS_DIR>\batch11\orb_battle.mp4. Awaiting owner review.
- Owner review 2026-10-04 (batch 11): Undecided: maybe something can be built from it.
