# Device Encryption: Cryptographic Defense of Data-at-Rest

*Status: Storage Cryptography Manual | Audience: Source Handlers and High-Risk Data Custodians*

If a physical device is seized while powered off, Full Disk Encryption (FDE) is your only line of defense. As a cryptographic software engineer, I must clarify that encryption algorithms are rarely "broken." The failure point is almost always weak key generation (passphrase entropy) or flawed implementation.

This guide details the deployment of FDE and deniable encryption architectures required to withstand targeted forensic extraction and GPU-accelerated brute-forcing.

---

## 1. Cryptographic Primitives and Entropy Requirements

Do not rely on default settings without understanding the math protecting your data.

### Recommended Primitives
When configuring encryption software (like VeraCrypt or LUKS), you will be prompted to select algorithms.
*   **Encryption Algorithm:** Use **AES-256**. It is the global standard, heavily audited, and hardware-accelerated on modern CPUs (AES-NI), providing fast read/write speeds without compromising security. The cipher mode should be **XTS** (XEX-based tweaked-codebook mode with ciphertext stealing), which is specifically designed to resist manipulation attacks on block storage.
*   **Hash Algorithm:** Use **SHA-512** or **Whirlpool**. This is used for Key Derivation (turning your password into the actual mathematical key).

### Passphrase Entropy Against GPU Brute-Forcing
Forensic adversaries (T3/T4) use massive clusters of GPUs to guess passphrases at a rate of millions per second.
*   **The Mandate:** Your passphrase must possess sufficient entropy (randomness) to make brute-forcing mathematically impossible before the heat death of the universe.
*   **Implementation:** Use a **Diceware** passphrase consisting of a minimum of **6 completely random words** (e.g., `correct horse battery staple...`). This generates over 77 bits of entropy, which is secure against all known conventional brute-force capabilities. Do *not* use a complex, memorized password containing substitutions (e.g., `P@ssw0rd!123`); cracking dictionaries defeat these instantly.

## 2. Full Disk Encryption (FDE) Deployments

FDE encrypts every sector of your drive, including the swap space and temporary files, which often contain fragments of unencrypted sensitive data.

### Linux (LUKS)
*   **Implementation:** Linux Unified Key Setup (LUKS) is the standard for Linux distributions. During the installation of a secure Linux OS (like Debian, Ubuntu, or Qubes OS), you will be prompted to encrypt the installation.
*   **Security Standard:** Ensure the installer uses LUKS2. LUKS2 utilizes the Argon2id Key Derivation Function (KDF). Argon2id is specifically designed to be memory-hard, exponentially increasing the financial cost and time required for an adversary to brute-force your passphrase using GPUs or ASICs.

### Cross-Platform (VeraCrypt)
For external hard drives, USB thumb drives, or creating encrypted containers on Windows/macOS, use **VeraCrypt** (the audited, open-source successor to TrueCrypt).

## 3. Deniable Encryption: The VeraCrypt Hidden Volume

If you face physical coercion or legal compulsion (a court order demanding your passphrase), standard FDE fails because you are forced to surrender the key. Deniable encryption solves this by creating two volumes in the same space: an Outer Volume and a Hidden Volume.

### The Mechanics of Plausible Deniability
VeraCrypt creates an Outer Volume filled with decoy data. Inside the seemingly random "free space" of that Outer Volume, it builds a Hidden Volume. There is no cryptographic signature proving the Hidden Volume exists.

If forced to surrender a passphrase, you provide the passphrase for the Outer Volume. The adversary decrypts the drive, finds the decoy data, and has no mathematical proof that secondary data is hidden inside.

### Configuration Protocol
1.  Open VeraCrypt and select **Create Volume**.
2.  Choose **Create a hidden VeraCrypt volume**.
3.  **Create the Outer Volume:**
    *   Set the Outer Volume passphrase.
    *   Mount it and fill it with plausible decoy data (e.g., tax documents, benign personal photos). The decoy data *must* look realistic.
4.  **Create the Hidden Volume:**
    *   VeraCrypt will now prompt you to create the Hidden Volume within the free space of the Outer Volume.
    *   Set a completely different, highly secure Diceware passphrase for the Hidden Volume.
5.  **Behavioral Constraint (CRITICAL):** When you mount the Outer Volume to add more decoy data, you *must* select "Protect hidden volume" in the mount options and enter the Hidden Volume's password. If you fail to do this, adding data to the Outer Volume will overwrite and permanently destroy the Hidden Volume.

_Last Updated: 2026_
