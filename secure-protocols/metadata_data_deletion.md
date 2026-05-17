# Metadata Scrubbing & Secure Data Deletion

This guide covers how to clean hidden data from files before sharing them and how to permanently delete data so it cannot be recovered by forensic tools.

## What is Metadata?

Metadata is "data about data." It is hidden information embedded inside files (photos, videos, documents).

*   **Photos/Videos (EXIF Data):** A picture taken on a smartphone often contains the exact GPS coordinates of where it was taken, the time and date, the phone model, and even the direction the camera was facing.
*   **Documents (Word, PDF):** These often contain the author's name, the organization name, the software used, and the date of creation.

If you post a protest photo online or send a planning document to a journalist without scrubbing the metadata, you may accidentally reveal your identity or location.

### Tools for Scrubbing Metadata

*   **Mobile (Android):** Use **ExifEraser** or **Scrambled Exif**. You share the photo to the app, it strips the metadata, and then you share the clean photo.
*   **Mobile (iOS):** Use **Metapho**.
*   **Desktop (Windows/Mac/Linux):** **MAT2** (Metadata Anonymisation Toolkit) is the gold standard. It works via the command line or as a plugin for the Tor Browser.
*   **Documents:** For PDFs and office documents, use **Dangerzone**. It converts the document into a safe PDF by rendering it into pixels and back, completely destroying all metadata and potential malware.

## Secure Data Deletion

When you drag a file to the "Trash" and empty it, the computer doesn't actually erase the file. It just marks the space as "available." Forensic software (like Cellebrite, used by police) can easily recover these "deleted" files.

### The Role of Full-Disk Encryption (FDE)

The most effective way to protect deleted data is to ensure your entire device is encrypted (Full-Disk Encryption).
*   If your hard drive is encrypted, and the police seize it while it's powered off, they cannot read *any* data, whether active or deleted.
*   Modern smartphones (iOS/Android) and modern operating systems (macOS FileVault, Windows BitLocker, Linux LUKS) use FDE. Ensure it is turned on.

### Secure Wiping Tools

If you need to ensure a specific file is destroyed while the computer is still in use:

*   **Desktop:** Use **BleachBit**. It can overwrite free space on a hard drive with random data, making recovery impossible.
*   **Note on SSDs:** Solid State Drives (SSDs) handle data differently than old magnetic hard drives. Repeatedly overwriting specific files on an SSD is unreliable and degrades the drive. Relying on Full-Disk Encryption is the safest approach for modern hardware.

_Last Updated: 2026_
