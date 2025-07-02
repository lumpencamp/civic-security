# Tails OS: An Anonymity Guide for Activists

## Introduction: The 'Why'

Tails OS is a complete operating system designed to protect your privacy and anonymity. Think of it as a secure, private bubble for your computer activities. It's designed to be run from a USB stick, not your computer's main hard drive.

For activists, Tails is a critical tool for two main reasons:

1.  **It leaves no trace:** When you use Tails on a computer, it runs entirely from the USB stick. Once you shut it down and remove the USB, it's almost impossible for someone to know what you did. It doesn't save files, browsing history, or passwords to the computer you're using.
2.  **It preserves anonymity:** All your internet connections are automatically forced through the Tor network. This hides your real location (IP address) and makes it extremely difficult for websites, internet providers, or surveillance agencies to track your online activity back to you.

In short, Tails helps you use the internet safely and privately, even on a computer you don't trust.

## The 'How': A Step-by-Step Setup Guide

To get started, you will need **two** separate USB sticks (at least 8GB each) and about an hour of your time.

### 1. Downloading Tails Safely

First, you need to download the official Tails software.

*   **Go to the official source:** Only download Tails from the official website: `https://tails.net`.
*   **Download the Image:** On the website, find the download page and get the USB image (a file ending in `.img`).
*   **Verify Your Download (Very Important!):** Verification is like checking the safety seal on a bottle of medicine. It confirms that the file you downloaded is the authentic, untouched version from the developers and hasn't been secretly modified by a third party to include malware.
    *   The Tails website provides easy-to-use verification tools, often a browser extension or a simple 'drag-and-drop' method. Follow their on-screen instructions carefully. **Do not skip this step.**

### 2. Creating a Bootable USB

Now you need to 'flash' the Tails image onto a USB stick. This process will erase everything on the USB, so make sure it's empty or you've backed up its contents.

We recommend using a tool called **Balena Etcher** because it's free and works on Windows, macOS, and Linux.

1.  **Download and install Balena Etcher:** Get it from `https://www.balena.io/etcher/`.
2.  **Open Etcher:** It has a simple three-step process.
3.  **Flash from file:** Click this and select the Tails `.img` file you downloaded and verified.
4.  **Select target:** Plug in your first USB stick and select it. **Double-check you are selecting the correct USB drive!**
5.  **Flash!:** Click the 'Flash!' button. It will take a few minutes to complete.

This first USB is your 'Tails Installer'. You will use it to create a final, more secure 'Tails USB'. The official Tails documentation guides you through this two-USB installation process, which adds another layer of security.

### 3. Booting into Tails

This can be the trickiest part because every computer is different.

1.  **Plug in your Tails USB stick** into the computer you want to use.
2.  **Restart the computer.**
3.  **Access the Boot Menu:** As the computer starts up, you need to press a specific key to open the 'Boot Menu'. This key is usually **F12, F2, ESC, or Delete**. The startup screen often briefly displays the correct key (e.g., "Press F12 for Boot Options").
4.  **Select the USB Drive:** From the menu, use your arrow keys to select the USB drive and press Enter.

If all goes well, you will see the Tails welcome screen. If it doesn't work, don't worry. Restart the computer and try a different key. If you're stuck, a quick web search for `"[Your Computer's Model] boot from USB"` will usually give you the answer.

## Persistent Encrypted Storage

By default, Tails forgets everything when you shut it down. This is great for anonymity, but sometimes you need to save things, like documents, Wi-Fi passwords, or browser bookmarks.

This is where **Persistent Encrypted Storage** comes in. It's an optional, encrypted space on your Tails USB stick where you can safely store your data. It's protected by a password you create.

**When should you use it?**
*   **Use it if:** You need to store files, settings, or software for ongoing work and you are confident you can keep the USB stick physically secure. It's convenient for saving research, secure messaging configurations, or a cryptocurrency wallet.

**When should you NOT use it?**
*   **Don't use it if:** There is a high risk that your USB stick could be lost or seized. The existence of a Persistent Storage volume proves that you are using Tails to store data, which could attract unwanted attention. In high-risk situations, it's safer to use Tails in its default 'amnesic' mode.

## Decision Flowchart: 'Should I Use Tails for This Task?'

Use this chart to help you decide if Tails is the right tool for what you need to do.

```mermaid
graph TD
    A[Start: I have a task to do] --> B{Is this task sensitive? (e.g., researching opponents, communicating with a journalist)};
    B -->|No| C[Use your regular computer or phone.];
    B -->|Yes| D{Do I need to hide the *fact* that I did this from someone with access to this computer?};
    D -->|Yes, absolutely| E[**Use Tails.** It leaves no trace on the machine.];
    D -->|No, not a concern| F{Do I need to hide my online identity/location (IP address)?};
    F -->|Yes| G[**Use Tails.** It forces all traffic through Tor.];
    F -->|No| H[Consider using Tor Browser on your regular OS. It's less secure than Tails but still anonymizes your browsing.];
```
