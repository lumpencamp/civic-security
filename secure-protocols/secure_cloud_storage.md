# Secure Cloud Storage & Organizational Collaboration

> [!CAUTION]
> **OPERATIONAL SECURITY & LEGAL NOTICE**
> End-to-End Encrypted (E2EE) cloud storage protects documents in transit and at rest on remote servers. However, it relies entirely on the security of your local account credentials and passphrases.
> - **Always** enforce strong, random master passwords and secure 2FA (hardware keys/TOTP) on your cloud storage accounts.
> - **Never** upload plain-text encryption keys or recovery phrases to any cloud service.
> - **Always** verify that collaborating nodes are also running secure, hardened local environments.

Activist groups, journalists, and legal support teams need to share documents, spreadsheets, and operational files. However, relying on mainstream consumer services creates massive, often invisible security vulnerabilities.

---

## 1. The Vulnerability of Google Drive and Dropbox

Services like Google Workspace, Google Drive, Microsoft OneDrive, and Dropbox hold the encryption keys to your data. They encrypt the data "at rest" on their servers, but *they* hold the key, meaning:
1.  **Automated Scanning:** They actively scan your files for content violations, malware, or copyright infringement. 
2.  **The Subpoena Threat:** **They will hand over your files to law enforcement** if they receive a subpoena or warrant, and often, gag orders prevent them from notifying you that your data has been compromised.
3.  **Insider Threat:** Rogue employees at these companies have historically abused internal tools to access user data.

For sensitive planning documents, member lists, financial records, or legal strategies, these platforms are fundamentally unsafe for T2+ threat levels.

---

## 2. The Solution: End-to-End Encrypted (E2EE) Architecture

E2EE storage fundamentally changes the trust model. The files are encrypted locally on your device (client-side) *before* they are uploaded to the cloud. 

The company hosting the files never possesses the decryption keys. If law enforcement subpoenas the server, or if a hacker breaches the company's database, they only acquire unreadable ciphertext.

---

## 3. Recommended Providers: Deep Dive

### Proton Drive (Highly Recommended for Organizers)
Operated from Geneva under strict Swiss privacy laws (FADP), Proton Drive provides zero-knowledge file encryption, secure file sharing, and robust E2EE collaborative document editing.
*   **Encryption Architecture:** Uses open-source client-side AES-256 and ECC (Elliptic Curve Cryptography). Even file names and folder structures are encrypted.
*   **Collaboration:** Features "Proton Docs," a secure alternative to Google Docs allowing real-time collaborative rich-text editing.
*   **Jurisdiction:** Switzerland. Not subject to US/EU dragnet surveillance agreements. Subpoenas require a Swiss court order, and even then, Proton can only hand over ciphertext.
*   **Pros:** Seamless integration with ProtonMail, highly polished mobile apps, excellent sharing controls (password protected links with expiration dates).
*   **Cons:** Paid tiers can be expensive for large teams. Currently lacks a native spreadsheet editor.

### CryptPad (Highly Recommended for Real-Time Collaboration)
CryptPad is a fully E2EE, zero-knowledge alternative to Google Workspace built by a French development team. 
*   **Features:** Offers collaborative rich text documents, spreadsheets (Excel compatible), Kanban boards, whiteboards, forms/polls, and presentation slides.
*   **Architecture:** Everything in the browser is encrypted before it touches the server. The server administrators cannot read your documents.
*   **Deployment:** You can use the main public instance (CryptPad.fr), or a tech-savvy organization can self-host their own instance on a private server for total sovereignty.
*   **Pros:** Incredible feature set for teams. No account required to participate in a shared document.
*   **Cons:** UI is less polished than Google. Because it's zero-knowledge, if you lose your password, the administrators absolutely cannot recover your account or data.

### Filen (Best Budget/Mass Storage Alternative)
A Germany-based zero-knowledge cloud storage provider utilizing strict AES-256 client-side encryption.
*   **Pros:** Highly competitive pricing (including lifetime plans), stable sync clients, and full open-source desktop and mobile applications.
*   **Cons:** Strictly file storage and syncing; no real-time document collaboration features like Proton Docs or CryptPad.

### Cryptomator (The Advanced DIY Fallback)
If you *must* use Google Drive or Dropbox (perhaps because an affiliated organization mandates it or already paid for a terabyte of storage), you can use Cryptomator.
*   **How it Works:** It is a free, open-source program that creates a localized encrypted vault on your computer. You put your files in the vault, Cryptomator encrypts them locally, and *then* you allow Google Drive/Dropbox to sync the encrypted vault to the cloud.
*   **Pros:** Free. Allows you to secure hostile cloud environments.
*   **Cons:** Clunky for teams. Sync conflicts can corrupt vaults if multiple people edit simultaneously.

---

## 4. Organizational Migration Guide (Google to E2EE)

Migrating an organization off Google Workspace requires planning to prevent data loss.

1.  **Data Export:** Use Google Takeout to export your organization's Drive data. Choose standard formats (.docx, .xlsx, .pdf).
2.  **Establish the New Base:** Create the organizational account on Proton Drive or CryptPad. 
3.  **Local Encryption Phase:** Download the exported data to a secure, locally encrypted hard drive (using VeraCrypt or LUKS). 
4.  **Upload & Organization:** Upload the files to the new E2EE provider. Re-establish your folder hierarchy.
5.  **Access Control:** Use role-based access. Do not share the entire root folder with every member. Create specific folders (e.g., "Logistics," "Media," "Legal") and share them via secure links only to the necessary sub-teams.
6.  **Team Onboarding (CRITICAL):** You must train your team on password management. Because these are zero-knowledge systems, **there is no "Forgot Password" reset button** that will recover the data. Mandate the use of KeePassDX or Bitwarden for all members.

---

## 5. Secure Access Control and Sharing

When sharing files externally (with journalists, allied orgs, or legal counsel):

*   **Never** use "Anyone with the link can view."
*   **Always** set an **Expiration Date** on the link (e.g., 48 hours).
*   **Always** set a **Password** on the link.
*   **Out-of-Band Delivery:** Send the link via one channel (e.g., ProtonMail) and the password via an entirely different, out-of-band channel (e.g., Signal). If an adversary intercepts one channel, they still cannot access the data.

---

## 6. Feature Comparison Matrix

| Feature | Proton Drive | CryptPad | Filen | Cryptomator | Google Drive (Baseline) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Zero-Knowledge E2EE** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes (Local) | ❌ No |
| **Real-Time Doc Collab** | ✅ Yes (Docs) | ✅ Yes (Docs/Sheets) | ❌ No | ❌ No | ✅ Yes |
| **Self-Hosting Option** | ❌ No | ✅ Yes | ❌ No | N/A | ❌ No |
| **Jurisdiction** | Switzerland | France | Germany | Germany (App) | USA |
| **Open Source Client** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No |

---

## 7. The 3-2-1 Backup Strategy

Cloud storage is sync, not a true backup. If a malicious actor gains access to a team member's device and deletes the files in the synchronized Proton Drive folder, those deletions will sync to the cloud, destroying the data globally.

Implement a 3-2-1 strategy for critical organizational data:
*   **3 Copies:** One active copy in the E2EE cloud, one local encrypted physical drive, one off-site encrypted physical drive.
*   **2 Formats:** Cloud storage and physical cold-storage (flash drives/HDDs).
*   **1 Offsite:** A trusted team member physically holding an encrypted flash drive (updated weekly) at a separate geographic location.

[← Back to Index](../index.md)
