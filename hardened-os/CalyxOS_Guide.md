# Guide: CalyxOS Post-Installation and Hardening

*Status: Mobile Privacy Engineering | Audience: Privacy-Conscious Activists*

> [!CAUTION]
> **OPERATIONAL SECURITY & LEGAL NOTICE**
> CalyxOS provides a critical balance between privacy and software usability. Hardening this operating system is a defensive measure to mitigate commercial telemetry and cellular tracking.
> - **Always** verify that your cellular carrier permits OEM bootloader unlocking before purchasing a device (Verizon in the US blocks unlocking).
> - **Never** rely on MicroG for completely zero-metadata communications.
> - **Always** keep your system updated to receive monthly security patches.

CalyxOS offers a vital bridge between absolute security (GrapheneOS) and daily usability. It is designed to strip away pervasive corporate surveillance while maintaining compatibility with necessary applications. However, to maximize its potential, you must actively configure its built-in privacy tools.

This manual details the entire process: installation, configuration of microG, network firewalling via Datura, and establishing a secure backup workflow.

---

## 0. Secure Installation Guide

CalyxOS provides a streamlined command-line utility called the "Device Flasher" to make installation as safe and error-free as possible.

### 0.1 Prerequisites
*   **Hardware:** An officially supported device (Google Pixel, Fairphone, or supported Motorola — see Section 9). **Ensure it is factory unlocked.**
*   **Host Computer:** Windows, macOS, or Linux.
*   **Cable:** A high-quality USB-C data cable.

### 0.2 The Flasher Process
1.  **Enable OEM Unlocking:** On your device, go to *Settings > About phone*. Tap the "Build number" 7 times to enable Developer options. Go back to *Settings > System > Developer options* and enable **OEM unlocking** and **USB debugging**.
2.  **Download the Flasher:** Navigate to [calyxos.org/install](https://calyxos.org/install/) on your computer and download the Device Flasher for your operating system.
3.  **Run the Utility:** Connect your phone to the computer. Open a terminal (macOS/Linux) or Command Prompt (Windows) and run the downloaded executable.
4.  **Follow On-Screen Prompts:** The Flasher will automatically detect your device, download the correct factory image, and walk you through rebooting into the bootloader.
5.  **Unlock the Bootloader:** When prompted on the phone screen, use the volume keys to select "Unlock the bootloader" and press power to confirm.
6.  **Flashing & Relocking:** The utility will flash CalyxOS. **Crucially, it will prompt you to lock the bootloader at the end of the process.** You must confirm this on the phone. Leaving the bootloader unlocked compromises the entire security model of the device.

---

## 1. Datura Firewall: Default-Deny Networking

The Datura Firewall is CalyxOS's most powerful built-in tool. By default, commercial apps will attempt to connect to the internet to harvest analytics, download ads, and report your IP address. Your stance must be **Default-Deny**.

### Granular App Configuration
You must manually whitelist network access for applications.
1.  Navigate to **Settings > Network and internet > Datura Firewall**.
2.  **The Default Stance:** Disable "Background data" globally for all non-essential applications.
3.  **Per-App Configuration:** For apps like a camera, calculator, or offline document reader (e.g., CryptPad offline), disable **all** network access (Wi-Fi, Mobile Data, and VPN). An offline tool has no legitimate reason to communicate with a remote server.
4.  **Network Isolation:** If an app requires internet access, but you only want it to sync when you are secure, restrict it to "Wi-Fi Only" (preventing it from using cellular data while you are in transit) or "VPN Only" (ensuring it cannot leak your true IP address if the VPN drops).

---

## 2. MicroG Configuration and Risk Mitigation

MicroG is the open-source replacement for Google Play Services. It allows push notifications and location services to function without giving Google deep system privileges. However, MicroG still talks to Google's servers. You must configure it to minimize this telemetry.

### The Risks of MicroG
When MicroG is fully enabled, your device registers a unique identifier with Google to receive Cloud Messaging (push notifications). This creates a metadata trail connecting your IP address to your device.

### Hardening the Configuration
1.  Open the **MicroG Settings** app.
2.  **Device Registration:** Disable this unless absolutely necessary. If disabled, apps cannot use Google's servers for push notifications. (Note: Secure apps like Signal use their own WebSocket connections and *do not* need MicroG to receive messages).
3.  **Cloud Messaging:** If you *must* use a proprietary app that requires push notifications (e.g., a specific secure email client or banking app), enable Cloud Messaging.
    *   *Mitigation:* Tap the three dots (menu) in Cloud Messaging and go to **Advanced**. Increase the "Ping interval" to reduce how often your device talks to the server.
4.  **Google SafetyNet:** Ensure this is **Disabled**. It is a remote attestation service that sends device hardware profiles to Google.
5.  **Location Modules:** Disable the "Google Location Service" backend. Rely solely on Mozilla Location Service (MLS) or DejaVu for privacy-respecting, offline Wi-Fi/Cell-tower location lookups.

---

## 3. The Panic Button: Emergency Deployment Workflow

The Panic Button is a "dead man's switch" designed to rapidly secure your device during physical apprehension or imminent threat.

### Deployment Workflow
You must configure the Panic Button *before* an action. Do not wait until you are detained.
1.  Open the **Panic Button** app from the app drawer.
2.  **Set the Trigger:** Configure the trigger mechanism (e.g., rapidly pressing the power button 5 times, or pressing a specific volume button combination).
3.  **Map the Actions:** Select exactly what the Panic Button will do when triggered.
    *   *T2 Threat Level (Protest/Crowd Control):* Map the button to **Uninstall Specific Apps** (e.g., instantly wipe Signal, Element, or your password manager) and **Hide Selected Apps**.
    *   *T3/T4 Threat Level (Targeted Seizure):* Map the button to **Send Emergency SMS** (notifying your jail support contact with your coordinates) followed immediately by a **Device Shutdown**.
4.  **Why Shutdown?** A complete device shutdown forces the phone back into the highly secure Before-First-Unlock (BFU) state, encrypting your data keys and locking out forensic extraction tools like Cellebrite.

---

## 4. SeedVault Encrypted Backup

When operating in high-risk environments, physical device loss (confiscation or destruction) is highly probable. CalyxOS includes **SeedVault**, a fully encrypted, privacy-respecting backup solution integrated directly into the OS.

### Configuration
1.  Navigate to **Settings > System > Backup**.
2.  SeedVault will generate a **12-word recovery phrase**. Write this down on physical paper and store it in a secure location (e.g., a physical safe). If you lose this phrase, your backups are permanently unrecoverable.
3.  **Backup Destination (Local vs Cloud):**
    *   *High Security (Local USB):* Plug in a USB-C flash drive. Tell SeedVault to back up directly to the flash drive. This keeps your data entirely off the internet.
    *   *High Availability (Nextcloud):* If you run a secure, self-hosted Nextcloud instance, you can configure SeedVault to encrypt the backup locally and upload the ciphertext directly to your cloud storage.

---

## 5. Aurora Store Configuration

Since you do not have the Google Play Store, you need a way to download mainstream apps (like a local banking app or transit app) without logging into a Google account.

### Using Aurora Store Anonymously
Aurora Store is an open-source client that interfaces with Google Play's servers.
1.  Open **Aurora Store** (pre-installed on CalyxOS).
2.  When asked how to log in, **always select Anonymous**. Aurora Store utilizes shared pool accounts to request the APK files from Google without tying the request to your personal identity.
3.  **Spoofing:** You can go into Aurora's settings and "spoof" your device model or location if an app claims it is incompatible with your device.

---

## 6. Recommended App Stack

CalyxOS comes pre-configured with several privacy apps. Augment them with the following stack, entirely available via F-Droid or Aurora Store:

*   **Browser:** **Cromite** or **Mull**. Both are hardened privacy browsers. Cromite is based on Chromium (excellent site isolation); Mull is based on Firefox (excellent tracking protection via arkenfox user.js).
*   **Communications:** **Signal** (for synchronous messaging) and **Element** (for decentralized Matrix chat).
*   **Anonymity:** **Orbot** (for routing traffic through Tor).
*   **Navigation:** **OsmAnd~** (for offline mapping).
*   **Authentication:** **Aegis Authenticator** (encrypted TOTP manager).
*   **Passwords:** **KeePassDX** (offline password manager).
*   **Media/Privacy:** **Scrambled Exif** (strips metadata from photos before you share them) and **NewPipe** (privacy-respecting YouTube client that requires no account and blocks ads).

---

## 7. CalyxOS vs. GrapheneOS: The Decision Matrix

While both strip out commercial spyware, they have fundamentally different architectural goals.

| Feature | CalyxOS | GrapheneOS |
| :--- | :--- | :--- |
| **Philosophy** | "Privacy by Default, Usability Intact" | "Absolute Security and Exploit Mitigation" |
| **Google Services Replacement** | microG (fools apps into thinking Play Services exists, some metadata leakage) | Sandboxed Play Services (runs Google code safely in an unprivileged cage) |
| **Device Support** | Pixels, Fairphone, Motorola | Google Pixels *only* |
| **Usability / Friction** | Extremely low. Almost all mainstream apps work perfectly out of the box. | High. Some apps will crash or refuse to run without native Google integration. |
| **Threat Model Fit** | Perfect for organizers avoiding mass commercial surveillance and local police dragnet tracking (T2/T3). | Necessary for journalists or dissidents targeted by nation-state actors with zero-day exploits (T3/T4). |

---

## 8. Updating and Maintenance

CalyxOS handles Over-The-Air (OTA) updates automatically. It is critical that you do not defer these updates.

*   **Security Patches:** CalyxOS generally pushes Android Open Source Project (AOSP) monthly security patches within days of Google releasing them.
*   **Verification:** Updates are cryptographically signed by the Calyx Institute. Your device will automatically verify the signature before applying the update in the background. Simply reboot when prompted.

---

## 9. Supported Devices & Device Lifecycle (May 2026)

CalyxOS officially supports Google Pixel, Fairphone, and select Motorola devices that permit secure bootloader relocking.

As of **May 2026**, the supported device catalog includes:
*   **Google Pixel:** Pixel 6 series, 7 series, 8 series, 9 series (including Fold and Tablet), and the newly released **Pixel 9a** and **Pixel 10 series** (Pixel 10, 10 Pro, 10 Pro XL, 10 Pro Fold, 10a).
*   **Fairphone:** Fairphone 4 and **Fairphone 5**.
*   **Motorola:** moto g 5G (2024), moto g84 5G, moto g34 5G, moto g45 5G, moto g52, moto g42, and moto g32.
*   **Upcoming Support:** SHIFTphone 8.

> [!WARNING]
> **Carrier OEM Bootloader Unlocking Warning**
> To install CalyxOS, you must be able to unlock your device's bootloader. Many carrier-branded devices—most notably **Verizon-branded Google Pixels** in the United States—completely prohibit bootloader unlocking at the hardware level. **Do not buy carrier-locked Pixels or Verizon-branded devices for custom OS installation.** Always purchase factory-unlocked devices directly from the manufacturer.

*Verify model compatibility on the official [CalyxOS device support page](https://calyxos.org/docs/guide/device-support/) before purchasing.*

[← Back to Index](../index.md)
