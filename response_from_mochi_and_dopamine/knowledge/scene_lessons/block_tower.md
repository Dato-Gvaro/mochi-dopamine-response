# block_tower — "Every block they pull makes it WOBBLE" (batch34, 2026-10-14)

Caption (baked, `--nocap` = base): "Every block they pull makes it WOBBLE" / "~Whoever topples it LOSES~" (WOBBLE + line 2 gold).
Deliverable: `<VIDEOS_DIR>\batch34\block_tower.mp4` (Full HD 9:16, 15.27 s, 916 frames). Seed 4.
Generic block-stacking game; never the trademarked name.

## Rule + choice
- 16-layer tower of wooden blocks (3 per layer, alternating), dimetric view (`proj`: KX 0.86, KY 0.22).
- Mochi = FAST YANK: middle blocks of A layers (long along +Y, her side), jerked out in 0.12 s, flicked onto the top
  with a full spin, lands 4-8 px off-centre (overshoot). Bolt = SLOW SLIDE: an EDGE block of a B layer, eased out
  over 0.50 s, placed dead-centre. Bolt picks the edge that minimises the static eccentricity (the "careful" choice);
  that is always the +Y edge, which narrows the support on Mochi's side.
- Turn starts every 1.40 -> 0.90 s (speed-up); 12 pulls; collapse on Mochi's yank at 12.00 s (layer 12), the tower
  tips toward Mochi at interface 8 (Bolt had narrowed layer 7, Mochi had hollowed layer 8).

## Physics (reduced model, honest)
- Each layer interface = Winkler contact over the EXACT crossing-block patches (fractional while a block slides).
  Per axis the hinges are a coupled linearised inverted pendulum: J phi'' + c phi' + ks I phi = m g e_eff + tau.
  KS 11, ZETA 0.045, MU 0.34, G 3000 px/s^2. Newmark (avg. acceleration), 4 substeps/frame.
- Pull force = mu (2N+1) g at the pulled block's height: Mochi a square pulse (jerk -> big sway), Bolt a sin^2 bell
  (quasi-static -> small sway). Landing impulse at the top from the flight's horizontal speed.
- danger = |COM offset over support centroid incl. lean| / distance to support edge (max over interfaces); >= 1 topples.
  The TILT gauge needle = danger, signed by the screen side of the lean.
- Collapse: part above the failing interface rotates rigidly about the support edge to 0.30 rad, then breaks into
  free blocks (rigid-body velocities, landing nudged 65% toward Mochi), height-field pile with 2 bounces, slump to the
  lowest nearby spot, Mochi's head = a dome (first hit = the BONK).
- Top sway measured: +-13..80 px per second, rising late (-80/+48 at 9-10 s).

## Hook / pacing
- Frame 0: Mochi stuck to a half-pulled block (yank in motion), Bolt's pre-roll block in flight, lands with a clack
  at 0.16 s; counter "BLOCKS PULLED: 2 -> 3" at 0.06 s. Pre-roll sim starts at -1.90 s.
- Banners: WOBBLE! 2.80 / 10.22 / 11.25 (danger peaks >= 0.75), TIMBERRR! 12.05, BOLT WINS! 12.95.
- End: bonk 12.42 (dizzy, stars), pile settled 13.70, eyes peek from a gap (annoyed), Bolt 2 happy hops.
  Loop: 0.6 s dissolve into sim frames -0.6..-1/60, so the cut to frame 0 is a normal step.

## Sound (no music; all synthesised in-scene, wood only)
- Per turn: push-off thump + hop swish, sticky tok on grab, yank "zzip" (110/s stick-slip grains, 2.2-4.2 kHz) or
  slow slide scrape (34/s grains, 0.9-1.9 kHz, sin bell), tok when free + flick whoosh, blob landing thump,
  placement CLACK (modal 0.85/1.7/2.7/3.9 kHz + settle re-hit). Creak on every danger peak >= 0.42 (louder/higher
  with danger), 1.5 s rising tension creak into the topple, crack + groan, crash (58 Hz thud + 14 clacks), every
  debris impact/settle a clack (>= 22 ms apart), soft hollow bonk on Mochi.
- Own mixer with an Onsets gap of 12 ms across all layers, then `audio.master(reverb=0.8)`; nothing after end-1.2 s.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 15.27 s. -14.02 LUFS, peak -1.83 dBFS, last 0.5 s -66.8 dBFS.
- flash_check PASS (0). Seam pre-encode 1.62 vs normal step 1.65 (half res); encoded seam 2.03 vs neighbours
  2.04/2.06 (busy mid-action frames, so the step itself is ~2).
- Args: --seed, --label, --cap 'a|~b~', --nocap, --report, --search N, --still --frame a,b, --audio-only.
- Render ~2.5 min Full HD. Other seeds: 0, 3, 7, 14 (collapse 11.2-12.0 s by Mochi toward +Y); seed 2/6/8 tip -Y (away).

## Owner review 2026-10-15
- "I don't like it, but if you remove that weird sound and use only wood tik tik sound, also animation is weird, the
  tower feels like jelly — change those and maybe it will be worth it."
- Lessons: the hinge-chain sway bent the tower into an S (jelly); wooden blocks must stay rigid. Creaks, groans,
  whooshes, the zzip, blob thumps and the bonk read as "weird": a wood scene gets ONLY wood ticks/toks/clacks.
- Rebuilt as `block_tower2` (rigid rocking + wood-only sound); this scene stays as it was.
