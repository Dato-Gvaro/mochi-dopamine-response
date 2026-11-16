# bolt_bubbles — Bolt pops bubbles on a trampoline

- Rule: two bubble machines blow faster and faster (2.4/s -> 10.4/s) and the share of big bubbles grows; a big bubble splits into 3 when popped (children are immune for 0.35 s). Bolt picks each jump by scoring candidate arcs for how many bubbles they sweep through.
- Loop: the sim runs from -1.5 s to dur+1.5 s, and the last 1.5 s cross-fades the continuation into the pre-roll that leads into frame 0. The audio is folded the same way.
- GOTCHA: map event times to the folded time BEFORE gap-thinning. Sorting by sim time put pre-roll events first and the 0.05 s gate swallowed the whole clip (the first render had 3 events). Fixed, and the audio was re-muxed with `-t` (render_soundtrack's wav is +2 s).
- s2: 35.5 s, spring_vivaldi on pops (+12 for small bubbles), bounce on landings. Theme lilac. Pops per 5 s [15, 24, 26, 49, 51, 79, 80].
- Measured: -13.9 LUFS, -3.6 dBTP, flash_check 0.
- Owner review 2026-10-03: Very cute.
