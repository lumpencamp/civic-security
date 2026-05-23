# Tails OS: Amnesic Operations and Volatile Memory Security

*Status: Forensics Countermeasure Manual | Audience: Whistleblowers and High-Risk Researchers*

Tails (The Amnesic Incognito Live System) is not a daily driver; it is a tactical deployment environment. Its primary utility is not just encryption—it is **amnesia**. It leaves zero trace on the host machine.

This guide details the exact operational constraints and hardware auditing required to deploy Tails safely.

---

## 1. Auditing the Host Computer (BIOS/UEFI Security)

Tails runs entirely in RAM. However, before it loads, the host computer's firmware controls the boot process. You must ensure the host hardware is not compromising the live environment.

### Boot Sequence Hardening
1.  **Enter UEFI/BIOS:** Power on the host machine and repeatedly press the setup key (usually F2, F12, Delete, or Esc).
2.  **Disable Secure Boot:** While designed to stop malware, Secure Boot often blocks live Linux USBs. Disable it temporarily for the operation.
3.  **Disable Fast Boot:** Fast Boot skips hardware initialization checks and can interfere with USB detection. Disable it.
4.  **Admin Password:** Set a BIOS/UEFI Administrator password. This prevents an adversary from altering the boot sequence to boot from a malicious USB before Tails loads if the machine is left unattended.

## 2. Cold-Boot Attacks and RAM Mitigation

When you shut down a computer, data stored in RAM (Random Access Memory) does not instantly vanish. Forensic investigators can perform a "cold-boot attack" by freezing the RAM modules (using compressed air or liquid nitrogen), transferring them to a specialized machine, and extracting the encryption keys before they degrade.

### Power-Down Protocol
Tails is designed to overwrite most of RAM during the shutdown process, but you must trigger this properly.
*   **Do Not Perform a Hard Reset:** Never simply hold down the power button. This leaves RAM intact.
*   **The Safe Shutdown:** Always shut down Tails through the system menu.
*   **The Emergency Pull:** If physically compromised during an operation, rapidly pull the USB stick out of the computer. Tails is engineered to instantly detect the removal, trigger an emergency memory wipe, and power down.

## 3. LUKS Persistent Storage: Configuration and Risks

An amnesic system forgets everything. If you must save files across sessions, you must configure a Persistent Storage volume. This introduces massive risk: if compromised, the volume contains an unalterable history of your operations.

### Secure Configuration
1.  Open **Applications** > **Tails** > **Persistent Storage**.
2.  Tails utilizes LUKS (Linux Unified Key Setup) for encryption.
3.  **Passphrase Entropy:** The volume must be secured with a passphrase of no less than 6 random words (diceware).
4.  *Forensics Warning:* The default LUKS iteration count in older versions was susceptible to GPU brute-forcing. Ensure you are running the latest version of Tails, which utilizes Argon2id key derivation, exponentially increasing the time required for brute-force attacks.

## 4. Avoiding the "Bridge Building" Trap

The most common way activists compromise a Tails session is through behavioral crossover—creating a "bridge" between their amnesic identity and their true identity.

### Operational Constraints
*   **Never Connect to Home Wi-Fi:** Tails routes all traffic through Tor, but your ISP and the Tor entry node will still see that a Tor connection was established from your home IP address at a specific time. If you are uploading leaked documents, an adversary can correlate the upload time with the Tor connection time at your residence. **Always use public, untrusted Wi-Fi for Tails operations.**
*   **The Single-Session Rule:** Never log into a personal account (e.g., your real Gmail) and an operational account (e.g., your anonymous ProtonMail) during the same Tails session. Even over Tor, exit nodes or advanced fingerprinting techniques can link the two sessions, completely burning your operational alias.
*   **Hardware Spoofing:** Tails automatically spoofs your network card's MAC address to hide your hardware identity from the public Wi-Fi router. **Do not disable this feature** on the welcome screen unless explicitly required to connect to a captive portal.

_Last Updated: 2026_
