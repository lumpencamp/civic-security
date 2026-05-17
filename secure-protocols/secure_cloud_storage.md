# Secure Cloud Storage & Collaboration

Activist groups need to share documents, spreadsheets, and files. However, using mainstream consumer services creates massive security vulnerabilities.

## The Problem with Google Drive and Dropbox

Services like Google Drive, Dropbox, and Microsoft OneDrive hold the encryption keys to your data. This means:
1.  They can scan your files for content violations.
2.  **They will hand over your files to law enforcement** if they receive a subpoena or warrant, often without notifying you.

For sensitive planning documents, member lists, or legal strategies, these platforms are unsafe.

## The Solution: End-to-End Encrypted (E2EE) Storage

E2EE storage means the files are encrypted on your device *before* they are uploaded to the cloud. The company hosting the files does not have the keys to decrypt them. If the police subpoena the server, they only get unreadable ciphertext.

### Recommended Providers

*   **Proton Drive:** Part of the Proton suite (ProtonMail, ProtonVPN). It offers a highly secure, easy-to-use interface for file storage and sharing.
*   **Tresorit:** A premium, highly polished E2EE cloud storage provider tailored for businesses and organizations that need strict security compliance.
*   **Cryptomator (Advanced DIY):** If you must use Google Drive or Dropbox (perhaps because an organization already paid for it), you can use Cryptomator. It is a free, open-source program that creates an encrypted vault on your computer. You put your files in the vault, Cryptomator encrypts them, and *then* you sync the encrypted vault to Google Drive.

## Secure Real-Time Collaboration (Alternatives to Google Docs)

If your group needs to write a document or build a spreadsheet together in real-time, Google Docs is the default, but it is not private.

*   **CryptPad.fr (Highly Recommended):** CryptPad is a fully E2EE alternative to Google Workspace. It offers collaborative rich text documents, spreadsheets, and presentation slides. Because it is E2EE, the server administrators cannot read your documents. You can use the main CryptPad.fr instance, or a tech-savvy organization can self-host their own instance.

_Last Updated: 2026_
