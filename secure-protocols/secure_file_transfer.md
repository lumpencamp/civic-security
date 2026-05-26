# Secure File Transfer: Sharing Sensitive Documents Safely

*Status: Level 2 | Audience: Organizers, journalists, and anyone sharing sensitive documents*

Sharing files securely is one of the most common operational security challenges. Email attachments are unencrypted by default, cloud storage services cooperate with law enforcement, and even "secure" platforms like WhatsApp can leak metadata. This guide covers the full toolkit for secure file transfer, from simple one-to-one sharing to anonymous source protection.

---

## 1. Threat Assessment for File Transfer

Before choosing a method, understand what you are protecting against:

| Threat | Concern | Appropriate Method |
|--------|---------|-------------------|
| ISP or network observer seeing file contents | Email, cloud sync | End-to-end encrypted transfer |
| Server operator reading stored files | Cloud services, email servers | Zero-knowledge encryption |
| Law enforcement subpoena to a service provider | Signal, cloud | Services with no content logs + warrant canary |
| Metadata revealing who sent what to whom | Signal (non-sealed), email | OnionShare, Magic Wormhole, sealed sender |
| File contents containing identifying metadata (EXIF, author info) | Photos, documents | Metadata stripping before transfer |
| Recipient identity | Normal channels | Anonymous transfer methods |

---

## 2. Signal for File Transfer

Signal is appropriate for most day-to-day sensitive file sharing within your trusted contact network.

**What Signal protects:**
- File contents (end-to-end encrypted)
- Metadata between you and Signal's servers (with sealed sender)

**Limitations:**
- Files stored on both sender and recipient devices until deleted
- Signal can see (and has historically been required to disclose) account metadata (when you registered, last connection time)
- Not suitable for anonymous transfer — Signal requires a phone number

**Best practices:**
- Enable disappearing messages so shared files are automatically deleted
- Confirm safety numbers with recipients before sharing highly sensitive documents
- Send files from airplane mode over Wi-Fi to avoid cellular network metadata

---

## 3. OnionShare

**OnionShare** is a free, open-source tool that creates a temporary .onion address on the Tor network and allows you to share files through it. The sender runs a local Tor Hidden Service directly on their machine — there is no intermediary server, no account, and no log.

**Capabilities:**
- Share files: recipients download directly from your machine over Tor
- Receive files: create an anonymous drop box for others to upload to you
- Host a temporary chat room: ephemeral, no accounts, no logs
- Host a website: temporary Tor-hosted site

**Why it's powerful:**
- **No server logs:** Files transfer directly between machines via Tor; no intermediary records the transaction
- **No account required:** Neither sender nor recipient needs an account
- **Anonymous for both parties:** Both sender and recipient are anonymized by Tor
- **No file size limit** (in practice, limited by connection speed and Tor bandwidth)

### 3.1 OnionShare Setup and Usage

**Installation:**
- Download from onionshare.org — verify the PGP signature
- Available for Windows, macOS, Linux (as a .deb or .rpm), and as an F-Droid package for Android

**Sharing files:**
1. Open OnionShare → *Share Files* tab
2. Drag files or folders into the window
3. Configure options:
   - *Stop sharing after files have been sent* (one-time share — recommended)
   - *Auto-start timer* (optional — share becomes available at a specific time)
4. Click *Start sharing* — OnionShare generates a .onion URL and a password (key)
5. Share the .onion address AND the key with your recipient via a secure channel (Signal)
6. The recipient opens Tor Browser, enters the .onion URL and key, and downloads the file
7. OnionShare shows real-time download status; close when complete

**Receiving files (drop box):**
1. OnionShare → *Receive Files* tab
2. Start the service — generate a .onion URL
3. Share this URL with people who need to send you files (e.g., journalist creating a source intake drop)
4. Files upload directly to a folder on your machine; you see uploads in real time

**Security note:** The recipient needs Tor Browser or Orbot to access .onion addresses. This limits the audience. Plan accordingly.

### 3.2 OnionShare for Source Protection (Journalists)

SecureDrop (below) is the industry standard for source intake, but OnionShare offers a simpler, lighter-weight alternative for individual journalists or smaller organizations:

- Use the "Receive Files" mode to create an anonymous drop box
- Share the .onion address publicly or selectively
- No account, no authentication required from the source
- Files arrive directly on your machine — no cloud intermediary

---

## 4. SecureDrop

SecureDrop is the gold standard for anonymous source-to-journalist communication, developed by Freedom of the Press Foundation (FPF). It is designed specifically to protect vulnerable sources sharing sensitive documents with news organizations.

**How it works:**
- Newsroom runs SecureDrop on a dedicated, air-gapped server
- Sources access it only via Tor Browser, receiving a random code name
- Journalists access SecureDrop only from a dedicated, air-gapped computer running Tails OS
- No account, no email, no identifying information required

**Which newsrooms have SecureDrop:**
The Freedom of the Press Foundation maintains a directory at freedom.press/news/directory

**For sources:** If you have sensitive information for a news organization, use their SecureDrop address — find it in the FPF directory. Access it only from Tor Browser on a trusted, private device.

**For organizations:** Setting up SecureDrop requires significant technical infrastructure. FPF provides support — contact them at freedom.press.

---

## 5. Magic Wormhole

Magic Wormhole is a command-line tool for fast, encrypted, one-time file transfer between two machines. It generates a simple code phrase that connects sender and receiver directly, with end-to-end encryption.

**Why use it:**
- Simpler than OnionShare when both parties are technical users comfortable with the command line
- Fast: Direct transfer, no Tor bandwidth limitation
- No account, no intermediary server (though it uses a relay server to initiate the connection)
- One-time code: each transfer uses a unique code that expires

**Limitation:** Does not provide anonymity — your IP is visible to the relay server and potentially to your peer. Use OnionShare if anonymity is required.

**Installation:**
```
pip install magic-wormhole
# or: brew install magic-wormhole (macOS)
# or: apt install magic-wormhole (Debian/Ubuntu)
```

**Usage:**
```
# Sender:
wormhole send /path/to/file.pdf
# Outputs: wormhole receive 7-crossword-galaxy (example code)

# Receiver (on different machine):
wormhole receive 7-crossword-galaxy
```

---

## 6. Encrypted Email (PGP)

PGP (Pretty Good Privacy) email encryption is the traditional method for encrypted file transfer via email. It is powerful but technically demanding, and most activists find Signal or OnionShare more practical for daily use.

**When PGP email makes sense:**
- Communicating with someone who only has email (no Signal)
- Archiving encrypted records that need to be stored long-term with verifiable authorship
- Signing documents to prove they have not been tampered with

### 6.1 PGP Basics

PGP uses asymmetric encryption:
- You have a **public key** you share widely — others use it to encrypt messages for you
- You have a **private key** you keep secret — you use it to decrypt messages sent to you
- You can **sign** messages with your private key to prove authorship

**Key concepts:**
- A signed document proves it came from you and has not been modified
- An encrypted file can only be read by whoever has the corresponding private key

### 6.2 PGP Tools

- **GPG (GNU Privacy Guard):** Command-line PGP implementation, available on all platforms. The foundational tool.
- **Kleopatra (Windows/Mac):** GUI front-end for GPG
- **GPG Suite (Mac):** Integrates PGP into macOS Mail and Finder
- **Enigmail (Thunderbird):** Thunderbird email client has built-in OpenPGP support

**Basic workflow:**
1. Generate a key pair: `gpg --full-generate-key`
2. Export your public key: `gpg --export --armor your@email.com > publickey.asc`
3. Share your public key with contacts
4. Encrypt a file for a recipient: `gpg --encrypt --recipient recipient@email.com file.pdf`
5. Send the encrypted file (safe to send over unencrypted email)
6. Recipient decrypts: `gpg --decrypt file.pdf.gpg`

### 6.3 PGP Limitations

- **Metadata:** PGP encrypts the message content but not the metadata — who sent what to whom, when, is visible to your email provider
- **Key management:** You must verify that the public key you encrypt to actually belongs to your intended recipient (otherwise you encrypt to an attacker's key). Use key signing parties, Signal to verify fingerprints out-of-band.
- **Complexity:** PGP is famously difficult to use correctly. For most activists, Signal and OnionShare are more practical and less error-prone.

---

## 7. Metadata Stripping

Even after using a secure transfer method, files often contain embedded metadata that can identify you.

### 7.1 Document Metadata

**Microsoft Office files (.docx, .xlsx, .pptx):** Contain author name (from Windows/Office account), organization, computer name, creation date, edit history, and sometimes revision history showing deleted content.

**Stripping in LibreOffice:**
1. *File → Properties → General → Reset Properties* (removes some metadata)
2. *File → Export → Export as PDF* then use PDF metadata stripping tool (more thorough)

**Stripping with ExifTool (command line):**
```
exiftool -all= document.docx
```

**PDF files:** Contain author, creation software, creation date, and sometimes GPS coordinates if created on mobile.
```
exiftool -all= document.pdf
```

### 7.2 Photo/Image EXIF Data

Photos contain extensive EXIF metadata:
- GPS coordinates (exact location where photo was taken, often accurate to meters)
- Device make and model
- Date and time
- Camera settings
- Sometimes: serial number of the camera

**Tools:**
- **ExifTool (all platforms):** The definitive tool
  ```
  exiftool -all= photo.jpg          # Remove all metadata
  exiftool -GPS= photo.jpg          # Remove only GPS data
  exiftool -j photo.jpg             # View all metadata
  ```
- **Scrambled EXIF (Android):** Share photos with metadata stripped via this app's share sheet
- **Image Scrubber (browser):** imgscrubber.com — drag and drop, strips EXIF in browser
- **Dangerzone:** For documents — converts them to PDFs in a sandboxed container, strips all metadata

### 7.3 Operational Rule

**Before sharing any photo or document from an action or sensitive context:**
1. Strip all metadata with ExifTool or equivalent
2. Verify the metadata is gone: `exiftool photo.jpg` should show no EXIF data
3. Then share via a secure channel

This should be a non-negotiable step in your information workflow.

---

## 8. Secure File Storage and Sharing for Teams

### 8.1 Proton Drive

**Proton Drive** (from the makers of Proton Mail) provides zero-knowledge encrypted cloud storage:
- Files are encrypted on your device before upload — Proton cannot read them
- Encrypted sharing links with expiration dates and passwords
- Based in Switzerland, subject to Swiss privacy law (stronger than U.S.)

**Use for:** Sharing sensitive organizational documents with team members; storing encrypted archives

### 8.2 Cryptomator

**Cryptomator** is an open-source tool that creates an encrypted "vault" on top of any cloud storage provider (Dropbox, Google Drive, iCloud, etc.):
- Files are encrypted locally before syncing to cloud
- The cloud provider sees only encrypted, unreadable files
- Works across Windows, macOS, Linux, iOS, Android

**Use for:** Adding zero-knowledge encryption to your existing cloud storage without switching providers.

### 8.3 Keybase Teams

**Keybase** provides end-to-end encrypted team file sharing:
- Files shared in Teams are encrypted and only readable by team members
- Integrates with encrypted chat, so file sharing and communication are in one place
- Account creation requires some identifying information; consider this in your threat model

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
