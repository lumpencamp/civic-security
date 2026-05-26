# Tor Browser: Anonymous Browsing and Onion Services

*Status: Level 2 | Audience: Organizers handling sensitive research, journalists, and high-risk users*

Tor (The Onion Router) is a free, open-source anonymity network that routes your internet traffic through three volunteer-operated nodes (relays), encrypting it at each hop. It was originally developed by the U.S. Naval Research Laboratory and is now maintained by the Tor Project, a nonprofit organization. Tor is used by journalists, activists, human rights workers, whistleblowers, law enforcement, and millions of ordinary people worldwide.

> **Tor is not a VPN.** A VPN replaces your ISP as the entity that can see your traffic and real IP address. Tor provides much stronger anonymity by ensuring no single node knows both who you are and what you are accessing. No node in the Tor network knows the full picture.

---

## 1. How Tor Works

### 1.1 The Three-Hop Circuit

When you use Tor, your traffic is:

1. **Encrypted in three layers** on your device
2. **Sent to the Guard/Entry node:** Knows your real IP address but not your destination
3. **Forwarded to the Middle node:** Knows neither your IP nor your destination
4. **Forwarded to the Exit node:** Knows your destination but not your real IP
5. **Sent to the destination website**

No single node has the complete picture. An adversary would need to simultaneously control your entry node and observe your destination traffic to de-anonymize you — this is the "traffic correlation attack" and represents Tor's primary practical limitation.

### 1.2 What Tor Protects Against

- **Your ISP** seeing which websites you visit
- **Websites** seeing your real IP address and location
- **Network-level observers** (on public Wi-Fi, your employer's network) seeing your destinations
- **T1–T2 level surveillance** that relies on IP-based identification

### 1.3 What Tor Does NOT Protect Against

- **Traffic correlation by a global adversary:** The NSA and similar agencies have the capability to observe traffic at the entry and exit nodes simultaneously and perform statistical correlation to de-anonymize users. This is the most serious practical limitation.
- **Malware on your device:** If your device is compromised, Tor does not protect you
- **Deanonymization through your behavior:** Logging into your personal Gmail in the Tor Browser immediately de-anonymizes your session
- **Exit node interception of unencrypted traffic:** The exit node can see unencrypted HTTP traffic. Always use HTTPS when using Tor.
- **Browser fingerprinting if you modify the Tor Browser:** The Tor Browser is specifically designed to make all users look identical. Adding extensions, changing settings, or enabling JavaScript on sensitive sites reduces this protection.

---

## 2. Installing and Using the Tor Browser

### 2.1 Download and Verification

**Critical:** Only download Tor Browser from the official Tor Project website: **torproject.org**

Verify the download signature:
1. Download the browser package and the corresponding .asc signature file from torproject.org/download
2. Import the Tor Project signing key: `gpg --keyserver keys.openpgp.org --search-keys "Tor Browser Developers"`
3. Verify: `gpg --verify tor-browser-linux64-XX_en-US.tar.xz.asc tor-browser-linux64-XX_en-US.tar.xz`
4. The output should show "Good signature from Tor Browser Developers"

If you cannot verify signatures, consider using an alternative download method such as Tor Browser in Tails OS (where it is pre-installed and pre-verified).

### 2.2 Security Level Configuration

The Tor Browser includes a "Security Level" setting that controls how much JavaScript and active content is allowed. Higher = more secure but potentially breaks some websites.

*In Tor Browser → Shield icon (top right) → Advanced Security Settings*

| Level | JavaScript | Use Case |
|-------|-----------|----------|
| Standard | Enabled | General browsing where anonymity is goal but not critical |
| Safer | Partially disabled | Research, journalism, activist communications |
| Safest | Disabled | Sensitive document access, whistleblowing, high-risk research |

**Recommendation for high-risk use:** Set to Safest. If a site requires JavaScript, evaluate whether you need to access it and whether there is a safer alternative.

### 2.3 Critical Operational Rules

**Never do the following in the Tor Browser:**
- Log into personal accounts (Google, Facebook, your real email) — this immediately de-anonymizes your session
- Open documents downloaded through Tor in other applications (especially PDFs and .docx files) — these can make network requests that bypass Tor
- Use BitTorrent over Tor — it defeats Tor's protections and harms the network for others
- Install additional browser extensions — they change your fingerprint and may introduce vulnerabilities
- Resize the browser window — window size is part of browser fingerprinting; Tor Browser opens at a standard size for this reason

**Always do:**
- Use HTTPS — look for the padlock icon. Tor Browser includes HTTPS Everywhere by default.
- Close the browser when done — this clears all session data
- Connect to the Tor Network before launching — if you need to use Tor and it's blocked in your country, configure a bridge first (see Section 4)
- Generate a new circuit for important tasks: *Tor icon in URL bar → New Circuit for This Site*

---

## 3. .Onion Services

.Onion services (also called "hidden services") are websites accessible only through Tor that have their own anonymity — the server's location is concealed, just as the user's location is.

### 3.1 Why Use .Onion Services

- **Both parties are anonymous:** Unlike regular websites accessed through Tor, .onion services hide the server's IP in addition to your IP
- **End-to-end encryption:** Traffic between you and the .onion service is encrypted within the Tor network, with no exit node that can observe it
- **Censorship resistance:** .Onion services cannot be blocked by a country's internet filter (though access to Tor itself can be restricted)

### 3.2 Key .Onion Services

**Secure journalism and whistleblowing:**
- **SecureDrop:** The standard platform for secure communication with media organizations. Most major news outlets have a .onion SecureDrop address. Access via their public websites.
- **DDoSecrets** (Distributed Denial of Secrets): Archive of leaked documents from governments and corporations — ddosecretspzwfy7bk6vmvyxky5xxlhqo4mfn2dzdmxktvgjzovqd.onion

**Search and reference:**
- **DuckDuckGo Onion:** duckduckgogg42xjoc72x3sjasowoarfbgcmvfimaftt6twagswzczad.onion
- **Ahmia:** Search engine for .onion sites — ahmia.fi (clearnet) or through DuckDuckGo .onion

**Communications:**
- **Proton Mail (Onion):** protonmailrmez3lotccipshtkleegetolb73fuirgj7r4o4vfu7ozyd.onion

### 3.3 .Onion Address Safety

Not all .onion sites are legitimate. Verify .onion addresses through the official clearnet websites of trusted organizations — do not use .onion addresses found through random searches or unverified sources.

---

## 4. Tor Bridges: Bypassing Censorship

If Tor is blocked in your country or network, bridges are unpublished Tor relays that circumvent blocks.

**Obtaining bridges:**
1. From torproject.org/bridges
2. By emailing bridges@torproject.org (from a Gmail or Riseup address)
3. Via the Tor Browser: *Connection Settings → Use a bridge → Request a bridge from Tor Project*

**Bridge types:**
- **obfs4:** The current standard; obfuscates traffic to look unlike Tor
- **Snowflake:** Routes traffic through WebRTC, making it look like video conferencing traffic
- **meek-azure:** Routes traffic through Microsoft Azure, making it look like legitimate cloud traffic

---

## 5. Tor on Mobile

### 5.1 Orbot (Android)

Orbot is the official Tor app for Android (from the Guardian Project). It can:
- Provide a Tor proxy for all apps on the device (with VPN mode)
- Route specific apps through Tor (selective routing)
- Integrate directly with Signal for metadata protection

**Setup:**
1. Install Orbot from Google Play or F-Droid (F-Droid is preferred for security-conscious users)
2. Tap *Start* to connect to Tor
3. Enable *VPN Mode* to route all device traffic through Tor (battery-intensive but thorough)
4. Or, use *Tor-Enabled Apps* to route only specific apps

**Signal + Orbot:**
In Signal: *Settings → Privacy → Advanced → Use proxy → SOCKS proxy → 127.0.0.1:9050*

This routes Signal's traffic through Tor, concealing from your ISP that you are using Signal at all.

### 5.2 Tor Browser for Android

The official Tor Browser app is available for Android from the Play Store or from torproject.org. Provides the same protections as the desktop version.

### 5.3 iOS Limitations

Apple's App Store policies prevent any app from routing all system traffic through Tor (VPN-mode equivalent). On iOS:
- **Onion Browser** (from Mike Tigas, endorsed by Tor Project): A Tor-connected browser. Similar to Tor Browser for Android.
- Limitation: Only browser traffic is anonymized; other apps are not routed through Tor

---

## 6. Tor + VPN Combinations

### 6.1 VPN → Tor (VPN then Tor)

Connect to VPN first, then use Tor.

**Advantages:**
- Your ISP sees VPN traffic, not Tor traffic — hides that you are using Tor from your ISP
- Protects against malicious entry nodes (your VPN IP is the entry, not your real IP)

**Disadvantages:**
- Your VPN provider can see that you're using Tor (but not what you're doing on Tor)
- You must trust your VPN provider

**Best for:** Situations where you need to hide Tor usage from your ISP while maintaining strong anonymity on the destination end.

### 6.2 Tor → VPN (Tor then VPN)

Use Tor to connect to a VPN, so the VPN appears as your exit IP.

**Advantages:**
- Your destination sees a VPN IP, not a Tor exit node IP (some sites block Tor exit nodes)
- Prevents exit node traffic analysis

**Disadvantages:**
- Complex to set up correctly
- VPN provider can see your traffic (they see the decrypted traffic from the Tor exit)
- Defeats much of Tor's purpose by centralizing trust in the VPN

**Generally not recommended** unless you have a specific reason to need a VPN IP at the destination.

---

*This guide does not constitute legal advice. Using Tor is legal in most countries but may attract attention in some jurisdictions. Know your local legal context.*

[← Back to Index](../index.md)
