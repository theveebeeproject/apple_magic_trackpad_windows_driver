# Apple Magic Trackpad Windows Driver & Daemon 🖱️✨

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![.NET 8.0](https://img.shields.io/badge/.NET-8.0-512BD4.svg?logo=dotnet)](https://dotnet.microsoft.com/)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011%20(x64)-0078D6.svg?logo=windows)](https://www.microsoft.com/windows)
[![Precision Touchpad](https://img.shields.io/badge/Windows-Precision%20Touchpad-brightgreen.svg)](https://learn.microsoft.com/windows-hardware/design/component-guidelines/touchpad-tuning-guidelines)
[![Release](https://img.shields.io/badge/Release-v1.0.0-orange.svg)](https://github.com/)

A high-performance, native Windows 10 & 11 driver and background system tray daemon for **Apple Magic Trackpad 2 and Magic Trackpad 3 (USB-C & Lightning)**. Completely free and open-source alternative to commercial subscriptions like Magic Utilities.

---

## 🌟 Key Highlights

- **Dual-Mode Operation**:
  1. **Official Windows Precision Touchpad (PTP) Integration**: Full Microsoft-compatible precision touchpad support allowing native Windows 11 gesture controls (3-finger & 4-finger gestures, virtual desktops, multitasking, smooth fluid pinch-to-zoom).
  2. **Custom User-Mode Tray Daemon (`MagicTrackpadDriver.exe`)**: High-performance, low-latency background daemon with a modern dark-mode Settings GUI.
- **Both Bluetooth & USB-C Supported**: Works seamlessly over wireless Bluetooth or plugged in via USB Type-C / Lightning cable.
- **Fluid Two-Finger Scrolling**: Pixel-smooth displacement with configurable natural (reverse) scrolling and momentum/inertia decay.
- **Ultra-Responsive Tap-to-Click**: Microsecond single-finger touch detection with temporal threshold filtering.
- **Configurable Sensitivity & Velocity Curve**: Tailor cursor acceleration to match macOS feel or standard Windows dynamics.
- **Automatic Device Reconnection**: Background polling and hot-plug detection seamlessly handle power cycles and Bluetooth re-connections.
- **Zero Kernel Hacks Required**: User-mode daemon uses raw HID input streams; optional kernel driver is fully WHQL-compatible with Microsoft Windows Hardware Compatibility Publisher signatures.

---

## 💻 Supported Hardware Matrix

| Model | Connection | Vendor ID (VID) | Product ID (PID) | Support Status |
| :--- | :--- | :--- | :--- | :--- |
| **Apple Magic Trackpad 3 (USB-C, Late 2024 / M4)** | USB-C & Bluetooth | `0x05AC` / `0x004C` | `0x0324` |  Tested & Working |
| **Apple Magic Trackpad 3 (Lightning)** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x0265` |  Tested & Working |
| **Apple Magic Trackpad 2** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x0320` |  Tested & Working |
| **Apple Magic Trackpad 2 (Older rev)** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x030E` |  Tested & Working |

---

## 🚀 Quick Start / 1-Click Driver Installation

You can download the ready-to-run driver package directly from the **[Releases](../../releases)** tab (`Apple-Magic-Trackpad-Precision-Driver-v1.0.0.zip` — **~250 KB**).

1. Download and extract **`Apple-Magic-Trackpad-Precision-Driver-v1.0.0.zip`**.
2. Right-click **`Install-Driver.bat`** and select **Run as administrator**.
3. Windows will instantly register the device as an official **Windows Precision Touchpad**.
4. Test and configure your gestures directly in Windows Settings:
   - Go to `Settings` ➔ `Bluetooth & devices` ➔ `Touchpad`.
   - Customize 2-finger scroll direction, pinch to zoom, 3-finger swipe (Switch apps / Task View), 4-finger swipe (Virtual desktops), and tap-to-click.

> **Zero Background Software Required:** Unlike commercial tools, you do not need any `.exe` or daemon running in the background. Windows natively manages your trackpad at the OS kernel level.
>
> **To Uninstall Driver:** Simply right-click `Uninstall-Driver.bat` and select **Run as administrator**.

---

## 💡 Why the Driver Solution is Superior to an .EXE

When you install the Precision Touchpad driver (`AmtPtpDevice.inf`), Windows assigns its own native touch pipeline directly to the trackpad:
- **No Background Process**: 0% CPU and 0 MB RAM usage.
- **Native OS Gestures**: Windows 11 handles fluid pinch-to-zoom, virtual desktop transitions, and swipe gestures natively with hardware acceleration.
- **No Conflict**: A user-mode `.exe` cannot hook the raw touch stream once the kernel driver claims the device, making an `.exe` redundant. The C# daemon code is preserved in `MagicTrackpadDriver/` for developers interested in userspace HID parsing.

---

## ⚙️ Settings UI & Features

The user-mode daemon includes a modern dark-mode configuration interface:

| Setting | Description |
| :--- | :--- |
| **Natural Scrolling** | Matches macOS natural scroll direction (swipe up to move content up, swipe down to move content down). Toggle off for standard Windows scroll direction. |
| **Cursor Sensitivity** | Adjustable velocity multiplier (0.5x to 3.0x) paired with an exponential acceleration curve for precise micro-movements and rapid screen traversals. |
| **Tap to Click** | Enables instant single-finger tap-to-click (< 220ms contact threshold) without needing physical button depress. |
| **Start with Windows** | Automatically launches the daemon at Windows startup via the user registry Run key. |

---

## 🛠️ Architecture Overview

```
 ┌─────────────────────────────────────────────────────────┐
 │             Apple Magic Trackpad (Hardware)             │
 └────────────────────────────┬────────────────────────────┘
                              │ Bluetooth / USB-C
                              ▼
        ┌─────────────────────────────────────────┐
        │       Multi-Touch HID Raw Stream        │
        └───────┬─────────────────────────┬───────┘
                │                         │
     [Direct Userspace]         [Precision Driver]
                │                         │
                ▼                         ▼
   ┌─────────────────────────┐   ┌─────────────────────────┐
   │ MagicTrackpadDriver.exe │   │    AmtPtpDevice.inf     │
   │  (C# .NET 8 Daemon)     │   │   (WHQL-Signed Driver)  │
   │                         │   │                         │
   │ • TouchPoint Parser     │   │ • Native Windows PTP    │
   │ • Velocity Curve        │   │ • 3/4-Finger Gestures   │
   │ • Momentum Scroll Engine│   │ • Virtual Desktops      │
   │ • Modern Dark WinForms  │   │ • Windows Settings App  │
   └────────────┬────────────┘   └────────────┬────────────┘
                │                             │
                ▼                             ▼
   ┌───────────────────────────────────────────────────────┐
   │               Windows OS Desktop & Apps               │
   └───────────────────────────────────────────────────────┘
```

---

## 🏗️ Building from Source

### Prerequisites
- Windows 10 or 11 (64-bit)
- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) or Visual Studio 2022 (v17.8+)

### Build Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/apple-magic-trackpad-windows.git
   cd apple-magic-trackpad-windows
   ```

2. Restore and publish the self-contained single-file executable:
   ```powershell
   dotnet publish MagicTrackpadDriver\MagicTrackpadDriver.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true
   ```

3. The compiled binary will be located at:
   `MagicTrackpadDriver\bin\Release\net8.0-windows10.0.19041.0\win-x64\publish\MagicTrackpadDriver.exe`

---

## ❓ Troubleshooting

<details>
<summary><b>1. The trackpad connects via Bluetooth but gestures do not respond</b></summary>

- Go to **Windows Settings ➔ Bluetooth & devices ➔ Devices**.
- Find your **Apple Magic Trackpad**, click **Remove device**.
- Power cycle the trackpad (slide the power toggle OFF for 3 seconds, then back ON).
- Re-pair the trackpad via Bluetooth.
- Run `Install-Driver.bat` as administrator.
</details>

<details>
<summary><b>2. SmartScreen or Antivirus flag</b></summary>

- `MagicTrackpadDriver.exe` is built with .NET 8 Single-File publish and accesses low-level HID endpoints (`HidSharp` / Win32 `SendInput`).
- If Windows Defender SmartScreen warns about an unknown publisher on first run, click **More info** ➔ **Run anyway**.
- The full source code is included in this repository for full auditability.
</details>

<details>
<summary><b>3. How to verify driver installation</b></summary>

- Open **Device Manager** (`devmgmt.msc`).
- Expand **Human Interface Devices**.
- Look for **Apple Magic Trackpad (Precision Touchpad)**.
- If present, open Windows Settings ➔ **Touchpad** to test 3-finger and 4-finger gestures.
</details>

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues).

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for more information.

---

## 🙏 Acknowledgments

- Microsoft Windows Precision Touchpad specification and community driver pioneers.
- [HidSharp](https://www.nuget.org/packages/HidSharp) for cross-platform low-level HID communication.
