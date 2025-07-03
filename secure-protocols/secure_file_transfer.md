# A Detailed Guide to Secure File Transfer

Sharing files securely is a critical task for activists. Whether you are sending research to a collaborator or leaking documents to a journalist, you must protect the contents of the file and the identities of both the sender and the receiver. This guide covers two powerful, gold-standard tools for different scenarios.

---

### **Method 1: OnionShare (For Direct, Peer-to-Peer Sharing)**

**Use Case:** You need to send a file directly to a specific person you trust. You want the transfer to be secure, anonymous, and leave no trace on a third-party server (like Google Drive or Dropbox).

**How it Works:** OnionShare temporarily turns your computer into a secure, anonymous web server using the Tor network. The file is transferred directly from your machine to the recipient's, encrypted and anonymized by Tor. Once the transfer is complete, the server disappears.

#### **Step-by-Step Instructions:**

1.  **Install Prerequisites:** You must have the **Tor Browser** installed and running for OnionShare to connect to the Tor network. Download it from `torproject.org`.
2.  **Install OnionShare:** Download the official OnionShare application from `onionshare.org`.
3.  **Start the Share:**
    *   Open OnionShare and navigate to the "Share Files" tab.
    *   Drag and drop the file(s) you wish to share into the window.
    *   Uncheck the box "Stop sharing after files have been sent (uncheck to allow downloading multiple times)" if you want the link to be single-use. This is highly recommended.
    *   Click **"Start Sharing."**
4.  **Share the Secret Address:**
    *   OnionShare will generate a unique `.onion` address and a private key (password).
    *   **This is the most critical step.** You must transmit this address and key to your recipient through a secure, end-to-end encrypted channel, such as **Signal** or **Session**. Do NOT send this link via email or regular text message.
5.  **Recipient Downloads the File:**
    *   The recipient opens their Tor Browser and navigates to the `.onion` address you provided.
    *   They will be prompted for the private key to access the download page.
    *   Once they download the file, the share automatically stops (if you left the default setting checked), and the link becomes invalid.

---

### **Method 2: SecureDrop (For Anonymous Whistleblowing)**

**Use Case:** You are a source who needs to anonymously submit sensitive documents to a media organization or NGO without revealing your identity.

**How it Works:** SecureDrop is a system used by journalists to receive files from anonymous sources. The entire process is designed to protect the source's identity. You do not run SecureDrop; you use the one provided by the organization.

#### **Step-by-Step Instructions:**

1.  **DO NOT USE YOUR OWN COMPUTER OR HOME NETWORK.** This is non-negotiable for high-risk submissions. Go to a location with public Wi-Fi that is not associated with you (e.g., a library or coffee shop far from your home or work).
2.  **Use the Tails Operating System:** For maximum security, you should use the Tails OS, which runs from a USB stick and forces all connections through Tor, leaving no trace on the machine. See our Tails OS guide for more information.
3.  **Find the SecureDrop Address:** From a regular browser on a safe device, find the organization's official SecureDrop `.onion` address. They will list this on their public website. Write it down carefully.
4.  **Connect and Upload:**
    *   On your Tails OS machine at the public Wi-Fi location, open the Tor Browser and navigate to the `.onion` address you wrote down.
    *   Follow the on-screen instructions to upload your files.
5.  **Receive Your Codename:**
    *   After uploading, the system will generate a **unique, secret codename**. This is your only key to the submission. **Memorize it or write it down on a piece of paper you can keep securely offline.** Do NOT save it on any computer.
6.  **Check for Replies:**
    *   Wait several days. Then, using the **exact same secure method** (Tails OS, public Wi-Fi), navigate back to the SecureDrop address and log in with your secret codename. This will allow you to see if the journalist has left you a message.
