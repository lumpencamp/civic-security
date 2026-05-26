# Password Management and Two-Factor Authentication

*Status: Level 1 | Audience: All members — foundational security hygiene*

Password hygiene is the single highest-return security investment you can make. Credential compromise — weak passwords, reused passwords, phishing, data breaches — is the most common way activists, journalists, and ordinary people get their accounts taken over. This guide covers password managers, strong password generation, and every form of two-factor authentication, from weakest to strongest.

---

## 1. The Password Problem

### Why You Cannot Manage Passwords Yourself

The average person has 100+ online accounts. The human brain cannot:
- Generate truly random, unique passwords
- Remember 100+ different complex passwords
- Know which of those passwords have been exposed in data breaches

**Common failure modes:**
- **Password reuse:** Using the same password on multiple sites means that when one site is breached (as all major sites eventually are), every account with that password is compromised
- **Weak passwords:** "Summer2024!" passes most site requirements but is crackable in seconds with modern tools
- **Predictable patterns:** "Password1!", "P@ssw0rd", name+birthday — all in attacker wordlists

### The Solution: A Password Manager

A password manager generates, stores, and auto-fills long, random, unique passwords for every site. You remember one master password; the manager handles the rest.

---

## 2. Password Manager Options

### 2.1 Bitwarden (Recommended for Most Users)

**What it is:** Open-source, audited, cross-platform password manager with free and paid tiers.

**Why it's recommended:**
- Open source — code is publicly auditable
- Zero-knowledge architecture — Bitwarden never sees your passwords; they are encrypted on your device before syncing
- Independent security audits published publicly
- Free tier includes everything most users need
- Works on iOS, Android, Windows, Mac, Linux, and as browser extensions

**Setup:**
1. Create an account at bitwarden.com using a secure email address
2. Install on all your devices and browsers
3. Generate a master password: long (16+ characters), memorable, unique — a passphrase works well: "correct-horse-battery-staple" style
4. Enable two-factor authentication on your Bitwarden account immediately (see Section 3)
5. Import existing passwords if you've used another manager, or add accounts as you log in

**Self-hosted option:** Bitwarden can be self-hosted using Vaultwarden — maximum control, no third-party servers. Requires some technical setup.

### 2.2 KeePassXC (Recommended for High-Risk Users)

**What it is:** Open-source, offline-only password manager. Stores your vault as an encrypted local file.

**Why choose it:**
- No cloud sync — your vault never leaves your device unless you explicitly copy it
- Open source and extensively audited
- Ideal for air-gapped setups or those who don't trust any cloud provider

**Trade-off:** You must manually manage syncing between devices (e.g., via an encrypted USB drive or Syncthing). More effort, more control.

### 2.3 1Password

Widely used commercial option with strong security track record. Not open source. Good if you need strong team/organizational password sharing features.

### 2.4 What NOT to Use

- **Browser built-in password managers** (Chrome, Firefox, Safari): Acceptable for low-stakes accounts, but they are tied to your Google/Apple/Mozilla account and do not provide the audit trail, organization, or cross-platform features of a dedicated manager
- **Spreadsheets or text files:** Never. Even encrypted ones are fragile.
- **Your memory alone:** Does not scale and cannot generate truly random passwords

---

## 3. Password Best Practices

### Generating Strong Passwords

**For random passwords (most accounts):** Use your password manager's generator. Configure it for:
- Length: 20+ characters
- Include: uppercase, lowercase, numbers, symbols
- Exclude ambiguous characters only if the site requires it

**For passphrases (master password, device unlock):** A passphrase is a sequence of random words:
- Example: `turbine-oracle-glacier-8-lamp`
- Length in words: 5 minimum, 6–7 for critical uses
- Use a word randomizer (Diceware methodology) — truly random, not words you chose
- Easier to type on a keyboard without a password manager
- Strong due to length even if individual words seem simple

### Account Priority for Password Hygiene

Address these in order:

1. **Email accounts** (most critical — email is the recovery vector for all other accounts)
2. **Password manager master password**
3. **Banking and financial accounts**
4. **Legal and medical accounts**
5. **Organizational accounts** (organizational email, shared platforms)
6. **Social media** (public-facing; compromise causes reputational harm)
7. **Everything else**

### Breach Monitoring

- **haveibeenpwned.com:** Check if your email has appeared in known data breaches. Run all your email addresses through this.
- **Bitwarden premium** includes automatic breach monitoring for stored passwords
- If a password has been breached, change it immediately everywhere it was used

---

## 4. Two-Factor Authentication (2FA)

Two-factor authentication adds a second verification step beyond your password. Even if your password is compromised, an attacker cannot access your account without the second factor.

### 4.1 2FA Methods: Weakest to Strongest

**⚠️ SMS/Text Message (Avoid for sensitive accounts)**
- A code is texted to your phone number
- Vulnerable to SIM swap attacks: attacker tricks your carrier into transferring your number to their SIM, receiving all your SMS
- Vulnerable to SS7 attacks: attackers exploit telecommunications infrastructure to intercept SMS globally
- **Use only if no stronger option is available. Never for email, password manager, or sensitive organizational accounts.**

**✓ Time-Based One-Time Password (TOTP) Apps (Good)**
- An app generates a 6-digit code that changes every 30 seconds
- Codes are generated locally — no SMS, no carrier dependency
- SIM swap attacks do not work against TOTP
- Still vulnerable to phishing (attacker creates a fake login page that captures both password and TOTP in real time)

**Recommended TOTP apps:**
- **Aegis Authenticator (Android):** Open source, encrypted backup, the current best option for Android
- **Raivo OTP (iOS):** Open source, iCloud backup (encrypted)
- **Bitwarden Authenticator:** Integrated with Bitwarden — convenient but means your 2FA and passwords are in the same vault (slight security trade-off)
- Avoid: Google Authenticator (no export), Authy (proprietary, some concerns)

**Setup:** When a site offers TOTP 2FA ("Authenticator App"), it shows a QR code. Scan it with your TOTP app. Store the backup codes the site provides in your password manager or encrypted vault.

**✓✓ Hardware Security Keys (Best)**
- A physical USB or NFC device (YubiKey, Google Titan) that you press to authenticate
- Immune to phishing — the key uses cryptography tied to the specific website domain; a fake site cannot use it
- Immune to SIM swapping — entirely offline authentication
- Immune to network-based interception

**Recommended hardware keys:**
- **YubiKey 5 series:** The industry standard. Works via USB-A, USB-C, or NFC. Support FIDO2/WebAuthn and TOTP. Buy two — one primary, one backup.
- **Google Titan Key:** Good alternative from Google, available in USB-A, USB-C, and Bluetooth versions

**Where to use hardware keys:**
1. Password manager (Bitwarden, 1Password)
2. Email (Gmail, Proton Mail, Fastmail)
3. GitHub, GitLab
4. Any service supporting FIDO2/WebAuthn

**Limitation:** Not all sites support hardware keys. Use TOTP where hardware keys are not supported.

---

## 5. Phishing Defense

2FA significantly reduces phishing risk, but does not eliminate it. Hardware keys are the most effective phishing countermeasure.

**Phishing red flags:**
- Email from an address that looks right but isn't (support@paypa1.com vs. support@paypal.com)
- Urgent language ("Your account will be suspended in 24 hours")
- Links to pages that look correct but have a different domain (paypal.com.security-update.net)
- Attachments you weren't expecting, especially .zip, .doc, .pdf, .exe

**Defending against phishing:**
- **Never click links in emails for sensitive accounts.** Type the URL directly into your browser or use a bookmark.
- **Verify the URL in your browser bar** before entering credentials. Look for the exact domain (signal.org, not signal.org.login.com)
- **Use a hardware key** — it will refuse to authenticate to a phishing site
- **Report phishing** to your organization so others are warned

---

## 6. Password Manager for Organizations

If your organization shares credentials (e.g., a shared social media account, shared servers), you need an organizational password manager:

- **Bitwarden Organizations:** Allows sharing specific credentials with specific team members, with full audit logs. The free tier covers small teams.
- **1Password Teams:** Strong option with good administrative controls
- **Vaultwarden** (self-hosted Bitwarden): Full control, no cloud dependency, requires technical setup

**Key organizational practices:**
- Do not share passwords verbally or via Signal — use the password manager's sharing feature
- Revoke access immediately when a member leaves or trust changes
- Use the audit log to monitor unusual access patterns
- Enable 2FA for all organizational accounts; make this a mandatory policy

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
