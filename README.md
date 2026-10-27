# Re-gret ZMK Module

This is a [ZMK Module](https://zmk.dev/docs/features/modules) for my [Re-gret keyboard](https://github.com/rschenk/re-gret).

To use this in your zmk-config, follow the [ZMK Module docs](https://zmk.dev/docs/features/modules) using the config below. You'll name your keymap `re-gret.keymap`.

## Usage

Add the following entries to `remotes` and `projects` in `config/west.yml`

```yaml
# config/west.yml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: rschenk
      url-base: https://github.com/rschenk
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: v0.4 # set to desired version
      import: app/west.yml
    - name: zmk-keyboard-re-gret
      remote: rschenk
      revision: v0.4 # set to same version as zmk above
  self:
    path: config
```

And then in your `build.yaml` file:

```yaml
# build.yaml
board: ["xiao_ble"]
shield: ["re-gret"]
```

## Keymap Editor

To edit this repository's keymap with [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/), select this repository and the branch containing these files:

- `config/re-gret.keymap` is the editable user keymap. ZMK uses it instead of the module's default keymap when building this repository.
- `config/re-gret.json` describes the 34-key layout for the editor. Its key order, positions, and rotations match `boards/shields/re-gret/re-gret-layouts.dtsi`; `row` and `col` describe the visual rows and columns, not the electrical matrix.

Layer references and combo idle times are written as numeric values in the user keymap so the editor can read and preserve them. The initial bindings, conditional layers, and combo timings match the module default.

The editor requires the complete keymap directly in `config/`; it does not discover the default keymap under `boards/shields/`. Keep personal keymap changes in `config/re-gret.keymap`. The keymap under `boards/shields/re-gret/` remains the default for other configs using this repository as a module.

For the GitHub source, commit and push these files before reloading the repository in the editor. For local editing, choose the File System source and open `config/re-gret.keymap`, using `config/re-gret.json` as the custom layout if prompted.

## Versioning

ZMK introduced some breaking changes with v0.4. I have updated this module to compile with v0.4 but you should [pin your ZMK version](https://zmk.dev/blog/2025/06/20/pinned-zmk) and pin the version of `zmk-keyboard-re-gret` to match
