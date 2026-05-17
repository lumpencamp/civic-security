# Guide: CalyxOS

CalyxOS is a privacy-focused mobile operating system based on the Android Open Source Project (AOSP). It is designed to be a more user-friendly alternative to GrapheneOS, while still providing a high level of privacy and security.

**Threat Model:** CalyxOS is slightly less strict on security hardening than GrapheneOS, but excels in usability. It is ideal for the average activist who wants to stop pervasive commercial tracking and "de-Google" their life without sacrificing the convenience of standard apps.

**How it Works:**
*   **microG:** CalyxOS includes microG, a free and open-source implementation of Google Play Services. This allows users to run many apps that rely on Google services without having to install the official, privacy-invasive Google Play Services.
*   **Privacy by Default:** CalyxOS includes the Datura firewall and bundles a suite of privacy-focused apps that can be installed offline during setup.
    *   *2026 App Updates:* Recent updates have replaced old tools with modern alternatives, such as **Tor VPN** (replacing Orbot), **CoMaps** (replacing Organic Maps), and **F-Droid Basic**.
    *   *Note:* As of the Android 16 release cycle, **CalyxVPN** and the **Panic Button** features have been temporarily removed while they undergo redevelopment and infrastructure upgrades.

### **Supported Devices**

CalyxOS supports a wider range of devices than GrapheneOS, prioritizing models that allow for bootloader relocking.

As of 2026, this includes:
*   **Google Pixel:** Pixel 4a (5G) through Pixel 9 series (including Fold and Tablet). Note: Pixel 4 and 4 XL are no longer supported.
*   **Fairphone:** Fairphone 4 and Fairphone 5.
*   **Motorola:** Select models like the Moto G 5G (2024), G84, G34/G45, G52, G42, and G32. *(Note: Non-Pixel devices may experience delays in receiving complete security patchsets compared to Pixels).*

*The list changes frequently. Always check the official [CalyxOS device support page](https://calyxos.org/docs/guide/device-support/) for the most current list and support timeline.*

_Last Updated: 2026_
