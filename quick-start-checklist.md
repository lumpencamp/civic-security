# Quick Start Checklist: High-Impact Security Actions

> [!CAUTION]
> **OPERATIONAL SECURITY & LEGAL NOTICE**
> This guide is intended strictly for lawful, defensive, and educational purposes. Some tactics detailed below may carry legal risks depending on your local jurisdiction. 
> - **Never** resist arrest or physically obstruct law enforcement.
> - **Always** consult local legal defense networks (e.g., National Lawyers Guild) for jurisdiction-specific advice.

*Status: High-Impact Action Directive | Audience: General Activists and Non-Technical Organizers*

Security can be overwhelming. If you are an organizer or activist preparing for civic action and do not have time to read the full manuals, perform these **six immediate, high-impact tasks** right now to secure your digital and physical footprint.

---

### 1. Enforce a Secure Alphanumeric Passcode & Disable Biometrics
Standard 4-digit or 6-digit PINs are trivial for police forensic tools (like Cellebrite) to brute-force if your device is seized. Furthermore, in many jurisdictions, biometrics (FaceID/TouchID) have weaker 5th Amendment legal protections than memorized passcodes; police can physically force your finger onto the sensor or hold the phone to your face.
*   **Action:** Go to your device's security settings and change your screen lock to a **random alphanumeric passphrase** (minimum 12 characters, mixing letters, numbers, and symbols).
*   **Protest Protocol:** Before entering any high-risk environment or protest, **disable biometrics completely**. 
    *   *On iOS:* Hold the Power and either Volume button for 2 seconds to enter the emergency screen. This initiates "Lockdown" mode, disabling FaceID until the passcode is entered.
    *   *On Android:* Enable "Show lockdown option" in lock screen settings, then select "Lockdown" from the power menu.

---

### 2. Harden Your Signal Account (Phone Number Privacy)
Signal is the gold standard for secure messaging, but revealing your phone number to large organizing groups exposes you to SIM swapping, harassment, and lateral mapping by adversaries.
*   **Action 1 (Create a Username):** Navigate to **Signal Settings > Profile** and set up a custom **Username**. Share only your username or QR code, not your phone number.
*   **Action 2 (Hide Your Phone Number):** Navigate to **Settings > Privacy > Phone Number**. Set **Who can see my number** to **Nobody** and **Who can find me by my number** to **Nobody**.
*   **Action 3 (Enforce Disappearing Messages):** Go to **Settings > Privacy > Default timer for new chats** and set it to **1 week or less**. This limits the historical data exposed if any group member's device is seized and unlocked by police.

---

### 3. Move Documents Off Google Drive & Dropbox
Centralized consumer cloud services possess the decryption keys to your files and routinely comply with law enforcement warrants and subpoena sweeps without your knowledge.
*   **Action:** Immediately transfer all member directories, spreadsheets, and operational planning documents off Google Drive, Google Docs, and Dropbox.
*   **Private Alternative:** Migrate all team documents to client-side encrypted zero-knowledge suites like **Proton Drive** or **CryptPad.fr** (which offers private, collaborative rich text editing and spreadsheets without tracking).

---

### 4. Eliminate Environmental Digital Footprints (RF Emissions)
Mobile devices continuously emit radio signals (Wi-Fi, Bluetooth, cellular) that allow commercial beacons, municipal surveillance arrays, and IMSI-catchers to track your movements.
*   **Action 1 (Turn off Background Scanning):** On Android/iOS, navigate to Location Settings and turn **OFF** "Wi-Fi scanning" and "Bluetooth scanning". This stops your device from broadcasting beacon signals even when you have manually toggled Wi-Fi/Bluetooth off.
*   **Action 2 (Faraday Bags):** During sensitive in-person planning meetings, **power down all mobile devices completely** and seal them inside certified **Faraday bags** to block all location tracking and ambient audio transmissions.

---

### 5. Configure Native Unwanted Bluetooth Tracker Alerts
Stalkers, counter-protesters, and adversaries use cheap Bluetooth trackers (AirTags, Tile) dropped into organizers' bags or attached to cars to secretly locate their homes and workspaces.
*   **Action:** Modern Android and iOS devices natively support the **Detecting Unwanted Location Trackers (DULT)** standard.
    *   **On Android:** Navigate to **Settings > Safety & emergency > Unknown tracker alerts**. Ensure that **Allow alerts** is toggled **ON**. Tap **Scan now** to perform a manual check of your surroundings after an action.
    *   **On iOS:** Ensure your device is updated to iOS 17.5+ to receive native cross-platform alerts. Ensure Bluetooth is enabled.

---

### 6. Memorize Your Legal Rights Assertion
If you are approached, detained, or arrested by law enforcement, the most critical physical and legal action is to verbally assert your constitutional rights and remain silent.
*   **Action:** Memorize and recite this three-sentence script word-for-word:
    1.  **"Am I free to leave, or am I being detained?"** (If free to leave, walk away calmly. Do not run).
    2.  **"I am invoking my Fifth Amendment right to remain silent. I choose not to answer any questions."**
    3.  **"I do not consent to any searches of my person, my belongings, or my digital devices. I want my lawyer."**
*   **Rule:** Once asserted, **remain completely silent**. Police are legally allowed to lie to you to solicit a confession. Never answer questions, sign documents, or provide your phone passcode without an attorney present.

[← Back to Index](./index.md)
