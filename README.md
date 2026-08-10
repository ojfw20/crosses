# Crosses ZMK config

Firmware for my GGGW Crosses/Bridges 36-key wireless split (SuperMini nRF52840,
trackball on the right half, no displays). The layout is a straight port of my
Charybdis nano keymap ([ojfw20/charybdis](https://github.com/ojfw20/charybdis)):
Colemak-DH with home-row mods, tri-layer nav/sym, explicit mouse and scroll
layers, and two game layers. Based on the official
[crosses-zmk](https://github.com/Good-Great-Grand-Wonderful/crosses-zmk) template.

Firmware builds in GitHub Actions on every push. Flash order for a fresh pair:
`settings_reset` on both halves, then `crosses_36_left` / `crosses_36_right`
(use the `_internal_osc` variants if Bluetooth is unstable on the SuperMinis).

Tuning knobs: scroll speed/direction is the `scroller` input-processor node in
`config/crosses.keymap`. Trackball CPI defaults to 700, set in the GGGW shield
module (`gggw-zmk-keebs`, `crosses_right.overlay`) - to change it, add an
overlay with `&trackball_central { cpi = <...>; };` and pass it to the right-half
builds via `-DEXTRA_DTC_OVERLAY_FILE` in `build.yaml` (it can't go in the shared
keymap; the node only exists on right-half builds).

![Keymap](keymap-drawer/crosses.svg)
