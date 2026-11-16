# ol_domino_style_test2 (DopamineEXE long video 1, style test v2, 2026-11-04)
- Why: the owner rejected test 1 (`archive\domino_style_pick\`): "lifeless, like a child made it in Paint, we will be called AI slop". The bar is Kurzgesagt-level craft (one colour mood, layered detail, rim light and glow, thin labels), in our own palette.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\domino_style_v2\` (6 survivors × earth/space PNG, overview.jpg, README with scores). Ranked: aurora > gloss > teal > dusk > paper > neon. Dropped: riso, clay.
- Imports `ol_longform_domino2.py` read-only (chain, contacts, clock). Tight camera: dist 2.75, target at (1130, 620).
- Moments: earth t=63.0 (domino 54 beats the giraffe), land t=105.4 (domino 90 beats the Eiffel Tower; the space-heavy styles gloss and neon), space t=242.35 (domino 224 beats the Sun).

## Technique (reuse in ol_longform_domino3)
- An object is a `Painter` of `Part`s in local units (measured size = 1, origin at the bottom centre, y up, facing +x). Each part is a closed path plus clipped details (`d_patches`, `d_spots`, `d_rings`, `d_strokes`, `d_bands`). Limbs are tapered `b_limb` outlines, never uniform strokes.
- Cel shading per part, by offset-clip: shade = the part minus itself shifted toward the light, painted MULTIPLY with tint = shade/base. Light band = shift away from the light, SCREEN. Rim = a small shift, OVER. The shade colour is hue-shifted and more saturated (`shade_color`), never grey: multiplying by grey made test 1 muddy.
- Haze on far objects: mix toward `haze_col` by (cidx - k)/26.
- Spheres use a similarity matrix (centre + radius). The affine base matrix skews big spheres.
- Emissive parts (`glow=True`) skip grading and shading. A part under 14 px gets a halo (`small_glow`).
- Domino near face (`zn`, the face the camera mostly sees) gets the sheen and bevel. Draw edge lights only when both adjacent faces are visible: hidden top edges draw stray diagonals on the near giants.
- Post-process: quarter-res gaussian bloom (`bloom`), `soft()` blur layers for aurora, clouds and paper shadows.
- Cost: Full HD frame 0.25-0.7 s (paper is the slowest).

## Gotchas
- The Bash heredoc breaks on apostrophes (THE MOON'S ORBIT): write edit scripts to files.
- At the Sun moment the planets are off-screen left; only dominoes 210-229 are in frame. The roster neighbours there are Saturn's rings, light in 1 s, Earth to Moon and the Moon's orbit.
- Riso halftone (4.6 px screen) is a video risk: shimmer and x264 cost.
