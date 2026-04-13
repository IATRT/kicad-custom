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

A **private, internal build** of KiCad 10.0 with IATRT-specific additions.
Not intended for public consumption. Not a PR. Not a proposal. Not a complaint.
Just a fork we use at work.

Upstream base: `gitlab.com/kicad/code/kicad` · branch `10.0`

---

## IATRT additions

### LCSC / EasyEDA Import Panel
New **LCSC Import** tab in the symbol chooser — import parts from LCSC/EasyEDA
without leaving the schematic editor.

- Parts stage to `/tmp/kicad_lcsc_<pid>/` on import; your library is untouched until **Add to Library** is clicked
- S-expression-aware symbol merge on save (no duplicates, no silent overwrites)
- Footprint copy with 3D-model absolute-path rewrite
- Symbol preview + unit dropdown for multi-unit parts
- Footprint 2D + 3D side-by-side preview
- 400 ms watchdog retries both previews if the first render missed (Wayland timing)

### Footprint Preview Zoom Fix
`fitToCurrentFootprint()` rewritten with `ToWorld/SetScale` + `CallAfter`
deferred fit — fixes silent autozoom failure on hidden canvases under Wayland.

### 3D Model Preview Widget
`FOOTPRINT_3D_PREVIEW_WIDGET` embeds the KiCad 3D viewer into any dialog.

### Wayland / EGL Build
EGL-native GAL backend; no XWayland required.
See [`WAYLAND_BUILD_CHANGES.md`](WAYLAND_BUILD_CHANGES.md).

---

## License

KiCad is [GNU GPL v3](LICENSE). This fork inherits that license. All IATRT
additions are likewise GPLv3 in compliance with upstream terms.

The KiCad name and trademarks belong to the KiCad project. Use here is
purely descriptive and implies no official relationship.

---

## Original KiCad documentation

For building, policies, and source documentation see the
[KiCad Developer Documentation](https://dev-docs.kicad.org) website.

You may also take a look into the [Wiki](https://gitlab.com/kicad/code/kicad/-/wikis/home),
the [contribution guide](https://dev-docs.kicad.org/en/contribute/).

For general information about KiCad and information about contributing to the documentation and
libraries, see our [Website](https://kicad.org/) and our [Forum](https://forum.kicad.info/).

## Build state

KiCad uses a host of CI resources.

GitLab CI pipeline status can be viewed for Linux and Windows builds of the latest commits.

## Release status
[![latest released version(s)](https://repology.org/badge/latest-versions/kicad.svg)](https://repology.org/project/kicad/versions)
[![Release status](https://repology.org/badge/tiny-repos/kicad.svg)](https://repology.org/metapackage/kicad/versions)

## Files
* [AUTHORS.txt](AUTHORS.txt) - The authors, contributors, document writers and translators list
* [CMakeLists.txt](CMakeLists.txt) - Main CMAKE build tool script
* [copyright.h](copyright.h) - A very short copy of the GNU General Public License to be included in new source files
* [Doxyfile](Doxyfile) - Doxygen config file for KiCad
* [INSTALL.txt](INSTALL.txt) - The release (binary) installation instructions
* [uncrustify.cfg](uncrustify.cfg) - Uncrustify config file for uncrustify sources formatting tool
* [_clang-format](_clang-format) - clang config file for clang-format sources formatting tool

## Subdirectories

* [3d-viewer](3d-viewer)         - Sourcecode of the 3D viewer
* [bitmap2component](bitmap2component)  - Sourcecode of the bitmap to PCB artwork converter
* [cmake](cmake)      - Modules for the CMAKE build tool
* [common](common)            - Sourcecode of the common library
* [cvpcb](cvpcb)             - Sourcecode of the CvPCB tool
* [demos](demos)             - Some demo examples
* [doxygen](doxygen)     - Configuration for generating pretty doxygen manual of the codebase
* [eeschema](eeschema)          - Sourcecode of the schematic editor
* [gerbview](gerbview)          - Sourcecode of the gerber viewer
* [include](include)           - Interfaces to the common library
* [kicad](kicad)             - Sourcecode of the project manager
* [libs](libs)           - Sourcecode of KiCad utilities (geometry and others)
* [pagelayout_editor](pagelayout_editor) - Sourcecode of the pagelayout editor
* [patches](patches)           - Collection of patches for external dependencies
* [pcbnew](pcbnew)           - Sourcecode of the printed circuit board editor
* [plugins](plugins)           - Sourcecode for the 3D viewer plugins
* [qa](qa)                - Unit testing framework for KiCad
* [resources](resources)         - Packaging resources such as bitmaps and operating system specific files
    - [bitmaps_png](resources/bitmaps_png)       - Menu and program icons
    - [project_template](resources/project_template)          - Project template
* [scripting](scripting)         - Python integration for KiCad
* [thirdparty](thirdparty)           - Sourcecode of external libraries used in KiCad but not written by the KiCad team
* [tools](tools)             - Helpers for developing, testing and building
* [translation](translation) - Translation data files (managed through [Weblate](https://hosted.weblate.org/projects/kicad/master-source/) for most languages)
* [utils](utils)             - Small utils for KiCad, e.g. IDF, STEP, and OGL tools and converters
