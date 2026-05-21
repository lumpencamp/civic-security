# Qubes OS Architecture: Xen Hypervisor Isolation

*Status: Enterprise Architecture Manual | Audience: Infrastructure Planners and High-Risk Targets*

## A Note on Desktop OS Choices

*   **For Beginners (Linux Mint / Ubuntu):** If you are currently using Windows or macOS and want a significant privacy upgrade without a steep learning curve, start by switching to a user-friendly Linux distribution like **Linux Mint** or **Ubuntu**. They are much less invasive than commercial operating systems.
*   **For High Security (Qubes & Tails):** If your threat model involves state-level adversaries or advanced surveillance, use Qubes OS (for daily, compartmentalized work) or Tails OS (for temporary, anonymous tasks).

---

Qubes OS does not rely on software sandboxing; it enforces security through bare-metal compartmentalization utilizing the Xen hypervisor. If a single application or domain is compromised by a zero-day exploit, the hypervisor guarantees that the infection cannot breach the hypervisor boundary to compromise other domains or the host hardware.

This manual details the step-by-step configuration of a hardened, multi-layered Xen domain infrastructure optimized for civic operations.

## 1. Network Topography: The Edge Domains

Network stacks are historically the most vulnerable attack surfaces. Qubes mitigates this by completely isolating the network hardware from the firewall, and the firewall from your operational applications.

*   **`sys-net` (Hardware Interface):** This AppVM has exclusive PCI passthrough access to your Wi-Fi and Ethernet controllers. It is inherently untrusted. If a malicious Wi-Fi driver exploits your network card, the attacker only gains access to `sys-net`, not your personal data.
*   **`sys-firewall` (Traffic Controller):** This AppVM sits behind `sys-net`. It contains no user data and has no direct hardware access. It strictly enforces `iptables` rules, governing which operational VMs are permitted to connect to `sys-net`.

## 2. Anonymous Routing: The Whonix Gateway/Workstation Pair

For high-risk OSINT research or whistleblower communications, standard VPNs are insufficient. You must implement a Tor-enforced architecture utilizing the Whonix template pair.

1.  **`sys-whonix` (The Gateway):** This ServiceVM connects directly to `sys-firewall`. Its sole cryptographic function is to force all incoming traffic through the Tor network. It is entirely ignorant of the user applications generating the traffic.
2.  **`anon-whonix` (The Workstation):** This AppVM connects *only* to `sys-whonix`. It contains your Tor Browser and operational files. Because it has no direct connection to `sys-firewall` or `sys-net`, it is physically impossible for an exploit inside `anon-whonix` to leak your true IP address.

## 3. Discardable Architecture: The Untrusted DispVM

Never open an untrusted attachment (PDF, Word Doc, image) sent from an unverified source in a persistent operational VM.

*   **Deployment:** Create a Disposable Virtual Machine (DispVM) template. When you open a downloaded file in an untrusted VM, right-click and select **View in DispVM**.
*   **Mechanics:** The Xen hypervisor instantiates a brand new, isolated VM in RAM, opens the document, and destroys the entire VM the moment you close the window. Any embedded malware or tracking pixels are instantly wiped from existence along with the DispVM.

## 4. The Air-Gapped Vault: Root Key Management

Your master PGP keys, cryptocurrency seeds, and password databases must never touch an internet-connected domain.

*   **`vault` (The Offline Enclave):** Create an AppVM based on a minimal Debian or Fedora template.
*   **Configuration:** Under the VM Settings, set **NetVM** to `none`. This severs the virtual ethernet cable.
*   **Usage:** Generate your PGP keys and store your KeePassXC database exclusively within this vault. You will pass encrypted data *out* of the vault, but the private keys never leave.

## 5. Secure Inter-VM Protocols (`qvm-copy` / `qvm-move`)

Because the hypervisor completely isolates your domains, you cannot drag-and-drop files or use a standard shared clipboard. This prevents malware from laterally migrating across your system.

*   **Clipboard Protocol:** To copy a password from your `vault` to a web browser in `personal`:
    1.  Highlight the text in `vault` and press `Ctrl+C`.
    2.  Press `Ctrl+Shift+C` to instruct the hypervisor to securely move the data to the global clipboard.
    3.  Select the `personal` VM window and press `Ctrl+Shift+V` to pull the data from the global clipboard.
    4.  Press `Ctrl+V` to paste the text into the browser.
*   **File Transfer Protocol:** To move an encrypted document from `work` to `sys-whonix` for transmission:
    1.  Open Dom0 terminal or use the GUI file manager.
    2.  Execute: `qvm-copy-to-vm [DestinationVM] [filename]` (e.g., `qvm-copy-to-vm anon-whonix manifest.pdf`).
    3.  The hypervisor will intercept the file, prompt you for explicit authorization, and securely inject it into the `QubesIncoming` directory of the target VM.

_Last Updated: 2026_
