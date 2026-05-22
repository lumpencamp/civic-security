# Tactical Protest Communications and SIGINT Defense

*Status: Tactical Operations Manual | Audience: Field Coordinators and Direct Action Teams*

During high-friction civic actions, you must assume the cellular grid will fail. Whether due to natural crowd congestion, intentional localized throttling, or deployment of cellular jammers/IMSI-catchers by state actors, your communication architecture must be resilient.

As a tactical signals intelligence (SIGINT) defense instructor, I mandate that no operation commences without a predefined, multi-tiered communications architecture.

---

## 1. The PACE Communication Plan

Every operational team must establish a PACE plan before deploying into the field. This ensures a seamless transition when the primary grid degrades.

*   **P - Primary (Encrypted Cellular):** Signal Messenger or Session. Used when the cellular network is functioning normally. All primary comms must be text-based to minimize bandwidth and noise footprint.
*   **A - Alternate (Decentralized Cellular):** Matrix/Element running on a self-hosted server. Used if Signal's central servers are blocked or experiencing throttling.
*   **C - Contingency (Off-Grid RF):** Meshtastic (LoRa) or Briar (Bluetooth/Local Wi-Fi). Used when the cellular network is completely blacked out or jammed. This requires pre-paired hardware and close physical proximity (for Briar) or line-of-sight relays (for LoRa).
*   **E - Emergency (Physical Protocol):** Acoustic signaling (whistles/air horns) and pre-designated physical rally points. Used when all digital and RF communications have catastrophically failed or devices have been seized.

### Executing the Comms Shift
A "Comms Shift" must be called explicitly. If a team leader recognizes Primary is failing (e.g., messages are hanging on "sending"), they issue the command: *"Grid degraded. Shift to Alternate."* All members immediately abandon Primary and move to the Alternate channel. Do not split communications across multiple tiers simultaneously.

---

## 2. Defeating Voice Fingerprinting & SIGINT

Voice communication over open radio frequencies (FRS/GMRS walkie-talkies) or unencrypted cellular channels is entirely transparent to SIGINT operations. State adversaries use voice-recognition algorithms to map individual organizers across multiple events.

### Brevity and Code-Word Protocols
If you must transmit via voice (e.g., on an unencrypted radio due to a Contingency shift):

*   **No True Names:** Never use real names, common nicknames, or organizational titles. Assign random, rotating callsigns for each operation (e.g., "Sierra-1," "Echo-Actual").
*   **Brevity Matrix:** Keep transmissions under 5 seconds. Use a pre-memorized brevity code.
    *   *Example:* Instead of "The police are moving in from the north street with riot gear," use: "Condition Red, North vector."
*   **Voice Disguise:** Do not shout or display recognizable emotional cadence. Speak in a flat, monotone whisper if transmitting near hostile forces.

---

## 3. Contingencies: Jamming and Cellular Blackouts

When facing localized cellular blackouts (often triggered by municipal authorities or Stingray deployment), digital coordination ends.

### Recognizing the Blackout
*   Messages fail to send, but the phone shows "full bars." (A strong indicator of a Stingray trap).
*   Complete loss of data connection (dropping to 1G/EDGE or "No Service") while in a dense urban environment.

### The Emergency Physical Protocol (Rally Points)
When shifting to the 'Emergency' tier, digital devices must be powered down and placed in Faraday bags to prevent tracking.

1.  **The Primary Rally Point (PRP):** A safe, observable location just outside the immediate zone of friction (e.g., a specific coffee shop three blocks away). If a team is scattered during a blackout, everyone moves independently to the PRP.
2.  **The Fallback Rally Point (FRP):** A secondary, highly secure location miles away from the event (e.g., a trusted residential safehouse).
3.  **The Time Protocol:** If separated, wait at the PRP for a pre-agreed duration (e.g., 15 minutes). If the team has not reunited or the PRP becomes hostile, proceed immediately to the FRP. Do not loiter. Do not attempt to use communications until reaching the FRP.

_Last Updated: 2026_
