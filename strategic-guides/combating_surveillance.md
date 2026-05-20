# Combating State Surveillance: Institutional Defense Strategy

*Status: Level 3 Directive | Audience: Board Members, Core Organizers, Legal Teams*

Defending against state-level dragnet surveillance (e.g., NSA PRISM-style metadata collection, federal fusion centers, mass data broker harvesting) requires more than encrypted chat apps. It requires embedding cryptographic resistance and legal firewalls directly into the infrastructure of your organization.

When facing an adversary with infinite resources, your primary objective is to **starve them of metadata** and **weaponize legal process** to buy time.

---

## 1. Zero-Knowledge Architecture (ZKA)

State surveillance relies on compelling service providers to hand over your data. If the provider does not hold the keys to decrypt your data, the subpoena is useless.

*   **Operational Constraint:** The organization will not utilize any digital service that holds the decryption keys to its data.
*   **Implementation:**
    *   **Cloud Storage:** Abandon Google Workspace and Microsoft 365 immediately. Transition all organizational documents to End-to-End Encrypted (E2EE) providers (e.g., Tresorit, Proton Drive, or self-hosted CryptPad).
    *   **Collaborative Work:** Use CryptPad for live document editing. The server operators cannot read the keystrokes.
    *   **Communications:** Transition all internal comms to a self-hosted Matrix server (with E2EE strictly enforced) or SimpleX to eliminate central metadata directories.

## 2. Ephemeral Data Policies (EDP)

Data that does not exist cannot be seized, subpoenaed, or leaked. Retaining historical communications is an existential threat to civic organizations.

*   **Operational Constraint:** All operational communications and non-essential records are subject to strict, automated destruction.
*   **Implementation:**
    *   **Disappearing Messages:** Signal and Matrix group chats must have a hardcoded expiration timer (maximum 7 days). No exceptions for "convenience."
    *   **The 30-Day Purge:** Financial records necessary for tax compliance are compartmentalized and encrypted offline. All other logistical, planning, or mapping documents must be securely wiped (using tools like BleachBit or MAT2) within 30 days of the operation's conclusion.
    *   **No Centralized Rosters:** The organization will not maintain a master digital list of volunteers, members, or donors. Rosters are segmented and kept on encrypted, air-gapped physical storage (e.g., Tails OS persistent volume).

## 3. Cryptographic Structural Verification

Infiltration by state informants is a statistical certainty over a long enough timeline. Your network must assume internal nodes are compromised.

*   **Operational Constraint:** Identity verification must be cryptographic, not just visual or behavioral.
*   **Implementation:**
    *   **Key Signing Parties:** Core members must physically meet to verify and sign each other's PGP keys or verify Matrix/Signal safety numbers via physical QR code scanning.
    *   **Out-of-Band Verification:** If an operational directive is issued digitally, it must be verified via a secondary, out-of-band channel (e.g., verifying a Matrix message via a pre-arranged physical dead drop or encrypted VoIP call) before execution.

## 4. Legal Firewalls and Charter Structuring

Your organizational charter must act as a legal shield, legally preventing any single member from unilaterally complying with warrantless demands.

*   **Operational Constraint:** No individual member possesses the authority or technical capability to decrypt the organization's entire data vault.
*   **Implementation:**
    *   **Distributed Key Management (Shamir's Secret Sharing):** Use cryptographic secret sharing to split the master decryption key for the organization's offline archives among five core members. Accessing the data requires three of the five members to combine their keys. This prevents the state from secretly compelling a single individual via a National Security Letter (NSL) or gag order.
    *   **The Warrant Canary:** The organization must publish a monthly "Warrant Canary" (a cryptographically signed statement asserting that the organization has *not* received any secret subpoenas or NSLs). If the canary is not updated on schedule, all members must immediately assume the organization is compromised and execute the Zero-Knowledge Protocol.
    *   **Legal Representation on Retainer:** Retain civil liberties counsel (e.g., EFF or regional equivalent). The standing order for all members regarding any interaction with federal intelligence or law enforcement is: *"I do not consent to searches, I will not answer questions, and I invoke my right to my attorney."*

_Last Updated: 2026_
