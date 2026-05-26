# Burner Phone Guide: Procuring, Configuring, and Retiring Operational Devices

*Status: Level 2 | Audience: Field Organizers and High-Risk Participants*

A "burner" is a temporary, unlinked device used for operational purposes that is then retired, limiting your exposure if the device is seized, examined forensically, or remotely compromised. This guide covers the full lifecycle: procurement, configuration, operational use, and retirement.

> **When do you actually need a burner?** Assess this honestly using your [Threat Model](../digital-security/threat_modeling_guide.md). For most T1–T2 situations, a hardened primary phone is sufficient. Burners are most valuable for T2–T3 threat environments where device seizure is a significant risk, or when the nature of the action demands identity separation that cannot be achieved on a primary device.

---

## 1. Procurement: Creating an Unlinked Device

The entire value of a burner depends on it being genuinely unlinked to your identity. Every step in procurement can create a link.

### 1.1 Choosing the Device

**Android is generally preferred** over iPhone for burners because:
- Can be activated and used without ever creating or linking an Apple ID
- Better support for alternative app stores (F-Droid) without account linking
- GrapheneOS or CalyxOS can be installed on Pixel devices for hardened security without any Google account

**iPhone burners** are possible but less ideal:
- Many features require an Apple ID, which links the device to an account
- Without an Apple ID, app installation is impossible through the App Store
- AltStore or sideloading are workarounds but add complexity

**Device options:**
- **Google Pixel (any model):** Best for installing GrapheneOS; widely available prepaid
- **Any Android with unlockable bootloader:** For CalyxOS
- **Generic Android prepaid phones:** More accessible and cheaper; less hardening capability but sufficient for most uses

**Where to buy:**
- Physical retailers: Walmart, Target, Best Buy, Dollar General, convenience stores — all sell prepaid Android phones with cash
- Do NOT order online: online purchases link shipping addresses, payment cards, and purchase history to the device

### 1.2 The Procurement Operation

**Before you go:**
- Leave your primary phone at home (or in Faraday bag). Your primary phone's location data will place you at the purchase location, creating a link between you and the device.
- Plan the purchase at a store you do not regularly frequent and at a time you are not easily tracked to your normal routine.
- Pay with cash. Credit or debit card purchases create a permanent transaction record linking your identity to the device and SIM's serial numbers.

**At the store:**
- Purchase the phone and a prepaid SIM card at the same time — or preferably at different stores.
- Do not speak to sales staff about your use case; do not provide name or contact info for any promotional sign-up.
- Use self-checkout if available.

**Transportation:**
- Do not take a rideshare or drive your personal vehicle to the purchase — both create location records. Walk or use public transit without your personal phone.

### 1.3 SIM Procurement

A SIM card purchased with cash and without identity verification is the key communications component.

- Many prepaid SIMs do not require ID for activation — Tracfone, Straight Talk, Mint Mobile prepaid SIMs purchased at retail are examples
- Some SIMs do require identity verification — avoid these for operational use
- Alternative: use the burner exclusively on Wi-Fi (no SIM) for Signal and Tor-based communications, accepting that you have no cellular voice/SMS capability

**SIM registration laws:** Several U.S. states and many international jurisdictions require ID for SIM registration. Check your local laws. In the U.S. at federal level, there is no universal SIM registration requirement for prepaid carriers.

---

## 2. Initial Configuration

Configure the burner before connecting to any network associated with your identity.

### 2.1 First Boot Configuration

During initial Android setup:
- **Skip all Google account setup.** You do not need a Google account. When prompted, select "Skip" or "Set up later."
- **Disable all optional telemetry, analytics, and feature personalization prompts.**
- **Do not connect to your home Wi-Fi.** Use a public Wi-Fi network far from your residence, or activate over cellular data.
- **SIM activation:** If activating via carrier website, use a browser over Tor or a VPN on a separate device to access the activation URL — do not use your personal devices.

### 2.2 Software Installation

**Without a Google account**, install apps via:
- **F-Droid:** An open-source app store for Android containing privacy-respecting free and open-source apps. No account required. Install F-Droid by downloading the APK from f-droid.org.
- **APK direct download:** For apps not in F-Droid, download APKs directly from official project websites. Verify checksums where possible.

**Essential apps for an operational burner:**
| App | Purpose | Source |
|-----|---------|--------|
| Signal | Secure communications | signal.org/android/apk or F-Droid |
| Orbot | Tor for Android | guardianproject.info or F-Droid |
| Briar | Peer-to-peer encrypted messaging; works over Tor and Bluetooth | F-Droid |
| OsmAnd | Offline maps (no Google Maps account needed) | F-Droid |
| Aegis Authenticator | TOTP 2FA | F-Droid |

**Do NOT install:**
- Social media apps (all collect device identifiers)
- Commercial email apps
- Any app that requires Google Play Services or a Google account unless you have deliberately set up an anonymous Google account over Tor for the burner only

### 2.3 Signal Setup on a Burner

Signal registration requires a phone number. Options:

**Option A: Register with the burner SIM number**
- Most straightforward
- The SIM number is the identifier; if the SIM is unlinked to your identity, Signal registration is also unlinked
- Limitations: if you retire the SIM, that Signal account retires with it

**Option B: Register with a VOIP number**
- Use JMP.chat (provides a real XMPP phone number, accessible over Tor)
- Register the JMP number at jmp.chat over Tor Browser
- This number can be maintained even after the physical burner is retired

**After registration:**
- Enable Registration Lock immediately (Settings → Account → Registration Lock)
- Set disappearing messages as default for all chats
- Disable read receipts, link previews, and typing indicators (see [Signal Guide](../digital-security/signal_guide.md))

### 2.4 Hardening the Device

- **Screen lock:** Alphanumeric passphrase, not PIN or biometric
- **Auto-lock:** 1 minute or less
- **Encryption:** Verify full disk encryption is enabled (modern Android: enabled by default)
- **Disable:** Bluetooth, NFC, location services — turn these on only when actively needed
- **Wi-Fi:** Do not set the device to auto-connect to any networks except a deliberate, controlled network
- **Randomized MAC:** Verify MAC address randomization is enabled for Wi-Fi connections (Settings → Network → Wi-Fi → [Network] → Privacy → Randomized MAC)
- **Google Play:** If Play Store is present (without account), disable it. Go to Settings → Apps → Google Play Store → Disable.
- **Disable Google Services:** Most Android phones include Google Play Services which aggressively collects telemetry. For maximum security, use a device running GrapheneOS (which ships without Google Play Services) or disable Google Play Services and related apps.

---

## 3. Operational Use

### 3.1 The Geographic Separation Rule

The burner's power comes from geographic and behavioral separation from your primary identity:

- **Never bring the burner to locations associated with your primary identity:** home, workplace, regular gym, family home
- **Never use the burner on networks associated with your identity:** home Wi-Fi, workplace Wi-Fi, networks you frequently use on your primary phone
- **Never power on the burner and your primary phone in the same location simultaneously** — this is the most common mistake. If both devices are in the same location, they can be correlated through cell tower data and Wi-Fi logs.
- **The Faraday bag protocol:** When transiting between locations with both devices, keep one in a Faraday bag (powered on in Faraday = still safe; powered off = safer still)

### 3.2 Operational Communications

- All operational communications happen through the burner's Signal
- The burner's number is shared only with operational contacts; personal contacts do not have it
- Do not use the burner for any personal communications, even "just once"
- If you receive a call on the burner from an unknown number, do not answer; assess through Signal whether a contact is trying to reach you

### 3.3 Photography and Documentation

If using the burner to document an action:
- Enable airplane mode before taking photos (prevents automatic upload to any cloud service)
- Strip EXIF data before sharing any photos (ExifTool or Scrambled EXIF)
- Transfer photos to your secure operational system, not to personal devices or accounts

---

## 4. Retirement: Safely Decommissioning a Burner

A burner that has served its purpose should be retired cleanly. An improperly retired burner that is later found and forensically analyzed can expose past operations.

### 4.1 Digital Retirement

1. **Delete all accounts** linked to this device (Signal account: Settings → Account → Delete Account)
2. **Delete all data:** Messages, photos, contacts, app data
3. **Factory reset:** Settings → General Management → Reset → Factory Data Reset
4. **Verify the reset:** After reset, the device should show the initial setup screen as if brand new

**Note on factory reset limitations:** A factory reset removes logical access to data but may not fully overwrite the physical storage — forensic tools can sometimes recover data from reset Android devices. For maximum security, use "Overwrite data" option if available, or manually fill storage before resetting (step 4.2).

### 4.2 Physical Retirement

After digital retirement, decide based on your threat model:

**Low-risk retirement:** Factory reset + remove the SIM → donate, sell, or simply stop using the device. The data is logically deleted; physical forensics is unlikely for most T1–T2 scenarios.

**High-risk retirement:** Factory reset → SIM removal → physical destruction of the device. Breaking the storage chip prevents forensic recovery. Methods:
- Disassemble and physically destroy the memory chip (requires tools)
- Demagnetization (degaussers — for magnetic storage only, not applicable to flash)
- Destruction: drill through the phone, particularly the memory chip area

**SIM retirement:** Remove the SIM. Destroy it physically (scissors through the chip) if the threat level warrants it. Dispose of the SIM and the device separately.

### 4.3 Handling the Physical Device Post-Retirement

- Do not sell a burner at a store that requires identification
- Do not dispose of it in your home trash if physical evidence of it could link it to you
- Electronics recycling bins at stores accept anonymous devices

---

## 5. Common Mistakes and How to Avoid Them

| Mistake | Consequence | Prevention |
|---------|------------|------------|
| Bringing burner and primary phone to the same location | Cell tower data links them | Strict physical separation; Faraday bag one device |
| Using home Wi-Fi on the burner | IP address links burner to your address | Never connect to any network linked to your identity |
| Buying with a credit card | Transaction record links you to device serial number | Always cash |
| Ordering online | Shipping record links your address to the device | Always physical store |
| Logging into a personal account "just once" | Permanently links your identity to the device | Never. Not even once. |
| Leaving the SIM in the burner after retirement | SIM records + device records can be cross-referenced | Remove and destroy the SIM on retirement |
| Taking burner into a protest in your pocket with your primary phone | Both appear in cell tower logs at the same action | Carry only one device at an action; put the other in Faraday bag or leave it home |

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
