# block_tower2 — rigid wood + wood-only sound (batch35, 2026-10-15)

Rebuild of `block_tower` after the owner review (tower felt like jelly; "weird" sounds). New file; block_tower untouched.
Caption (baked, `--nocap` = base): "Every block they pull makes it WOBBLE" / "~Whoever topples it LOSES~".
Deliverable: `<VIDEOS_DIR>\batch35\block_tower2.mp4` (Full HD 9:16, 17.52 s, 1051 frames). Seed 5.
Mochi = she/her.

## What changed vs block_tower
- RIGID physics. No hinge chain, no bending. The stack above one interface rocks as ONE rigid body about a real contact
  edge (Housner rocking block): restoring torque m g (d cos th - h sin th); on the way back it slams onto the other
  edge and keeps RESTI 0.55 of its angular speed, so every rock is a short sharp tik-tik-tik that speeds up and
  dies out. It tips when th passes atan(d/h); then the whole stack rotates on that same edge and breaks into tumbling
  rigid blocks (pile as before).
- Kicks: Mochi's jerk = friction mu (2N+1) g x JERK (breakaway peak, 1.0 -> 2.6 over 12 s: she yanks harder as she
  speeds up). Only the part of the torque that the stack's weight cannot hold down (F*lever - m g d) lifts it.
  Bolt's eased pull delivers 5% of that (BOLT_KICK) -> his pulls do not rock it. Placement impulse = landing
  speed (Mochi flings at 700 px/s, Bolt sets it down at 140). The stack that ends closest to tipping
  (kinetic / tipping energy) is the one that rocks.
- Mochi's jerk drags the block resting on hers 3-6 px (friction): a visible shift.
- Mochi now aims higher over time (KT 6 -> 13): lighter stacks rock more, so the rocking escalates.
- Opening re-timed: Mochi's pre-roll block lands at -0.05 s, so frame 0 has the top rocking (ticks from 0.05 s) and
  Bolt mid-slide (block out at 0.29 s).
- SOUND = wood only. s_tick (maple tick: 1.85/3.3/5.1 kHz modes, 16/9/5 ms, + click) and s_clack (block knock).
  Grab = soft tok, Mochi's yank = 7 rapid ticks, Bolt's slide = 8 slow soft ticks, block out = tok, placement = clack,
  every rocking impact >= 6 = a tick, topple = tok + 8-clack break burst + the 26 hardest debris impacts (12 ms
  rule spreads them into a rattle) + settle ticks, a muted tok when a block lands on Mochi. Removed: creaks, groans,
  tension creak, whoosh/swish, zzip, blob thumps, bonk. master(reverb=0.5).
- WOBBLE! banner = a visible rock >= 2.5 deg that survives.

## Run (seed 5)
- 13 pulls, turn interval 1.55 -> 0.95 s. Rocking peaks per Mochi turn: 3.9 (opening), 0.6, 1.3, 3.5, 5.3, 7.3 deg,
  then her yank at 14.25 s tips the stack above interface 7 toward her. Bolt's pulls never rock it (contrast).
- Banners: WOBBLE! 7.58 / 9.78 / 12.28, TIMBERRR! 14.30, BOLT WINS! 15.20. Pile settled 16.03, quiet from 16.3.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps; -14.01 LUFS, peak -2.33 dBFS, last 0.5 s -78.3 dBFS.
- flash_check PASS (0). Seam pre-encode 0.53 vs steps 0.57/0.53 (half res); encoded 0.90.
- Render ~5 min Full HD. Other seeds (IV 1.55/0.95): 0, 1, 8 (collapse ~12.1-12.2 s, by Mochi toward her).

Owner review (2026-10-15): moved to reserve by the owner.
