# Metadata and Data Deletion: Removing Digital Traces

*Status: Level 1 | Audience: All members*

Every file you create, every photo you take, every document you edit generates invisible metadata — data about data. This metadata often reveals more than the content itself: who created a file, when, where, with what software, and on what device. This guide covers finding, stripping, and permanently destroying metadata and sensitive data.

---

## 1. What Is Metadata and Why It Matters

### 1.1 Types of Metadata

**File metadata (EXIF, document properties):**
- Photos: GPS coordinates (exact location), timestamp, camera model, lens, camera serial number, editing software, photographer's name if stored in camera settings
- Documents: Author name (from OS/Office settings), organization, computer name, creation date, modification dates, edit history, sometimes tracking changes and deleted content
- Audio/Video: Recording device, timestamp, GPS coordinates if recorded on a smartphone

**System metadata:**
- File access logs (when a file was last opened)
- Thumbnail caches (previews of images, including deleted ones)
- Browser history, cookies, cached pages
- Application logs (what apps were opened, when, for how long)
- Printer spool metadata (many printers embed invisible machine identification codes in every printed document)

**Network metadata:**
- IP address logs (which IP accessed which service, when)
- DNS queries (which domain names were resolved, from which IP)
- Connection timing and size (usable for traffic analysis even when content is encrypted)

### 1.2 Real-World Consequences of Unmanaged Metadata

- **Bari/Cherney bombing (1990):** Judi Bari and Darryl Cherney, Earth First! organizers, were injured in a car bombing. The FBI misidentified them as suspects partly based on investigation of their materials and associations — a case study in how document analysis serves investigation.
- **Reality Winner (2017):** NSA contractor who leaked a classified document. The document contained hidden printer dots — machine identification codes embedded by the printer — that identified the specific printer she used, leading to her identification and arrest.
- **Countless doxxing cases:** Photos of activists shared on social media retained GPS EXIF data that revealed their home address.

---

## 2. Stripping File Metadata

### 2.1 ExifTool (All Platforms) — The Essential Tool

ExifTool is the definitive open-source tool for reading and removing metadata from virtually every file type. It is command-line based but powerful.

**Installation:**
- macOS: `brew install exiftool`
- Ubuntu/Debian: `sudo apt install exiftool`
- Windows: Download from exiftool.org
- F-Droid (Android): Not available directly; use Scrambled EXIF for photos

**Essential commands:**

```bash
# View all metadata in a file
exiftool photo.jpg
exiftool document.docx
exiftool video.mp4

# Remove ALL metadata from a file
exiftool -all= photo.jpg

# Remove all metadata from ALL files in a directory
exiftool -all= /path/to/folder/

# Remove only GPS coordinates, keep other data
exiftool -GPS= photo.jpg

# Batch remove metadata and save originals as _original files
exiftool -all= -overwrite_original_in_place photo.jpg

# Verify: view what remains after stripping
exiftool photo.jpg  # Should show minimal or no EXIF fields
```

### 2.2 Photo Metadata on Mobile

**Android — Scrambled EXIF:**
- F-Droid app
- Share a photo to Scrambled EXIF; it strips EXIF and creates a clean copy
- Alternatively: built into some camera apps (Camera of CalyxOS strips by default)

**iOS — Image Metadata Viewer:**
- iOS 16+: *Photos → Select Photo → Share → Remove Location* (removes only GPS; does not remove all EXIF)
- For complete stripping: use a third-party app like Metapho (paid) or export the photo to Files and process with a Shortcut using ExifTool-compatible actions
- Best practice: use Scrambled EXIF on a trusted Android device or process desktop-side before sharing

**Signal:** Signal automatically strips metadata from photos shared through the app. Images received through Signal also have metadata stripped. This is one reason to share photos via Signal rather than via email or cloud link.

### 2.3 Document Metadata

**Microsoft Office / LibreOffice documents:**

Built-in stripping:
- *File → Inspect Document → Inspect* (Office): Finds and removes personal information, tracked changes, hidden content, comments
- *File → Properties → Statistics/Description*: Check and clear the author fields

ExifTool for documents:
```bash
exiftool -all= document.docx
exiftool -all= presentation.pptx
exiftool -all= spreadsheet.xlsx
```

**Safer approach: Convert to PDF with Dangerzone**

**Dangerzone** (dangerzone.rocks) is a free, open-source tool that:
1. Opens your document in a sandboxed container (Docker)
2. Renders it to a pixel-perfect image
3. Converts the image back to a PDF
4. This process strips ALL embedded metadata, macros, active content, and potential malware from the document

The resulting PDF contains only visual information — no author names, no edit history, no embedded code. This is the safest method for sharing documents from unknown sources or sharing documents where you want zero metadata leakage.

### 2.4 Printer Steganography (Machine Identification Codes)

Many color laser printers embed invisible yellow tracking dots in every printed page. These dots encode:
- The printer's serial number
- The date and time of printing

This was how Reality Winner was identified. EFF maintains a list of printers known to use this system (eff.org/issues/printers).

**Countermeasures:**
- Print from a printer not associated with your identity (library, print shop — cash, no loyalty card)
- Use a printer not on EFF's list of identified printers
- For extremely sensitive documents: print then photograph the document and share the photograph (metadata scrubbed) rather than the printed document or the original file

---

## 3. Secure Data Deletion

### 3.1 Why Normal Deletion Doesn't Work

When you "delete" a file, the operating system marks the space as available for reuse — but the data remains on the disk until it is overwritten by new data. Forensic tools (Autopsy, EnCase, FTK) can recover "deleted" files from conventional hard drives and sometimes from SSDs and flash storage.

### 3.2 Securely Deleting Files

**On traditional hard drives (HDDs):**
Overwriting with random data makes recovery computationally infeasible.

- macOS: `rm -P file.txt` (deprecated in newer macOS; use Disk Utility's secure erase for drives)
- Linux: `shred -vzn 3 file.txt` (overwrites 3 times with random data, then zeros, then deletes)
- Windows: Eraser (free tool) or `sdelete -z -p 3 file.txt` (Sysinternals SDelete)

**On SSDs, flash drives, and phones:**
SSDs use wear-leveling algorithms that spread data across the physical storage in ways that make individual file overwriting unreliable. The data you "shred" may not be the data that ends up overwritten.

**Best practice for SSDs and phones:**
- Enable full-disk encryption from the start (if the drive was always encrypted, deleted data is encrypted garbage even if technically recoverable)
- For retiring an SSD or phone: factory reset + fill the drive with garbage data + factory reset again
- For highest security: physical destruction of the storage chip

### 3.3 Securely Wiping Entire Drives

**When retiring a device:**

*macOS:*
- For internal drives: *Disk Utility → Select Drive → Erase → Security Options → 3-Pass Secure Erase* (not available on SSDs in modern macOS — use encryption + reset instead)
- FileVault-encrypted drives: Erase the drive (the data is already encrypted garbage)

*Linux:*
```bash
# Wipe an entire drive (replace /dev/sdX with target drive — BE CAREFUL)
sudo shred -vzn 3 /dev/sdX

# Or with dd:
sudo dd if=/dev/urandom of=/dev/sdX bs=1M status=progress
```

*Windows:*
- Download DBAN (Darik's Boot and Nuke) for wiping HDDs from bootable media
- For SSDs: use the manufacturer's secure erase utility, or use BitLocker encryption + format

### 3.4 Tails for Ephemeral Operation

The most thorough approach to data deletion: never write sensitive data to persistent storage in the first place.

Tails OS runs entirely in RAM. When you power off a Tails computer, all RAM is cleared. No traces remain on the host machine. This is the gold standard for sensitive work.

See the [Tails OS Guide](../digital-security/tails_os_guide.md) for setup instructions.

---

## 4. Browser and Application Data

### 4.1 Browser Data Cleanup

Browsers store significant amounts of potentially sensitive data:

**What to clear regularly:**
- Browsing history
- Download history
- Cookies and site data
- Cached images and files
- Saved form data and autofill
- Saved passwords (use a dedicated password manager instead)

**Firefox:**
*Settings → Privacy & Security → Clear Data* → select all categories → Clear

**Automation:** Configure Firefox to clear all data on close (*Settings → Privacy & Security → Cookies and Site Data → Delete cookies and site data when Firefox is closed*)

**For maximum privacy:** Use the Tor Browser (clears all session data on close by design) or use Firefox in Private Browsing mode for sensitive sessions.

### 4.2 Application Logs and Caches

Operating systems and applications generate extensive logs:

*macOS:*
- System logs: `/var/log/` (requires root to fully access)
- Application logs: `~/Library/Logs/` — clear these periodically
- Crash reports contain system information: `~/Library/Logs/DiagnosticReports/`
- Recent items: *Apple Menu → Recent Items → Clear Menu*

*Linux:*
- `/var/log/` — system logs, may require root to delete
- `journalctl --vacuum-time=1d` — clear systemd journal logs older than 1 day
- BleachBit (free tool): automates cleanup of application caches, logs, and temporary files

*Windows:*
- Event Viewer logs: `eventvwr.msc` → Right-click each log → Clear Log
- Prefetch files: `C:\Windows\Prefetch` — delete (records of recently run programs)
- Temporary files: `%temp%` in Run dialog → delete all
- BleachBit for Windows automates comprehensive cleanup

### 4.3 Signal Cleanup

Signal stores messages on your device. When you delete a conversation or message in Signal, it is deleted from Signal's local database — but may not be immediately overwritten in storage.

- **Disappearing messages** is the most reliable cleanup method — use it as your default
- Periodic full app data clear: uninstall and reinstall Signal (you will lose message history — back up if needed first)
- Note: Signal backups (Android) are encrypted; store them only on encrypted drives

---

## 5. Data Minimization: Generating Less in the First Place

The most effective metadata management is not generating it at all.

**Principles:**
- Use apps and services that collect less data: Signal instead of WhatsApp, Firefox instead of Chrome, DuckDuckGo instead of Google
- Disable automatic cloud sync and backup for sensitive data
- Use apps in offline mode when syncing is not needed
- Take fewer photos of sensitive situations; what doesn't exist can't be analyzed
- Review and delete old messages, files, and photos regularly — if you don't need it, delete it

**Monthly data hygiene practice:**
- [ ] Clear browser history, cookies, and cache
- [ ] Review and delete unnecessary files and photos from your devices
- [ ] Check application permissions for any apps with broad data access you haven't reviewed recently
- [ ] Review and delete any app data you no longer need
- [ ] Run ExifTool on any photos you plan to share publicly

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
