# Core OPSEC Principles: A Dynamic Workflow Compartmentalization Manual

*Status: Level 1 Directive | Audience: All Organizers — Read This First*

Operational Security (OPSEC) is not a checklist — it is an active, continuous state of defensive posture. It is the discipline of protecting sensitive information by identifying what data you generate, who wants it, and what they can do with it. This manual outlines the exact mechanics of identity compartmentalization, information flow control, and dynamic workflow management necessary to prevent cascading failure against adversaries at any tier.

> **The Golden Rule of OPSEC:** The strength of your security is determined by its weakest link. One person using WhatsApp in a Signal group, one photo uploaded with EXIF data, one unencrypted email to a lawyer — any of these alone can unravel an otherwise solid operational posture. OPSEC is a collective practice, not an individual one.

---

## 1. The Five-Step OPSEC Process

The U.S. military's classical OPSEC framework, adapted for civic use:

1. **Identify Critical Information (CI):** What information, if known by an adversary, would harm your organization? Names of participants, meeting locations, planned action dates, legal strategy, financial sources, internal conflicts.

2. **Analyze Threats:** Who wants your critical information? (See [Threat Modeling](./threat_modeling_guide.md).) What are their collection capabilities?

3. **Analyze Vulnerabilities:** Where does your critical information leak? Social media posts, phone metadata, credit card transactions, overheard conversations, digital device data.

4. **Assess Risk:** For each vulnerability, calculate likelihood × impact. Focus your effort on HIGH and CRITICAL risks first.

5. **Apply Countermeasures:** Implement specific, actionable protections. Reassess continuously.

---

## 2. Identity Compartmentalization (The "Air Gap" Principle)

The fundamental rule of modern OPSEC is the **strict, permanent separation of personas**. Your personal identity (true name, family, employment, home address) must never intersect with your operational identity (alias, network, operations). A single intersection creates an immutable link that retroactive analysis can exploit.

### 2.1 Hardware Separation

**Rule:** Never use personal devices for organizational operations.

**Why it matters:** Device identifiers (IMEI, serial number, MAC address, advertising ID) are permanent and unique. Wi-Fi and Bluetooth radios broadcast these identifiers passively. Your personal phone connects to cell towers near your home, workplace, gym — building a precise pattern-of-life map. If that device appears at a restricted location, your identity is linked to it.

**Implementation:**
- Procure "clean" operational devices (phones, laptops) using untraceable cash at a physical store. Do not order online — shipping records link your address.
- These devices must **never** connect to your home Wi-Fi network. Even connecting to establish VPN compromises the device's location history.
- Do not pair operational devices with personal Bluetooth accessories (earbuds, keyboards, fitness trackers).
- Store operational devices in Faraday bags when not in active use. This prevents passive cellular polling, Stingray capture, and over-the-air exploits. Quality Faraday bags: Silent Pocket, Mission Darkness.
- Do not charge operational devices at home using chargers that remain plugged in (smart power strips can log energy use patterns).

### 2.2 IP Address and Network Separation

**Rule:** Never allow operational traffic to share the same IP footprint as personal traffic.

**Why it matters:** Your home IP address is registered to your ISP account under your legal name and billing address. Every website, service, and platform you access logs this IP. If you log into an operational account from your home IP even once, that account is permanently linked to your identity through ISP subpoena records.

**Implementation:**
- All operational devices must route exclusively through anonymizing networks. In ascending order of anonymity: **VPN only** → **VPN + Tor** → **Tor only** → **Tails OS + Tor**.
- VPNs alone are insufficient for T2+ adversaries: your VPN provider can be subpoenaed. Use providers with strong no-log policies, offshore jurisdiction, and a proven track record of resisting legal demands (Mullvad is the current gold standard).
- Use public Wi-Fi far from your residence or regular locations for any operational activity that cannot be done over Tor. Rotate locations; do not return to the same café repeatedly.
- Never log into an operational account from a personal IP, and never log into a personal account from an operational device/IP. A single intersection creates an immutable cryptographic link in platform logs that retroactive analysis will find.
- For the highest sensitivity, use **Tails OS** booted from USB on a non-personal machine. Tails routes all traffic through Tor by default and leaves no trace on the host machine.

### 2.3 Account and Identity Separation

**Rule:** Every operational account must be created and maintained exclusively from operational devices and IPs.

**Implementation:**
- Create operational email accounts using a privacy-respecting provider (Proton Mail, Tutanota) over Tor or a clean VPN, not linked to any personal recovery information.
- Use a unique username for each platform that does not reflect your real name, location, or any other persistent identifier.
- Do not reuse usernames across platforms. Reused usernames are trivially cross-referenced using OSINT tools.
- Never provide a real phone number for account recovery. Use a VOIP number (JMP.chat over Tor, MySudo) or skip phone verification entirely where possible.
- Do not link operational accounts to any personal payment method. Use privacy.com virtual cards funded by cash-purchased gift cards, or Monero for maximum privacy.

### 2.4 Behavioral Separation (Pattern-of-Life)

**Rule:** Your operational alias must exhibit a distinct "Pattern of Life" (PoL) from your true identity.

**Why it matters:** Even without direct identification, behavioral analysis can de-anonymize you. If you always post online between 9 PM and 1 AM in U.S. Central time, write in American English with specific idiosyncratic spellings, and your true-name accounts go silent precisely when your alias is active — these correlations are statistically significant.

**Implementation:**
- **Writing style:** Alter vocabulary, avoid signature phrases, adjust grammar patterns. AI writing assistants can help, but also introduce their own patterns. Practice before deployment.
- **Activity timing:** Do not access operational accounts exclusively during the hours your personal accounts are inactive. Introduce deliberate noise.
- **Topic correlation:** Do not discuss operational topics on personal accounts even obliquely. "Can't say much, but something big is happening" is a leak.
- **Geographic:** Avoid posting photos or checking in at locations that, combined with your posting time, could triangulate your location.

---

## 3. Dynamic Workflow Compartmentalization

Operations must be divided into independent, non-overlapping cells based on strict **need-to-know** access control. This is not bureaucratic obstruction — it is the fundamental architecture that prevents a single compromise from destroying the entire organization.

### 3.1 The Cellular Structure

**Structure:** Organize into discrete cells (e.g., Logistics, Communications, Legal, Outreach, Direct Action). Members of one cell know only the identities of members in their own cell and a single, designated liaison to adjacent cells.

**Rationale:** If a Logistics cell member is arrested and their device is seized, the extracted information compromises only the Logistics cell. The Action cell remains intact. Without this structure, any single arrest exposes the entire network.

**Implementation:**
- Cells of 4–7 people are optimal. Smaller cells are more secure; larger cells become unmanageable and leak-prone.
- Liaisons between cells must be your most experienced, security-trained members.
- Operational decisions that require cross-cell coordination happen through liaisons only, never through direct cross-cell communication.
- Document nothing that doesn't need to be documented. If a decision can be made verbally in-person and executed without a paper trail, prefer that.

### 3.2 The Need-to-Know Principle

**Rule:** No one receives information beyond what they require to perform their specific task.

**Common violations to avoid:**
- Sharing full participant lists when task-specific subgroups would suffice
- CC'ing everyone on emails that concern only a subset
- Posting action details in a general channel instead of a specific, role-appropriate channel
- Verbally sharing information "just to keep people in the loop"

**Implementation:**
- Maintain separate Signal groups for each cell. The general all-hands group receives only information that all members need.
- Legal and medical information (participant arrest records, health conditions) is strictly need-to-know, held only by the designated legal/medical coordinator.
- Financial information (donor identities, bank accounts) is need-to-know at the organizational treasury level only.

### 3.3 Information Classification

Apply a simple classification framework to all organizational information:

| Level | Label | Definition | Handling |
|-------|-------|-----------|----------|
| 0 | **Public** | Intentionally published; anyone can know | Social media, flyers, press releases |
| 1 | **Internal** | For members generally; not sensitive | General Signal group, internal wiki |
| 2 | **Sensitive** | Restricted to relevant cell; exposure causes disruption | Cell-specific Signal group, need-to-know verbal |
| 3 | **Critical** | Core operational security; exposure causes significant harm | In-person only, no digital record, specific liaisons |

---

## 4. Counter-Intelligence: Detecting and Managing Infiltration

Every significant civic organization should assume the possibility of infiltration. This is not paranoia — it is historical fact documented through FOIA releases (COINTELPRO, files on environmental groups, anti-war organizations, Black Lives Matter chapters).

### 4.1 Behavioral Indicators of a Potential Informant

No single indicator is definitive. Patterns of multiple indicators warrant investigation:
- Consistently pushes for escalation to tactics that would generate serious criminal charges
- Asks unusually detailed questions about operational specifics, timelines, or participant identities that are not relevant to their role
- Arrived without a verifiable social trust network (no one can independently vouch for them)
- Resists security protocols, frames privacy as paranoia or elitism
- Has unexplained financial resources inconsistent with stated background
- Immediately seeks positions of authority or access to sensitive information
- Is frequently unavailable or has vague explanations for absences
- Subtly creates division between key organizers

### 4.2 The Vouching System

**Implementation:**
- New participants in sensitive spaces require **personal vouching by two existing trusted members** who can independently verify the person's identity and history.
- Vouching carries responsibility: if someone you vouched for turns out to be an informant, your judgment is questioned.
- Maintain a probationary period for new members: full participation in public activities, restricted participation in sensitive operational discussions until trust is established.
- Never vouch for someone you know only online.

### 4.3 The Canary Trap (for suspected leaks)

If you suspect a specific person is the source of leaks but cannot confirm, use a controlled information test:
1. Provide subtly different versions of a non-critical piece of operational information to each suspect individually.
2. Monitor whether that specific variant surfaces externally (in police activity, press reports, or adversarial online posts).
3. The variant that surfaced identifies the source.
4. **Caution:** Execute this only with experienced leadership. False positives destroy trust and can be used against innocent members.

### 4.4 When You Confirm an Infiltrator

- **Do not confront them immediately.** Confrontation tips them off, potentially alerting their handlers and triggering increased surveillance.
- **Assess the damage:** What did they have access to? What may be compromised?
- **Consult legal counsel immediately.** Your lawyer can advise on how to proceed in a way that doesn't create additional legal exposure.
- **Quietly limit their access** while the situation is assessed.
- **After full assessment and legal consultation**, make an organizational decision about disclosure and next steps.

---

## 5. Secure In-Person Meetings

Digital security is irrelevant if your physical meetings are surveilled or your conversations are recorded.

### 5.1 Location Selection
- Never meet in the same location repeatedly for sensitive discussions. Rotate.
- Avoid locations with surveillance cameras at entry points, or arrive/depart in ways that avoid facial recognition capture.
- Private residences are generally safer than commercial venues (no surveillance cameras, no staff as potential witnesses). Trade off against ALPR/CCTV capturing vehicle license plates en route.
- Outdoor locations (parks, woods) defeat audio recording but introduce other surveillance risks (aerial observation, long-range directional microphones). Assess accordingly.
- Never conduct sensitive conversations in vehicles: modern vehicles have multiple microphones, Bluetooth radios, and cellular chips that can be exploited remotely.

### 5.2 Device Policy at Sensitive Meetings
- **Phones off and in Faraday bags, or left in vehicles.** "Airplane mode" is insufficient: it disables network connections but does not disable all radios, and it can be toggled on by exploits. Physical separation is required.
- Conduct a sweep for unfamiliar electronic devices in the space before beginning.
- Instruct participants not to bring smart watches, fitness trackers, or smart home devices.
- If recording the meeting for organizational memory, use a dedicated recorder on airplane mode, stored encrypted, and explicitly approved by all participants.

### 5.3 Audio Countermeasures
- White noise machines placed near doors and windows dramatically reduce the effectiveness of directional microphones and contact microphones on glass.
- Do not hold sensitive conversations near windows (glass vibration can be read by laser microphones from significant distances).
- Speak at normal volume; whispering and covering your mouth reads as suspicious on surveillance video and does not defeat sophisticated audio capture.

---

## 6. Digital Hygiene Fundamentals

### 6.1 The Minimal Footprint Principle
Generate the minimum necessary data to accomplish each task. Data you never create cannot be seized, subpoenaed, or leaked. Specifically:
- Delete operational messages after they are actioned (use Signal's disappearing messages)
- Do not take photographs at sensitive meetings
- Do not use cloud sync for operational files
- Delete browser history, cookies, and local storage after every session on operational devices
- Remove apps you are not actively using

### 6.2 Software Updates
Unpatched software is the most common attack surface exploited by both commercial hackers and law enforcement digital forensics. Enable automatic updates on all devices. There is no security advantage to running old software versions.

### 6.3 Application Permissions Audit
Conduct a monthly audit of app permissions on all devices:
- Revoke location access from all apps that do not require it to function
- Revoke microphone and camera access from all apps that do not require it
- Delete apps with broad permissions that have no operational justification (Facebook, TikTok, commercial weather apps — all have documented histories of broad data collection)

### 6.4 Browser Security
- Use **Firefox** with **uBlock Origin** for operational browsing. Configure "Enhanced Tracking Protection" to Strict mode.
- For maximum anonymity, use the **Tor Browser** — it routes through Tor, standardizes fingerprinting, and blocks JavaScript by default.
- Never use Chrome for sensitive operational work. Chrome is a data collection instrument for Google.
- Use separate browser profiles (or separate browsers entirely) for operational and personal browsing.
- Consider **Brave** as a middle-ground for everyday use, but do not use it as a substitute for Tor when anonymity is required.

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
