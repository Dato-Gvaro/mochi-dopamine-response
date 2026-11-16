# sand_rise2
- New file from sand_rise (owner review 2026-10-15). Same rule, sim, seed search and race (s183 is identical up to Bolt's escape at 12.63 s). Two changes:
  1. **Sound.** The pour bed is now a warm low rush (low-pass 700 Hz, high-pass 70 Hz) plus a soft grain patter (sparse impulses, band 350-1900 Hz). BED_GAIN is 0.022 (was 0.050, with a 2.6-9.5 kHz hiss). Avalanche slides moved down to 300-1700 Hz. The bed sits 10-14 dB under the events (v1: 6-8 dB), so the crunchy landings, pops, ticks and tugs carry the clip.
  2. **Rescue ending** (no burial). At the escape both valves close, and the loser's hatch jams (slam, LOCKED, red lamp). Times are seconds after the escape:
     - 0.50-0.70: the winner climbs out of its hatch.
     - 0.70-1.50: three hops across both roofs (metal pok + sand crunch).
     - 1.55: a stomp unjams the loser's hatch (clank, lid flips open, EXIT green).
     - 1.65-1.95: the rope lowers to the loser's head.
     - 2.10-2.85: three tugs (a soft dry rope "thup", no creak: owner dislikes creaks). The winner leans back on each, and the loser rises through the sand and out of the hatch, squeezed, with sand sliding off.
     - 2.85: pop. The loser sits half out of the hatch with a BORED face ("annoyed" flat lids, flat mouth, deadpan at camera). A "thanks." banner and a soft pfff; HUD shows "SAVED".
     - 3.60: the hold ends, then the 36-frame dissolve into the pre-roll.
- s183: clip 16.83 s (1010 frames).
- Checks (encoded Full HD):
  - h264 yuv420p 1080x1920, 60 fps.
  - -14.03 LUFS, peak -5.4 dBFS. Last 0.5 s peak -34.7 dBFS.
  - flash_check PASS (0).
  - Encoded seam 0.84.
- Delivered <VIDEOS_DIR>\batch35\sand_rise2.mp4. Owner review: pending.
- Fix 2026-10-15: the rope creak was replaced by a dry thup (a 140->90 Hz thump + a 300-1400 Hz brush, 90 ms). The winner stands at ROOF_STAND = ROOF_Y + 14 so his sprout clears caption line 2. Re-checked: -14.03 LUFS, peak -5.4, last 0.5 s -34.7 dBFS, flash PASS, seam 0.84.

Owner review (2026-10-15): only issue is the sound: don't simulate sand; use tik-tik or no sand sound -> sand_rise3.
