# Apple Magic Trackpad Windows Precision Touchpad Driver 🖱️✨

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011%20(x64)-0078D6.svg?logo=windows)](https://www.microsoft.com/windows)
[![Precision Touchpad](https://img.shields.io/badge/Windows-Precision%20Touchpad-brightgreen.svg)](https://learn.microsoft.com/windows-hardware/design/component-guidelines/touchpad-tuning-guidelines)
[![Release](https://img.shields.io/badge/Release-v1.0.0-orange.svg)](https://github.com/)

An official **Microsoft Windows Precision Touchpad (PTP)** driver for **Apple Magic Trackpad 2 and Magic Trackpad 3 (USB-C & Lightning)**. Completely free and open-source alternative to commercial subscription software like Magic Utilities.

---

## 🌟 Key Highlights

- **100% Native Windows Precision Touchpad (PTP)**: Turns your Apple Magic Trackpad into a native Windows Precision Touchpad.
- **Zero Background Software**: Runs entirely at the kernel driver level. **0% CPU and 0 MB RAM overhead**—no system tray utilities or third-party background daemons needed.
- **Full Windows 11 & 10 Gestures**:
  - **2-Finger**: Fluid pixel-accurate scrolling & smooth pinch-to-zoom.
  - **3-Finger Swipe Up**: Task View / Multitasking view.
  - **3-Finger Swipe Left / Right**: Switch between running applications (Alt+Tab).
  - **3-Finger Tap**: Windows Search / Cortana / middle-click.
  - **4-Finger Swipe Left / Right**: Switch between Virtual Desktops.
- **Both Bluetooth & USB-C Supported**: Works seamlessly over wireless Bluetooth or plugged in via USB Type-C or Lightning cable.
- **Native Windows Settings Integration**: Configure scroll direction (natural vs standard), cursor speed, and gestures directly inside `Windows Settings ➔ Bluetooth & devices ➔ Touchpad`.
- **Microsoft WHQL Compatible**: Signed driver package installable via standard Windows Driver Management.

---

## 💻 Supported Hardware Matrix

| Model | Connection | Vendor ID (VID) | Product ID (PID) | Support Status |
| :--- | :--- | :--- | :--- | :--- |
| **Apple Magic Trackpad 3 (USB-C, Late 2024 / M4)** | USB-C & Bluetooth | `0x05AC` / `0x004C` | `0x0324` |  Tested & Working |
| **Apple Magic Trackpad 3 (Lightning)** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x0265` |  Tested & Working |
| **Apple Magic Trackpad 2** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x0320` |  Tested & Working |
| **Apple Magic Trackpad 2 (Older rev)** | Lightning & Bluetooth | `0x05AC` / `0x004C` | `0x030E` |  Tested & Working |

---

## 🚀 1-Click Installation Guide

### Step 1: Download
Download the latest ready-to-use driver package:
**[`Apple-Magic-Trackpad-Precision-Driver-v1.0.0.zip`](../../releases/latest)** *(~250 KB)*

### Step 2: Install
1. Extract the downloaded `.zip` file.
2. Right-click **`Install-Driver.bat`** and select **Run as administrator**.
3. Windows will prompt to register and activate the Precision Touchpad driver.

### Step 3: Enjoy & Customize
Open Windows Settings to customize gestures to your liking:
- Navigate to **Settings** ➔ **Bluetooth & devices** ➔ **Touchpad**.
- Customize scroll direction (**Down motion scrolls down** / natural scrolling), pinch-to-zoom, tap sensitivity, 3-finger gestures, and 4-finger gestures.

> **How to Uninstall:** If you ever wish to remove the driver, simply right-click **`Uninstall-Driver.bat`** and select **Run as administrator**.

---

## 🖐️ Native Gestures Supported

| Gesture | Action | Configurable in Windows |
| :--- | :--- | :---: |
| **1-Finger Tap** | Single click / Left click |  |
| **2-Finger Tap** | Right click |  |
| **2-Finger Drag** | Fluid vertical and horizontal scrolling |  |
| **2-Finger Pinch / Stretch** | Smooth zoom in / zoom out |  |
| **3-Finger Tap** | Windows Search / Notification Center / Middle click |  |
| **3-Finger Swipe Up** | Task View (All open windows) |  |
| **3-Finger Swipe Down** | Show desktop |  |
| **3-Finger Swipe Left / Right** | Switch between apps (Alt + Tab) |  |
| **4-Finger Swipe Left / Right** | Switch between Virtual Desktops |  |

---

## 🛠️ Architecture Overview

```
 ┌─────────────────────────────────────────────────────────┐
 │             Apple Magic Trackpad (Hardware)             │
 └────────────────────────────┬────────────────────────────┘
                              │ Bluetooth / USB-C
                              ▼
 ┌─────────────────────────────────────────────────────────┐
 │               AmtPtpDevice Driver Package               │
 │            (AmtPtpDevice.inf / AmtPtpHidFilter.sys)      │
 └────────────────────────────┬────────────────────────────┘
                              │ Native PTP HID Translation
                              ▼
 ┌─────────────────────────────────────────────────────────┐
 │         Windows Precision Touchpad Engine (OS)          │
 └────────────────────────────┬────────────────────────────┘
                              │ Native OS Shell & Windows Settings
                              ▼
 ┌─────────────────────────────────────────────────────────┐
 │        Windows 10 / 11 Shell & Desktop Applications     │
 └─────────────────────────────────────────────────────────┘
```

---

## ❓ Troubleshooting & FAQ

<details>
<summary><b>1. Gestures do not work after pairing via Bluetooth</b></summary>

- Go to **Windows Settings ➔ Bluetooth & devices ➔ Devices**.
- Find your **Apple Magic Trackpad**, click **Remove device**.
- Turn the trackpad power switch **OFF** for 3 seconds, then slide it back **ON**.
- Re-pair the trackpad with Windows via Bluetooth.
- Re-run `Install-Driver.bat` as administrator.
</details>

<details>
<summary><b>2. How can I confirm the driver is active?</b></summary>

- Open **Device Manager** (`devmgmt.msc`).
- Expand **Human Interface Devices**.
- Look for **Apple Magic Trackpad (Precision Touchpad)**.
- Open **Windows Settings ➔ Bluetooth & devices ➔ Touchpad**; if the page displays touchpad gesture settings, the driver is working properly.
</details>

<details>
<summary><b>3. Does this require any background software running?</b></summary>

- **No.** This is a native driver-level solution. Once installed, Windows manages the trackpad natively without consuming memory or CPU in the background.
</details>

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues).

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingImprovement`)
3. Commit your Changes (`git commit -m 'Add support for new PID'`)
4. Push to the Branch (`git push origin feature/AmazingImprovement`)
5. Open a Pull Request

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for more information.

---

## 🙏 Acknowledgments

- Microsoft Windows Precision Touchpad specification and community driver pioneers.
- Bingxing Wang and Vito Plantamura for foundational driver implementations.
