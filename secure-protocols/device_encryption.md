# Device Encryption: Full-Disk and File-Level Protection

*Status: Level 1 | Audience: All members — non-negotiable baseline security*

Device encryption is your last line of defense when a device is physically seized. Without it, anyone who takes your phone or laptop can access every photo, message, document, and credential on it — no password needed. With full-disk encryption correctly configured, a seized device is an encrypted brick that requires your passphrase to access.

> **The Law and Encryption:** The Fifth Amendment may protect you from being compelled to reveal a passcode (courts are split; see [Know Your Rights](../legal-rights/know_your_rights.md)). Physical encryption is your technical protection; legal rights are your legal protection. You need both.

---

## 1. Mobile Device Encryption

### 1.1 iPhone / iOS

**Status by default:** All iPhones since iPhone 3GS (2009) encrypt data on the device. **However, the strength of this encryption depends entirely on your passcode.**

**Why the passcode matters:** iOS uses your passcode as part of the encryption key derivation. A 6-digit numeric PIN has 1,000,000 combinations — crackable in minutes by commercial forensic tools (GrayKey, Cellebrite UFED) if the device is not in a high-security mode.

**Hardening your iPhone:**
1. *Settings → Face ID & Passcode → Change Passcode → Passcode Options → Custom Alphanumeric Code*
2. Set a passphrase of 8+ random characters (mixed case, numbers, symbols)
3. Disable Face ID and Touch ID for device unlock (these can be physically compelled)
   - Face ID: *Settings → Face ID & Passcode → Use Face ID for → iPhone Unlock → OFF*
   - Touch ID: *Settings → Touch ID & Passcode → iPhone Unlock → OFF*
4. Enable *Erase Data* after 10 failed passcode attempts (*Settings → Face ID & Passcode → Erase Data*)
5. Set *Require Passcode* to *Immediately*

**Emergency lockdown:**
- Rapidly press the power button + volume button to trigger Emergency SOS mode — this disables biometric unlock until the passcode is entered
- Alternatively, power off the device completely before anticipated police contact

**Verify encryption is active:**
- *Settings → [Your Name] → iCloud → iCloud Backup* — if backups are active, confirm they are encrypted
- *Settings → Privacy & Security → Device Analytics & Improvements* — disable to reduce data shared with Apple

### 1.2 Android

**Status:** Android has supported full-disk encryption since Android 5.0 (2014) and file-based encryption since Android 7.0 (2016). Most modern Android devices enable encryption by default, but this varies by manufacturer.

**Verify and enable:**
1. *Settings → Security → Encryption & Credentials → Encrypt Phone*
   - On Samsung: *Settings → Biometrics and Security → Encrypt Device*
   - On Pixel: *Settings → Security → Encryption & Credentials*
2. If "Encrypted" or "Device encrypted" is shown, you're good
3. If not, the encryption process will prompt you — it takes 30–60 minutes

**Hardening your Android:**
1. Set a strong alphanumeric PIN or passphrase (*Settings → Security → Screen Lock*)
2. Disable fingerprint and face unlock
3. Enable *Lock immediately* when screen turns off
4. Enable *Automatically factory reset* after 10 failed attempts (if your device supports it)
5. Consider **GrapheneOS** or **CalyxOS** for significantly hardened encryption and privacy (see separate guides)

### 1.3 The Exploit Reality

Commercial forensic tools (Cellebrite, GrayKey) can sometimes extract data from encrypted devices using:
- Known operating system vulnerabilities (patched versions are immune)
- Brute-force passcode cracking (alphanumeric passphrases resist this; 4–6 digit PINs do not)
- Data extraction from device memory when the device is in an "After First Unlock" (AFU) state

**Critical:** A device that has been unlocked since last boot (AFU state) is significantly more vulnerable than one that has been powered off completely. **Power off your device before anticipated police contact.** A powered-off, encrypted device in "Before First Unlock" (BFU) state is dramatically harder to forensically analyze.

---

## 2. Laptop and Desktop Encryption

### 2.1 macOS: FileVault 2

FileVault is Apple's built-in full-disk encryption for macOS. It uses AES-256 encryption.

**Enable FileVault:**
1. *System Preferences (or System Settings) → Privacy & Security → FileVault → Turn On*
2. Choose whether to use your iCloud account or a local recovery key to unlock the disk if you forget your password
   - **For high-risk users:** Create a local recovery key, store it in your password manager, and **do not** link to iCloud. iCloud recovery keys can potentially be obtained through Apple via legal process.
3. Allow FileVault to encrypt the disk (happens in background, may take hours on older machines)
4. Reboot to complete setup

**Verify:** *System Settings → Privacy & Security → FileVault → FileVault is turned on*

**Security notes:**
- FileVault protects data only when the machine is powered off or in hibernation
- When logged in and running, the disk is decrypted in memory
- Set your Mac to require password *immediately* after screen saver or sleep (*System Settings → Lock Screen → Require password after screen saver begins or display is turned off → Immediately*)
- Enable FileVault on the startup disk AND any external drives containing sensitive data

### 2.2 Windows: BitLocker

BitLocker is Windows's built-in full-disk encryption, available on Windows 10/11 Pro, Enterprise, and Education. (Windows Home does not include full BitLocker, but has "Device Encryption" on supported hardware.)

**Enable BitLocker:**
1. Open the *Control Panel → System and Security → BitLocker Drive Encryption*
2. Select your drive and click *Turn on BitLocker*
3. Choose a startup authentication method:
   - **TPM + PIN** (recommended): Combines the hardware Trusted Platform Module with a PIN for strong protection
   - TPM only: Less secure — protects only against physical disk removal, not against someone who has the device powered on
4. Save or print the recovery key — store in your password manager, **not** in OneDrive or any Microsoft account (these can be subpoenaed)
5. Choose to encrypt only used space (faster) or entire drive (more thorough for drives with deleted data)

**Enable on Windows 10/11 Home:**
- *Settings → Update & Security → Device Encryption* — available on devices meeting modern standby requirements with a Microsoft account
- Limitation: The recovery key is automatically backed up to your Microsoft account — consider the legal implications

### 2.3 Linux: LUKS (Linux Unified Key Setup)

LUKS is the standard disk encryption method for Linux. Most distributions offer it during installation.

**Setting up LUKS during installation:**
- Ubuntu, Fedora, Debian, and most major distributions offer a "Encrypt the disk" checkbox during installation. Select it. Set a strong passphrase.

**Verify:** `lsblk -f | grep LUKS`

**Full-disk LUKS:**
- The LUKS passphrase is entered at boot, before the operating system loads
- The entire disk is encrypted at rest
- Power off = fully encrypted; logged in = decrypted in memory

**VeraCrypt for portable encryption on Linux:**
- Use VeraCrypt for encrypted containers or external drives you share between OSes (see Section 3)

### 2.4 Tails OS

Tails is a live operating system you boot from a USB drive. It routes all traffic through Tor, leaves no trace on the host machine, and uses encrypted persistent storage for any data you save between sessions.

**For the highest-sensitivity work** (handling sources, working with leaked documents, planning sensitive operations), Tails provides encryption + anonymity + amnesia in one package. See the [Tails OS Guide](../digital-security/tails_os_guide.md) for full setup instructions.

---

## 3. External Drives and Portable Storage

### 3.1 VeraCrypt (All Platforms)

VeraCrypt is free, open-source, and creates encrypted containers or fully encrypted drives compatible across Windows, macOS, and Linux.

**Use cases:**
- Encrypted archive of sensitive documents on an external drive
- Encrypted container on a cloud service (zero-knowledge storage — even if the cloud is breached, the container is encrypted)
- Creating a "hidden volume" for plausible deniability (advanced)

**Creating an encrypted container:**
1. Download VeraCrypt from veracrypt.fr — verify the signature
2. Open VeraCrypt → *Create Volume*
3. Select *Create an encrypted file container*
4. Choose *Standard VeraCrypt Volume*
5. Select a location and file name (looks like any file)
6. Choose encryption algorithm (AES is standard and fast; AES-Twofish cascade for paranoid usage)
7. Set size and a strong passphrase
8. Format and mount — the container appears as a drive letter/mount point
9. Unmount when done — the file is fully encrypted at rest

**Hardware-encrypted drives:**
- Apricorn Aegis series: Physical PIN pad, no host software required, hardware encryption that cannot be brute-forced from software. Recommended for field use.
- iStorage datAshur: Similar physical PIN pad hardware encryption, FIPS 140-2 certified

### 3.2 Encrypted USB Drives

**Never use an unencrypted USB drive for sensitive data.** USB drives are easily lost, easily stolen, and easily seized.

Options:
- **Hardware-encrypted drives** (Apricorn, iStorage): The gold standard
- **VeraCrypt container** on a regular USB drive: Works, but requires VeraCrypt installed to access
- **macOS:** Use Disk Utility to create an encrypted DMG or format the USB drive as APFS (Encrypted)
- **Linux:** Use LUKS to format the USB drive (`cryptsetup luksFormat /dev/sdb`)

---

## 4. Encrypted Backups

An unencrypted backup defeats the purpose of device encryption.

### 4.1 iPhone Backups (iTunes/Finder)
When backing up to a computer (not iCloud):
- In iTunes or Finder, select *Encrypt local backup* and set a strong passphrase
- This backup passphrase is separate from your device passcode — store it in your password manager
- An encrypted local backup cannot be read by law enforcement even with the backup file, without this passphrase

**iCloud backups:**
- iCloud backups are encrypted in transit and at rest, but Apple holds the encryption keys and can provide them to law enforcement
- For high-risk users: disable iCloud backup (*Settings → [Your Name] → iCloud → iCloud Backup → Off*) and use encrypted local backups instead

### 4.2 Android Backups
- Disable automatic Google backup if you are high-risk (*Settings → System → Backup → Off*)
- Use a local encrypted backup tool (Seedvault, available on GrapheneOS/CalyxOS) for local encrypted backups

### 4.3 Computer Backups
- Use Time Machine (macOS) with an encrypted backup drive (enable *Encrypt Backup* when setting up the destination)
- Use Duplicati or Restic for cross-platform encrypted backups — they encrypt before upload, so even cloud storage is protected
- Maintain backups on encrypted external drives; store at a separate location from your primary device (in case of physical seizure at your home)

---

## 5. Encryption Hygiene Checklist

**Monthly checks:**
- [ ] All devices (phone, laptop, external drives) have encryption active and verified
- [ ] Encryption passphrases are stored securely (password manager)
- [ ] Recovery keys are stored separately (not on the encrypted device itself)
- [ ] Operating systems are fully updated (patches fix vulnerabilities that forensic tools exploit)
- [ ] Biometrics disabled on devices used for sensitive work

**Before any high-risk situation:**
- [ ] Device powered off (not just locked) before any anticipated police contact
- [ ] Sensitive data deleted or on an unconnected encrypted drive

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
