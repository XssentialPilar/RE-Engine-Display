# RE Engine Display Fix — 3.0.0 development

A separate display adaptation project targeting **Resident Evil 7**, **Resident Evil 2 Remake**, and **Resident Evil 3 Remake**. RE7 is the runtime test target. RE2 and RE3 remain unverified.

## Current candidate

`3.0.0-preview.7` is an **RE7 screen and interface correction candidate**. It is not a completed release. Previews 4 and 5 failed the user's multi-resolution test and must not be treated as stable.

- **Native camera protection.** Automatic mode performs no camera writes. Direct camera aspect and projection-axis overrides have been removed; changing a 4:3 or 16:9 camera to the monitor's 16:10 aspect at render boundaries was an unsafe mismatch with the engine's projection and temporal data. Manual FOV remains an explicit horizontal-angle setting; leave it off during regression testing. Render-target sizes, lighting, shadows and shaders are not modified.
- **Independent presentation target.** Preview 5 selected the aspect from a scene surface that its own display setting had changed. That feedback could keep a 1920×1200 output letterboxed at 1920×1080. Preview 6 selects the native display preset from the actual DXGI output buffer, with the native window as a fallback. The monitor's desktop resolution is not used as a substitute. Exact supported ratios use native proportional presets; other ratios use native Fit and remain unverified in game. Scene size and the present rectangle are observations, never inputs that can shrink the presentation target.
- **Shared coordinates for screen interfaces.** Ordinary menu, HUD and inventory views use a uniform virtual canvas based on the observed presentation rectangle. One root resolution transform supplies the same uniform scale to drawing and native coordinate conversion, including lower resolutions. Nested stretch adjustments are neutralized. Settled conversion measurements validate the result without feeding stale conversion caches back into the layout.
- **Independent placement and backgrounds.** Inventory grid, item icons, drag imagery and selection use the same right/top basis, including the previously omitted icon container. Objectives and autosave use the actual top/left canvas; ammunition and guides use their own edge anchors. Solid footer bands can fill the width independently of their controls. Full-screen solid/blur layers fill the output; textured menu backgrounds cover it with uniform scaling and centered cropping. Background expansion does not resize sibling text, icons or buttons.
- **Native loading activity.** This candidate no longer vetoes the loading indicator draw callback. The indicator is promoted to an overlay while the captured chapter artwork is visible. Loading progress and save state remain game-owned; actual loading and cinematic transitions require the next runtime check.
- **Proportional videos.** The preview 2 video policy is retained: cover by default, optional contain framing, and decoded dimensions when an attached native movie component exposes them. Cover can crop edges; contain can leave bars. Neither mode stretches the picture.
- **Native input and specialized views.** The mouse canvas, world-space tape-recorder menu and wrist-monitor render-to-texture canvas retain their specialized native behavior. Ordinary 2D corrections must not be applied to offscreen or world-space displays.
- **Reversible settings.** Changed-only property setters, ownership-based restoration, reset defaults, actual DX11/DX12 backbuffer detection and debounced configuration persistence remain available.
- **Animation-safe placement.** Ownership is tracked separately for each position and size component. A native animation that changes one axis can no longer capture an already shifted second axis as a new baseline and repeatedly accumulate its offset. Disabling the correction restores owned components while retaining independent native animation changes.

The user confirmed improved video framing and subtitle proportions in preview 2. Later previews still failed inventory alignment and resolution changes. Preview 6 addresses two reproducible code defects: presentation feedback and accumulated placement offsets. Complete inventory alignment, loading visibility, video transitions and arbitrary-ratio behavior still require runtime acceptance. Mathematical checks do not establish universal game compatibility. Generated replacement artwork is not bundled or installed.

During a separate test with both REFramework and REDisplay disabled, the user found that the lighting defect persists when RE7 ray tracing is disabled. This candidate focuses on display geometry; it does not claim to repair that native rendering issue. Keep graphics settings unchanged during the screen comparison.

## Install and test in RE7

Requires an existing compatible REFramework host with plugin API 1.15 or later. The loader is not bundled or replaced.

1. Close RE7 normally. Extract the ZIP's `reframework` folder into the directory containing `re7.exe`. When upgrading, keep your existing `reframework/data/REDisplay.ini` if you wish to retain settings. The source project's `tools/REDisplay.Install.ps1 -GamePath <game directory> -KeepSettings` also preserves exact prior files in a timestamped backup.
2. Open RE7 and confirm **3.0.0-preview.7** in the plugin panel, opened with `;` or through REFramework.
3. Enable display correction, adaptive interface and full-screen backgrounds. Leave FOV override off for the comparison. Keep REFramework's separate ultrawide correction off to avoid competing layout policies.
4. Check inventory grid boundaries, item movement, pointer alignment and click targets; ammunition, interaction and autosave icons; pause, load/save and Options backgrounds; and the bottom help guide.
5. Load a save to check the native loading indicator, then play an introductory video and compare subtitles. Test your available windowed, borderless and fullscreen output modes and more than one aspect ratio.
6. Close the game normally when finished. With diagnostics enabled, the log distinguishes the independent presentation target from the native game surface, and records preset changes, present rectangles, GUI conversions and settled transform metrics. These are diagnostic observations, not a claim that a screenshot passed visual inspection.

The installer does not alter executable files, saves, REFramework settings, DirectX runtimes or RE8 modules. Keep the previous candidate until the new behavior has been checked.

## Build and package

From the full source project: Windows x64, Visual Studio C++ tools, Windows SDK and CMake:

```powershell
powershell -ExecutionPolicy Bypass -File tools/REDisplay.Build.ps1
powershell -ExecutionPolicy Bypass -File tools/REDisplay.Package.ps1
```

The scripts default to Visual Studio 2026; pass `-Generator 'Visual Studio 17 2022'` if needed. Sources, configuration, tools and verification evidence are separated under `native/`, `config/`, `tools/`, `tests/`, `docs/` and `artifacts/`; distributable ZIPs are under `dist/`. The package script checks build and source hashes before packaging.

The source derives from RE8Display 2.7.0 with attribution in LICENSE. Vendored REFramework API headers retain their upstream attribution. No game artwork or Microsoft preview runtime is bundled. Agility, DirectStorage, water changes, fog and enemy culling are outside this adaptation candidate.
