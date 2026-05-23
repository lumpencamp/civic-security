# Mullvad VPN: Commercial Optimization and Kill-Switch Implementation

*Status: Network Security Hardening Manual | Audience: Activists and Privacy-Conscious Users*

A VPN does not provide anonymity; it provides privacy by shifting trust from your Internet Service Provider (ISP) to the VPN company. As a network security engineer, I recommend Mullvad because it is one of the few commercial entities architected from the ground up to minimize data collection, allowing you to establish a truly private tunnel.

This manual details the technical configuration required to deploy Mullvad securely against ISP-level dragnet surveillance and traffic analysis.

*For a deep dive into the threats posed by mass surveillance, read Mullvad's [Total Surveillance Manifesto (PDF)](https://mullvad.net/pdfs/Total_surveillance.pdf).*

---

## 1. Anonymous Account Generation and Funding

Most VPN providers demand your email address, billing name, and credit card, immediately linking your real identity to your VPN traffic.

*   **The Mullvad System:** Mullvad requires zero personal data. When you sign up, the system generates a random 16-digit account number. That number *is* your account. There are no passwords or emails to hack or subpoena.
*   **Funding (The OPSEC Protocol):**
    *   *Standard Security:* Pay via an anonymized, prepaid gift card or Monero (XMR). Do not use Bitcoin, PayPal, or your personal credit card.
    *   *Maximum Security:* Write your 16-digit account number on a piece of paper, place physical cash in an envelope, and mail it directly to Mullvad headquarters in Sweden. This creates a complete disconnect between your financial identity and your network traffic.

## 2. WireGuard Deployment and Kill-Switches

OpenVPN is robust, but WireGuard is the modern standard—it is faster, uses less battery, and has a significantly smaller cryptographic attack surface.

### Protocol Configuration
1.  Open the Mullvad app. Navigate to **Settings > VPN settings**.
2.  Change the **Tunnel protocol** from Automatic to **WireGuard**.

### The Hard-Coded Kill-Switch (Lockdown Mode)
A kill-switch is useless if it only activates *after* the VPN app crashes, allowing your real IP to leak for several seconds. You must enforce a hard kill-switch at the OS level.

*   **Desktop Configuration:** In Mullvad Settings, enable **Lockdown mode**. This alters your system's firewall rules so that your computer *cannot* connect to the internet unless the Mullvad tunnel is active.
*   **Android Configuration:**
    1.  Go to your Android **Settings > Network & internet > VPN**.
    2.  Tap the gear icon next to Mullvad VPN.
    3.  Toggle **Always-on VPN** and **Block connections without VPN** to **ON**. This enforces a strict OS-level block against any non-tunneled traffic.

## 3. Multi-Hop Routing and Traffic Analysis Defense

Advanced adversaries monitor the size and timing of data packets entering a VPN server and leaving it, attempting to correlate the traffic and identify the user (Traffic Analysis).

### Configuring Multi-Hop
Routing your traffic through two separate VPN servers in different jurisdictions significantly complicates traffic analysis.

1.  In the Mullvad app, go to **Settings > VPN settings > WireGuard settings**.
2.  Enable **Enable multihop**.
3.  Choose an Entry Server (e.g., in Switzerland) and an Exit Server (e.g., in Iceland). Your traffic is encrypted twice: your ISP only sees a connection to Switzerland, and the destination website only sees traffic originating from Iceland.

*(Note: Multi-hop increases latency and reduces speed. Use only when necessary for elevated operational security).*

## 4. Private DNS Resolver Integration

Your ISP monitors every website you visit by logging your DNS (Domain Name System) requests. By routing DNS queries through Mullvad's encrypted resolvers, you blind your ISP.

1.  Navigate to **Settings > VPN settings > DNS filtering**.
2.  Enable **Block trackers**, **Block ads**, and **Block malware**.
3.  **The Advantage:** Mullvad uses its own DNS servers over the encrypted WireGuard tunnel. This prevents your ISP from harvesting your browsing history and blocks connections to known state-sponsored blocklists and telemetry trackers at the network level, before they even reach your browser.

_Last Updated: 2026_
