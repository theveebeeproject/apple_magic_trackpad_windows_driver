# Contributing to Apple Magic Trackpad Windows Driver

Thank you for your interest in contributing to this project! We welcome code contributions, bug reports, documentation enhancements, and feature requests.

## Code of Conduct
Please be polite, respectful, and collaborative. We aim to foster an open and welcoming community.

## How Can I Contribute?

### Reporting Bugs
Before submitting an issue, please search existing issues to avoid duplicates.
When submitting a bug report:
- Specify your Windows version and build (e.g., Windows 11 23H2 x64).
- State your trackpad hardware model (e.g., Magic Trackpad 3 USB-C, Magic Trackpad 2 Lightning).
- State connection mode (Bluetooth or direct USB cable).
- Provide steps to reproduce the issue.
- Include debug logs if available from the console or debug output.

### Suggesting Enhancements
Feature requests are tracked via GitHub issues. Clearly describe the problem you wish to solve and the desired behavior.

### Pull Requests
1. Fork the repository and create your branch from `main`.
2. Keep code style consistent with modern C# (.NET 8 standards).
3. Ensure the project builds without errors or warnings.
4. Verify your changes with actual hardware if altering `GestureEngine.cs` or `TrackpadManager.cs`.
5. Submit a pull request with a descriptive title and summary of changes.

## Development Setup
- Install [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0).
- Open `MagicTrackpadDriver.sln` in Visual Studio 2022 or VS Code.
- Build using:
  ```powershell
  dotnet build MagicTrackpadDriver\MagicTrackpadDriver.csproj
  ```

Thank you for helping make Apple Magic Trackpad on Windows great!
