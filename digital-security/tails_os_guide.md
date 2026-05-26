# Tails OS Guide: The Amnesic Anonymous Operating System

*Status: Level 3 | Audience: High-risk users, journalists, and those handling extremely sensitive information*

Tails (The Amnesic Incognito Live System) is a live operating system you boot from a USB drive. It is specifically designed to:
1. **Leave no trace** on the host computer you use it on
2. **Route all internet traffic through Tor** by default
3. **Provide a secure, consistent environment** regardless of what's installed on the host machine

Tails is used by journalists, whistleblowers, activists, and human rights workers worldwide. It was used by Glenn Greenwald and Laura Poitras to receive and process the Snowden documents.

---

## 1. When to Use Tails

Tails is not for everyday use — it is a specialized tool for specific high-stakes situations:

**Use Tails when:**
- Handling extremely sensitive documents (leaked files, legal strategy, source communications)
- Communicating with confidential sources from a journalist or organizational context
- Working at a computer you do not trust (public library, someone else's machine, a device that may be compromised)
- Accessing materials where you need to ensure no forensic trace remains
- Working in an environment where your devices may be monitored or seized

**Tails is probably overkill if:**
- You just want Signal or a VPN
- You are doing routine organizational communications
- The primary concern is your phone rather than your laptop

---

## 2. How Tails Works

### 2.1 The Live System Architecture

Tails boots entirely from the USB drive — the host computer's hard drive is never accessed and never written to. When you shut down Tails:
- All RAM is automatically overwritten (cleared)
- No session data, downloaded files, or encryption keys remain on the host machine
- The USB drive returns to its normal state unless you explicitly saved to the encrypted Persistent Storage

### 2.2 Tor Integration

Every network connection in Tails is routed through Tor automatically. If an application attempts to make a direct internet connection (bypassing Tor), Tails blocks it. This ensures that even if an application behaves unexpectedly, your real IP address is not leaked.

### 2.3 Pre-installed Security Tools

Tails ships with:
- **Tor Browser:** Configured for maximum anonymity
- **Thunderbird with OpenPGP:** For encrypted email with journalists and organizations
- **KeePassXC:** Offline password manager
- **OnionShare:** Anonymous file sharing
- **Electrum:** Bitcoin wallet (for anonymous transactions)
- **LibreOffice:** Full office suite for working with documents
- **LUKS encryption tools:** For creating encrypted volumes
- **MAT2:** Metadata anonymization tool for documents and images
- **Kleopatra:** PGP key management GUI

---

## 3. Installing Tails

### 3.1 Requirements

- A USB drive of **at least 8 GB** (16+ GB recommended for Persistent Storage)
- A computer that can boot from USB
- A second device (phone or different computer) to follow the installation instructions
- About 30–60 minutes for installation

### 3.2 Obtaining Tails

**Only download Tails from the official website: tails.boum.org**

Tails provides very clear installation instructions with signature verification. Follow them exactly:
1. Go to tails.boum.org/install
2. Select your operating system for the detailed instructions
3. Download the Tails image
4. **Verify the cryptographic signature** — Tails provides step-by-step verification instructions. This step confirms your download has not been tampered with.

### 3.3 Installation Methods

**From macOS:**
1. Install Etcher (balena.io/etcher) or use the command line
2. Insert USB drive
3. Open Etcher → Flash from file → Select Tails image → Select USB drive → Flash

**From Windows:**
1. Install Rufus (rufus.ie) or Balena Etcher
2. Insert USB drive
3. Open the tool → Select Tails image → Select USB drive → Write

**From Linux:**
```bash
# Verify the USB device name first: lsblk
sudo dd if=tails-amd64-X.XX.img of=/dev/sdb bs=16M oflag=direct status=progress
# Replace /dev/sdb with your USB drive — DOUBLE CHECK before running
```

### 3.4 Booting Tails

1. Insert the Tails USB into the computer
2. Restart the computer
3. Access the boot menu (typically F12, F9, or Delete key during startup — varies by computer)
4. Select the USB drive to boot from
5. Tails welcome screen appears — click *Start Tails*

**If the computer won't boot from USB:**
- Disable Secure Boot in BIOS/UEFI settings (Tails is not signed for Secure Boot on older versions — check current Tails documentation)
- Ensure USB is plugged into a USB 2.0 or 3.0 port directly (not a hub)

---

## 4. Persistent Storage

By default, Tails forgets everything when you shut down. Persistent Storage allows you to save specific types of data on the USB drive between sessions.

### 4.1 Setting Up Persistent Storage

In Tails: *Applications → Tails → Configure persistent volume*

Set a **strong passphrase** — this protects your persistent data if the USB drive is seized.

### 4.2 What to Persist

Configure only what you actually need to persist. Each category of persistent data is a potential forensic target if the USB is seized.

**Reasonable to persist:**
- Browser bookmarks (Tor Browser)
- KeePassXC password database
- OpenPGP keys (for journalists needing ongoing source communication)
- SSH keys (for server access)
- LUKS encryption keys for specific containers

**Do NOT persist:**
- Communications history beyond what is operationally necessary
- Sensitive documents you are working with (store these on a separate encrypted drive and mount when needed)

### 4.3 Using Persistent Storage

When starting Tails with an existing Persistent Storage:
1. At the welcome screen, enter your Persistent Storage passphrase
2. Tails loads your saved configuration
3. Your KeePassXC database, browser bookmarks, etc. are available

---

## 5. Operational Use

### 5.1 Tor Browser in Tails

The Tor Browser in Tails is pre-configured for maximum anonymity:
- JavaScript disabled by default in "Safest" security level
- No extension installation recommended (alters fingerprint)
- Window size standardized

For accessing .onion services (SecureDrop, Proton Mail onion, etc.), type the .onion address directly into the URL bar.

### 5.2 Working with Documents

**Receiving documents:**
- Download files through Tor Browser
- Before opening, consider running through **MAT2** (metadata anonymization) or **Dangerzone** (if available in your Tails version)
- Open documents in Tails' LibreOffice — they are NOT automatically safe just because they are opened in Tails
- Malicious documents (macros, JavaScript in PDFs) can still execute; use Tails' Document Converter or open with caution

**Exfiltrating documents:**
- After scrubbing metadata, share via OnionShare or SecureDrop
- Save processed versions to Persistent Storage or an encrypted external drive

### 5.3 Email in Tails (Thunderbird + OpenPGP)

Tails includes Thunderbird configured for secure email with OpenPGP encryption:
1. Add your email account (use Proton Mail or similar for end-to-end encryption)
2. Configure your PGP key in Thunderbird's OpenPGP settings
3. Verify your contacts' keys before sending sensitive messages

**For journalists:** Configure Tails with your Proton Mail account and use it exclusively for source communications. This provides: Tor anonymization of your connection + Proton Mail encryption in transit + your own PGP encryption of content.

---

## 6. Security Considerations

### 6.1 What Tails Cannot Protect Against

- **Hardware implants:** If the computer you're using has a hardware-level keylogger or network implant, Tails cannot detect it
- **Shoulder surfing:** People watching your screen
- **Malicious documents:** A document with active exploits can still compromise the Tails session (use Tails' Document Converter for untrusted files)
- **BIOS/UEFI rootkits:** If the firmware of the host computer is compromised, Tails cannot detect it
- **Weak operational security:** Logging into personal accounts from Tails, for example, de-anonymizes you immediately

### 6.2 Protecting the Tails USB Drive

Your Tails USB (especially with Persistent Storage) is sensitive:
- Store it separately from your regular devices
- Do not carry it in situations where it could be seized
- Consider having a "clean" Tails USB (no persistent storage) for general use and a separate one with persistent storage for ongoing sensitive projects
- If it's seized, Persistent Storage is encrypted with your passphrase — do not provide the passphrase

### 6.3 Trusted vs. Untrusted Computers

Tails is designed to run on untrusted computers — you don't need to trust the computer you're booting from. However:
- Hardware with physical keyloggers or network-level monitoring cannot be protected against by Tails
- Use the most trustworthy available hardware when the stakes are highest
- Libraries and public computers are generally fine for low-to-medium-risk Tails use; use your own hardware for the most sensitive work

---

## 7. Getting Help with Tails

- **Official documentation:** tails.boum.org/doc (comprehensive, clear, regularly updated)
- **Tails help desk:** tails.boum.org/support (support team responds within 1–3 business days)
- **Access Now's Digital Security Helpline:** accessnow.org/help — provides direct security assistance to civil society organizations and activists globally

---

*This guide does not constitute legal advice. Tails is legal in most jurisdictions but may attract attention in surveillance contexts. Know your local legal environment.*

[← Back to Index](../index.md)
