# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-10-25

### Added
- **Apple Magic Trackpad 3 USB-C (Late 2024 / M4) Support**:
  - Added support for Product ID `0x0324` across both USB-C wired and Bluetooth connections.
- **Apple Magic Trackpad 2 & Lightning Support**:
  - Support for Product IDs `0x0265`, `0x0320`, and `0x030E`.
- **Microsoft Windows Precision Touchpad (PTP) Integration**:
  - Full native Windows 10 and 11 multi-touch gesture support:
    - 2-finger smooth scrolling and pinch-to-zoom.
    - 3-finger swipe up for Task View / Multitasking.
    - 3-finger swipe left/right for application switching (Alt+Tab).
    - 4-finger swipe for Virtual Desktop switching.
  - Native gesture configuration in `Windows Settings ➔ Bluetooth & devices ➔ Touchpad`.
- **Automated Installer & Uninstaller Scripts**:
  - `Install-Driver.bat`: 1-click elevated driver installation using Windows `pnputil`.
  - `Uninstall-Driver.bat`: Dynamic driver detection and clean uninstallation from the Windows Driver Store.
- **Zero Background Footprint**:
  - Operates purely at the Windows driver level with 0% CPU and 0 MB RAM overhead.
