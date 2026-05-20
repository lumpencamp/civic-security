# Core OPSEC Principles: A Dynamic Workflow Compartmentalization Manual

*Status: Level 1 Directive | Audience: Core Organizers and High-Risk Nodes*

Operational Security (OPSEC) is not a checklist; it is an active, continuous state of defensive posture. This manual outlines the exact mechanics of identity compartmentalization and dynamic workflow management necessary to prevent cascading failure against sophisticated adversaries.

---

## 1. Identity Compartmentalization (The 'Air Gap' Principle)

The fundamental rule of modern OPSEC is the strict separation of personas. Your personal identity (True Name, family, employment) must never intersect with your organizational identity (Alias, network, operations).

### Hardware Separation
*   **Rule:** Never use personal devices for organizational operations.
*   **Mechanics:** Procure "clean" devices (burner laptops/phones) using untraceable cash. These devices must never connect to your home Wi-Fi network or be associated with your personal cellular accounts.
*   **Physical Isolation:** Store operational devices in Faraday bags when not in active use to prevent passive location polling and ambient audio recording.

### IP and Network Separation
*   **Rule:** Never allow operational traffic to share the same IP footprint as your personal traffic.
*   **Mechanics:** All operational devices must route exclusively through anonymizing networks (Tor) or dedicated, cash-purchased VPNs running on physically separate access points (public Wi-Fi far from your residence). Never log into an operational account from a personal IP, and vice versa. A single intersection creates an immutable cryptographic link.

### Behavioral Separation
*   **Rule:** Your operational alias must exhibit a distinct "Pattern of Life" (PoL) from your true identity.
*   **Mechanics:** Alter your writing style (use different vocabulary, grammar, and sentence structure). Do not access operational and personal accounts concurrently. If your true identity works a 9-to-5 job, your operational alias should not exhibit activity exclusively outside those hours, as this creates a recognizable negative correlation.

---

## 2. Dynamic Workflow Compartmentalization

Operations must be divided into independent, non-overlapping cells based on strict "need-to-know" access.

### The Cellular Structure
*   **Structure:** Organize into discrete cells (e.g., Logistics, Communications, Action). Members of one cell only know the identities (aliases) and functions of members within their own cell.
*   **Communication:** Cross-cell communication is handled strictly through designated "Cut-Outs" (single-point liaisons). This ensures that if the Logistics cell is compromised, the adversary has no lateral access to the Communications cell.

### The Hazard of Habituation
Adversaries use machine learning to map predictable human behavior (Pattern-of-Life analysis). Habituation is a critical vulnerability.
*   **Transit:** Never take the same route to a meeting or operational site twice. Vary modes of transport (walk, bus, bike) and randomly alter departure/arrival times.
*   **Digital Transmissions:** Do not establish predictable communication windows. Randomize the timing of message sending. Utilize delay-send features over Tor to decouple your physical activity from your network activity.

---

## 3. Threat Mitigation Matrix: Responding to Node Compromise

When a single node (an individual or a device) is suspected of being compromised, immediate, pre-planned action is required to prevent a cascading failure across the network.

| Condition | Indicator | Immediate Action (T-0) | Secondary Action (T+24h) |
| :--- | :--- | :--- | :--- |
| **Suspected Device Compromise** | Unexplained battery drain, unexpected reboots, intercepted comms. | Power down device immediately. Place in Faraday bag. Do NOT attempt to investigate on the device. | Purge remote session keys. Initiate secure wiping protocols if remote wipe is configured. Assume all data on device is captured. |
| **Alias Compromise** | Alias is publicly linked to True Name (Doxing) or targeted by specific spear-phishing. | Sever all communications with the compromised alias. The alias is considered "burned." | Assess blast radius. Alert all connected cells via secondary channels that the alias is burned. Rotate all shared credentials. |
| **Physical Arrest / Seizure** | Node is detained by law enforcement; devices are seized. | Initiate **Zero-Knowledge Protocol**. Connected nodes immediately sever all links to the seized node's aliases. | Rotate all organizational communication channels. Abandon physical meeting locations known to the compromised node. Assume adversary has full access to the node's memory and data. |
| **Informant Discovery** | Irrefutable evidence that a node is collaborating with an adversary. | **Silent Isolation.** Do not confront. Gradually restrict the node's access to sensitive information ("Swimming in your lane"). | Feed compartmentalized, false information (Canary Trap) to map the extent of the leak and identify the adversary's intelligence priorities. Prepare to sever cleanly. |

---
**Directive:** Trust is a vulnerability. Rely on compartmentalization, cryptography, and rigid behavioral discipline.

_Last Updated: 2026_
