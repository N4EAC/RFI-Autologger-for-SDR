# RFI Autologger for SDR by N4EAC

**Version:** `1.0.0`  
**Platform:** Windows 10/11  
**Status:** Final Release

RFI Autologger for SDR by N4EAC is a field-oriented RF interference logging tool for SDR receivers. It is designed to help locate and document RF interference by receiving a signal, measuring tuned-channel signal level in dBFS, recording GPS position, and exporting logs to CSV and Google Earth KML.

The interface is intentionally simple and instrument-like: frequency, mode, signal value, GPS status, logging status, gain controls, and SDR selection.

---

## Release Notes for v1.0.0

This first final release focuses on reliable field logging with HackRF and RTL-SDR, plus functional beta support for SDRplay. The UI has been simplified for readability, with KML export, editable color thresholds, optional signal labels, and tuned-channel pre-demod IQ dBFS measurements for better RF mapping.

## Supported SDR Receivers

### Stable
- **HackRF One**
- **RTL-SDR** compatible dongles

### Beta
- **SDRplay** receivers using the official SDRplay API

SDRplay support is functional but still marked beta. For SDRplay, connect the receiver before launching the application. Hot-plug detection is a known limitation.

---

## Main Features

- SDR receiver selection: HackRF, RTL-SDR, SDRplay
- Modes: AM, NFM, WFM, USB, LSB
- Live audio monitor
- Frequency entry with Enter-to-tune
- Tuning step buttons
- LNA/VGA gain controls
- AMP and ATT -10 dB controls
- GPS serial connection support
- CSV logging with GPS, frequency, mode, signal, and gain data
- KML export for Google Earth
- Optional KML signal text labels for cleaner map display
- Editable KML color thresholds based on `Signal_dBFS`
- Tuned-channel pre-demod IQ dBFS measurement for better RF mapping
- Retro CDE-inspired purple/beige field UI
- Simplified, readable panel layout
- Clean shutdown when closing with the Windows X button

---

## Recommended First Tests

Before field use, test each receiver with a known local signal.

### NOAA Weather Radio
Use NFM mode:

```text
162.400 MHz
162.425 MHz
162.450 MHz
162.475 MHz
162.500 MHz
162.525 MHz
162.550 MHz
```

### FM Broadcast
Use WFM mode with a strong local FM station, for example:

```text
94.700000 MHz
100.100000 MHz
```

---

## Recommended Baseline Gain Settings

For comparable RFI maps, keep gain settings fixed during each survey.

### HackRF
```text
LNA: 16 dB
VGA: 16 dB
AMP: OFF
ATT: OFF
```

### RTL-SDR
```text
Gain: around 20–30 dB
ATT: OFF
```

### SDRplay
```text
LNA: 15
VGA: 0
ATT: OFF
```

Use ATT only when a very strong signal appears to overload the receiver or compress the signal range.

---

## Logging

CSV logging records values such as:

- UTC timestamp
- Latitude
- Longitude
- Frequency
- Mode
- Signal_dBFS
- SDR type
- Gain values
- ATT state

The signal value is based on tuned-channel pre-demod IQ dBFS so it is more useful for RF mapping than post-demod audio level.

---

## KML Export

KML export creates color-coded map points for Google Earth using `Signal_dBFS`.

Default recommended thresholds after testing:

```text
Green   < -60 dBFS
Yellow  -60 to -50 dBFS
Orange  -50 to -40 dBFS
Red     > -40 dBFS
```

Thresholds are editable in the application before exporting KML.

KML placemarks are intentionally compact. The pin color shows signal category and the placemark includes practical values such as frequency, mode, timestamp, and dBFS.

---

## Known Limitations

- SDRplay is beta.
- SDRplay must be connected before launching the app.
- SDRplay hot-plug / refresh recovery is not reliable yet.
- dBFS is not dBm. It is useful for relative RF mapping but depends on SDR type and gain settings.
- For best RFI survey results, do not change LNA/VGA/AMP/ATT during a logging run.

---

## Build Instructions

From the source folder on Windows:

```bat
run_dev.bat
```

To build a standalone EXE:

```bat
build_exe.bat
```

The generated executable name is:

```text
RFI_Autologger_for_SDR_by_N4EAC_v1.0.0-rc2a.exe
```

---

## Dependencies

Python packages are listed in `requirements.txt`.

Runtime SDR dependencies included or expected:

- HackRF: `hackrf.dll`, `libusb-1.0.dll`, `pthreadVC2.dll`
- RTL-SDR: `rtlsdr.dll`, `libusb-1.0.dll`
- SDRplay: install the official SDRplay API for Windows. The app prefers the official installed API and does not rely on a bundled SDRplay DLL.

---

## Project Purpose

This tool is not intended to replace a full SDR program such as SDR++, SDR#, or SDRuno. Its purpose is narrower:

```text
Receive → Listen → Measure → GPS Log → Map
```

The goal is practical RF interference hunting in the field.

---

## Credits

Created through iterative testing and development with N4EAC.



## v1.0.0-rc2 UI refinement

RC2 is a cosmetic/layout release candidate intended to reduce visual clutter and UI refresh work while keeping the SDR/audio/GPS/KML logic from RC1a intact.

Changes:

- Removed duplicate GPS and SDR status text from the top-right corner.
- Removed the bottom status line.
- Renamed the display area to **Receiver Panel**.
- Removed LNA/VGA values from the receiver panel and moved them next to their sliders.
- Renamed **RF Gain** to **LNA**.
- Removed slider range labels.
- Frequency entry tunes with **Enter**; the Tune button was removed.
- PPM correction applies with **Enter**; the Apply button was removed.
- GPS controls moved to **Settings > GPS Settings**.
- Connect/Refresh SDR moved below the mode buttons.
- Start/Stop Logging and Save KML moved into the Logging Status panel.
- ATT -10 dB and AMP positions swapped.
- GPS coordinates/time remain visible in the Receiver Panel.

Known limitation: SDRplay should be connected before launching the app; SDRplay hot-plug is not yet reliable.


## v1.0.0 UI update

- Reworked the UI to fit 1280x720-class screens without a scrollbar.
- Panels now use a two-column adaptive layout and expand on larger displays.
- Reversed the CDE-inspired colors: purple background with beige foreground.
- No SDR, DSP, audio, GPS, CSV, or KML logic changes.


## v1.0.0 UI refinement

- Kept the RC5 two-column layout for 1280x720-class screens.
- Changed only the Receiver Panel dot-matrix display to a dark recessed instrument-style background.
- Kept the CDE-inspired purple/beige application shell.
- No SDR, DSP, audio, GPS, logging, or KML logic changes.


## v1.0.0 UI fit refinement
- Compact Receiver Panel display to reduce wasted space.
- Equalized the two main UI columns so controls remain visible on 1280x720-class screens.
- Reduced receiver dot-matrix panel height and spacing.
- Kept the dark recessed receiver display and purple/beige CDE-style theme.
- No SDR/DSP/audio/GPS/KML logic changes.


## v1.0.0 layout refinement

- Reworked the Mode / SDR section so all mode buttons remain visible on 1280x720-class displays.
- Moved Mode / SDR below the frequency controls.
- Arranged mode buttons in a compact two-row grid.
- Increased the minimum window width/height to prevent controls from disappearing off the edge.
- No SDR, DSP, audio, GPS, logging, or KML logic changes.


## v1.0.0 UI refinement

- Improved 1280x720 layout consistency.
- Removed CW-U and CW-L mode buttons from the main UI for RFI-hunting focus.
- Moved PPM from the Receiver Panel into SDR Controls; pressing ENTER applies it.
- Widened the frequency entry and clarified ENTER-to-tune behavior.
- Reduced Receiver Panel display height and tightened dot-matrix spacing.
- Renamed KML threshold labels to full color names: Green, Yellow, Orange.
- Renamed KML label option to “Show signal labels”.
- No SDR/DSP/audio/GPS/KML logic changes.


## v1.0.0 layout refinement

- Reduced the minimum window height to avoid the unused lower-half blank area.
- Compact Receiver Panel dot-matrix display.
- Preserved RC8/RC9 two-column control layout with all mode buttons visible at 1280x720-class screens.
- No SDR, DSP, audio, GPS, logging, or KML logic changes.


## v1.0.0 UI layout correction

- Reworked the minimum/default window geometry to reduce empty lower-window space.
- Darkened the CDE purple background to a less pink shade.
- Cleaned up the Receiver Panel dot-matrix rows to avoid pixel overlap.
- Removed the remaining PPM `ENTER applies` helper text.
- No SDR, DSP, audio, GPS, CSV, or KML logic changes.


## v1.0.0 UI cleanup

- Replaced the dot-matrix receiver display with simple, readable instrument-style labels.
- Improved panel spacing and removed cramped receiver text overlap.
- Kept the purple/beige CDE-inspired theme with a dark receiver display area.
- No SDR, DSP, GPS, logging, or KML logic changes.
