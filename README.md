# IATRT Internal KiCad Build

> **⚠ THIS IS NOT OFFICIAL KICAD ⚠**
>
> This repository is an **internal fork** maintained by
> [IATRT](https://github.com/IATRT) for in-house hardware development.
> It is **not affiliated with, endorsed by, or supported by the KiCad project**
> or its developers in any way.
>
> - Do **not** report bugs found here to the official KiCad bug tracker
> - Do **not** assume anything here represents planned or accepted KiCad functionality
> - Do **not** use this build outside IATRT without fully understanding it carries
>   unsupported, untested-by-upstream modifications
>
> **For official KiCad visit [kicad.org](https://kicad.org)**

---

## What is this

A **private, internal build** of KiCad 10.0.1 with IATRT-specific additions.
Not intended for public consumption. Not a PR. Not a proposal. Not a complaint.
Just a fork we use at work.

Upstream base: `gitlab.com/kicad/code/kicad` · tag `10.0.1`

Built and tested on **Ubuntu 26.04 LTS (Resolute Ringtail)**.

---

## IATRT additions

### LCSC / EasyEDA Import Panel

New **LCSC Import** tab in the symbol chooser — import parts from LCSC/EasyEDA without leaving the schematic editor.

Type an LCSC part number, hit Import, and the symbol, footprint, and 3D model are fetched and staged immediately. Symbol and footprint previews update live. Click **Add to Library** to permanently save the part into your local LCSC_Parts library.

![LCSC Import tab — symbol preview (Unit A) and 2D footprint](https://github.com/IATRT/kicad-custom/releases/download/kicad_custom_10.0.1_ubuntu26/Screenshot.From.2026-04-13.10-17-57.png)
*LCSC Import tab showing INA2143U (C1346558) — Unit A symbol preview with 2D footprint below*

![LCSC Import tab — Unit B and 3D footprint preview](https://github.com/IATRT/kicad-custom/releases/download/kicad_custom_10.0.1_ubuntu26/Screenshot.From.2026-04-13.10-18-13.png)
*Switching to Unit B and the 3D tab — SOIC-14 model renders live in the dialog*

Once added, the part is immediately searchable in the standard Library tab with full metadata:

![Part visible in Library tab after import — 2D view](https://github.com/IATRT/kicad-custom/releases/download/kicad_custom_10.0.1_ubuntu26/Screenshot.From.2026-04-13.10-18-51.png)
*Part appears in the Library tab under LCSC_Parts with symbol, 2D footprint, and full datasheet/manufacturer metadata*

![Part visible in Library tab after import — 3D view](https://github.com/IATRT/kicad-custom/releases/download/kicad_custom_10.0.1_ubuntu26/Screenshot.From.2026-04-13.10-19-00.png)
*3D footprint preview available directly in the Library tab after import*

**Under the hood:**
- Parts stage to `/tmp/kicad_lcsc_<pid>/` on import; your library is untouched until **Add to Library** is clicked
- S-expression-aware symbol merge on save (no duplicates, no silent overwrites)
- Footprint copy with 3D-model absolute-path rewrite
- Unit dropdown for multi-unit parts (dual op-amps etc.)
- 400 ms watchdog retries both previews if the first render missed (Wayland timing)

---

### Footprint Preview Zoom Fix

`fitToCurrentFootprint()` rewritten with `ToWorld/SetScale` + `CallAfter` deferred fit — fixes silent autozoom failure on hidden canvases under Wayland.

---

### 3D Model Preview Widget

`FOOTPRINT_3D_PREVIEW_WIDGET` embeds the KiCad 3D viewer into any dialog.

---

### Wayland / EGL Build

EGL-native GAL backend; no XWayland required.
System `libwxgtk3.2-dev` on Ubuntu 26.04 includes Wayland/EGL natively — no custom wxWidgets build needed.
See [`WAYLAND_BUILD_CHANGES.md`](WAYLAND_BUILD_CHANGES.md).

---

## License

KiCad is [GNU GPL v3](LICENSE). This fork inherits that license. All IATRT
additions are likewise GPLv3 in compliance with upstream terms.

The KiCad name and trademarks belong to the KiCad project. Use here is
purely descriptive and implies no official relationship.
