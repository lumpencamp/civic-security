# Advanced Threat Modeling for Civic Organizations

*Status: Level 2 Directive | Audience: Operations Planners and Security Teams*

Threat modeling is not paranoia — it is the calculated, objective assessment of your operational environment. This framework adapts corporate security methodologies (STRIDE, PASTA, and DREAD) into an actionable, quantitative model specifically for non-state actors, activists, and civic organizations.

> **Core Rule:** Never prepare for a higher-tier adversary than the one you actually face. Over-engineering your security creates operational paralysis, burns out participants, and isolates potential supporters. Under-engineering it gets people arrested, doxxed, or harmed. Calibrate precisely.

---

## 1. Adversary Profiling: The Threat Tiers

To defend effectively, you must understand your adversary's **capabilities**, **budget**, **legal authorizations**, and **political constraints**. Each tier requires a qualitatively different defensive posture.

### T1: The Noise (Doxxers, Trolls, Harassment Networks)
*   **Examples:** Far-right forums (4chan, Telegram channels), counter-protest groups, stalkers, opportunistic harassers.
*   **Capabilities:**
    - Open-Source Intelligence (OSINT): Google dorking, reverse image search, LinkedIn/Facebook scraping, data broker aggregation
    - Social engineering (phishing calls, fake accounts)
    - Physical presence at public events
    - Platform-level attacks: mass account reporting, review bombing
    - Swatting (false emergency calls to dispatch armed police to your location)
*   **Limitations:** No legal authority, no guaranteed funding, generally low technical sophistication, subject to civil lawsuits, vulnerable to counter-OSINT
*   **Primary Countermeasures:** Data broker opt-outs, pseudonymous public presence, private social accounts, disciplined information hygiene, community early warning networks

### T2: Local Law Enforcement (Police, Sheriffs, Regional Fusion Centers)
*   **Examples:** Municipal police, county sheriffs, joint terrorism task forces (JTTFs), DEA, fusion centers like Chicago CLOCC.
*   **Capabilities:**
    - Arrest and detention authority
    - Physical surveillance (tails, fixed observation posts)
    - Cell-Site Simulators (CSS/IMSI catchers, "Stingrays"): Capture IMEI/IMSI numbers and intercept unencrypted SMS within a geographic radius
    - Automated License Plate Readers (ALPRs): Real-time and retroactive location tracking
    - Facial recognition databases (often with low accuracy thresholds and racial bias)
    - Access to commercial data brokers: location data, social graphs, purchase history
    - Subpoena power for domestic technology companies (Google, Apple, Meta, Verizon)
    - Confidential informants embedded in activist communities
    - National Crime Information Center (NCIC) database queries
    - Tower dump requests: all devices connected to a cell tower in a time window
*   **Limitations:** Bureaucratic friction, chain of command, budget constraints, geographic jurisdiction boundaries, civil rights litigation risk, public accountability (body cameras, FOIA)
*   **Primary Countermeasures:** Encrypted communications (Signal), device lockdown, counter-surveillance training, facial concealment, legal observer networks, know-your-rights training, Faraday bags, no personal devices at actions

### T3: Corporate Intelligence (Private Security Firms, Industry Groups)
*   **Examples:** Pinkerton (now Securitas), Kroll, Guidepost Solutions, industry-funded "threat intelligence" firms like TigerSwan (Dakota Access Pipeline surveillance).
*   **Capabilities:**
    - Deep financial resources, often funded by corporations or industry associations
    - Infiltration via professional-quality informants with sustained identities
    - Advanced OSINT tools (Palantir, Maltego, ShadowDragon)
    - Surveillance of financial flows and nonprofit filings
    - Strategic litigation (SLAPP suits) to bankrupt and silence organizations
    - Coordinating with or hiring off-duty law enforcement officers
    - Media manipulation and disinformation campaigns
    - Background investigations on organizers' employers, families, associates
*   **Limitations:** No direct arrest authority (they must involve police), subject to civil liability and bad PR, infiltration risks exposure (their agents can turn), bound by RICO and conspiracy law if they cross lines
*   **Primary Countermeasures:** Need-to-know cellular structures, financial hygiene, legal entity separation, counter-intelligence protocols, document all intimidation attempts for civil litigation

### T4: Federal State-Level Intelligence (FBI, DHS, NSA, Military Intelligence)
*   **Examples:** FBI COINTELPRO successors, DHS threat assessment teams, NSA collection programs, DEA wiretaps, state fusion centers with federal grants.
*   **Capabilities:**
    - Essentially unlimited budget for designated targets
    - National Security Letters (NSLs): secret subpoenas with gag orders, no judicial review required
    - FISA surveillance warrants covering foreign contacts and their domestic associates
    - NSA metadata collection: call records, email headers, location data at scale
    - Zero-day device exploits (Pegasus, Triangulation-class): remote compromise of fully-patched phones
    - "Black bag" covert operations: physical entry, device implants
    - Coordinated prosecution: crafting criminal charges from surveilled activity
    - Border search authority: warrantless search of devices at all U.S. ports of entry
    - Indefinite material witness detention
    - International intelligence-sharing with Five Eyes partners
*   **Limitations:** Very high threshold for deployment (significant resources required); genuine civil liberties litigation (ACLU, EFF) has constrained some programs; political exposure for targeting purely domestic activism; whistleblowers exist
*   **Realistic Applicability:** Unless your organization is directly disrupting critical infrastructure, has international funding deemed adversarial, or has been formally designated a domestic terrorism threat, sustained dedicated T4 targeting is unlikely. Incidental collection and fusion center data-sharing is more probable.
*   **Primary Countermeasures:** Tails OS, air-gapped devices for the most sensitive work, end-to-end encrypted communication for everything, no cloud services for operational data, physical compartmentalization, legal organizational structure, public transparency as a shield

---

## 2. The 5×5 Risk Assessment Matrix

Risk is defined as **Likelihood × Impact**. Assess each threat vector using this matrix before allocating security resources.

**Likelihood Scale (1–5):**
| Score | Label | Description |
|-------|-------|-------------|
| 1 | Rare | Has almost never happened to similar groups |
| 2 | Unlikely | Has happened occasionally but not recently |
| 3 | Possible | Has happened to comparable groups in this city |
| 4 | Likely | Has happened to your group or close affiliates |
| 5 | Almost Certain | Is actively happening or anticipated imminently |

**Impact Scale (1–5):**
| Score | Label | Description |
|-------|-------|-------------|
| 1 | Negligible | Minor inconvenience, recoverable in hours |
| 2 | Minor | Short disruption, no lasting harm |
| 3 | Moderate | Significant disruption, short-term detention, partial info leak |
| 4 | Severe | Key organizer arrested, major information compromise |
| 5 | Critical | Organizational collapse, long-term incarceration, physical harm |

**Risk Score = Likelihood × Impact** (Range: 1–25)

| Score Range | Priority | Action Required |
|-------------|----------|-----------------|
| 20–25 | **CRITICAL** | Implement all countermeasures immediately |
| 12–19 | **HIGH** | Prioritize; implement within 48 hours |
| 6–11 | **MEDIUM** | Schedule; implement before next action |
| 1–5 | **LOW** | Monitor; document; accept or mitigate opportunistically |

---

## 3. Threat Modeling Worked Examples

### Example A: Local Tenants Union (T1/T2 Threat Environment)
*Organizing rent strikes against a large property management company.*

| Threat Vector | Likelihood | Impact | Score | Priority |
|---------------|-----------|--------|-------|----------|
| Doxxing of lead organizers | 4 | 3 | 12 | HIGH |
| Landlord hires private investigators | 3 | 2 | 6 | MEDIUM |
| Police observe public meetings | 2 | 2 | 4 | LOW |
| Eviction as retaliation | 4 | 4 | 16 | HIGH |
| Infiltration of WhatsApp group | 3 | 3 | 9 | MEDIUM |

**Key Countermeasures:** Signal instead of WhatsApp, pseudonymous public spokespeople, data broker opt-outs, legal observer at all public meetings.

### Example B: Journalist Covering Federal Law Enforcement (T2/T4 Threat Environment)
*Reporting on immigration enforcement operations.*

| Threat Vector | Likelihood | Impact | Score | Priority |
|---------------|-----------|--------|-------|----------|
| Source identification from metadata | 4 | 5 | 20 | CRITICAL |
| Device seizure at border | 3 | 4 | 12 | HIGH |
| Subpoena for communications | 3 | 4 | 12 | HIGH |
| Targeted digital intrusion | 2 | 5 | 10 | MEDIUM |
| Physical surveillance of source meetings | 2 | 4 | 8 | MEDIUM |

**Key Countermeasures:** Signal with disappearing messages, SecureDrop for source intake, Tails OS for sensitive document handling, encrypted device at border crossings, legal counsel on retainer.

---

## 4. The STRIDE Threat Framework (Adapted)

STRIDE is a structured methodology for identifying attack vectors. Assess each category against your organization's specific assets.

| Category | Definition | Activist Example | Countermeasure |
|----------|-----------|------------------|----------------|
| **S**poofing | Adversary impersonates a trusted identity | Fake "ally" joins Signal group | Verification protocols, in-person trust establishment |
| **T**ampering | Data or systems are modified without authorization | Evidence doctored, communications altered | Cryptographic signatures, chain of custody |
| **R**epudiation | Actions taken without accountability | Informant denies leaking; legal disputes | Secure timestamped records, witness documentation |
| **I**nformation Disclosure | Sensitive information exposed | OSINT reveals organizer's home address | Data minimization, strict need-to-know |
| **D**enial of Service | Disruption of operations | Platform bans, DDoS of website | Redundant channels, offline capabilities |
| **E**levation of Privilege | Gaining unauthorized access | Account compromise, device theft | Strong authentication, device encryption |

---

## 5. Ongoing Threat Assessment Protocol

Threat modeling is not a one-time exercise. Re-assess after every significant event.

**Reassess immediately when:**
- A member is arrested, detained, or has their device seized
- New technology is deployed by law enforcement in your city (e.g., new camera network, facial recognition contract)
- A known informant or infiltrator is identified
- Your organization receives unusual legal or media attention
- A member reports being approached or recruited by law enforcement
- Significant escalation in the political environment (new legislation, crackdowns)

**Regular review cadence:** At minimum, conduct a full threat modeling session quarterly, or before any major planned action.

---

*This guide does not constitute legal advice. Laws vary by jurisdiction. For legal matters, consult a licensed attorney.*

[← Back to Index](../index.md)
