# A Guide to Password Management & 2FA

Passwords are the keys to your digital life. If an adversary gains access to your passwords, they gain access to your communications, your files, and your identity. This guide covers the essential practices for securing your accounts.

## The Problem with Passwords

Most people make two critical mistakes:
1.  **Reusing Passwords:** If you use the same password for your email and a random forum, and that forum is hacked, the hackers now have the password to your email.
2.  **Using Weak Passwords:** "Password123" or your pet's name are easily guessed by automated software in seconds.

## The Solution: Password Managers

A password manager is a secure vault that generates, stores, and autofills strong, unique passwords for every single account you have. You only need to remember one strong "Master Password" to unlock the vault.

### Recommended Password Managers

*   **Bitwarden (Highly Recommended):** Open-source, free tier is excellent, and supports all platforms (iOS, Android, Windows, Mac, Linux).
*   **KeePassXC:** Open-source and offline-only. Your password database is stored locally on your device, not in the cloud. Excellent for high-security threat models, but requires manual syncing between devices.

### What NOT to Use

*   **Browser Built-in Managers:** Do not use Chrome, Safari (iCloud Keychain), or Firefox's built-in password managers for sensitive activist accounts. If someone gains physical access to your unlocked computer, they can easily extract all your passwords.

## Multi-Factor Authentication (MFA / 2FA)

Even the strongest password can be stolen via phishing (fake websites) or keyloggers. Multi-Factor Authentication (MFA), also known as 2-Factor Authentication (2FA), adds a second layer of security. It requires not just *something you know* (your password), but also *something you have* (a physical device).

### The Hierarchy of 2FA Methods

1.  **Hardware Security Keys (Best):** Small USB devices like a **YubiKey** or Google Titan key. You physically plug it in or tap it via NFC to log in. This is entirely immune to phishing attacks. **Highly recommended for high-risk organizers.**
2.  **Authenticator Apps (Good):** Apps like **Aegis** (Android) or **Raivo OTP** (iOS) that generate temporary 6-digit codes. Much safer than SMS. Avoid Google Authenticator as it lacks proper backup features and is closed-source.
3.  **SMS / Text Messages (DANGEROUS):** Using text messages for 2FA is fundamentally insecure. Hackers or state actors can easily intercept SMS messages or perform a "SIM swap" attack (convincing your phone carrier to transfer your number to their SIM card). **Never use SMS 2FA if other options are available.**

_Last Updated: 2026_
