# The Ultimate Device Encryption Guide

This guide provides a practical approach to device encryption, covering the 'why' and the 'how' to protect your data at rest.

---

## 1. The 'Why': Understanding Threat Models for Encryption

Device encryption protects **data at rest** (data on your drive when the device is off) from physical threats like theft or seizure. It does **not** protect against malware on a running system or social engineering.

---

## 2. Full-Disk Encryption (FDE) vs. File-Based Encryption

*   **Full-Disk Encryption (FDE):** Encrypts the entire operating system. This is your essential first line of defense. Examples include BitLocker (Windows), FileVault (macOS), and LUKS (Linux). **Action: Enable FDE on all your devices now.**

*   **File-Based/Container Encryption:** Creates an encrypted 'virtual disk' to store your most sensitive files. This provides a second layer of protection even when your computer is on and unlocked. The gold-standard tool for this is **VeraCrypt**.

---

## 3. A Detailed Guide to VeraCrypt

### Step-by-Step: Creating a Standard Encrypted Container

1.  **Install VeraCrypt** from `https://www.veracrypt.fr`.
2.  **Create Volume:** Launch VeraCrypt, click `Create Volume`, and choose `Create an encrypted file container` -> `Standard VeraCrypt volume`.
3.  **Select File Location:** Choose a location and give your container an innocuous name (e.g., `notes.dat`).
4.  **Encryption Options:** Use the defaults: `AES` and `SHA-512`.
5.  **Set Volume Size:** Specify the size you need (e.g., 10 GB).
6.  **Set Password:** Use a long, unique passphrase of 20+ characters. **There is no recovery if you forget it.**
7.  **Format:** Move your mouse randomly in the window to generate strong cryptographic keys, then click `Format`.

### How to Use Your Volume

1.  Open VeraCrypt, select a drive letter (e.g., `G:`), select your container file, and click `Mount`.
2.  Enter your password. The drive will appear in your file explorer.
3.  When finished, select the drive in VeraCrypt and click `Dismount`.

### Advanced: Plausible Deniability with a Hidden Volume

A hidden volume is a secret volume created inside the free space of a standard 'outer' volume, protected by a different password. This allows you to reveal the outer password under coercion without exposing your most sensitive data.

1.  **Creation:** When creating a volume, select `Hidden VeraCrypt volume`. You will first provide the password for the outer volume, then go through the creation process again for the hidden volume with a **different password**.
2.  **Critical OPSEC:** After creating a hidden volume, **never write new files to the outer volume**. To protect against this, when mounting the outer volume, use the `Mount Options` to `Protect hidden volume when mounting outer volume` by providing the hidden volume's password.
