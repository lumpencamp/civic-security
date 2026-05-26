# Signal Alternatives: Choosing the Right Secure Messenger

*Status: Level 2 | Audience: Organizers evaluating communication tools for specific threat environments*

Signal is the default recommendation for most activist communications, but it is not the right tool for every situation. This guide evaluates the most relevant Signal alternatives, explaining what they protect against that Signal doesn't (and vice versa), and when to use each.

---

## 1. When Signal Might Not Be Enough

Signal's limitations in specific threat scenarios:

- **Phone number requirement:** Signal requires a phone number for registration. This creates an identity link — even with a VOIP number, a sophisticated adversary can potentially trace registration patterns.
- **Metadata visibility:** While Signal conceals content, your ISP and network observers can see that you are connecting to Signal's servers. This is meaningful in jurisdictions where Signal is monitored or blocked.
- **Centralized infrastructure:** Signal is operated by a nonprofit corporation with U.S.-based servers. While Signal has a strong track record of resisting subpoenas (they have very little data to give), they are a targetable legal entity.
- **Network dependence:** Signal requires internet connectivity (Wi-Fi or cellular). If networks are disrupted or monitored at a chokepoint, Signal becomes unavailable or risky.

---

## 2. Briar

**Best for:** Situations where internet access is unavailable, blocked, or specifically monitored

**How it works:**
- Peer-to-peer, encrypted messaging with no central server
- Connects over Tor (when internet is available), Wi-Fi (local mesh), or Bluetooth (direct device-to-device)
- Messages are stored on your device, not on any server
- No phone number or email required — identity is based on cryptographic keys

**What makes it unique:**
- Works without the internet at all, using Bluetooth and Wi-Fi mesh networking. Devices within approximately 10 meters can exchange messages over Bluetooth; within Wi-Fi range over local Wi-Fi.
- No metadata stored on servers because there are no servers
- Open source, maintained by the Briar Project

**Limitations:**
- Smaller user base — both parties must have Briar installed
- Bluetooth range is limited (~10 meters); Wi-Fi slightly more
- No voice or video calls (messaging only)
- Syncs only when devices are in range (for offline mesh mode)

**Threat model fit:**
- ✅ Internet disruption (protests with communications blocked)
- ✅ No phone number exposure
- ✅ T2 threat environments where Signal usage is itself monitored
- ❌ Everyday communications (less convenient than Signal)
- ❌ Large groups (Bluetooth/Wi-Fi mesh scales poorly)

**Download:** briarproject.org (Android only; iOS development is in progress)

---

## 3. Session

**Best for:** Situations requiring no phone number and decentralized infrastructure

**How it works:**
- Decentralized onion routing network (similar to Tor) for routing messages
- No phone number or email required — identity is a randomly generated alphanumeric "Session ID"
- No central servers to subpoena — messages route through the Session decentralized network
- Built on Signal Protocol encryption

**What makes it unique:**
- Zero account information required: you receive a Session ID, share it with people you want to contact
- Decentralized routing makes traffic analysis harder
- Open source; operated by OPTF (Oxen Privacy Tech Foundation), a nonprofit based in Australia

**Limitations:**
- Relatively new; smaller user base
- No sealed sender equivalent (metadata harder to conceal at routing layer)
- Desktop client available but less mature than Signal Desktop
- Voice calls are available but lower quality than Signal

**Threat model fit:**
- ✅ Phone number not linked to identity
- ✅ Decentralized infrastructure (no single subpoenable entity)
- ✅ Organizational communications that need to be fully compartmentalized from phone identity
- ❌ Does not outperform Signal for everyday message content security
- ❌ Smaller community makes adoption ask harder

**Download:** getsession.org

---

## 4. Element / Matrix

**Best for:** Organizational communications requiring persistent, self-hosted group infrastructure

**How it works:**
- Matrix is an open, federated communication protocol
- Element is the primary client (like how Gmail is a client for email)
- You can host your own Matrix homeserver (eliminating dependence on any third party)
- End-to-end encryption available for rooms (must be explicitly enabled)
- Bridges to other platforms (Signal, Telegram, IRC, Slack) are possible

**What makes it unique:**
- **Self-hosting:** Run your own server. Your messages never touch third-party infrastructure. Law enforcement subpoenas have no U.S. company to serve.
- **Persistent group rooms:** Unlike Signal groups, Matrix rooms can have persistent history that members can scroll back in (configurable). Better for organizational coordination.
- **Federation:** Matrix rooms can include members across different homeservers, like email — you control your server, others control theirs, all can communicate.

**Limitations:**
- Setup complexity: self-hosting requires technical infrastructure (server, domain, maintenance)
- End-to-end encryption requires deliberate configuration; not all rooms are encrypted by default
- Verification of other users' keys is more complex
- Hosted Matrix accounts (matrix.org) are subject to that company's legal jurisdiction

**Threat model fit:**
- ✅ Organizational persistent communication (projects, working groups)
- ✅ Self-hosted = no third-party server to subpoena
- ✅ T3 threat environments where corporate server compromise is a concern
- ❌ Not appropriate for anonymous use (account creation typically requires email)
- ❌ Overkill for most personal communications

**Download:** element.io | Matrix homeserver: matrix.org (hosted) or matrix.org/docs/guides/homeserver-setup (self-hosted)

---

## 5. SimpleX Chat

**Best for:** Maximum metadata protection for bilateral conversations

**How it works:**
- No user accounts, no phone numbers, no user IDs of any kind — fully decentralized
- Messages route through relay servers, but relay servers cannot associate sender and receiver identities
- Each conversation uses a unique, one-time connection address
- Open source, built by SimpleX Chat Ltd.

**What makes it unique:**
- The most radical metadata protection of any mainstream messenger: relay servers literally cannot know who is talking to whom, because connection addresses are one-time use and not linked to persistent identities
- No centralized identity registry to subpoena

**Limitations:**
- No groups yet (in development)
- Relatively new; smaller user base
- No phone number means sharing connection QR codes or links out-of-band to start a conversation

**Threat model fit:**
- ✅ Maximum metadata protection for one-on-one conversations
- ✅ Source protection (journalists receiving tips from sources)
- ✅ Situations where even the existence of a communication relationship needs to be concealed
- ❌ Not yet suitable for group organizational communication

**Download:** simplex.chat

---

## 6. Wire

**Best for:** Teams needing professional-grade encrypted communication without personal phone numbers

**How it works:**
- End-to-end encrypted messaging, voice, video, and file sharing
- Account can be created with only an email address (no phone number required)
- Wire Pro version marketed to enterprises; Wire Personal is free

**Limitations:**
- European company with server infrastructure — subject to EU legal process
- Metadata: Wire stores some metadata about communications
- The company has received law enforcement requests

**Threat model fit:**
- ✅ Teams uncomfortable with Signal's phone number requirement
- ✅ Professional organizational use
- ❌ Not recommended for high-risk communications — Signal is stronger overall

---

## 7. Decision Guide

| Question | Recommendation |
|---------|---------------|
| Everyday secure messaging with known contacts | **Signal** |
| No phone number, no server account | **Briar** or **Session** |
| Communications when internet is unavailable | **Briar** (Bluetooth/Wi-Fi mesh) |
| Organizational persistent group infrastructure | **Element/Matrix** (self-hosted) |
| Maximum metadata protection, one-on-one | **SimpleX Chat** |
| Team collaboration without personal phone numbers | **Wire** or **Session** |
| Source-to-journalist anonymous communication | **SecureDrop** + **Signal** |

---

## 8. What to Never Use for Sensitive Organizational Communications

| Platform | Why Not |
|---------|--------|
| **WhatsApp** | Meta-owned; metadata harvested; business model is data |
| **Telegram** | Not end-to-end encrypted by default; default chats are server-encrypted; Telegram cloud stores all non-secret chats |
| **Facebook Messenger** | Meta surveillance infrastructure; not E2E encrypted by default |
| **Discord** | No E2E encryption; U.S. company with extensive law enforcement cooperation history |
| **Slack** | Designed for corporate surveillance; admins see all messages; no E2E encryption |
| **Standard email (unencrypted)** | No content protection; metadata extensively logged |
| **SMS/Text** | No encryption; interceptable by Stingrays; carrier records retained |

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
