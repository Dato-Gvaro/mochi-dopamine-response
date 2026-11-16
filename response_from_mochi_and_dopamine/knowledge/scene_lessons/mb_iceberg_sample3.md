# mb_iceberg_sample3: "Mochi & Bolt vs The Iceberg" v3 (16:9 SHORT test, 32.4 s)

- **Sources.**
  - Owner review: docs/REVIEW_1114_iceberg.md.
  - Built from `scenes/mb_iceberg_sample2.py`, which is untouched (see docs/scenes/mb_iceberg_sample2.md for the fracture, targeting and spacing rules, all still in force).
- **Review files.**
  - The video is `<VIDEOS_DIR>\MochiAndBolt\review\mb_iceberg_sample3.mp4`.
  - README, PROGRESS, the sheet, crops and stills are in `...\review\mb_iceberg_sample3_files\`.

## What changed vs v2
- **Hidden objects.**
  - The object is drawn first. The intact cells go on top as ONE opaque fill (the FROST gradient), followed by `draw_frost`: a seeded per-ice texture in local coords, cached in `_TEX` (milky blobs, hairline cracks, bubble clusters, speckle).
  - The only hint is `hint`, a faint shapeless radial shadow (alpha 0.17).
  - Melting cells: alpha = 1 - 0.8 * clamp((mf - 0.05) / 0.75). Chunks are opaque too.
  - OBJ_K 0.66 (v2 0.52): a bigger object means each hole shows a part.
- **The berg ship.**
  - It is drawn under the ice, clipped to the berg's original outline, with SHIP = (-160, 112, 520) local.
  - At y 150 the hull was fully exposed by 26 s. At 112 it shows plank by plank, and the split (26.7 s) is the big reveal.
- **Inventory.**
  - `draw_slot` / `draw_badge` / `draw_inventory` replace the racks. INV_S 86, gap 10, a 2x2 grid per side, x 24..206 / 1714..1896, y 404..586, with a face icon above.
  - An item goes to its OWNER's side (a shared block goes to the finisher), inner column first. It flies (t + 0.35 → t + 0.95, snapped to G), snaps with a pop, a gold glow, sparkles and a click.
  - ITEM_PTS is added to the HUD score at the snap (`item_bonus`). The sim scores exclude it.
- **Speed.**
  - TEMPO 1.3 (`TS = 1/1.3`). Every v2 duration is multiplied by TS: ENTRY_S, the boss entry/hits/crack/split, the stall breaker, and the label and flight times.
  - desc_v and the character spring (k x TEMPO^2) are multiplied by TEMPO. Handover 0.45 s, TBC_S 3.4, PRE_S 1.9.
- **Cells.**
  - Cubes are 12 / 11 / 8 (v2 9 / 10 / 8): more, smaller pieces give a piece-by-piece reveal.
  - **L3 at 10 cells, or all at 12, makes the sim run away (it stalls).** Keep L3 at 8.
- **Drips.** `post_drips`: melting cells shed up to 4 drops each. A drop plinks with a ripple on the snow, or turns to steam on the hot tool. Drops over a character or Bolt's tool are not spawned.

## Audio (ASMR-led)
- **No `audio.mix_events`.** Each SFX is synthesised in the scene: `sfx_crack`, `sfx_snap`, `sfx_thud`, `sfx_tinkle`, `sfx_slush`, `sfx_plink`, `sfx_tss`, `sfx_click`, `sfx_rumble`, `sfx_chime`, plus a glass-harp `ding`.
- **The sizzle bed** (`sizzle_bed`) is a continuous bed whose envelope follows the heat hits (40 ms attack, 250 ms release), panned to the tool.
- **Cracks are pitched to the prelude's arpeggio note** (+12), so the hits still play the tune quietly.
- **12 ms onset rule:** any onset within 12 ms of the previous one is nudged +12 ms. Nothing is ever dropped.
- **Balance** is set by per-kind LUFS before mastering. Full SFX is -15:
  - crack -19 (centroid 2.9 kHz; the first version measured 9.9 kHz, "hissy");
  - thud -20 (it was -14 and drowned everything);
  - snap -21;
  - tinkle and sizzle -24;
  - slush and plink -25;
  - click -26;
  - chime -27.
- **Music.** The bgm prelude_c bed is scaled to MUSIC_UNDER = 9 dB under the SFX stem's integrated LUFS. Then `audio.master(peak_db=-6)`.
- **Measured gap** at the master's gain: 9.0 dB integrated, 11.1 dB (SFX P90 momentary vs music median), 12.3 dB peak.
- **Tools.**
  - `--stems` writes `output/mb_iceberg_sample3_stem_{sfx,music}.wav` and prints the gap.
  - `--remux <mp4>` rebuilds only the soundtrack (no `-shortest`).
  - The events sidecar is `<name>_events.json`. tools/regen_audio does NOT know this pipeline; use `--remux`.

## Numbers (FHD, encoded)
- **File:** 32.40 s, 1944 frames, h264 High yuv420p 1920x1080 60 fps; AAC 48k stereo.
- **Loudness:** -14.0 LUFS, TP -5.2 dBTP, tail -84 dBFS.
- **Checks:** flash PASS (worst 1 flash per 1 s); freezedetect: none ≥ 0.3 s.
- **Sim:**
  - first reveal 2.52 s;
  - hits/s: L1 2-6, L2 5-8, L3 10-15, boss 13-17;
  - lowest ice L1/L2/L3: 561 / 669 / 738 (heads 890);
  - boss HP ends at 33%;
  - 97 bodies, 69 drips (48 plink).
- **Render times:** FHD 72 s, FAST 40 s, `--plan` 2 s, `--stems` 10 s.

## Commands
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
python scenes/mb_iceberg_sample3.py --plan
$env:NF_FAST='1'; python scenes/mb_iceberg_sample3.py --still --frame 0s,1.6s,3.66s,8.2s,15.5s,25.5s --label s; Remove-Item Env:NF_FAST
python scenes/mb_iceberg_sample3.py --stems
# full renders: take output/render.lock first
$env:NF_SCALE='1.0'; python scenes/mb_iceberg_sample3.py --label fhd1 --review
```

## Lessons
- Opaque ice needs a bigger object (OBJ_K). At 0.52, holes in the outer cells showed only sky.
- Peak-normalised synth SFX lie about loudness. Balance per kind by LUFS, not by gain numbers.
- Low thuds dominate integrated LUFS fast; keep them about 1 dB under the per-hit crack.

## Open
- The SFX rate eases after the split (27-29 s) before the end card. The same shape as v2, but the "rate climbs to the last frame" rule is not met in the boss tail.
- Owner questions are in the README: ship exposure, points badges, boss HP.
