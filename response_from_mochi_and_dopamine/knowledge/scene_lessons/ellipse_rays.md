# ellipse_rays — THE ELLIPSE SECRET (every ray from one focus finds the other)

- NEW format (2026-10-08, "brain-satisfying maths"). The idea is taken from VisualMan's parabola rays video: hidden geometric order shown by many rays. The parabola, parallel rays and look are NOT copied: here it is an ellipse, a point source, and both characters sit at the foci.
- Mirror: ellipse a 480, b 388 (0.89 of the width), centre (540, 900), foci +-282.6 on the axis. Dark indigo stage, glowing white-violet wall over a dark glass band. Characters r 50. A ray is absorbed when it enters a circle of r 46 round the target.
- Exact ray tracing (closed-form ellipse intersection, reflection about the true wall normal, up to 8 bounces). The maths shown on screen:
  - Every ray from F1 reflects into F2.
  - |F1P| + |PF2| = 2a for every wall point P, so every ray also ARRIVES AT THE SAME INSTANT. The expanding ring of heads reflects into a ring that collapses onto Bolt.
- Ladder (fire -> arrival; speed 560 -> 700 px/s):

  | Volley | Fire | Arrival | Result |
  |---|---|---|---|
  | 8 | 0.10 s | 1.73 s | ALL HIT. Bolt: wow |
  | 36 | 2.85 s | 4.37 s | ALL HIT. Bolt: wince + worried |
  | 180 | 5.55 s | 6.98 s | ALL HIT. Bolt glows brighter |
  | 360, Mochi slid 150 px OFF the focus | 8.75 s | — | the rays form a caustic. ONLY 98 / 360 HIT. Bolt laughs, Mochi stares annoyed |
  | 720, back on the focus | 12.45 s | 13.76 s | ALL HIT. Bolt overloads |
  | reverse 720, from Bolt | 15.35 s | 16.66 s | ALL return to Mochi at once. Mochi's eyes widen, Bolt laughs |

- Overload: the halo grows by 150 px and 3 thin expanding rings play. It is NEVER a filled flash.
- The focus volleys skip a 9 deg cone aimed straight at the other focus. Those rays would hit directly and arrive early, which would break the "same instant" collapse. The miss volley uses the full 360 deg. Its rays are traced to 2a + 250 and then the whole volley fades.
- Rendering:
  - Each ray is its own ADD stroke, so overlapping light really adds up. With 40 hue buckets, 720 rays showed sawtooth "teeth" near the wall.
  - Each ray has a glow layer (w 3.6-9) and a core layer (w 1.25-2.6), with alpha min(1, 4.4/sqrt(N)).
  - Bright heads; wall sparks for 0.32 s.
  - After arrival the tail drains into the target at 2.6 v.
  - Rainbow by emission angle, symmetric top/bottom.
- HUD: baked caption "Every ray finds Bolt|~The ELLIPSE secret~". "RAYS: N" at 0.752h, popping when N changes. A verdict badge at 0.795h ("ALL N HIT BOLT" / "OFF THE FOCUS: ONLY 98 HIT" / "ALL 720 BACK TO MOCHI"). The counter fades back to "RAYS: 8" 0.75 s before the seam.
- Sound:
  - Melody: pachelbel_canon (+12) on glassharp. One note per volley fire and one per arrival.
  - The 720 arrival gets a chord (-5, -12, nudged +13 ms). The miss gets a soft note an octave down. The return lands an octave UP with a fourth (shorter ring, so the seam is silent).
  - Bed: a glass tick per wall reflection, D-major pentatonic, pitch climbing with reflection order (the sweep runs from the near vertex to the far one), descending for the reverse. Rate caps 0 / 40 / 34 / 26 ms give 8 -> 12 -> 23 -> 13 (miss) -> 29 -> 29 ticks per volley. A soft D-chord shimmer swells under the overload.
  - The bed is not in the sidecar, so regen_audio cannot rebuild it.
- Loop: Mochi absorbs the returned light, then settles to frame 0's glow (q 0.32). The fire anticipation squash wraps the seam. Blinks are suppressed within 0.3 s of the seam. Pre-encode seam mean 0.023.
- Checks (encoded Full HD): h264 yuv420p 1080x1920, 60 fps, 1179 frames = 19.65 s. -14.00 LUFS, peak -6.69 dBFS, last 0.5 s -68 dBFS. Encoded seam 0.192. flash_check 0 flashes, mean luminance 0.013 = PASS.
- Args: --label, --cap ("a|~b~", '' = none), --melody, --off DX,DY (Mochi's miss spot relative to F1; 150,0 default). Other spots: 40,-190 gives an intricate asymmetric caustic with 50/360 hits; -120,0 gives 128 hits. Also --still --frame.
- Render: ~1-2 min Full HD.
- Delivered: <VIDEOS_DIR>\batch19\ellipse_rays.mp4 (Full HD). Owner review: pending.
- Owner review 2026-10-09: Good melody and more space: smaller characters, rays travel further -> ellipse_rays2.
