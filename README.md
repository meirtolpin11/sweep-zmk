# NXTKB Ferris Sweep ZMK Config

[![Firmware Build](https://img.shields.io/github/actions/workflow/status/nxtkb/zmk-config-4-ferris-sweep/build.yml?branch=main&label=firmware%20build&style=flat-square)](https://github.com/nxtkb/zmk-config-4-ferris-sweep/actions/workflows/build.yml)
[![Docs Status](https://img.shields.io/website?url=https%3A%2F%2Fnxtkb.com%2Fdocs%2Fsetup%2Fkeymap%2Fferris-sweep-keymap%2F&label=docs&up_message=online&up_color=2f6f6f&down_message=offline&down_color=8b1e3f&style=flat-square)](https://nxtkb.com/docs/setup/keymap/ferris-sweep-keymap/)
[![Keymap Source](https://img.shields.io/badge/keymap-cradio.keymap-5f6fbf?style=flat-square)](./config/cradio.keymap)
[![ZMK Config](https://img.shields.io/badge/ZMK-cradio.conf-6b7280?style=flat-square)](./config/cradio.conf)
[![ZMK Studio](https://img.shields.io/badge/ZMK-Studio-8b5cf6?style=flat-square)](https://zmk.studio/)
[![Input Tester](https://img.shields.io/website?url=https%3A%2F%2Finput-test.nxtkb.com%2F&label=input%20tester&up_message=online&up_color=2f6f6f&down_message=offline&down_color=8b1e3f&style=flat-square)](https://input-test.nxtkb.com/)

[中文](./README-zh_CN.md) | English

This repository contains the ZMK firmware configuration for the NXTKB Ferris
Sweep keyboard. It is based on the [Sweep](https://github.com/davidphilipbarr/Sweep)
layout, builds with [ZMK](https://github.com/zmkfirmware/zmk), and supports
[ZMK Studio](https://zmk.studio/) for live keymap edits when the firmware
enables it. Use this repository to inspect, fork, and build firmware. For
setup, flashing, keymap diagrams, and day-to-day usage notes, start with the
public NXTKB docs.

## Official Docs

- [Getting Started](https://nxtkb.com/docs/setup/)
- [Ferris Sweep Keymap](https://nxtkb.com/docs/setup/keymap/ferris-sweep-keymap/)
- [Ferris Sweep Configuration](https://nxtkb.com/docs/firmware/ferris-sweep-configuration/)
- [How to Update Keymaps](https://nxtkb.com/docs/setup/keymap/how-to-update-keymaps/)
- [How to Flash Firmware](https://nxtkb.com/docs/firmware/how-to-flash-a-firmware/)
- [Keyboard & Mouse Test](https://nxtkb.com/docs/setup/keymap/input-tester/)

Chinese docs are also available:

- [入门指南](https://nxtkb.com/zh/docs/setup/)
- [Ferris Sweep 键位映射](https://nxtkb.com/zh/docs/setup/keymap/ferris-sweep-keymap/)
- [Ferris Sweep 配置文件](https://nxtkb.com/zh/docs/firmware/ferris-sweep-configuration/)

## Repository Layout

- `config/cradio.keymap`: layers, key bindings, home-row modifiers,
  conditional layers, mouse layer, bootloader keys, soft-off behavior, and ZMK
  Studio unlock.
- `config/cradio.conf`: board-level ZMK settings for this keyboard.
- `build.yaml`: GitHub Actions build matrix for generated firmware artifacts.
- `.github/workflows/build.yml`: firmware build workflow that reuses ZMK's
  user config build.

## Pinned Dependencies

[![ZMK revision](https://img.shields.io/badge/zmk-8feeb52-5f6fbf?style=flat-square)](https://github.com/zmkfirmware/zmk/tree/8feeb52)
[![zmk-behavior-report revision](https://img.shields.io/badge/zmk--behavior--report-476f43da-2f6f6f?style=flat-square)](https://github.com/nxtkb/zmk-behavior-report/tree/476f43da1f98b4a6150c9c0e499a257bd64a29a0)

The firmware build is pinned through `config/west.yml`:

| Project | Remote | Revision |
| :--- | :--- | :--- |
| `zmk` | `zmkfirmware/zmk` | `8feeb52` |
| `zmk-behavior-report` | `nxtkb/zmk-behavior-report` | `476f43da1f98b4a6150c9c0e499a257bd64a29a0` |

## Firmware and Keymap Workflow

For persistent configuration changes:

1. Fork this repository.
2. Edit `config/cradio.keymap` or `config/cradio.conf`.
3. Let GitHub Actions build the firmware artifacts.
4. Flash the generated UF2 file to the matching keyboard half.

For quick keymap edits, use [ZMK Studio](https://zmk.studio/) when this
firmware supports it. For the full decision guide, see
[How to Update Keymaps](https://nxtkb.com/docs/setup/keymap/how-to-update-keymaps/).

## Keymap Summary (Sofle Mirrored)

![Ferris Sweep Sofle Mirrored Layout](docs/images/layout.jpg)

This configuration mirrors the Sofle ergonomic setup (`mtolpin-ergo-setup`) on the 34-key Ferris Sweep:

- **Base Layer (Mac / Windows)**: QWERTY layout with Home Row Modifiers and standard `;` and `/` positions.
- **Thumbs**: 
  - Left Outer: `Shift`
  - Left Inner: `Space` (Tap) / **Lower Layer** (Hold)
  - Right Inner: `Enter` (Tap) / **Raise Layer** (Hold)
  - Right Outer: `Backspace`
- **Lower Layer (Left Thumb Hold)**: Left-hand ESDF Arrow Navigation + Right-hand 10-key Numpad block.
- **Raise Layer (Right Thumb Hold)**: Brackets (`{}`, `()`, `[]`) on right hand + math/code symbols (`-`, `_`, `=`, `+`, `\`, `:`).
- **Tri Layer (Function & BT)**: Activated when holding both thumb layer keys simultaneously (`F1-F12`, Bluetooth profiles, Soft-off, Studio unlock).
- **Combos**:
  - `Q + W` = `ESC`
  - `A + S` = `TAB`
  - `O + P` = `BSPC`
  - `I + O` = `DEL`
  - `L + ;` = `'`
  - `Z + X` = Language Switch Macro
  - `X + C` = Close Tab Macro

## Bootloader and Flashing Notes

To enter bootloader mode, use one of these methods:

1. Press the keymap's `Boot` key while the keyboard is connected.
2. Double-click the reset button.
3. Short `RST` to `GND` twice if the reset button is not available.

Firmware artifact names normally indicate the target half:

- `left`: left half firmware.
- `right`: right half firmware.
- `reset`: reset firmware for clearing Bluetooth pairing information.

If you only changed key bindings or the keyboard name, you usually only need to
flash the left half. If you changed split behavior, board settings, or
right-half behavior, flash the affected half as well. See
[How to Flash Firmware](https://nxtkb.com/docs/firmware/how-to-flash-a-firmware/)
before updating a board.
