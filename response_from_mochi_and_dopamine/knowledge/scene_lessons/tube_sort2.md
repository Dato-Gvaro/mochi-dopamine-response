# tube_sort2
- **Why:** owner review of tube_sort (2026-10-11): "one sort game; remove music and add ASMR good sound; make the colours like CHEMICALS".
- **Reuses tube_sort:** the puzzle logic (`import tube_sort as ts1`: gen / moves / apply / A*) and the pour geometry (tilt so the liquid just reaches the lip, level surfaces). Everything is ~2x bigger.
- **Board:** ONE board, 10 tubes in 2 rows of 5.
  - Each tube is 124 x 276 px inside; the rows fill 0.88 of the width over y 0.29h-0.70h.
  - Display slots are remapped (`SLOTMAP`) so the solved board's 2 spare tubes sit bottom-right on frame 0.
- **Solver:** Bolt runs A* (optimal 22 pours, puzzle seed 1, 2,862 positions). Mochi watches and reacts: "wow" at each completion, worried at the lava flare, cheers at the end.
  - Header: BOLT'S POURS x/22 and SORTED x/8.
  - The caption stake "Can it be done in 22 pours?" is answered by "SORTED IN 22 POURS!".
- **The 8 chemicals:**

  | Chemical | Look | Completion reaction |
  |---|---|---|
  | NEON | pulsing pink glow | glow ring |
  | LAVA | crust + glowing cracks, embers, slow thick stream | flare + ember burst |
  | ACID | rising bubbles | fizz bubbles out of the mouth |
  | GALAXY | swirling nebula + twinkling stars | star spiral |
  | MERCURY | metallic bands + sheen, thin stream | ripples |
  | ICE | frost crystals | frost creeps up the glass + flakes |
  | HONEY | amber, slow bubbles, thick stream | golden glints |
  | SMOKE | black with drifting wisps | smoke puff |

  - Each completion also gets a pop label with the chemical's name, then the cork drops 0.4 s later.
  - Viscosity sets the pour pace: lava ×1.45, honey ×1.4, mercury ×0.8.
- **Timeline:**
  - The first pour lands at 0.80 s. Pours gently accelerate from about 1.0 s to 0.7 s apart.
  - Tubes fill at 7.57 (acid), 9.78 (lava), 12.62 (galaxy), 14.40 (ice), 18.77 (neon), 19.54 (smoke), 20.33 (mercury) and 21.40 s (honey).
  - The clip is 25.0 s long.
- **Hook / loop:**
  - Frame 0 = the solved, corked, glowing board plus "SORTED IN 22 POURS!".
  - 0.04-0.56 s: the rewind (units fly back, corks pop off).
  - Every idle animation is periodic in T_END, so frame 1500 ≡ frame 0. Still diff f0 vs f1499 is 0.43 % of pixels (one frame of idle motion). The encoded seam mean delta is 0.45.
- **Banners:** readable from their first frame (start at 92 % size, overshoot to 108 %).
- **Audio:** no music. Everything is synthesised in the scene and run through the orc.render bus (wave parts only, reverb 0.16, air -3 dB):
  - A per-chemical pour: lowpassed stream noise + Minnaert "bloop" bubbles.
    - Lava: deep slow glugs + crackle.
    - Acid: fizz + tiny bubbles.
    - Mercury: tinkly droplets.
    - Ice: crystal ticks.
    - Honey: slow thick glugs.
    - Smoke: airy.
  - An impact glug as the stream lands.
  - Glass ticks on lift and set-down.
  - On completion: a glass-harp chime rising on the G pentatonic, a material reaction sound and a cork pop.
  - Sparse soft bubbling throughout.
  - A reversed pour under the rewind.
  - A final G-major glass chord + sine pad.
- **Mix balance:** pours were raised and the reaction swells lowered after the first measure (pours had been -21 dB against -14 dB at the completions).
- **v1 (2026-10-11):** 25.0 s, Full HD.
  - Audio: -14.00 LUFS, peak -3.6 dBFS, tail silent, energy above 6 kHz 0.2 % (warm).
  - Picture: flash_check PASS, 0 flashes.
- **Gotcha:** `scipy.signal` takes ~30 s to import on this PC, so it is imported lazily inside the audio helpers (stills render in ~2 s).
- Owner review (2026-10-11): good; background: tubes sitting on a wooden shelf in a medieval (witch's) house; TWO variants: current pour sounds + better, more ASMR pouring -> tube_sort3a/3b.
