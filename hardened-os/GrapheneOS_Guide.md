# Guide: GrapheneOS Post-Installation and Hardening

*Status: High-Risk Endpoint Defense | Audience: Targets of Advanced Forensic Exploitation*

> [!CAUTION]
> **OPERATIONAL SECURITY & LEGAL NOTICE**
> This guide is intended strictly for lawful, defensive, and educational purposes. Custom mobile operating system hardening is a defensive mechanism against unauthorized physical and digital forensic exploitation. 
> - **Always** remember your alphanumeric passphrase; biometric overrides are disabled upon device reboot or lockdown.
> - **Never** use GrapheneOS to bypass legitimate law enforcement activities.
> - **Always** verify your device's bootloader lock state.

GrapheneOS is a private and secure mobile operating system. It is a hardened fork of the Android Open Source Project (AOSP). However, base installation is insufficient against physical capture by T3/T4 adversaries equipped with modern forensic extraction tools (e.g., Cellebrite Premium, GrayKey).

This guide focuses on the complete lifecycle: from initial secure installation to post-installation hardening to ensure your device survives physical seizure and remains in an un-exploitable state.

---

## 0. Secure Installation Guide

Installing GrapheneOS is remarkably straightforward thanks to the official WebUSB installer, but strict adherence to the process is required to maintain the hardware security model.

### 0.1 Requirements
*   **Hardware:** An officially supported Google Pixel device (see Section 9). Never buy a carrier-locked device (e.g., Verizon); the bootloader cannot be unlocked.
*   **Host Computer:** Windows, macOS, Linux, or ChromeOS.
*   **Browser:** You *must* use a Chromium-based browser (Google Chrome, Microsoft Edge, Brave, or Chromium) that supports WebUSB. Firefox and Safari will not work.
*   **Cable:** A high-quality data cable (the one that came with the phone is recommended).

### 0.2 The Installation Process
1.  **Enable OEM Unlocking:** On your Pixel, go to *Settings > About phone*. Tap the "Build number" 7 times to enable Developer options. Go back to *Settings > System > Developer options* and enable **OEM unlocking**.
2.  **Boot to Fastboot:** Power off the phone, then hold the Volume Down button while pressing the Power button until the Fastboot menu appears. Plug the phone into your computer.
3.  **Use the Web Installer:** Go to [grapheneos.org/install/web](https://grapheneos.org/install/web) in your Chromium browser.
4.  **Unlock Bootloader:** Click the "Unlock bootloader" button on the web page. A prompt will appear on your phone; use the volume keys to select "Unlock the bootloader" and press the power button to confirm.
5.  **Flash the OS:** Click "Download release" on the web page, wait for it to download, and then click "Flash release". Do not touch the device or cable during this process.
6.  **Relock Bootloader (CRITICAL):** Once flashing is complete, click "Lock bootloader" on the web page. Confirm the prompt on your phone screen. **If you do not lock the bootloader, you have no physical security. An unlocked bootloader allows trivial tampering.**
7.  **Disable OEM Unlocking:** Boot into GrapheneOS, skip Wi-Fi setup initially, go to Developer Options, and disable "OEM unlocking". Finally, disable Developer Options entirely.

### 0.3 Verifying Verified Boot
GrapheneOS supports Android Verified Boot, which ensures the OS hasn't been tampered with. When booting the phone, you should see a yellow warning screen briefly stating that the bootloader is loading a custom OS. This is normal and proves the bootloader is locked but recognizing the GrapheneOS signature keys.

---

## 1. Achieving Before-First-Unlock (BFU) Dominance

When a device is powered on but has not yet been unlocked with a PIN/password, it is in a "Before-First-Unlock" (BFU) state. In BFU, the encryption keys remain securely encrypted in the Titan M2 hardware chip. Modern forensic tools cannot practically brute-force a strong alphanumeric password while the device is in BFU.

If the device is seized while unlocked, or after it has been unlocked once (After-First-Unlock or AFU), the encryption keys reside in the device's RAM, making extraction trivial. **Your goal is to ensure the device returns to BFU as quickly as possible when not in use.**

### Configure Auto-Reboot
Force the device to return to the BFU state after a short period of inactivity.
1.  Navigate to **Settings > Security > Auto reboot**.
2.  Set the timer to **10 Minutes** (maximum 30 minutes for operational necessity).
3.  *Warning:* You must memorize your primary passcode. If you are detained and the device auto-reboots, biometric unlock (fingerprint) is disabled.

### Implement PIN Layout Randomization
Defeat "smudge attacks" (forensics mapping finger grease on the screen) and visual shoulder-surfing.
1.  Navigate to **Settings > Security > Screen lock** (gear icon).
2.  Toggle **Scramble PIN layout** to **ON**.
3.  Ensure your screen lock is a minimum 6-digit random PIN, though a 12-character alphanumeric passphrase is the gold standard.

---

## 2. Advanced Compartmentalization: Storage Scopes & Profiles

Do not grant global storage permissions to any application, especially messaging or social media clients.

### Enforce Storage Scopes
Instead of granting "Allow access to all files," utilize GrapheneOS Storage Scopes to feed applications a heavily restricted, fake filesystem.
1.  Navigate to an app's **App Info** page > **Permissions > Photos and videos**.
2.  Select **Configure Storage Scopes**.
3.  Tap **Add file** or **Add folder** to explicitly whitelist *only* the specific media the app needs to function. The app will believe it has full storage access, but it is cryptographically blind to anything outside the scope.

### Multi-User Profiles for Isolation
Separate distinct operational personas using hardware-level user profiles.
1.  Navigate to **Settings > System > Multiple users**.
2.  Create separate profiles (e.g., "Comms," "OSINT," "Logistics").
3.  *Crucial:* Toggle **Send notifications to current user** to **OFF** to prevent metadata bleed between profiles.
4.  Profiles utilize separate encryption keys. When a secondary profile is not active, its data is at rest (BFU).

---

## 3. Sandboxed Google Play Implementation

Some operations require proprietary applications (e.g., specific encrypted VoIP platforms) that rely on Google Play Services for push notifications. GrapheneOS allows running Play Services as a standard, unprivileged app.

### Zero-Privilege Installation
1.  Open the default **Apps** repository on the GrapheneOS home screen.
2.  Install **Google Play services**, **Google Play Store**, and **Google Services Framework**.
3.  Navigate to **Settings > Apps > Google Play services > Permissions**.
4.  Revoke *all* permissions (Location, Contacts, Network, etc.).
5.  Toggle **Sensors** to **OFF** to prevent the framework from polling gyroscope/accelerometer data to build a physical pattern-of-life profile.

---

## 4. Network and Connectivity Hardening

Limit the device's RF emissions to prevent active tracking via IMSI-catchers or crowd-monitoring beacons.

### Disabling Legacy and Background Emissions
1.  Navigate to **Settings > Network and internet > Internet > [Your Carrier]** (gear icon).
2.  Toggle **Allow 2G** to **OFF** to defeat standard Stingray downgrade attacks.
3.  Navigate to **Settings > Location > Location services**.
4.  Toggle **Wi-Fi scanning** and **Bluetooth scanning** to **OFF**. (This prevents the OS from continuously polling for nearby access points even when Wi-Fi/Bluetooth are disabled).
5.  Navigate to **Settings > Network & internet**. Toggle **Turn off Wi-Fi automatically** and **Turn off Bluetooth automatically** to the shortest possible durations.

### Connection Scrambling and MAC Randomization
By default, GrapheneOS implements strong MAC address randomization per connection. Verify it is active:
1. Navigate to **Settings > Network and internet > Internet**.
2. Tap a saved Wi-Fi network gear icon, go to **Privacy**, and ensure it is set to **Use randomized MAC**.
3. Note: GrapheneOS goes further than AOSP by implementing DHCP anonymity, preventing your device hostname from leaking to local networks.

---

## 5. Camera and Microphone Indicators

GrapheneOS includes hardware-backed privacy indicators to immediately alert you if an application attempts covert recording.

*   When any app accesses the microphone or camera, a green dot or icon will appear persistently in the top right corner of the status bar.
*   **Sensor Toggles:** You can globally disable the camera and microphone via the Quick Settings dropdown tiles. This cuts off access at the OS level, meaning even system apps cannot access the sensors until toggled back on.
*   **Audit Access:** Go to **Settings > Privacy > Privacy dashboard** to see a chronological timeline of exactly which apps requested Location, Camera, or Microphone access within the past 24 hours.

---

## 6. Exploit Protection Features

GrapheneOS integrates massive under-the-hood exploit mitigations that prevent zero-day attacks from succeeding. You do not need to configure these; they are active by default.

*   **Hardened Malloc:** GrapheneOS replaces the standard Android memory allocator with a hardened version designed to crash the application immediately if a memory corruption vulnerability (like a buffer overflow) is triggered. This turns a severe remote-code-execution exploit into a harmless app crash.
*   **Exec Spawning:** Unlike standard Android which forks new processes from a central "Zygote" (sharing the same memory layout space, making exploits easier), GrapheneOS spawns fresh processes to ensure strong Address Space Layout Randomization (ASLR).
*   **MTE (Memory Tagging Extension):** On Pixel 8 and newer devices, GrapheneOS supports hardware-accelerated ARM MTE. This detects and blocks memory safety bugs at the CPU hardware level in real-time, effectively neutralizing entire classes of memory corruption exploits without severe performance penalties.

---

## 7. Recommended App Configuration

Since you will likely not be using the Google Play Store directly, you must rely on secure open-source repositories.

### F-Droid and Alternative Repositories
1.  Download the **F-Droid** APK from fdroid.org.
2.  Add trusted third-party repositories:
    *   **DivestOS Repo:** Offers hardened forks of common apps (e.g., Mull browser).
    *   **Guardian Project Repo:** Maintains Orbot and other high-risk communication tools.

### Recommended Tool Stack
*   **Browser:** **Vanadium** (built into GrapheneOS). It is a hardened Chromium fork that implements strict site isolation. Do not use Firefox on Android, as it lacks per-site process isolation.
*   **Communications:** **Signal** (download the APK directly from signal.org or use the Sandboxed Play Store to receive timely updates).
*   **Anonymity:** **Orbot** (Tor proxy) for routing specific apps through the Tor network.
*   **Navigation:** **OsmAnd~** (via F-Droid) for offline, non-tracking maps. Download your region's map data over Wi-Fi.
*   **2FA & Passwords:** **Aegis Authenticator** for TOTP tokens and **KeePassDX** for password management.
*   **Camera:** The default GrapheneOS Camera app strips all EXIF metadata (GPS, device info, timestamps) from photos and videos by default. Use it for all operational photography.

---

## 8. GrapheneOS vs. CalyxOS Decision Guide

Both operating systems are excellent, but they serve different threat models. 

| Feature | GrapheneOS | CalyxOS |
| :--- | :--- | :--- |
| **Primary Focus** | Absolute security, exploit mitigation, sandboxing | Privacy, de-Googling, broad app usability |
| **Google Services** | Sandboxed Play Services (runs as a normal, unprivileged app) | microG (open-source reimplementation of Google Services) |
| **Threat Model** | Targets of state actors, high-risk investigative journalists (T3/T4) | Privacy advocates, general organizers avoiding commercial surveillance (T2/T3) |
| **Exploit Defense** | Industry-leading (Hardened Malloc, MTE, Exec Spawning) | Standard AOSP level |
| **Usability** | High friction (some mainstream apps will not work properly) | Low friction (microG fools most apps into working normally) |
| **Device Support** | Only Google Pixels | Pixels, Fairphone, select Motorola |
| **Verdict** | Choose this if your life or liberty depends on device integrity. | Choose this if you want maximum privacy without sacrificing daily convenience. |

---

## 9. Supported Devices & Device Lifecycle (May 2026)

GrapheneOS has highly rigorous hardware security standards, including requirements for a secure hardware enclave (Titan M2), hardware-based remote attestation, and hardware memory tagging (MTE) [GrapheneOS Supported Devices, https://grapheneos.org/faq#supported-devices, May 2026]. Consequently, it **only officially supports Google Pixel devices**.

As of **May 2026**, the officially supported device catalog includes:
*   **Pixel 10 Series:** Pixel 10, Pixel 10 Pro, Pixel 10 Pro XL, Pixel 10 Pro Fold, Pixel 10a
*   **Pixel 9 Series:** Pixel 9, Pixel 9 Pro, Pixel 9 Pro XL, Pixel 9 Pro Fold, Pixel 9a
*   **Pixel 8 Series:** Pixel 8, Pixel 8 Pro, Pixel 8a
*   **Pixel 7 Series:** Pixel 7, Pixel 7 Pro, Pixel 7a
*   **Pixel 6 Series (Critical EOL Warning):** Pixel 6, Pixel 6 Pro, Pixel 6a
*   **Other Form Factors:** Pixel Fold, Pixel Tablet

> [!WARNING]
> **Pixel 6 Series EOL Alert (October 2026)**
> Google's guaranteed software and firmware security updates for the Pixel 6, 6 Pro, and 6a will terminate in **October 2026**. After this date, GrapheneOS can no longer receive critical proprietary vendor firmware patches (blobs) for these devices, meaning the Pixel 6 series will reach End of Life (EOL) on GrapheneOS. **For secure high-risk operations, migrate to a Pixel 7 or newer hardware before October 2026.**

*Always verify your model on the official [GrapheneOS releases page](https://grapheneos.org/releases) before purchasing a device.*

[← Back to Index](../index.md)
