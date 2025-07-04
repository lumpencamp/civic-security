# The Complete Guide to Device Encryption

This guide covers the 'why' and 'how' of device encryption, from the essential full-disk encryption on your main devices to advanced, file-based encryption for your most sensitive data.

---

## Part 1: Full-Disk Encryption (FDE) - The Essential First Layer

Full-Disk Encryption (FDE) encrypts the entire operating system drive. It is your non-negotiable first line of defense against physical theft or seizure. When your device is off, all your data is protected.

### **Windows: BitLocker**

1.  **Check Your Version:** BitLocker is available on Windows Pro, Enterprise, and Education editions.
2.  **Enable:** Go to Control Panel > System and Security > BitLocker Drive Encryption. Click "Turn on BitLocker" for your C: drive.
3.  **Save Your Recovery Key:** This is CRITICAL. You will be prompted to save a recovery key. **Save this key somewhere safe and separate from the computer itself.** A password manager, a printed copy in a safe, or a secure cloud storage account are good options. Losing this key and your password means losing your data forever.

### **macOS: FileVault**

1.  **Enable:** Go to System Settings > Privacy & Security > FileVault. Click "Turn On..."
2.  **Recovery Key:** You will be given the option to use your iCloud account or create a local recovery key. For maximum security, **choose to create a local recovery key** and store it securely offline, just like the BitLocker key.

### **iOS & Android**

Modern smartphones (iOS and Android) have device encryption enabled by default. Your primary protection is a **strong, alphanumeric passcode**. Do not rely solely on biometrics (Face ID, fingerprint), as they can sometimes be legally compelled. A strong passcode is your best defense.

---

## Part 2: VeraCrypt - Advanced Container-Based Encryption

For your most sensitive files, you need a second layer of protection. VeraCrypt allows you to create a password-protected, encrypted 'virtual disk' (a container) that is only accessible when you mount it.

### **Step-by-Step: Creating a Standard Encrypted Container**

1.  **Install VeraCrypt** from `https://www.veracrypt.fr`.
2.  **Create Volume:** Launch VeraCrypt, click `Create Volume`, and choose `Create an encrypted file container` -> `Standard VeraCrypt volume`.
3.  **Select File Location:** Choose a location and give your container an innocuous name (e.g., `research.dat`).
4.  **Encryption Options:** Use the defaults: `AES` and `SHA-512`.
5.  **Set Volume Size:** Specify the size you need (e.g., 10 GB).
6.  **Set Password:** Use a long, unique passphrase of 20+ characters. **There is no recovery if you forget it.**
7.  **Format:** Move your mouse randomly in the window to generate strong cryptographic keys, then click `Format`.

### **How to Use Your VeraCrypt Volume**

1.  Open VeraCrypt, select a drive letter (e.g., `G:`), select your container file, and click `Mount`.
2.  Enter your password. The drive will appear in your file explorer.
3.  When finished, select the drive in VeraCrypt and click `Dismount`. The drive disappears, and your data is secure.

### **Advanced: Plausible Deniability with a Hidden Volume**

A hidden volume is a secret volume created inside the free space of a standard 'outer' volume, protected by a different password. This allows you to reveal the outer password under coercion without exposing your most sensitive data.

1.  **Creation:** When creating a volume, select `Hidden VeraCrypt volume`. You will first provide the password for the outer volume, then go through the creation process again for the hidden volume with a **different password**.
2.  **Critical OPSEC:** After creating a hidden volume, **never write new files to the outer volume**. To protect against this, when mounting the outer volume, use the `Mount Options` to `Protect hidden volume when mounting outer volume` by providing the hidden volume's password.
