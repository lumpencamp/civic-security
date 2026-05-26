# Mullvad VPN: Privacy Hardening and Traffic Analysis Defense

> [!CAUTION]
> **OPERATIONAL SECURITY & LEGAL NOTICE**
> This guide is intended strictly for lawful, defensive, and educational purposes. Some tactics detailed below may carry legal risks depending on your local jurisdiction.
> - **Never** resist arrest or physically obstruct law enforcement.
> - **Never** engage in illegal RF jamming or property damage.
> - **Always** consult local legal defense networks (e.g., National Lawyers Guild) for jurisdiction-specific advice.

*Status: Network Security Hardening Manual | Audience: Activists and Privacy-Conscious Users*

A VPN does not provide anonymity — it provides privacy by shifting trust from your Internet Service Provider (ISP) to the VPN company. Mullvad is the gold-standard recommendation for activists because it was architected from the ground up to minimize data collection, accepts anonymous payment, and has pioneered open-source defenses against advanced traffic analysis that no other commercial VPN matches.

This manual covers the full security configuration: anonymous account setup, WireGuard + kill-switch, DAITA (Defense Against AI-guided Traffic Analysis), multi-hop routing, and encrypted DNS.

*For deeper context on mass surveillance, read Mullvad's [Total Surveillance Manifesto (PDF)](https://mullvad.net/pdfs/Total_surveillance.pdf).*

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

## 4. DAITA: Defense Against AI-guided Traffic Analysis

> [!IMPORTANT]
> DAITA is one of Mullvad's most significant security innovations and is unique among commercial VPNs. Enable it if you are at T2+ threat level or if concealing *that you are using a VPN* — or *what you are doing within it* — is important.

### 4.1 What Is AI-guided Traffic Analysis?

A VPN encrypts your traffic contents, but it cannot hide the **shape** of your traffic — packet sizes, timing patterns, and inter-arrival intervals. Sophisticated adversaries (T3–T4 tier: NSA, GCHQ, academic researchers working with law enforcement) use machine learning classifiers trained on millions of captured sessions to fingerprint what you are doing inside an encrypted VPN tunnel.

**Examples of what traffic analysis can reveal:**
- Which website you are visiting — even through HTTPS and a VPN — by matching the packet-size "fingerprint" of the page load against a trained database
- Whether you are using Signal, Tor, or other sensitive applications, even when that traffic is routed through a VPN
- Timing patterns that link your encrypted VPN session to activity visible on the other end of the tunnel (correlation attack)

This attack class is not theoretical. Academic research ("Website Fingerprinting Attacks and Defenses," WF research) has demonstrated 90%+ accuracy against naive VPN users.

### 4.2 How DAITA Works

DAITA uses a framework called **Maybenot** (open source, developed by Mullvad) to defeat fingerprinting attacks at the network level:

**Random Packet Padding:**
Every packet leaving your device is padded to a random size before encryption. This destroys the packet-size fingerprint that ML classifiers rely on. A 200-byte Signal message looks the same as a 1,400-byte web request because both are padded to indistinguishable random sizes.

**Dummy Traffic Injection:**
DAITA injects randomly timed dummy traffic between real packets. This breaks the timing patterns (inter-arrival intervals, burst structure) that correlation attacks exploit. The observer sees a constant, noisy stream — not the distinctive burst patterns of a webpage load or a video call.

**Why this is hard to defeat:**
Without knowing which packets are real and which are dummy, and without knowing the pre-padding sizes, a traffic analysis classifier cannot distinguish between different types of activity. The signal-to-noise ratio collapses.

### 4.3 How to Enable DAITA

**On Desktop (Windows/macOS/Linux):**
1. Open the Mullvad app
2. Go to **Settings → VPN settings → WireGuard settings**
3. Toggle **DAITA** to **ON**

**On Android:**
1. Open the Mullvad app
2. Tap the **settings cog** in the bottom navigation bar
3. Navigate to **VPN settings → WireGuard settings**
4. Toggle **DAITA** to **ON**

**On iOS:**
1. Open the Mullvad app
2. Tap **Settings** → **VPN settings**
3. Toggle **DAITA** to **ON** (available in Mullvad app version 2024.8+)

### 4.4 DAITA + Multi-Hop (Maximum Protection)

DAITA is most powerful when combined with multi-hop routing:

- **Without multi-hop:** DAITA protects the segment between your device and the Mullvad entry server. An adversary who can observe both the entry server's traffic and the exit server's traffic can still attempt correlation.
- **With multi-hop + DAITA:** DAITA obfuscates the traffic entering the first hop. The traffic between Mullvad's internal servers is not visible to external adversaries. This defeats even a partial network observer who controls some but not all of the path.

**Enable both simultaneously:**
- Multi-hop: **Settings → VPN settings → WireGuard settings → Enable multihop** → choose entry + exit servers
- DAITA: toggle ON in the same WireGuard settings menu

> [!NOTE]
> DAITA adds a modest overhead (5–15% more bandwidth used due to padding and dummy traffic; slight increase in latency). For most use cases this is imperceptible. Disable temporarily on very slow connections if performance is unacceptable, but re-enable for any sensitive operational work.

### 4.5 Threat Model Fit

| Threat | DAITA Helps? |
|--------|-------------|
| ISP seeing which sites you visit | ✅ Yes — with padding, fingerprinting fails |
| Law enforcement traffic correlation | ✅ Significantly harder |
| NSA-class global network observer (correlation attack) | ✅ Much harder when combined with multi-hop |
| Mullvad being served a subpoena | ❌ No — Mullvad has no logs, but DAITA doesn't change the legal exposure |
| Device-level malware reading traffic before encryption | ❌ No — VPN doesn't protect against device compromise |

---

## 5. Private DNS Resolver Integration

Your ISP monitors every website you visit by logging your DNS (Domain Name System) requests. By routing DNS queries through Mullvad's encrypted resolvers, you blind your ISP.

1.  Navigate to **Settings > VPN settings > DNS filtering**.
2.  Enable **Block trackers**, **Block ads**, and **Block malware**.
3.  **The Advantage:** Mullvad uses its own DNS servers over the encrypted WireGuard tunnel. This prevents your ISP from harvesting your browsing history and blocks connections to known state-sponsored blocklists and telemetry trackers at the network level, before they even reach your browser.

_Last Updated: May 2026_
