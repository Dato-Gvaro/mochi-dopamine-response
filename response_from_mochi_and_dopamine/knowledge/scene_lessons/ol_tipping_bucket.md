# ol_tipping_bucket (DopamineEXE, batch75 #3): stills stage, NEEDS REDESIGN
- Valve -> edge-fed wheel (housed) -> a corner-pivot tipping bucket (snap-through counterweight at (30,15)) -> funnel -> rain-gauge see-saw (pivot friction) -> a GIANT bucket on an axle 30 px above its bottom. Rigid 1-DOF parts coupled two ways through the PBD contact impulses.
- Lessons:
  - A counterweight below-right of the pivot gains leverage as the bucket tips, so it never snaps over.
  - Water landing on a tipped bucket holds it down, so the bucket must swing out of the stream.
  - A granular "water" CoM must rise above the giant's axle before it flips, so a high axle never tips.
  - Dump impacts rock the giant over early.
  - The see-saw caps throughput at about 40-60/s.
- Current: tips at 14.25 s with about 300 balls (about 20% full), clip 18.25 s; 50%+ of the water sprays or overflows to the floor.
- v2 (batch75 round 2): no see-saw. Two corner-pivot buckets + the giant. All tipping parts are driven by the STATIC moment of the balls inside the cup + the counterweight (not contact impulses: stream impacts pinned buckets). Giant TIP = the measured fill when it left its stop (686 balls, line 118/140 px), one big dump at 11.5 s into a splash pool. Sheet `review\batch75\ol_tipping_bucket_sheet_v2.png`. Weak: a mild tip-rate climb, spray at x16.
