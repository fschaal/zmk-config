# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a ZMK firmware configuration repository for an Eyelash Corne split keyboard with nice!view displays and ZMK Studio support.

## Build Process

Firmware builds are automated via GitHub Actions. Pushing to the repository triggers the build workflow, which produces downloadable firmware artifacts.

The build matrix is defined in `build.yaml`:
- Left half: `eyelash_corne_left` with `nice_view` and ZMK Studio enabled
- Right half: `eyelash_corne_right` with `nice_view`
- Settings reset: `nice_nano_v2` with `settings_reset`

To trigger a build, push changes to the repository. Download the compiled `.uf2` files from the GitHub Actions artifacts.

## Key Configuration Files

### `config/eyelash_corne.keymap`
The main keymap file using Devicetree syntax. Contains:
- **Combos**: Key combinations that trigger actions (Enter, Tab, Escape, Lock, Equals)
- **Behaviors**: Custom hold-tap configurations for home row mods (balanced flavor with positional hold-trigger)
- **Layers**: BASE (custom layout), FUNC (F-keys and media), SYMB (symbols and numbers), WIN (window management)

### `config/eyelash_corne.conf`
Board configuration options:
- Bluetooth power boost enabled (`CONFIG_BT_CTLR_TX_PWR_PLUS_8`)
- Deep sleep enabled (15 min timeout, 30 sec idle)
- RGB underglow with auto-off on idle
- Encoder (EC11) support
- Pointing device/mouse support
- Soft off support
- NKRO enabled

### `config/west.yml`
West manifest defining external dependencies:
- ZMK firmware v0.3.0 from `zmkfirmware/zmk`
- Eyelash Corne board definitions from `a741725193/zmk-new_corne`

## Keymap Structure

The keyboard uses a custom non-QWERTY layout. Key positions are numbered 0-41 for a 3x6+3 split keyboard layout.

Home row mods use positional hold-tap behaviors:
- `Hold_tap_left`: Triggers hold on right-hand keys
- `Hold_tap_right`: Triggers hold on left-hand keys

Layer access:
- Hold left thumb `SPACE` for FUNC layer
- Hold right thumb `ENTER` for SYMB layer
- Hold left pinky `TAB` for WIN layer

## ZMK Studio

The left half is built with ZMK Studio support, allowing real-time keymap editing via USB connection.

## ZMK Documentation

For ZMK-specific syntax and features, refer to:
- Keymap behaviors: https://zmk.dev/docs/behaviors
- Combos: https://zmk.dev/docs/features/combos
- Hold-tap: https://zmk.dev/docs/behaviors/hold-tap
- Pointing devices: https://zmk.dev/docs/features/pointing
