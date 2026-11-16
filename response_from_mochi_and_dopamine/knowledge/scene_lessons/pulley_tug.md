# pulley_tug
- New scene (batch37). Rule: "Every pulley DOUBLES his pull". Choice: Mochi pulls with RAW STRENGTH (the rope is tied round her waist; she leans and does run-up HEAVES). Bolt uses PULLEYS: he is tied to the same rope and hauls himself back with a block-and-tackle to a stake behind him, biting the free end. The strands go x1 -> x2 -> x4 -> x8. Caption (baked, `--cap`): `Every pulley ^DOUBLES^ his pull|~Strength or pulleys?~`.
- World: a dark dusk stage. There is a coral light on the left and a teal light on the right. A mud bowl sits between two banks (lips x 306 / 496, ground y 1010, mud y 1056). A wooden stake stands at x 868 (< 0.85w). The gold flag is tied at the rope's centre.
- HUD and labels:
  - One counter, at y 400: "<NAME>: n cm from the MUD", showing whoever is closer to the pit. It turns red under 15 cm and reads IN THE MUD! at the end.
    - The brief asked for "FLAG: n cm from the pit". A centre flag hangs over the pit, so that wording would not mean anything. The flag is kept as the motion marker instead.
  - The force meter `PULL ON THE ROPE (newtons)` shows two bars: MOCHI `n N` and BOLT `f N × n`. A gold dot marks the stronger side.
  - Other labels: "RAW STRENGTH" / "PULLEYS ×n" and "x.x m of rope hauled" (the trade-off). The hauled rope also piles up as a coil at Bolt's feet.

## Physics (1-D, 1 px = 1 cm, both tied to one rope, so e_mochi + e_bolt = 1.10 m)
- Equation of motion: `M dv/dt = n·f(v) − F_M(t) − C·v`, with M 150 kg and C 600 N·s/m (skid damping on the mud bank).
- Bolt's bite, f:
  - While hauling in, `f = F0 (1 − n·v/V_R)` (Hill force-velocity, V_R 8 m/s of free end). The trade-off is honest: at ×8 he must haul 8 cm of rope per cm, so his bite drops to ~110-140 N while moving.
  - While losing ground, the rope slips through his teeth at 1.1·F0. F0 is 232-246 N.
- Mochi, F_M:
  - Her lean is B (505-535 N) with a ±5% sway.
  - Each heave is a 0.14 s wind-up (pull dips to 62%) followed by a yank to A×B, decaying over ~0.6 s.
  - Normal heaves: A 1.55-1.95, every 0.95-1.4 s.
  - SECOND WIND (the first time she is within 20 cm at ×4 or more): 8-11 heaves, A 2.5-2.8, every 0.55-0.72 s.
- Bolt's pulleys:
  - Each new pulley drops onto the stake and seats in 0.4 s.
  - ×2 comes at the start. ×4 comes when he is within 26 cm. ×8 comes when he is within 20 cm after having led.
  - The tackle is drawn as strands: stake/back sheaves 1/0, 2/1, 4/3. Strands scroll at k/n of the rope speed.
  - Caveat: in a real tackle the doubling comes from the strands, not from each single wheel. Each upgrade is shown as "+1 PULLEY". A pedant may comment.
- Over the lip = the loser slides down the wall (0.42 s) and SPLORTs into the mud. Tension drops, so the winner topples backwards and then cheers.
- Seed search (`--search N --from S`). Filter:
  - ×4 by 1.0-3.4 s.
  - A near miss for Bolt before ×4, one for Mochi, and a late one for Bolt (after ×4 + 3 s).
  - At least 3 lead changes, clip 14.8-19 s, and rope in the coil never under 0.3 m.
  - Ranked by near-miss depth and clip ≈ 16.3 s. Frame-0 Bolt must be ≤ 52 cm, so the counter starts on him.
  - Every hit is a Bolt win. Mochi wins only with `--trig8 15` (he rigs ×8 too late, "×8... TOO LATE!"), and those clips run ~13 s.

## s181 (default)
- 0.0: Bolt is 51 cm from the mud and sliding (x1). Mochi winds up; a pulley is already falling onto the stake.
- 0.15: first yank thump. 0.35: CLICK +1 PULLEY ×2.
- 1.15: ALMOST (Bolt 7.8 cm). 1.28: ×4. 3.38: BOLT LEADS.
- 4.52: SECOND WIND. 4.8 / 5.37: ALMOST for Mochi (5.1 cm).
- 8.4: MOCHI LEADS (1231 N vs 907). 10.98: ALMOST for Bolt (4.7 cm), then ×8 at 11.23. 12.38: BOLT LEADS.
- 13.37: Mochi goes over the lip. SPLORT at 13.79; she is mud-covered with an annoyed stare. Bolt topples backwards and cheers.
- 14.09: BOLT WINS + chime. 9.8 m of rope hauled in total.
- Clip 16.30 s (978 frames). The last 0.6 s dissolves into the pre-roll.

## Sound
No music, no beds, no whoosh, hiss, creak or groan. Everything is synthesized in the scene:
- Tug thump: a soft dry 118 Hz glide plus a 640 Hz tuk. Mochi's yanks are big; Bolt's chomp strokes are small, every 0.42 / 0.39 / 0.34 / 0.29 s by stage.
- Pulley seat: a metallic CLICK (3.1 kHz modes) then a clack 26 ms later, pitched up per stage.
- Ratchet tick: one per 0.30 m of rope through the blocks, 2.35 kHz up to +20% by stage. It speeds up with ×8.
- Foot scuff ticks: one per 4.5 cm slid, alternating Mochi/Bolt.
- Splort: a gliding low blorp with a 26 Hz wobble plus 7 rising bubble bloops; 2 plops after.
- Back-landing thump, glass-harp win chime, a cheer pok.
- Onsets are kept ≥ 12 ms apart. No events in the last 1.0 s. `master(peak_db=-6)` and a 0.6 s tail fade.

## Flags
`--seed --label --cap --vote` (OFF by default: "Team Mochi or Team Bolt?" with a drawn arrow from splort+0.65 s to the dissolve, at y 690) `--search N --from S --dry --still --frame N` (negative = pre-roll) `--sound 0`. Tuning flags: `--c --vr --s0 --trig --trig8 --fury --fa0 --fa1 --fn0 --fn1 --bk --fk --v0 --a1 --rig1 --etot --lead8`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 978 frames, 16.30 s.
- -14.01 LUFS, peak -5.4 dBFS, last 0.5 s at -48.1 dBFS.
- flash_check PASS (0 flashes).
- Seam: encoded 0.60, against a normal step of 0.32-0.36 (I-frame step; inside the good band). check_loop reports "MISMATCH" by design: the last frame is the pre-roll frame one step before frame 0, as in coin_bridge2.
- Events per 5 s: 73 / 63 / 78 (214 sound events).
- Safe zone: caption y 200-275; content ends at ~1250 (< 0.71h); HUD at 1290-1440; the stake is at x ≤ 885.
- Render ~25 s Full HD.

Delivered <VIDEOS_DIR>\batch37\pulley_tug.mp4. Owner review: pending.

Owner review (2026-10-16): too complicated -> moved to reserve by the owner.
