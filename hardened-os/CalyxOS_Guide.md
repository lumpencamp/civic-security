# Guide: CalyxOS Post-Installation Hardening

*Status: Mobile Privacy Engineering | Audience: Privacy-Conscious Activists*

CalyxOS offers a vital bridge between absolute security (GrapheneOS) and daily usability. It is designed to strip away pervasive corporate surveillance while maintaining compatibility with necessary applications. However, to maximize its potential, you must actively configure its built-in privacy tools.

This manual details the granular configuration required to harden CalyxOS against both corporate data harvesting and localized surveillance.

---

## 1. Datura Firewall: Default-Deny Networking

The Datura Firewall is CalyxOS's most powerful built-in tool. By default, apps will attempt to connect to the internet to harvest analytics, download ads, and report your IP address. Your stance must be **Default-Deny**.

### Granular App Configuration
You must manually whitelist network access for applications.

1.  Navigate to **Settings** > **Network and internet** > **Datura Firewall**.
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

*(Note: While temporarily disabled in early Android 16 test builds, the Panic Button remains a core feature of the stable CalyxOS architecture).*

The Panic Button is a "dead man's switch" designed to rapidly secure your device during physical apprehension or imminent threat.

### Deployment Workflow
You must configure the Panic Button *before* an action. Do not wait until you are detained.

1.  Open the **Panic Button** app from the app drawer.
2.  **Set the Trigger:** Configure the trigger mechanism (e.g., rapidly pressing the power button 5 times, or pressing a specific volume button combination).
3.  **Map the Actions:** Select exactly what the Panic Button will do when triggered.
    *   *T2 Threat Level (Protest/Crowd Control):* Map the button to **Uninstall Specific Apps** (e.g., instantly wipe Signal, Element, or your password manager) and **Hide Selected Apps**.
    *   *T3/T4 Threat Level (Targeted Seizure):* Map the button to **Send Emergency SMS** (notifying your jail support contact with your coordinates) followed immediately by a **Device Shutdown**.
4.  **Why Shutdown?** A complete device shutdown forces the phone back into the highly secure Before-First-Unlock (BFU) state, encrypting your data keys and locking out forensic extraction tools like Cellebrite.

### **Supported Devices**

CalyxOS supports a wider range of devices than GrapheneOS, prioritizing models that allow for bootloader relocking.

As of 2026, this includes:
*   **Google Pixel:** Pixel 4a (5G) through Pixel 9 series (including Fold and Tablet). Note: Pixel 4 and 4 XL are no longer supported.
*   **Fairphone:** Fairphone 4 and Fairphone 5.
*   **Motorola:** Select models like the Moto G 5G (2024), G84, G34/G45, G52, G42, and G32. *(Note: Non-Pixel devices may experience delays in receiving complete security patchsets compared to Pixels).*

*The list changes frequently. Always check the official [CalyxOS device support page](https://calyxos.org/docs/guide/device-support/) for the most current list and support timeline.*

_Last Updated: 2026_
