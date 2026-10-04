# Reelhouse

An educational case study in bringing an iOS application to other platforms with AI-assisted design and development.

Reelhouse explores how to understand an existing iOS app, separate its reusable behaviour from its native interface, and implement clients for desktop and TV. **KayakTime / DELvEK** is the example application used for this interoperability research; Reelhouse is an independent experiment, not an official port or an affiliated product.

The interface design comes from **Claude Design (Anthropic)**. **Codex (OpenAI)** assists with implementation, investigation, testing and documentation, with the project owner making decisions and reviewing the results. The aim is to learn what these tools can help with—and where testing and human judgement are still needed.

### What we are learning

- Translating an iOS app's behaviour into clients for other operating systems.
- Sharing API, session and state logic while adapting networking, controls and presentation to each platform.
- Turning a Claude Design handoff into a working interface and checking it against the original design.
- Developing a thick client that runs on the user's device without an application server.
- Testing AI-assisted work with fixtures, platform checks and real-device validation.
- Building, versioning and distributing experimental applications reproducibly.

**Current status:** macOS, Windows and Android TV downloads are available. Experimental iPhone/iPad builds are included in nightlies only, for sideload feedback; integrated iOS device validation is pending. These are learning prototypes, with platform limitations documented below. Read the [project disclaimer](DISCLAIMER.md).

## Download

- **[Stable releases](https://github.com/rickhcchan/reelhouse-releases/releases?q=draft%3Afalse+prerelease%3Afalse)** — deliberate releases for Mac, Windows and Android TV.
- **[Nightly previews](https://github.com/rickhcchan/reelhouse-releases/releases?q=draft%3Afalse+prerelease%3Atrue)** — builds from merged changes on `main`. Previews may contain bugs.

iPhone/iPad testers should choose the latest nightly; stable releases do not include iOS.

| Your device | Choose |
| --- | --- |
| Mac with Apple Silicon (M-series chip) | `Reelhouse-Mac-Apple-Silicon-<version>.dmg` |
| Mac with an Intel processor | `Reelhouse-Mac-Intel-<version>.dmg` |
| Windows PC (64-bit Intel/AMD) | `Reelhouse-Windows-Installer-<version>.exe` |
| Windows PC, portable version | `Reelhouse-Windows-Portable-<version>.exe` |
| Android TV / compatible Android box (Android 8+) | `Reelhouse-Android-TV-<version>.apk` |
| iPhone / iPad (iOS/iPadOS 15.4+, experimental nightly only) | `Reelhouse-iOS-Unsigned-<version>.ipa` |

Filenames include the full version, such as `0.2.0` for stable or `0.2.0-nightly.20261001.12345` for a nightly preview. Mac downloads are DMG only. Downloaded apps include their runtime; no application server is required. The iOS IPA requires signing through your sideloader.

Choose the labelled app download for your platform. GitHub also adds automatic “Source code” ZIP/TAR links; these contain only this public downloads repository, **not the private application source**. They are not app installers. `SHA256SUMS` and `release-manifest.json` are download-verification files.

Current Mac builds are not Apple-notarized and Windows builds are unsigned. See the [installation instructions](#installation-and-security-warnings) below if your operating system blocks opening the app.

The app checks for updates in your installed channel: nightly or stable. Updates are optional; download and install a newer version when you choose. Only versions explicitly retired by the maintainer are blocked. A version check is required when opening the app and starting a new video; if that check cannot be reached, retry when your connection is available.

## Installation and security warnings

### macOS

1. Download the DMG for your Mac, open it and drag **Reelhouse** into **Applications**.
2. Open Reelhouse. If macOS says Apple cannot verify the app, click **Done**.
3. Open **System Settings → Privacy & Security**, scroll down to **Security**, then select **Open Anyway** for Reelhouse and confirm. See [Apple's instructions](https://support.apple.com/en-gb/102445).

If **Open Anyway** is missing, the following workaround has been tested for this app. Only use it for a Reelhouse download from this repository that you trust. With Reelhouse installed in Applications, open **Terminal** and run:

```sh
xattr -dr com.apple.quarantine /Applications/Reelhouse.app
```

Then open Reelhouse again. This removes the download quarantine only from Reelhouse; it does not disable Gatekeeper globally. A newly downloaded replacement may need approval again.

Mac builds currently have ad-hoc signatures for bundle integrity, but no Apple Developer ID signature or notarization. A free Apple developer / Personal Team account is insufficient for those distribution services; Apple Developer Program membership is required. Developer ID signing and notarization are not configured for these releases. See [Apple's membership information](https://developer.apple.com/help/account/basics/about-your-developer-account/) and [Developer ID guidance](https://developer.apple.com/developer-id/).

### Windows

Download **Windows Installer** to install Reelhouse, or **Windows Portable** to run it without installation. Both are unsigned and may trigger **Microsoft Defender SmartScreen**, including a **“Windows protected your PC”** warning.

For an unrecognized-app warning, if you trust this repository's download and the options are available, choose **More info → Run anyway**. Signing future builds would identify the publisher and help establish reputation, but would not guarantee immediate removal of SmartScreen warnings. See [Microsoft's explanation](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation).

Windows 11 **Smart App Control** or an administrator's policy may block the app without a **Run anyway** option. Smart App Control has no individual-app exception; the current preview may not run in that configuration. See [Microsoft's Smart App Control FAQ](https://support.microsoft.com/en-us/windows/security/threat-malware-protection/smart-app-control-frequently-asked-questions).

The Mac workaround was tested on an installed release. The Windows warning/approval flow has not yet been manually verified on a Windows PC; these instructions follow Microsoft's documentation.

### Android TV

Download the Android TV APK and transfer it to your box. Open it with the box's file manager, allowing that app to install unknown apps if Android asks. Open **Reelhouse** and use the directional pad, OK and Back on your remote.

Install later APKs over the existing app to keep its saved data. Development builds named **Reelhouse Preview** are separate installations with separate saved data.

### iPhone / iPad — experimental

Download the unsigned IPA from a nightly release and sign/install it with your sideloader, such as iLoader or Sideloadly. This is a GitHub sideload build, not an Apple TestFlight invitation. Actual-device feedback is needed; PiP and AirPlay are disabled. iOS update notices stay on the nightly channel.

## Trying the prototype

The example application provides practical cases for data-driven navigation, search and filtering, detail screens, native media controls, device identity and saved state. Press **F** to toggle fullscreen and **Esc** to leave fullscreen when testing the player.

An internet connection is required. Third-party service availability is outside the project's control. Saved state is currently associated with the installation/device and does not synchronize between computers.

## What's available

Preview downloads are available for macOS, Windows and Android TV. Experimental iOS downloads use the same nightly version and are excluded from stable releases.

Nightly previews contain merged development changes from `main`; “nightly” is a preview channel, not an overnight schedule. Builds may be produced manually or by automation. Stable releases follow a deliberate release decision. PR test builds stay private and are never published to this downloads repository.

## Feedback

[Report a problem or suggest an improvement](https://github.com/rickhcchan/reelhouse-releases/issues). Include your app version, operating system and what happened. Please leave out personal file paths, account/device identifiers and credentials.

This repository contains the case-study overview, prototype downloads and feedback. Development source and build workflows are maintained separately.

## Educational project notice

Reelhouse is an independent educational project based on reverse engineering and interoperability research on the **KayakTime / DELvEK iOS app**, and a demonstration of development assisted by AI coding agents and LLMs. The UI design comes from **Claude Design (Anthropic)**; **Codex (OpenAI)** assists with implementation, investigation, testing, documentation and release automation, under the project owner’s direction and review. It is not an official or affiliated product. Educational use does not grant rights to third-party content or override access restrictions. Read the [full disclaimer](DISCLAIMER.md).

This is a record of experimentation with these tools, not a claim that AI-generated designs or code are automatically correct.

## Contributors

Created and maintained by [rickhcchan](https://github.com/rickhcchan), with UI design from **Claude Design (Anthropic)** and AI-assisted development by **Codex (OpenAI)**. See [contributor credits](CONTRIBUTORS.md).
