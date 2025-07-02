# Guide: Device Encryption (Cross-Platform)

Full-disk encryption is one of the most critical security features you can enable. It scrambles all the data on your device, making it unreadable without your passcode. If your device is lost, stolen, or seized, encryption is your last and best line of defense.

### **Windows (BitLocker)**
1.  **Check for it:** Search for "BitLocker" in the Start Menu. If you have Windows Pro, Enterprise, or Education, it's built-in.
2.  **Enable:** Open "Manage BitLocker." Select the drive you want to encrypt (usually C:) and click "Turn on BitLocker."
3.  **Save Your Key:** **THIS IS CRITICAL.** You will be given a recovery key. Save it somewhere safe, completely separate from your computer. A password manager or a printed copy in a secure location are good options. Without this key, you could lose all your data.
4.  **Encrypt:** Choose to encrypt the entire drive and select "New encryption mode." The process can take several hours.

### **macOS (FileVault)**
1.  **Enable:** Go to System Settings > Privacy & Security > FileVault. Click "Turn On."
2.  **Save Your Key:** You will be given a recovery key. Store it safely, separate from your Mac.
3.  **Verify:** Once enabled, the setting will show "FileVault is turned on for disk [Your Disk Name]."

### **iOS (iPhone/iPad)**
Encryption is **enabled by default** as long as you have a passcode set. Go to Settings > Face ID & Passcode (or Touch ID & Passcode). If you have a passcode, scroll to the very bottom. You should see the message: "Data protection is enabled."

### **Android**
Modern Android devices are also **encrypted by default** as long as you have a secure screen lock (PIN, pattern, or password). You can verify this by going to Settings > Security > Advanced settings > Encryption & credentials. It should say "Encrypted."
