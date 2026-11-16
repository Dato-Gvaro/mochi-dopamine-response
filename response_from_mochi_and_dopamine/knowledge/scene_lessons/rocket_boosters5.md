# rocket_boosters5 — the honest race, then a SKYHOOK (real physics) (batch71)

- Brief: docs/BRIEF_batch71.md §4 (owner: "no to that carpet ... a physics trick"). New file `scenes/rocket_boosters5.py` (from rb4; rb2/rb4 untouched). Race bit-for-bit rb2/rb4.
- Skyhook (HASTOL class): race time-lapse ×16.74 (sqrt(g_video/g)); catch at Bolt's burnout sim 9.60, 193.8 km, 4.378 km/s. Arm 300 km, hub 493.8 km circular (7.620 km/s), tip spin 3.242 km/s (= hub − Bolt, so 0 relative at the cusp), ω 0.01081 rad/s = 1 turn / 9.69 min, 3.57 g. Altitude after the catch h = H_HUB − L cos θ; screen x = cycloid in Bolt's moving frame (KX 0.9 px/km).
- Result: Mochi wins (sim 10.23); Bolt reaches the line sim 16.53 (116 real s after the catch), 6.3 s later. A win would need ~20 km/s: impossible. Coast-only would touch 400 km at 12.58 (altitude-only model).
- Clip clock: FAST-FORWARD ×6 (smooth ramp, labelled) sim T_CAD+0.55 → T_X−0.30.
- Checks (encoded Full HD, label b71): h264 yuv420p 1080x1920 60 fps, 946 f = 15.77 s; −14.00 LUFS, peak −2.0, last 0.5 s silent; flash PASS; seam 1.67 (space → sky dissolve, as rb4).
- Delivered review/batch71/rocket_boosters5.mp4. Owner review: pending.

## v2 (coordinator, batch71): finish = first into a STABLE ORBIT
- Rule: ≥400 km AND orbital speed (V_NEED 7.673 km/s at 400 km); release = first moment the tip state gives a bound orbit with perigee ≥ P_MIN 200 km. 2D inertial model (hub circular, arm prograde), RK4 free flight after release.
- Mochi: top speed 3.19 km/s, 2.28 at 400 km (sim 10.23), apex 664 km sim 24.1 → never in orbit (earlier episodes' "orbit" was altitude-only). Bolt rocket top 4.38.
- Bolt: released sim 23.02 (225 real s after the catch) at 669 km, 9.84 km/s, perigee 200 km → BOLT WINS. FF ×10 sim 11.08-22.72. KX 0.35, hub slides left→right (tether away from Mochi/banners). Cadence on the release.
- Checks (label b71v2): 978 f = 16.30 s; −14.01 LUFS, peak −2.0; flash PASS; seam 1.17. Delivered (replaced v1).

## v2 (coordinator, batch71): finish = first into a STABLE ORBIT
- Rule: ≥400 km AND orbital speed (V_NEED 7.673 km/s at 400 km); release = first moment the tip state gives a bound orbit with perigee ≥ P_MIN 200 km. 2D inertial model (hub circular, arm prograde), RK4 free flight after release.
- Mochi: top speed 3.19 km/s, 2.28 at 400 km (sim 10.23), apex 664 km sim 24.1 → never in orbit (earlier episodes' "orbit" was altitude-only). Bolt rocket top 4.38.
- Bolt: released sim 23.02 (225 real s after the catch) at 669 km, 9.84 km/s, perigee 200 km → BOLT WINS. FF ×10 sim 11.08-22.72. KX 0.35, hub slides left→right (tether away from Mochi/banners). Cadence on the release.
- Checks (label b71v2): 978 f = 16.30 s; −14.01 LUFS, peak −2.0; flash PASS; seam 1.17. Delivered (replaced v1).
