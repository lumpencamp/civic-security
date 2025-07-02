# Guide: Secure File Transfer

### **OnionShare**
OnionShare is a tool for securely and anonymously sharing files of any size. It works by starting a web server on your computer, making it accessible as a Tor onion service, and generating an unguessable URL to access the files.

1.  **Install:** Download OnionShare from the official website.
2.  **Share Files:** Drag and drop the files you want to share into OnionShare. Click "Start Sharing."
3.  **Send the Link:** It will generate a `.onion` address. Securely send this address to the recipient. They will need the Tor Browser to open it and download the files. The transfer is direct from your computer to theirs, encrypted and anonymized by Tor.

### **SecureDrop**
SecureDrop is an open-source whistleblower submission system that media organizations use to securely accept documents from anonymous sources. You don't run SecureDrop yourself; you use it to submit information to journalists.

*   **How it Works:** A source uses the Tor Browser to access the organization's SecureDrop `.onion` address. They can upload files and receive a unique codename. They can use this codename to log back in later to check for messages from the journalist. The entire process is anonymous and encrypted.
