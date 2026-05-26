# Protest Communications Guide: Real-Time Field Coordination

*Status: Level 2 | Audience: Action Coordinators and Affinity Group Leaders*

Effective communication during a direct action is the difference between a coordinated, effective event and a chaotic, vulnerable one. This guide covers communication architecture, tool selection, field protocols, and degraded-mode operation when communications are disrupted.

---

## 1. Communication Architecture

### 1.1 The Layered Communications Model

Design your communications system with redundant layers. If the primary channel fails, participants fall back to the secondary channel without confusion.

| Layer | Tool | Purpose | Resilience |
|-------|------|---------|-----------|
| Primary digital | Signal (group) | Coordination, updates, emergency alerts | Internet-dependent |
| Secondary digital | Briar (mesh) | When internet is disrupted or monitored | Bluetooth/Wi-Fi mesh |
| LoRa mesh | Meshtastic | Long-range off-grid mesh | No infrastructure |
| Physical/analog | Prearranged signals | Direct communication without devices | No failure mode |
| Emergency audio | Whistle signals | Simple, unambiguous, no battery | Always works |

### 1.2 Cell-Based Communication Structure

Mirror your organizational cell structure in your communications channels:
- **Action-wide Signal group:** Minimal traffic — only action-wide updates (route change, dispersal, medical emergency)
- **Affinity group channels:** 4–7 people per channel for real-time affinity group coordination
- **Leadership/coordinator channel:** Action leads, legal liaison, medic lead
- **Jail support / off-site:** Separate thread with your off-site jail support coordinator

**Limit notifications:** High-traffic all-hands channels that chime constantly during an action will be muted or ignored. Send to the widest channel only what everyone truly needs to know.

---

## 2. Pre-Action Communication Setup

### 2.1 Signal Group Configuration

Before the action:
- [ ] Create action-specific Signal groups (do not use standing organizational groups for operational traffic)
- [ ] Add all participants to their appropriate groups
- [ ] Set disappearing messages: 1 week for action groups, 1 day or less for most sensitive operational channels
- [ ] Confirm all participants have Signal properly configured (registration lock, no biometrics)
- [ ] Designate two group admins per channel (so if one person is arrested, the group continues)

### 2.2 Code Words and Signals

Establish a shared vocabulary before the action:
- **All clear:** Code word meaning you are safe and accounted for
- **Disperse [direction]:** Code word for ordered dispersal toward a specific exit
- **Medical [location]:** Medical emergency at specified location
- **Legal:** Someone is being detained or arrested
- **Go green/go red:** Proceed as planned / abort and disperse

Physical signals (for when device use is restricted or impossible):
- **Raised right fist:** Stop; hold position
- **Raised left arm:** Move to the left
- **Open palms forward:** Back up
- **Single whistle blast:** Attention; stop and look for a coordinator
- **Three whistle blasts:** Emergency; immediate dispersal

Discuss, agree upon, and practice these signals before the action. Novel signals under stress are unreliable.

### 2.3 Information Discipline Briefing

Brief all participants before the action on communication protocols:
- What goes in the all-hands Signal group vs. affinity group channels
- No real-time social media during the action (wait until you are safely away)
- No photos of other participants' faces without consent
- Code words and physical signals review
- Off-site jail support number confirmation (written on body)

---

## 3. During the Action

### 3.1 Digital Communication Protocols

**Volume control:**
- All-hands Signal: broadcast only critical updates (route change, police movement, medical need)
- Affinity group Signal: real-time local coordination
- Resist the urge to share real-time "color commentary" in the all-hands group — it creates noise that buries critical messages

**Message format for critical updates:**
Use a structured format for time-sensitive messages that can be scanned instantly:
```
[TYPE]: [BRIEF CONTENT] | [LOCATION/DIRECTION] | [ACTION NEEDED]

Example:
POLICE: Large group moving east on Clark | Approaching from Michigan | Hold position / be ready to disperse west
```

### 3.2 Affinity Group Check-In Protocol

Establish a check-in cadence for affinity groups:
- Every 30 minutes or at each phase transition (arrival, beginning, transition, dispersal)
- Designated affinity group lead sends a check-in to the coordination channel: "Group [identifier]: All [N] members accounted for, [location]"
- Missing check-in triggers inquiry to affinity group channel, then to jail support if no response

### 3.3 When Someone Is Detained or Arrested

The affinity group has immediate responsibilities:
1. Note the time, location, and which officer(s) made the detention/arrest (badge number if visible)
2. Attempt to stay with the detained person until separated by police
3. Note the direction they were taken
4. Send immediately to coordination channel: "LEGAL: [name or identifier] detained at [location] by [officer ID] at [time]"
5. Coordination channel notifies jail support with the identifying information

**The detained person's responsibilities:**
- Repeat the Fifth Amendment assertion; say nothing else
- Comply physically; do not resist
- Note everything they can; reconstruct when released

### 3.4 Medical Communication

- Designate a specific identifier for medical emergencies: "MEDIC: [type of need] at [location]"
- Medical information is pre-positioned with the designated medics — affinity group leaders do not need to broadcast medical details
- Medics and coordination have a dedicated channel for medical coordination that does not clog the all-hands channel

---

## 4. Degraded-Mode Communications

When normal communication channels fail, fall back to prearranged alternatives.

### 4.1 Internet Disruption

If cellular data and Wi-Fi are unavailable (targeted disruption, Stingray interference, network congestion in high-density crowd):
- Switch to Briar over Bluetooth mesh (pre-install before the action; ensure all participants have it)
- Briar does not require internet — it creates a direct peer-to-peer mesh between nearby phones
- Effective range: ~10m (Bluetooth), more over Wi-Fi mesh
- Limitation: messages propagate across the mesh; people at the edge of the mesh receive messages with delay

### 4.2 Device Seizure

If key communicators' devices are seized:
- Pre-designated backup coordinators assume coordination responsibilities
- Communication channels continue (no single person's arrest should collapse the communication structure)
- Remaining coordinators send a brief notification: "Coordinator [identifier] is detained. [Backup identifier] now coordinating."

### 4.3 Full Comms Failure

If all digital communications fail:
- Fall back to prearranged physical signals (Section 2.2)
- Fall back to prearranged assembly points (establish 2–3 before the action)
- Affinity groups operate autonomously using their prearranged dispersal plans
- **Critical:** Every affinity group must be able to operate independently if all communication fails. Prearrange: where do we go? What are our dispersal routes? When do we reassemble?

---

## 5. Post-Action Communications

### 5.1 Dispersal Check-In

After dispersal:
- Each affinity group does a headcount and reports to the coordination channel: "Group [identifier]: all [N] accounted for, [location]"
- Missing members trigger the jail support protocol

### 5.2 Post-Action Operational Security

- Continue using action-specific Signal group for coordination about arrested members, legal follow-up, and debrief logistics
- Delete or archive the action Signal group once the legal/operational situation is resolved
- Do not post to public social media until you are safely away and until you have scrubbed all photos of identifiable faces and metadata

### 5.3 Media and Narrative Coordination

- Designate a specific communications coordinator for media interactions
- Establish who is authorized to speak publicly about the action and who is not
- Ensure any released video or photos have been metadata-scrubbed and faces of non-consenting participants blurred
- The narrative about what happened should go through your communications cell, not be ad-hoc from individual participants

---

## 6. Communications Security Summary

| Practice | Why |
|---------|-----|
| Use Signal (not SMS, WhatsApp, or social media) | End-to-end encryption; no metadata to seize from you |
| Separate action groups from standing org groups | Limits exposure of organizational network if action group is compromised |
| Disappearing messages enabled | Seized phones have no message history to analyze |
| Code words for sensitive situations | Reduces clarity of communications to observers |
| Physical signals pre-planned | Survives any communications failure |
| Jail support on separate channel | Always reachable even if action coordinators are arrested |
| No real-time social media | Real-time info aids adversary situational awareness |

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
