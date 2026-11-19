# DevilutionX – Nintendo Switch 2

Experimental Nintendo Switch 2 build of [DevilutionX](https://github.com/diasurgical/devilutionX), the open-source engine for Diablo and Diablo: Hellfire.

This unofficial build was successfully compiled using ounce-devkit and libounce and tested on real Nintendo Switch 2 hardware through kaiHEN.

## Download

[Download the experimental Nintendo Switch 2 build](https://github.com/Cerebral-Context/DevilutionX/releases/tag/Switch-2-port)

## Current status

- Successfully compiled into a native `.nro`.
- Successfully launched on Nintendo Switch 2.
- Diablo gameplay confirmed working.
- Audio, controller functionality, saving, and Hellfire expansion require additional compatibility testing.

## Installation

1. Download `devilutionx.nro` from the Releases page.
2. Create `/switch/` on your SD card.
3. Copy the `.nro` into that directory.
4. Copy `DIABDAT.MPQ` from your legally obtained Diablo installation into same folder.
5. For Hellfire, also copy `hellfire.mpq`, `hfmonk.mpq`, `hfmusic.mpq`, and `hfvoice.mpq` into same folder.
6. Launch DevilutionX through the kaiHEN homebrew menu.

Your SD card should look like this:

```text
switch/
    ├── devilutionx.nro
    ├── DIABDAT.MPQ
    ├── hellfire.mpq
    ├── hfmonk.mpq
    ├── hfmusic.mpq
    └── hfvoice.mpq
```

Game data is not included.

## Building from source

The initial successful build used DevilutionX source revision `29a062c9c` and the official libounce Switch 2 CMake toolchain.

With the ounce-devkit Docker image already available, configure the source directory using:

```bash
sudo docker run --rm \
  -v "$PWD:/workspace" \
  -w /workspace \
  ounce-devkit:latest \
  sh -c '
    export DEVKITPRO=/opt/devkitpro
    . /opt/devkitpro/switch2vars.sh
    git config --global --add safe.directory /workspace
    cmake -S . -B build-switch2 \
      -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_TOOLCHAIN_FILE=/opt/devkitpro/libounce/cmake/Switch2.cmake
  '
```

Then compile:

```bash
sudo docker run --rm \
  -v "$PWD:/workspace" \
  -w /workspace \
  ounce-devkit:latest \
  sh -c '
    export DEVKITPRO=/opt/devkitpro
    . /opt/devkitpro/switch2vars.sh
    cmake --build build-switch2 -j4
  '
```

The resulting file is `build-switch2/devilutionx.nro`.

## Credits

Special thanks to:

- [DevilutionX](https://github.com/diasurgical/devilutionX) and all contributors for the original game engine.
- Original Devilution contributors for foundational reverse-engineering work.
- devkitPro developers for the development toolchain.
- libounce contributors for Switch 2 compatibility and toolchain support.
- kaiHEN contributors for the Switch 2 homebrew environment.
- SDL contributors for multimedia functionality.

The Switch 2 build was compiled and tested on real hardware with AI-assisted build instructions and troubleshooting.

## Disclaimer

This is an unofficial experimental community build and is not an official DevilutionX release.

Diablo and Hellfire are copyrighted games. No commercial game assets are included.

The original project's license and copyright notices remain applicable.
