# sk83 Recomp Project

Experimental ReXGlue recompilation project for Skate 3.

This repository intentionally does not include any game files, extracted assets, generated recompilation output, or binaries. Users must provide their own legally obtained copy of the game and generate/build locally.

## What Is In This Repo

- ReXGlue project files
- Build configuration
- Handwritten host entry code
- Recompilation configuration metadata

## What Is Not In This Repo

- `default.xex`
- Extracted `data/` assets
- Movies, audio, `.big` archives, or other game content
- Generated C++ output under `generated/`
- Built executables
- Crash dumps or logs

## Local Asset Layout

After extracting your own copy of the game, place files like this:

```text
assets/
  default.xex
  data/
    audio/
    big/
    content/
    fe/
    movies/
    webkit/
```

The executable expects `assets` at the project root.

## Requirements

- Windows x64
- CMake 3.25+
- Ninja
- LLVM/Clang
- ReXGlue SDK checkout from the `sk83-support` branch of this fork:
  `https://github.com/chasmlol/rexglue-sdk`
- A legally obtained Skate 3 Xbox 360 game dump/ISO
- An Xbox 360 ISO extractor, such as `extract-xiso`

## Build

Clone this repo and the patched ReXGlue SDK branch:

```powershell
git clone https://github.com/chasmlol/rexglue-sdk C:/rexglue-sdk
cd C:/rexglue-sdk
git checkout sk83-support
```

Then configure this project with `REXSDK_DIR` pointing at that SDK checkout:

```powershell
cd C:/path/to/sk83-recomp
cmake --preset win-amd64-debug -DREXSDK_DIR=C:/rexglue-sdk
```

Place your extracted game files in `assets/`, then generate the recompilation output:

```powershell
cmake --build --preset win-amd64-debug --target sk83_codegen
```

Build the executable:

```powershell
cmake --build --preset win-amd64-debug
```

Run:

```powershell
.\out\build\win-amd64-debug\sk83.exe
```

## Troubleshooting

If codegen reports hundreds of function errors, make sure you are using the `sk83-support` ReXGlue SDK branch above, then delete local `generated/` and `out/` folders and run the configure/codegen/build steps again.

## Current Status

This is not a finished PC port. It currently reaches in-game execution on the local test setup, but crashes are still being fixed as more indirect-call/function-boundary cases are discovered.

## Legal

Do not upload or redistribute game files, generated code derived from game binaries, or built packages containing copyrighted game content. This project is intended for local research and development using files from a copy of the game you own.
