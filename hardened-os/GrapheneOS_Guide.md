# Guide: GrapheneOS Post-Installation Hardening

*Status: High-Risk Endpoint Defense | Audience: Targets of Advanced Forensic Exploitation*

GrapheneOS is a private and secure mobile operating system. It is a hardened fork of the Android Open Source Project (AOSP). However, base installation is insufficient against physical capture by T3/T4 adversaries equipped with modern forensic extraction tools (e.g., Cellebrite Premium, GrayKey).

This guide focuses exclusively on **post-installation hardening** to ensure your device survives physical seizure and remains in an un-exploitable state.

---

## 1. Achieving Before-First-Unlock (BFU) Dominance

When a device is powered on but has not yet been unlocked with a PIN/password, it is in a "Before-First-Unlock" (BFU) state. In BFU, the encryption keys remain securely encrypted in the Titan M2 hardware chip. Modern forensic tools cannot practically brute-force a strong alphanumeric password while the device is in BFU.

If the device is seized while unlocked, or after it has been unlocked once (After-First-Unlock or AFU), the encryption keys reside in the device's RAM, making extraction trivial. **Your goal is to ensure the device returns to BFU as quickly as possible when not in use.**

### Configure Auto-Reboot
Force the device to return to the BFU state after a short period of inactivity.

1.  Navigate to **Settings** > **Security** > **Auto reboot**.
2.  Set the timer to **10 Minutes** (maximum 30 minutes for operational necessity).
3.  *Warning:* You must memorize your primary passcode. If you are detained and the device auto-reboots, biometric unlock (fingerprint) is disabled.

### Implement PIN Layout Randomization
Defeat "smudge attacks" (forensics mapping finger grease on the screen) and visual shoulder-surfing.

1.  Navigate to **Settings** > **Security** > **Screen lock** (gear icon).
2.  Toggle **Scramble PIN layout** to **ON**.
3.  Ensure your screen lock is a minimum 6-digit random PIN, though a 12-character alphanumeric passphrase is the gold standard.

---

## 2. Advanced Compartmentalization: Storage Scopes & Profiles

Do not grant global storage permissions to any application, especially messaging or social media clients.

### Enforce Storage Scopes
Instead of granting "Allow access to all files," utilize GrapheneOS Storage Scopes to feed applications a heavily restricted, fake filesystem.

1.  Navigate to an app's **App Info** page > **Permissions** > **Photos and videos**.
2.  Select **Configure Storage Scopes**.
3.  Tap **Add file** or **Add folder** to explicitly whitelist *only* the specific media the app needs to function. The app will believe it has full storage access, but it is cryptographically blind to anything outside the scope.

### Multi-User Profiles for Isolation
Separate distinct operational personas using hardware-level user profiles.

1.  Navigate to **Settings** > **System** > **Multiple users**.
2.  Create separate profiles (e.g., "Comms," "OSINT," "Logistics").
3.  *Crucial:* Toggle **Send notifications to current user** to **OFF** to prevent metadata bleed between profiles.
4.  Profiles utilize separate encryption keys. When a secondary profile is not active, its data is at rest (BFU).

---

## 3. Sandboxed Google Play Implementation

Some operations require proprietary applications (e.g., specific encrypted VoIP platforms) that rely on Google Play Services for push notifications. GrapheneOS allows running Play Services as a standard, unprivileged app.

### Zero-Privilege Installation
1.  Open the default **Apps** repository on the GrapheneOS home screen.
2.  Install **Google Play services**, **Google Play Store**, and **Google Services Framework**.
3.  Navigate to **Settings** > **Apps** > **Google Play services** > **Permissions**.
4.  Revoke *all* permissions (Location, Contacts, Network, etc.).
5.  Toggle **Sensors** to **OFF** to prevent the framework from polling gyroscope/accelerometer data to build a physical pattern-of-life profile.

---

## 4. Network and Connectivity Hardening

Limit the device's RF emissions to prevent active tracking via IMSI-catchers or crowd-monitoring beacons.

### Disabling Legacy and Background Emissions
1.  Navigate to **Settings** > **Network and internet** > **Internet** > [Your Carrier] (gear icon).
2.  Toggle **Allow 2G** to **OFF** to defeat standard Stingray downgrade attacks.
3.  Navigate to **Settings** > **Location** > **Location services**.
4.  Toggle **Wi-Fi scanning** and **Bluetooth scanning** to **OFF**. (This prevents the OS from continuously polling for nearby access points even when Wi-Fi/Bluetooth are disabled).
5.  Navigate to **Settings** > **Network & internet**. Toggle **Turn off Wi-Fi automatically** and **Turn off Bluetooth automatically** to the shortest possible durations.

### **Supported Devices**

GrapheneOS has very strict hardware security requirements. As a result, it **only officially supports Google Pixel phones**.

As of 2026, this generally includes:
*   Pixel 10, Pixel 10 Pro, Pixel 10 Pro XL, Pixel 10 Pro Fold, Pixel 10a
*   Pixel 9, Pixel 9 Pro, Pixel 9 Pro XL, Pixel 9 Pro Fold, Pixel 9a
*   Pixel 8, Pixel 8 Pro, Pixel 8a
*   Pixel 7, Pixel 7 Pro, Pixel 7a
*   Pixel 6, Pixel 6 Pro, Pixel 6a
*   Pixel Fold, Pixel Tablet

*Always check the official [GrapheneOS releases page](https://grapheneos.org/releases) for the most current list before purchasing a device.*

_Last Updated: 2026_
