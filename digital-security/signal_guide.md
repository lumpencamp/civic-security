# Signal Messenger: Complete Security Guide

*Status: Level 1 | Audience: All members — start here for secure communications*

Signal is the gold standard for encrypted messaging among activists, journalists, lawyers, and security researchers. It uses the Signal Protocol — a state-of-the-art end-to-end encryption system that has been independently audited, is open source, and is trusted by cryptographers worldwide. This guide covers not just installation, but every security-relevant feature and setting.

> **Why Signal and not WhatsApp?** WhatsApp uses the Signal Protocol for message encryption, but is owned by Meta (Facebook), subject to U.S. legal process, retains metadata (who you talk to and when), and has a troubled history of security vulnerabilities in its implementation. Signal's metadata collection is minimal by design, and it is operated by a nonprofit foundation with no commercial interest in your data.

---

## 1. Installation and Initial Security Setup

### 1.1 Download Signal Correctly

- **Android:** Download from the Google Play Store (signal.org/android/apk for a direct APK download without Play Store if needed)
- **iOS:** Download from the Apple App Store
- **Desktop:** Download only from signal.org — never from third-party sites

**Verify the download:** On signal.org, compare the checksum of the APK against the published checksum before installation. This protects against tampered downloads.

### 1.2 Phone Number Considerations

Signal requires a phone number for registration. This is a significant limitation for high-risk users:

- **Option 1 (Most users):** Use your real mobile number. Signal does not expose this number to people unless you specifically share it, but law enforcement subpoenas to Signal could reveal your number is registered (though Signal retains minimal data — see their transparency report).
- **Option 2 (Higher risk):** Register with a VOIP number (Google Voice, JMP.chat) for separation from your real number. JMP.chat over Tor is the most private option.
- **Option 3 (Highest risk):** Register with a prepaid SIM purchased with cash, activated over public Wi-Fi. Use this number only for Signal, never for any other purpose.

### 1.3 Registration Lock

**Enable immediately after installation:**

*Settings → Account → Registration Lock*

Registration Lock prevents anyone from re-registering your Signal number without your PIN — even if they obtain your SIM card (SIM swap attack). This is critical protection. Set a strong PIN and store it securely.

---

## 2. Critical Privacy Settings

Open *Settings → Privacy* and configure the following:

### 2.1 Phone Number Privacy
- **Who can see my phone number:** Set to "Nobody" or "My Contacts"
- **Who can find me by phone number:** Set to "Nobody"

*This prevents people from finding your account via your number, even if they have it.*

### 2.2 Disappearing Messages
- **Default Timer for New Chats:** Set a default disappearing message timer for all new conversations.
  - **Recommendation for most users:** 1 week
  - **Recommendation for high-risk communications:** 1 day or less
  - **For the most sensitive conversations:** 1 hour, with explicit agreement from the other party

*Disappearing messages protect you if your device is seized. Messages that no longer exist cannot be read.*

### 2.3 Read Receipts and Typing Indicators
- **Show Read Receipts:** Disable
- **Show Typing Indicators:** Disable

*These reveal behavioral patterns (when you read messages, when you are typing) that, while seeming minor, contribute to a surveillance picture.*

### 2.4 Link Previews
- **Generate Link Previews:** Disable

*Link previews require Signal to access the URL — this creates a record that the URL was accessed, potentially from your IP if not using a VPN.*

### 2.5 Screen Lock
- **Screen Lock:** Enable
- Set a timeout of 5 minutes or less

### 2.6 Screen Security
- **Screen Security (Android):** Enable — prevents Signal from appearing in the app switcher and disables screenshots within the app

### 2.7 Incognito Keyboard
- **Incognito Keyboard (Android):** Enable — prevents your keyboard app from learning and storing what you type in Signal

---

## 3. Individual Conversation Security

### 3.1 Safety Numbers Verification

Every Signal conversation has a "Safety Number" — a cryptographic fingerprint unique to your conversation with that specific person on their specific device.

**Why it matters:** If law enforcement or an attacker performs a man-in-the-middle attack (inserting themselves between you and your contact), the Safety Number will change.

**How to verify:**
1. Open a conversation → tap the contact's name → *Verify Safety Numbers*
2. Compare the safety number **in person** or through a separate secure channel (not through Signal — if it's compromised, a compromised confirmation is useless)
3. Mark as verified once confirmed

**When to re-verify:**
- If Signal notifies you that the safety number changed (this could mean the contact got a new device, reinstalled Signal, or — more concerning — someone else has their number)
- Before sharing highly sensitive information
- After any period of time where security has been in question

### 3.2 Note to Self

Use the "Note to Self" conversation as an encrypted personal notepad. Messages you send to yourself are end-to-end encrypted and disappear on your set timer. Use it to store:
- Temporary sensitive information that needs to be accessible briefly
- Notes from in-person meetings
- Legal contact information

### 3.3 Message Requests

If someone you haven't talked to before messages you, it appears as a "Message Request." You can accept or delete without the sender knowing you received the message. This prevents strangers from immediately knowing your account is active.

---

## 4. Group Security

Groups are the most complex security surface in Signal.

### 4.1 Group Administration

- **Admin Permissions:** Configure so that only admins can add new members and change group settings (*Group Settings → Permissions*)
- **Keep admin count small:** 2–3 admins maximum. More admins means more potential compromise points.
- **Review membership regularly:** Remove members who have left the organization or whose trust is uncertain
- **Group links:** Disable group links (*Group Settings → Group Link*) unless you are actively using them for a controlled recruitment push. An open group link can allow anyone with the link to join.

### 4.2 What Groups Do NOT Protect

Even in an end-to-end encrypted Signal group:
- **Any group member can screenshot or forward messages.** There is no technical prevention.
- **Any group member can reveal the group's existence and general membership.**
- **Group metadata** (that a group of a certain size exists, and that specific numbers are members) may be visible to Signal's servers in some configurations.
- **Large groups are inherently more likely to contain unvetted members.** Treat large groups as semi-public.

**Operational rule:** The group is only as secure as its least secure member. Do not share information in a group that you would not want the least-trusted member to have.

### 4.3 Group Segmentation

Follow the cellular model: maintain separate, small groups for each operational cell. Do not maintain one large group for all organizational business.

- **All-hands group:** Public-facing announcements, publicly known information, morale and community building
- **Cell-specific groups:** Operational discussion restricted to that cell's members
- **Leadership group:** Strategic coordination among core organizers
- **Legal group:** Includes lawyers and affected participants only; strictly need-to-know

---

## 5. Calls and Video

### 5.1 Signal Calls
- Signal voice and video calls are end-to-end encrypted
- On Android, you can enable *Relayed Calls* (*Settings → Privacy → Advanced → Always Relay Calls*), which routes call audio through Signal's servers instead of directly between devices. This hides your IP address from your contact at the cost of slightly higher latency. **Enable this for high-risk contacts.**

### 5.2 Group Calls
- Signal supports encrypted group calls for up to 50 participants
- The same rules apply as group chats — the call is only as secure as its least-secure participant

---

## 6. Sealed Sender

*Settings → Privacy → Advanced → Sealed Sender*

Sealed sender is a feature where the metadata about who is sending a message to whom is concealed even from Signal's servers. Enable "Allow from Anyone" to receive sealed-sender messages from contacts not in your list, and ensure you have it enabled for sending.

---

## 7. Note to Self: What Signal Cannot Protect Against

Signal encrypts message contents in transit and on your device. It cannot protect against:

- **Device compromise:** If your phone has malware or a zero-day exploit, an attacker can read your messages as you type them, regardless of encryption
- **Physical device access:** If your device is seized and your passcode is obtained, all messages that have not yet disappeared are accessible
- **Participant betrayal:** Signal is a tool, not a vetting system. A person who has legitimate access to a conversation can always reveal its contents
- **Endpoint metadata:** Signal cannot hide that you are using Signal (your ISP and network operators can see connections to Signal's servers, though not the contents)
- **Operational mistakes:** Saying the wrong thing to the wrong person, using Signal on an otherwise insecure device

---

## 8. Signal for Desktop

Signal Desktop is useful for typing longer messages and coordinating from a computer. Security considerations:

- **Linked device:** Signal Desktop is a secondary linked device — it shares your Signal identity and has access to all your messages
- **Physical security:** Your computer may be less secured than your phone; consider who has physical access to it
- **Screen lock:** Enable screen lock on the desktop app
- **Note:** If law enforcement seizes your computer, Signal Desktop messages are accessible if the computer is unlocked or the encryption is defeated. Disappearing messages apply equally.

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
