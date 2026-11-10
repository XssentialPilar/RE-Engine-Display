# RE Engine Display Fix

### A better fit for the Resident Evil experience.

**RE Engine Display Fix** is a display and interface adaptation project for **Resident Evil 7: Biohazard**, **Resident Evil 2 Remake**, and **Resident Evil 3 Remake**. Its goal is simple: make the image, menus, cinematics, and on-screen information feel properly proportioned on different displays—without compromising the game's original presentation.

**Current development preview:** `3.0.0-preview.7`  
**Tested game:** Resident Evil 7  
**Resident Evil 2 and 3 Remakes:** Not yet verified

> **Development preview:** The latest RE7 candidate has been tested and accepted for its visible improvements, with minor corrections still planned. It is **not** the final 3.0.0 release.

## See the difference

<img width="4000" height="6066" alt="REDisplay_3 0 0-preview 7_RE7_Gallery_20261110_001549" src="https://github.com/user-attachments/assets/3463d464-f863-424d-84c2-c10fd0b48213" />



*Resident Evil 7 in-game captures (1920 × 1200, 16:10). The gallery highlights improvements to cinematic framing, subtitles, menus, inventory, map and HUD placement. Images show one tested output, not proof of compatibility with every display.*

## What makes it different?

### An image that keeps its shape

Screen changes should never leave characters, environments, or interface elements looking stretched. RE Engine Display Fix improves how the game adapts its presentation to the selected output while respecting its native camera behavior.

### Menus that belong on your screen

Pause, Options and other everyday interfaces receive proportional sizing and more consistent placement. Backgrounds can fill the screen without forcing the controls, labels or buttons to stretch with them.

### A more consistent HUD and inventory

Inventory slots, item icons, selection elements, maps, objectives, interaction prompts and bottom guides are brought into a more coherent screen layout. Earlier builds could display these elements flattened, clipped or separated from their intended positions; this preview substantially improves those results in RE7.

### Cinematics that preserve their presentation

Video framing and subtitle proportions have been improved, with proportional presentation retained through the project's video policy. Some scenes may crop at the edges or show unused space depending on the chosen framing mode; the video itself is not intentionally stretched.

### Your game, your settings

Display and interface corrections can be enabled or disabled. Optional manual FOV control is available separately, while automatic correction avoids rewriting the native camera projection.

## Game compatibility

| Game | Current status |
| --- | --- |
| **Resident Evil 7: Biohazard** | **Preview tested and accepted**; minor issues may remain |
| **Resident Evil 2 Remake** | Targeted, but **not tested or verified** |
| **Resident Evil 3 Remake** | Targeted, but **not tested or verified** |

RE7 is the current testing and development focus. Similar engine technology does **not** guarantee that the same corrections work safely in RE2 or RE3. Their compatibility will be announced only after dedicated runtime testing.

## Installation — Resident Evil 7

1. Close Resident Evil 7.
2. Download the current **RE Engine Display Fix** preview ZIP from this repository's **Releases** section.
3. Extract the ZIP's **`reframework`** **`dinput8`** folder and file into the game's installation directory, alongside **`re7.exe`**. If upgrading, preserve your existing **`reframework/data/REDisplay.ini`** to retain settings.
4. Launch RE7 and open the plugin panel using **`;`** or the REFramework interface. Confirm **`3.0.0-preview.7`** appears.
5. Make sure you have enabled **Display Correction**, **Adaptive Interface** and **Full-Screen Backgrounds**. For the initial comparison, leave **Manual FOV Override** disabled and turn off REFramework's separate ultrawide correction to avoid conflicting adjustments.

No game executable, save file or DirectX runtime needs to be replaced by this installer.

## What is still being worked on?

- Further refinement of inventory interactions, overlays, loading sequences and less common menus.
- Dedicated support verification for Resident Evil 2 and Resident Evil 3 Remakes.
- Ongoing adjustments based on reproducible community reports.

## Feedback and issue reports

If something looks wrong, please open a GitHub Issue and include:

- Game and game version/build, if known.
- Screen resolution, aspect ratio and display mode (windowed, borderless or fullscreen).
- A screenshot or short video of the affected menu, HUD element or scene.
- Whether other display or ultrawide fixes were enabled.

Precise reports make it easier to reproduce problems and improve the next preview. **Thank you for helping make RE Engine Display Fix better.**

## Project notes and credits

RE Engine Display Fix is a separate adaptation project, developed from **RE8Display 2.7.0** with attribution recorded in **LICENSE**. It uses the separately installed **REFramework** host and retains attribution for its vendored API headers.

The project does not bundle copyrighted game artwork, modified game executables, or REFramework itself. Resident Evil and RE Engine belong to their respective owners. This is an independent, unofficial community project and is not affiliated with or endorsed by Capcom.
