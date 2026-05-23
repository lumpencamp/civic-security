# Secure File Transfer: Exfiltration and Ingestion Infrastructure

*Status: Infrastructure Administrative Manual | Audience: Source Handlers, Journalists, and Technical Operators*

The exfiltration and ingestion of highly sensitive documents (leaks, evidence, raw footage) is the most perilous phase of any operation. Standard cloud services (Google Drive, Dropbox) are completely compromised by centralized metadata logging and subpoena compliance.

All file transfers occur over decentralized or physically isolated architectures designed to eliminate IP footprints and sender/receiver correlation.

---

## 1. Local, Offline Sharing (For Protests & Crowds)

**Use Case:** You are at a protest or action. Cell service is jammed, shut down, or you suspect police are using Stingrays (IMSI catchers) to monitor the network. You need to quickly share a photo, video, or document with an affinity group member standing next to you.

**How it Works:** You use tools that rely on local device-to-device connections (Bluetooth or creating a temporary Wi-Fi hotspot) to transfer the file without ever touching the internet.

*   **LocalSend (Highly Recommended):** LocalSend is a free, open-source app available for iOS, Android, macOS, Windows, and Linux. It requires no internet connection and no account. Both devices must be on the same local Wi-Fi network (one device can create a mobile hotspot, and the other connects to it, without cellular data turned on). It is fast and secure.
*   **Briar:** While primarily a messaging app, Briar can also transfer files peer-to-peer over Bluetooth. It is slower than LocalSend but requires no Wi-Fi setup.
*   **A Warning on AirDrop / Nearby Share:** Apple's AirDrop and Android's Nearby Share are convenient but have known privacy flaws (they broadcast device names and sometimes phone numbers/Apple IDs to nearby scanners). If you use them, set them to "Contacts Only" and turn them completely off immediately after the transfer is complete. Never leave them on "Everyone."

---

## 2. OnionShare: Ephemeral P2P Routing

**Use Case:** Direct, one-to-one transfer across geographic distances where neither party wishes to reveal their IP address, and no intermediary server is trusted.

**The Mechanics:** OnionShare temporarily spins up a localized web server on your machine and binds it to a Tor V3 Onion Service. The file never leaves your computer until the recipient downloads it directly via the Tor network.

### Operational Execution
1.  **Deployment:** Open OnionShare and select **Share Files**. Load the operational assets.
2.  **Configuration:** Ensure **Stop sharing after files have been sent** is checked. This ensures the service self-destructs the moment the transfer is complete, preventing replay or discovery attacks.
3.  **Address Generation:** OnionShare will generate a randomized `.onion` address and an authentication private key.
4.  **Out-of-Band (OOB) Verification:** The `.onion` link and password must **never** be sent over the same channel that negotiated the transfer. If you agreed to the transfer via Signal, send the OnionShare link via a PGP-encrypted email or a secure Matrix channel. This prevents an adversary compromising one channel from intercepting both the intent and the payload.
5.  **Termination:** Once the recipient confirms receipt, shut down OnionShare. The `.onion` address ceases to exist.

---

## 3. SecureDrop: Institutional Ingestion Architecture

**Use Case:** An organization (NGO, newsroom, civic defense group) needs a persistent, highly secure method to receive anonymous leaks without compromising the source or infecting the organization's internal network.

**The Mechanics:** SecureDrop is not a single app; it is a complex, hardware-isolated network architecture running over Tor. It physically separates the network ingestion phase from the viewing phase to defeat zero-day malware embedded in submitted documents.

### The Four-Tier Hardware Isolation Rule

To safely ingest anonymous files, the organization must deploy the following physical architecture:

1.  **The Application Server (The Landing Page):**
    *   *Function:* This server faces the Tor network. It hosts the `.onion` site where the source uploads the document. It generates a unique cryptographic "codename" for the source to allow for secure two-way communication.
    *   *Security:* It immediately encrypts incoming documents with the organization's public PGP key. It does not possess the private key to decrypt them.
2.  **The Monitor Server:**
    *   *Function:* Continuously monitors the Application Server for intrusion attempts or unusual behavior.
3.  **The Secure Viewing Station (SVS) - [Air-Gapped]:**
    *   *Function:* This is a dedicated, physically air-gapped laptop running Tails OS from a read-only USB drive. It possesses the private PGP key necessary to decrypt the documents. It **never** connects to the internet.
    *   *Protocol:* A technical operator downloads the encrypted files from the Application Server onto an encrypted "Transfer USB." They physically carry the Transfer USB to the SVS. The files are decrypted and viewed on the SVS. If the files contain zero-day malware designed to phone home or exfiltrate data, it fails because the SVS has no network hardware.
4.  **The Export Station:**
    *   *Function:* If a document is verified as safe and necessary for publication, it is heavily scrubbed of metadata (using tools like MAT2 or Dangerzone) on the SVS, moved to a clean Export USB, and transferred to a standard operational machine.

*Directive: Bypassing the air-gap protocol by downloading and decrypting SecureDrop submissions on an internet-connected workstation is a terminal violation of organizational security.*

_Last Updated: 2026_
