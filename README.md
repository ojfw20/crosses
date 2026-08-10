# Crosses ZMK config

Firmware for my Crosses/Bridges 36-key wireless split, the **AliExpress
"MiaoMiao PCB" variant**, not a genuine GGGW board (SuperMini nRF52840 clones,
PMW3610 trackball on the right half, no displays). Matrix GPIOs, `row2col`
diodes and trackball SPI wiring come from
[maatthc/zmk-crosses](https://github.com/maatthc/zmk-crosses) (the 42-key clone
config); I mapped the 3x5 matrix positions with a diagnostic firmware. The outer column
of the 42-key design is unpopulated, and the thumbs sit on row 3 cols 3/4/5 and
11/10/9.

The layout is a straight port of my Charybdis nano keymap
([ojfw20/charybdis](https://github.com/ojfw20/charybdis)): Colemak-DH with
home-row mods, tri-layer nav/sym, explicit mouse and scroll layers, and two
game layers. The trackball scrolls on layers 5-7 via the PMW3610 driver's
`scroll-layers` property.

Firmware builds in GitHub Actions on every push. Flash order for a fresh pair:
`settings_reset` on both halves, then `crosses_36_left` / `crosses_36_right`.
The SuperMini clones have no external 32 kHz crystal, so `config/crosses.conf`
sets `CONFIG_CLOCK_CONTROL_NRF_K32SRC_RC=y`; without it the firmware hangs at
boot.

Trackball tuning lives in the shield's `crosses_right.conf`:
`CONFIG_PMW3610_CPI` / `CONFIG_PMW3610_CPI_DIVIDOR` (1600/4 = 400
effective), orientation/invert flags alongside.

![Keymap](keymap-drawer/crosses.svg)
