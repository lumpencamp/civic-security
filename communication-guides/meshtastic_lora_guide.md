# Meshtastic & LoRa: Decentralized Off-Grid Communications

*Status: RF Engineering & Deployment Manual | Audience: Network Architects and Tactical Comms Teams*

When state actors disable cellular networks (or you must assume all telecom infrastructure is compromised), operations require a secondary, decentralized communication layer. LoRa (Long Range) is an ultra-low power, low-bandwidth radio protocol operating in the ISM band (e.g., 915 MHz in the US). Combined with the open-source Meshtastic firmware, it allows for the deployment of a peer-to-peer text messaging mesh network decoupled from corporate ISPs.

This guide details the technical deployment and severe SIGINT vulnerabilities of a tactical LoRa mesh.

---

## 1. Hardware Selection and Firmware Flashing

Rely on hardware built around the modern Semtech SX1262 LoRa transceiver. Older chips (like the SX1276) have inferior sensitivity and higher power consumption.

*   **Recommended Nodes:** LILYGO T-Echo or Heltec V3 (for mobile operators); RAK Wireless WisBlock (for low-power, solar-equipped stationary repeater nodes).
*   **Deployment:** Flash the latest stable Meshtastic firmware via `flasher.meshtastic.org`.
*   **Operational Constraint:** **Do not use the default "LongFast" channel settings for high-stakes civic operations.** The default channel is public, unencrypted, and highly congested.

## 2. Cryptographic Channel Configuration

To secure the mesh, you must establish a closed, authenticated channel utilizing AES-256 encryption.

1.  **Key Generation:** Using the Meshtastic CLI or mobile app, create a new channel and set the encryption to **AES256**. The software will generate a 256-bit cryptographic key.
2.  **Out-of-Band (OOB) Distribution:** *Never* transmit the channel configuration URL or QR code over the public LoRa channel or via standard SMS. The key must be distributed out-of-band via Signal, encrypted Matrix chat, or in-person physical QR code scanning.

## 3. The Unencrypted Header Vulnerability

While Meshtastic utilizes AES-256-CTR encryption for message payloads, the network architecture requires certain routing metadata to be broadcast in the clear. To allow the mesh to function, nodes must be able to route packets even if they don't possess the decryption key. This "blind relay" capability means the packet header is always unencrypted.

| Data Point | Encrypted? | Location |
| :--- | :--- | :--- |
| **Sender Node ID** | No | Packet Header |
| **Destination ID** | No | Packet Header |
| **Hop Limit / Routing** | No | Packet Header |
| **Channel Hash** | No | Packet Header |
| **Message Content** | Yes | Payload |
| **GPS Location** | Yes | Payload |
| **Node Names** | Yes | Payload |

## 4. The Threat: Passive Listening & SIGINT

Because headers are transmitted in plaintext, an adversary does not need to break your encryption to understand your network.

1.  **Traffic Analysis:** A passive listener using inexpensive Software Defined Radios (SDRs) can map the exact topology of your network. They can see which nodes act as central hubs, who is communicating with whom, and the frequency of those communications.
2.  **Physical Triangulation (Fox Hunting):** Every transmission is a beacon. Using directional antennas or a distributed array of SDRs calculating Time Difference of Arrival (TDOA), an adversary can physically triangulate the origin of the RF signal.
3.  **Hardware Fingerprinting:** The Node ID (e.g., `!a1b2c3d4`) is derived directly from the radio's hardcoded MAC address. Because this ID is in the unencrypted header, once an adversary correlates a specific Node ID to a specific person or location, they can track that radio anytime it transmits.

## 5. Mandatory OpSec Guidelines

If facing sophisticated threat actors, explicitly follow these rules:

*   **Kill the GPS:** Disable all automated GPS and position broadcasting. Even though GPS data is encrypted in the payload, continuous broadcasting acts as an RF beacon, making physical triangulation trivial. Furthermore, Meshtastic lacks Perfect Forward Secrecy (PFS); if a single node is captured by an adversary and its keys extracted, all previously intercepted GPS data becomes readable retroactively.
*   **Anonymize Node Names:** Long and Short names are stored in the encrypted payload, but if the network key is compromised, those names are exposed. Never use real names, common online handles, or predictable aliases.
*   **Eliminate Telemetry:** Disable battery, voltage, and device status telemetry. The less a device transmits, the harder it is to track physically.
*   **Use "Blind" Relays:** If the network relies on unattended relay nodes (e.g., solar-powered repeaters placed on roofs or hills), do not configure the private channel key on them. Unattended nodes are highly susceptible to physical capture. They will still relay unencrypted headers blindly without needing the key to decrypt your payloads.
*   **Understand the Limits of LoRa:** Meshtastic is resilient against infrastructure failure, but it is highly vulnerable to targeted RF jamming and Signals Intelligence (SIGINT). It provides off-grid capability, not invisibility.

## 6. RF Parameter Optimization (Urban vs. Rural)

LoRa relies on Chirp Spread Spectrum (CSS) modulation. You must tune the Spreading Factor (SF) and Bandwidth (BW) based on your operational environment.

### Dense Urban Operations (Protests/Cities)
In a city, signal bounce and RF noise are high, but physical distances are typically short.
*   **Settings:** Use a lower Spreading Factor (SF 7 or 8) and higher Bandwidth (250 kHz or 500 kHz).
*   **Result:** This significantly increases data speed and reduces airtime (saving battery and reducing the RF detection window).
*   **Hop Limit:** Set the Max Hops to **3**. In a dense crowd, a hop limit of 7 (the default) will cause a broadcast storm.

### Open Field Operations (Rural/Long-Range)
*   **Settings:** Use a high Spreading Factor (SF 11 or 12) and low Bandwidth (125 kHz).
*   **Result:** This maximizes sensitivity and range (often 10+ miles line-of-sight) but significantly reduces data speed.
*   **Hop Limit:** Increase to 5-7 to allow packets to traverse multiple miles across sparse repeater nodes.

_Last Updated: 2026_
