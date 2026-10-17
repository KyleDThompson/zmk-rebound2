# zmk-rebound2 — Rebound v4 ZMK overlay (updated for ZMK main)

This repository provides a ZMK shield/overlay and keymap for the Monsinger Rebound v4 keyboard. I updated the repository on branch `update/zmk-main-studio` to make it compatible with ZMK "main" and ZMK Studio with minimal changes.

What I changed
- Fixed a device-tree property name in `config/rebound_v4.keymap`: `tapping_term_ms` -> `tapping-term-ms` (DT properties use hyphens).
- Created this README with quick build and ZMK Studio instructions.

What I did NOT change
- I kept your keymap layout and behavior nodes the same to minimize risk. Further behavior renames may be required if ZMK main has changed behavior binding names; we can iterate on that after a test build.

Build / test instructions (shortest path)
1. Install Zephyr SDK, west, and other ZMK prerequisites per ZMK docs: https://zmk.dev/docs/ or https://zmk.dev/.
2. Initialize the west workspace using the manifest included here:

```bash
# from the repo root
west init -m config/west.yml -s config
west update
west zephyr-export   # if required by your Zephyr/west setup
```

3. Build for your board (Nice!Nano clone / nRF52840):

```bash
west build -b nice_nano_v2 app
```

(If you named a different board in your local toolchain, replace `nice_nano_v2` with the board name shown by `west boards`.)

Flashing
- Use `west flash` (and ensure the board is in bootloader mode), or use your usual nrfutil/DFU tool to program the resulting .hex/.uf2 in `build/zephyr`.

ZMK Studio
- In ZMK Studio, open "Open Repository from GitHub" and paste: https://github.com/KyleDThompson/zmk-rebound2 and choose branch `update/zmk-main-studio`.
- Let Studio fetch the workspace (it uses the manifest at `config/west.yml`). You should be able to remap layers and recompile from Studio; if compilation fails, open an issue here and I'll iterate.

Next steps I can take
- Run a local build (CI) to catch compile-time errors and fix any device-tree or behavior renames.
- If you want, I'll open a PR from `update/zmk-main-studio` to `master` including build logs and any additional fixes required for ZMK main.

If you want me to proceed to run builds and make further fixes, say "Please run builds and fix errors" and I will iterate until it compiles.