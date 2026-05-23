# Signal: Cryptographic Hardening and Operational Security

*Status: Software Audit & Hardening Manual | Audience: Activists, Sources, and Organizers*

Signal is the gold standard for end-to-end encrypted messaging. However, its default configuration is optimized for user convenience, not for surviving targeted state-level surveillance or physical device capture. Signal's encryption only protects data *in transit*. Once data arrives on a device, it relies entirely on the device's local security.

This guide details the strict cryptographic account locking required for high-risk operations.

---

## 1. Mandatory Account Locking (Registration & PINs)

The most common attack against Signal users is not breaking the encryption; it is hijacking the account by taking over the underlying phone number (via SIM swapping or SS7 attacks) and re-registering Signal on an adversary's device.

### The Registration Lock
You must physically bind your Signal account to a cryptographic PIN, severing the reliance on SMS verification.

1.  Navigate to **Settings** > **Account** > **Registration Lock**.
2.  Toggle **ON**.
3.  *The Mechanism:* If an adversary steals your phone number and attempts to register Signal, they will be blocked without your custom PIN. After 7 days of inactivity, the lock expires, but by then, you will have realized your number is compromised.

### Custom Alphanumeric PIN Configuration
Do not use a 4-digit PIN. It is trivial to brute-force if an adversary captures the hash.

1.  Navigate to **Settings** > **Account** > **Change your PIN**.
2.  Select **Create Alphanumeric PIN**.
3.  Input a robust, random passphrase (minimum 12 characters, stored in an offline password manager like KeePassXC).

## 2. Safety Number Verification (Mitigating MitM Attacks)

End-to-End Encryption is useless if you are encrypting your messages with an adversary's public key instead of your contact's. This is a Man-in-the-Middle (MitM) attack.

### Out-of-Band Verification Protocol
You must verify the cryptographic "Safety Number" for every operational contact *before* sharing sensitive assets.

1.  Open the chat with your contact, tap their name, and select **View Safety Number**.
2.  **The Golden Rule:** Never verify a safety number over Signal itself, and never verify it over an unencrypted channel like SMS.
3.  **Out-of-Band Methods:**
    *   *In-Person:* The absolute safest method. Physically scan the QR code on their device.
    *   *Encrypted VoIP/Video:* If physical meeting is impossible, call them via an independent encrypted channel (e.g., Wire, Matrix, or PGP-encrypted email) and read the numbers aloud to confirm they match.
4.  Once verified, tap the **Mark as Verified** toggle. If the number ever changes, Signal will throw a red warning banner. *Stop all communication immediately if this occurs.*

## 3. Data Minimization: Aggressive Disappearing Messages

If your device is seized while unlocked (AFU - After First Unlock), all decrypted messages are accessible. You must enforce aggressive data minimization.

*   **The 5-Minute Rule:** For active, high-risk operational planning, set the disappearing message timer to **5 minutes or less**.
*   **Implementation:** Navigate to **Settings** > **Privacy** > **Default timer for new chats**.
*   *Operational Rationale:* Disappearing messages ensure that the "blast radius" of a compromised device is limited to a 5-minute window of conversation, rather than months of historical network mapping.

## 4. The Vulnerability of Signal Desktop

Linking your mobile Signal account to a desktop application (Windows, macOS, or Linux) exponentially increases your attack surface.

### The SQLite Database Risk
Signal Desktop does not utilize the hardware-backed keystores (like Titan M) available on modern smartphones.

1.  **Local Storage:** Signal Desktop stores all messages locally in an SQLite database file.
2.  **The Extraction Threat:** On Windows and macOS, the key used to encrypt this local database is often stored in the OS's standard credential manager (Keychain/Credential Manager). If an adversary gains local execution privileges on your computer via malware, or seizes the laptop while powered on, they can trivially extract the encryption key and dump the entire unencrypted SQLite database of your communications.
3.  **The Mandate:** **Do not use Signal Desktop for high-risk operations.** If you must use a desktop for secure communication, utilize a decentralized protocol like Matrix running within an isolated, compartmentalized virtual machine (e.g., Qubes OS `work` domain).

_Last Updated: 2026_
