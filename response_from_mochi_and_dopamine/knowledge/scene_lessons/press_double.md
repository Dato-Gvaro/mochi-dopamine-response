# press_double — press family, ONE change: "Bolt's TINY press DOUBLES every hit"

- Brief: docs/BRIEF_mochi_1113.md clip 1. New file `scenes/press_double.py` on press_split2's engine (press_split2 untouched).
- Rule (both, the family's): every ball crushed splits into 3 at 0.66x radius; 7 crushes = DUST (r 4.5, never splits). 1 ball -> exactly 3^7 = 2,187 grains = "ALL DUST" (meter under each chamber from frame 0).
- Mochi: one plate, fixed at 1/2 the chamber width (`--mw`). Bolt: 1/64 (`--b0`), doubling every hit to x64 = full width at hit 7.
- A press crushes only what is UNDER it: a ball's centre within the plate +- r/2 and joined to the plate by contacts inside that column. Both aim at the column with the most uncrushed balls (same rule). Bolt strikes half a period after Mochi (B_OFF 0.354 s): an event every ~0.4 s.
- Stroke clock: period 1.0 s, -0.025 per stroke, min 0.72 s.
- Contact = the wave reaches an uncrushed ball (loose dust above the pile is pushed ahead); stall counts only balls under the plate. Without these the plate stalled on stray grains / ball flanks and missed whole strokes.
- Seed 2 (searched 0-11; Bolt wins on every seed, lead change 1-3 s before the finish): LEAD CHANGE 7.93 s, ALL DUST 9.50 s, Mochi 1,371 vs 2,187. The race ends there: both finish the stroke in progress and rest (letting Mochi go on took her to 2,169 by the loop: a near-tie that blurred the finish).
- Crushes per second: 3 6 13 30 84 238 200 434 391 379.
- Sound: Fur Elise (Beethoven WoO 59, PD; verified vs Mutopia 931) one note per crush group (60 ms), a bigger hit plays a run of up to 4 notes (70 ms apart); squash per split +12 ms; thunk/clank per press sized by plate; a chime per doubling; riser into Bolt's last hit; thunk + rolled A minor at ALL DUST; bed fades over the 0.6 s dissolve.
- Physics source: pressure acts through the contact area; under a loaded footing the vertical stress sits in a "pressure bulb" below the footprint and falls off quickly past its edge (Boussinesq 1885; e.g. Das, Principles of Foundation Engineering). Simplification: no lateral stress spread is modelled, and both presses are strong enough to crush any ball (a bigger plate at the same force would press softer).

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/press_double.py --still --frame 0,300,560 --label x`
- `NF_SCALE=1.0 python scenes/press_double.py --label fhd` (sim ~6 s, cached in output/*.pkl; render ~2 min)
- `python scenes/press_double.py --search 0 12`
