# Advanced Threat Modeling for Civic Organizations

*Status: Level 2 Directive | Audience: Operations Planners and Security Teams*

Threat modeling is not paranoia; it is the calculated, objective assessment of your operational environment. This framework adapts corporate security methodologies (STRIDE and PASTA) into an actionable, quantitative model specifically for non-state actors, activists, and civic organizations.

---

## 1. Adversary Profiling (The Threat Tiers)

To defend effectively, you must understand your adversary's capabilities, budget, and legal authorizations. Do not prepare for a T4 adversary if your actual threat is T1; doing so will cause operational paralysis.

*   **T1: The Noise (Doxxers, Trolls, Counter-Protestors)**
    *   **Capabilities:** Open-Source Intelligence (OSINT), social engineering, physical harassment at public events, denial-of-service (reporting accounts).
    *   **Limitations:** No legal authority, minimal funding, low technical sophistication.
*   **T2: Local Enforcement (Police, Regional Fusion Centers)**
    *   **Capabilities:** Arrest authority, physical surveillance, Cell-Site Simulators (Stingrays), ALPRs (License Plate Readers), facial recognition databases, access to data brokers, subpoena power for domestic tech companies.
    *   **Limitations:** Bureaucratic friction, geographic boundaries, budget constraints.
*   **T3: Corporate Intelligence (Private Security, Pinkertons)**
    *   **Capabilities:** Deep financial resources, infiltration/informants, advanced OSINT tools, litigation/lawsuits (SLAPPs), hiring off-duty law enforcement.
    *   **Limitations:** No direct arrest authority, subject to civil liability, highly sensitive to bad PR.
*   **T4: State-Level Intelligence (Federal Agencies, Three-Letter Entities)**
    *   **Capabilities:** Unlimited budget, zero-day device exploits (Pegasus), national dragnet surveillance, NSA/FISA intelligence sharing, border search authority, covert black-bag operations.
    *   **Limitations:** High threshold for deployment. Unless you are involved in massive critical infrastructure disruption or designated as a national security threat, you are unlikely to face dedicated T4 targeting.

---

## 2. The 5x5 Risk Assessment Matrix

Risk is calculated using two variables: **Likelihood** (How probable is the attack?) and **Impact** (How devastating is the consequence?).

*   **Likelihood (1-5):** 1 = Rare, 3 = Possible, 5 = Almost Certain.
*   **Impact (1-5):** 1 = Minor inconvenience, 3 = Operation disrupted/Short-term detention, 5 = Critical organizational failure/Long-term imprisonment/Loss of life.

**Risk Score = Likelihood × Impact**

| Likelihood \ Impact | 1 (Minor) | 2 (Moderate) | 3 (Significant) | 4 (Severe) | 5 (Critical) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5 (Certain)** | 5 (Low) | 10 (Med) | 15 (High) | 20 (Extreme) | **25 (ABORT)** |
| **4 (Likely)** | 4 (Low) | 8 (Med) | 12 (High) | 16 (Extreme) | 20 (Extreme) |
| **3 (Possible)** | 3 (Low) | 6 (Med) | 9 (Med) | 12 (High) | 15 (High) |
| **2 (Unlikely)** | 2 (Low) | 4 (Low) | 6 (Med) | 8 (Med) | 10 (Med) |
| **1 (Rare)** | 1 (Low) | 2 (Low) | 3 (Low) | 4 (Low) | 5 (Low) |

### Hard Thresholds (The Go/No-Go Rule)
*   **Score 1-8 (Acceptable):** Proceed with standard OPSEC.
*   **Score 9-14 (Elevated):** Proceed with heightened countermeasures. Restrict "need-to-know" access.
*   **Score 15-20 (Critical):** Operation is on hold until mitigations reduce the score below 15.
*   **Score 21-25 (ABORT):** Mandatory operational abort. The environment is too hostile.

---

## 3. Threat Modeling Template (STRIDE for Activists)

Use this template to quantify your vulnerabilities before any major operation.

### Phase 1: Asset Identification
*List what you must protect.*
*   **Asset 1:** (e.g., The identity of the whistleblower)
*   **Asset 2:** (e.g., The physical location of our secure server)
*   **Asset 3:** (e.g., Our encrypted communication channels)

### Phase 2: Adversary Mapping
*Identify who wants to compromise those assets.*
*   **Target Adversary:** (e.g., T2 - Local Fusion Center)
*   **Their Goal:** (e.g., Identify the organizers and seize communication logs)

### Phase 3: Vulnerability Assessment & Mitigation
*Map the attack vectors and calculate the risk using the 5x5 Matrix.*

| Asset | Attack Vector (How will they get it?) | Base Likelihood | Base Impact | Base Risk Score | Mitigation Strategy (What will we do?) | New Likelihood | New Impact | Adjusted Risk Score |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Identity of Source** | T3 Adversary uses subpoenas on our Google Workspace. | 4 | 5 | **20 (EXTREME)** | Migrate source communication to Signal; store files on E2EE CryptPad. | 1 | 5 | **5 (LOW)** |
| **Protest Route** | T1 Trolls infiltrate public Telegram group to dox attendees. | 5 | 3 | **15 (HIGH)** | Vetting protocol for group entry; move sensitive comms to private Matrix server. | 2 | 2 | **4 (LOW)** |
| **Devices** | T2 Police seize phones during mass arrest. | 4 | 4 | **16 (EXTREME)** | Enforce burner phone protocol; use Faraday bags; 12-character alphanumeric passcodes. | 4 | 1 | **4 (LOW)** |

### Phase 4: Operational Go/No-Go Checklist
*   [ ] Have all assets been identified?
*   [ ] Is the primary adversary tier correctly classified?
*   [ ] Have all adjusted risk scores been brought below the 15-point threshold?
*   [ ] Are all participating nodes trained on the mitigation strategies?

If any box is unchecked, the operation is a **No-Go**.

_Last Updated: 2026_
