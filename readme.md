# diy_louder

![diy_louder](gallery/IMG_3381.jpg)

A 4x12 (48-key) ortholinear mechanical keyboard powered by an RP2040 microcontroller running QMK firmware.

📁 **[View more photos in the Gallery](./gallery)**

---

## About the Project

**diy_louder** is my first handwired keyboard project, built in 2025 and inspired by the Work Louder XYZ board.

I personally designed and 3D modeled the case from scratch, which was also my first time learning CAD software. Because Work Louder hadn't released their case design publicly at the time, I modeled it entirely by studying reference images and photos from their website.

---

## Specifications

* **Keyboard Maintainer**: [irxd](https://github.com/irxd)
* **Form Factor**: 4x12 Ortholinear (48 keys)
* **Microcontroller**: Raspberry Pi RP2040
* **Bootloader**: RP2040 (`.uf2`)
* **Diode Direction**: `COL2ROW`
* **Features Enabled**: Bootmagic, Extrakey (Media controls), Mousekey, NKRO

### Pinout Configuration

* **Rows (4)**: `GP0`, `GP1`, `GP2`, `GP3`
* **Cols (12)**: `GP4`, `GP5`, `GP6`, `GP7`, `GP8`, `GP9`, `GP15`, `GP14`, `GP13`, `GP12`, `GP11`, `GP10`

---

## Step-by-Step Setup Guide

### 1. Prerequisites

Make sure you have the QMK CLI installed and configured on your computer:

```bash
python3 -m pip install --user qmk
qmk setup
```

### 2. Add keyboard to QMK directory

Link or copy this `diy_louder` directory into your `qmk_firmware/keyboards/` directory:

```bash
# Option A: Symlink (recommended for development)
ln -s "$(pwd)" ~/qmk_firmware/keyboards/diy_louder

# Option B: Direct Copy
cp -r . ~/qmk_firmware/keyboards/diy_louder
```

### 3. Compile the Firmware

Compile the default keymap:

```bash
qmk compile -kb diy_louder -km default
```

*(Alternatively using make from inside `~/qmk_firmware`)*:

```bash
make diy_louder:default
```

This will produce a `.uf2` file (e.g. `diy_louder_default.uf2`).

### 4. Enter Bootloader Mode

To flash the board, place the RP2040 into bootloader mode using one of these methods:

* **Physical Button**: Hold down the `BOOT` / `BOOTSEL` button on your RP2040 board while plugging in the USB cable (or hold `BOOT` and press `RESET`).
* **Bootmagic Reset**: Hold down the top-left key (`Esc` at row 0, col 0) while plugging in the keyboard.

Once in bootloader mode, a removable drive named **`RPI-RP2`** will appear on your computer.

### 5. Flash the Firmware

Choose either method below:

* **Method A (Direct Drag & Drop - Recommended)**:
  Drag and drop the generated `diy_louder_default.uf2` file into the `RPI-RP2` drive. The drive will automatically unmount and the keyboard will reboot with your firmware.

* **Method B (QMK CLI)**:
  Run the flash command while the board is in bootloader mode:
  ```bash
  qmk flash -kb diy_louder -km default
  ```

---

## Keymap Layers

The default keymap includes 3 layers:

* **Base (`_BASE`)**: Standard 4x12 QWERTY ortholinear layout. Space keys are split, flanked by `RAISE` and `LOWER` momentary layer toggles.
* **Raise (`_RAISE`)**: Access to number row (`1`–`0`), minus/equal keys, and function keys (`F1`–`F11`).
* **Lower (`_LOWER`)**: Access to symbols, brackets/braces (`()`, `[]`, `{}`), macOS screenshot shortcuts (`Cmd+Shift+3/4/5`), volume control, and media playback keys (`Play/Pause`, `Prev`, `Next`).

Custom keymaps can be configured in [`keymaps/default/keymap.c`](./keymaps/default/keymap.c).

---

## Gallery

Check out the build and hardware photos in the [gallery folder](./gallery):
* [IMG_3381.jpg](./gallery/IMG_3381.jpg)
* [IMG_3382.jpg](./gallery/IMG_3382.jpg)
* [IMG_3383.jpg](./gallery/IMG_3383.jpg)
* [IMG_3386.jpg](./gallery/IMG_3386.jpg)

---

## To-Do

- [ ] Add layout configuration
- [ ] Add case 3D model files (STL / STEP files for 3D printing)
- [ ] Add complete components list & Bill of Materials (BOM) (switches, diodes, RP2040 board, hardware/screws)
