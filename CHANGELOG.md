# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-10-25

### Added
- **Apple Magic Trackpad 3 USB-C (Late 2024 / M4) Support**:
  - Added support for Product ID `0x0324` across both USB wired and Bluetooth links.
- **Apple Magic Trackpad 2 & Lightning Support**:
  - Support for Product IDs `0x0265`, `0x0320`, and `0x030E`.
- **Dual Operating Modes**:
  - Official Microsoft WHQL-signed Windows Precision Touchpad (PTP) driver (`AmtPtpDevice.inf`) with automated installer script `Install-Driver.bat`.
  - Self-contained, portable C# .NET 8 user-mode daemon (`MagicTrackpadDriver.exe`).
- **Precision Gesture Engine**:
  - 1-finger relative cursor movement with custom velocity/acceleration curve.
  - 2-finger parallel vertical & horizontal scrolling with inertia/momentum decay.
  - 1-finger quick tap-to-click detection (< 220ms temporal threshold).
  - Configurable natural (macOS-style) vs standard Windows scrolling direction.
- **Modern System Tray Interface**:
  - Dark-mode responsive Settings window.
  - Interactive sensitivity slider, tap-to-click toggle, and natural scrolling switch.
  - Auto-start with Windows toggle utilizing CurrentUser Run key.
  - Tray status indicator and safe exit hook.
- **Automated Reconnection & Resilience**:
  - Background device scanner with automatic reconnection on Bluetooth sleep or power cycle.
  - Robust HID multi-touch endpoint resolution, preventing conflicts with Windows `mouhid.sys`.
