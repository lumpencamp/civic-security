# Counter-Surveillance in the Field

*Status: Level 2 | Audience: Field Organizers and Security Teams*

Counter-surveillance is the active practice of detecting and responding to surveillance before or during an operation. The goal is not to become invisible — modern surveillance infrastructure makes that impossible in urban environments — but to:
1. Know when you are being actively surveilled (vs. passively scanned by fixed infrastructure)
2. Prevent mobile surveillance teams from confirming your identity or destination
3. Document surveillance for legal and organizational use
4. Make surveillance operationally expensive enough to deter it

---

## 1. Understanding the Surveillance Landscape

### 1.1 Fixed Surveillance Infrastructure

**Closed-Circuit Television (CCTV):**
- Chicago operates one of the densest camera networks in the United States: over 32,000 cameras across city departments, with integration into the Strategic Decision Support Center (SDSC)
- Facial recognition software is increasingly integrated with these systems (Clearview AI has contracts with numerous law enforcement agencies)
- Cameras are concentrated at: transit stations (CTA), intersections, commercial corridors, government buildings, parks, and schools
- Coverage is not uniform: residential side streets and alleys have significantly less coverage than arterial streets

**Automated License Plate Readers (ALPRs):**
- Mounted on police vehicles (mobile) and fixed infrastructure (stationary)
- Read every license plate in range — not just suspect vehicles — and timestamp/geocode each read
- Data is retained for 60+ days in most jurisdictions (longer in federal databases)
- If your vehicle is read at multiple action locations over time, a pattern emerges in the database
- Countermeasures: park away from likely ALPR coverage and walk; use transit; carpool with vehicles not previously associated with activism

**Cell-Site Simulators (Stingrays):**
- Mimic cell towers; all devices in range connect to them and transmit IMEI and IMSI
- Can intercept unencrypted calls and SMS
- Cannot decrypt Signal or other encrypted traffic
- Detected by apps like SnoopSnitch (Android, requires root) or EFF's CellSpy Catcher
- Primary countermeasure: airplane mode when not needing cellular; encrypted communications for all calls

**Aerial Surveillance:**
- Fixed-wing aircraft and helicopters have been used by FBI and local law enforcement for persistent area surveillance (Baltimore's Cessna program operated for years before public disclosure)
- Drones (UAVs) are increasingly deployed — some equipped with thermal imaging
- Limited countermeasures: wide-brimmed hats and umbrellas defeat overhead cameras; being inside buildings eliminates aerial visual surveillance

### 1.2 Mobile Surveillance Teams

Physical surveillance by mobile teams (foot, bicycle, vehicle) is resource-intensive and therefore used selectively for higher-value targets. A standard surveillance team typically includes:
- 2–6 individuals on foot, rotating "point" (closest to subject) position
- 1–2 vehicles for mobile support and aerial perspective
- A coordinator monitoring radio communications

**Indicators of mobile surveillance:**
- The same individual or vehicle appearing more than twice in apparently unrelated locations
- Someone who seems to be loitering without purpose and shifts when you shift
- Eye contact avoidance combined with sustained proximity
- Vehicles with tinted windows parked with sight lines to your location
- Someone entering the same stores, restaurants, or transit cars as you without apparent purpose

---

## 2. Surveillance Detection Routes (SDRs)

An SDR is a planned route designed to expose surveillance by forcing it to reveal itself. You are not trying to "lose" surveillance — you are creating conditions that make it difficult to maintain without becoming obvious.

### 2.1 SDR Principles

**Natural cover:** Every action you take on an SDR should have a plausible, mundane explanation. Stopping suddenly, changing direction abruptly, or doing obviously evasive maneuvers tells a surveillance team you are surveillance-aware and may cause them to escalate.

**Chokepoints:** Build in natural chokepoints — narrow passages, one-way doors, elevators — where a surveillance team must choose to maintain coverage or break off. Revolving doors, for example: if someone behind you enters the same revolving door segment in the opposite direction, they are maintaining surveillance under pressure.

**Time and distance:** Give surveillance time to commit. A mobile surveillance team is most likely to reveal itself over a 20–30+ minute route with natural direction changes.

### 2.2 A Basic Urban SDR

A simple surveillance detection route for urban environments:

1. **Start normally:** Leave your origin point in your normal manner. Do not look around conspicuously.

2. **First anchor point:** Enter a store, restaurant, or public building with multiple exits. Browse or sit for 5–10 minutes. Observe who else enters after you.

3. **Change direction:** Exit in a different direction than you entered. Note anyone who also changed their apparent destination.

4. **Second anchor point:** Use a multi-floor building (department store, library, transit station) — take an elevator, observe who waits for the same one or takes the stairs when you take the elevator.

5. **Transit segment:** Take a bus or train. Observe who boards at the same stop. De-board one stop early and observe if the same people also de-board.

6. **Final evaluation:** After 20–30 minutes and 3 direction changes, who has you seen more than twice? What conclusion do you draw?

### 2.3 What to Do if You Detect Surveillance

**Do not tip them off that you've made them.** This is critical. If a surveillance team knows you've identified them, they will simply be replaced with a team you haven't identified.

Options, in order of escalation:
1. **Cancel the operational purpose of the route.** Do not proceed to the meeting or location you were headed. Return home or go to a completely mundane destination.
2. **Introduce an unexplained delay.** Go somewhere for 60–90 minutes that has no operational relevance. Surveillance teams have limited shifts.
3. **Switch to a pre-established alternate communication channel** to advise your contacts of the situation.
4. **Document what you observed:** Physical descriptions, vehicle makes/models/partial plates, times and locations. This documentation is useful for civil litigation and organizational learning.

---

## 3. Protecting Your Location

### 3.1 Home Address

Your home address is typically the most valuable piece of identifying information an adversary can have. Reduce its availability:
- Opt out of data broker databases (see [OSINT Defense](../strategic-guides/osint_defense.md))
- Use a P.O. Box or mail service address for all non-essential mail
- Change your voter registration to a P.O. Box if your state permits it
- Do not receive packages at home that are connected to your activist identity
- Be aware that utility accounts, lease agreements, and property records create physical-world links to your address

### 3.2 Meeting Locations

- **Rotate meeting locations** for any sensitive gatherings. Never use the same location twice in consecutive weeks for high-sensitivity meetings.
- **Sweep for surveillance devices** before sensitive meetings: check for unknown electronic devices, look for cameras (hidden cameras are often concealed in smoke detectors, power strips, and decorative items)
- **Approach from different directions** each time you visit a regularly used location
- **Vary your travel time** to any regularly visited location — predictable patterns create surveillance opportunities

### 3.3 Vehicle Tracking

Physical GPS tracking devices can be placed on vehicles. Check your vehicle:
- **Under the front and rear bumpers** (most common placement — magnetic trackers adhere here)
- **Wheel wells:** Reach into each wheel well and feel for foreign objects
- **Under the vehicle** along the frame rails
- **Inside the vehicle:** Under the dashboard, in the OBD-II port (can be used for tracking and data extraction)

Detection:
- A handheld RF detector (available online for $30–100) can detect active GPS trackers transmitting signals
- Passive trackers (store data for later download) are harder to detect; visual inspection is the primary method
- Professional counter-surveillance sweeps use more sophisticated equipment

---

## 4. Facial Recognition Countermeasures

### 4.1 The State of Facial Recognition

Facial recognition has been deployed by law enforcement widely and without consistent oversight:
- Chicago PD uses Clearview AI, which has scraped 20+ billion facial images from public internet sources
- CBP uses facial recognition at all major U.S. airports
- Accuracy rates vary significantly by race (documented higher error rates for darker-skinned faces)
- Mass surveillance systems operate at scale: your face in a crowd at an action can be retroactively identified

### 4.2 Effective Concealment

**What works:**
- N95 or KN95 mask covering nose, mouth, and chin — reduces visible facial landmark surface significantly
- Sunglasses or clear anti-UV glasses — conceals eye region geometry
- A hat with a brim that casts shadow over the upper face in overhead camera angles
- Combined: mask + glasses + hat provides meaningful friction against facial recognition

**What does not work as well:**
- Surgical or cloth masks that leave the nose and eyes exposed
- Infrared blocking makeup (requires perfect application, laboratory conditions to test)
- Anti-facial recognition glasses with specific designs — inconsistent effectiveness against modern systems

**Important:** Facial recognition can also use gait analysis (the way you walk), body geometry, and clothing patterns as secondary identifiers. Vary your outer clothing; choose non-distinctive footwear.

### 4.3 Photography and Documentation at Actions

- **Do not photograph other participants' faces** without explicit consent — even with the best intentions, those photos may end up in law enforcement databases through your device, social media, or legal discovery
- **Before sharing any photo from an action:** Blur all identifiable faces and remove EXIF metadata
- **Assume all your photos may eventually be seen by adversaries:** If you don't want law enforcement to have a photo, don't take it or don't store it

---

## 5. Digital Counter-Surveillance at Actions

### 5.1 Device Management in Stingray-Affected Areas

- Power off your device completely or engage airplane mode before entering the action area
- Stingrays capture IMEI and IMSI regardless of whether you make a call; they capture by association
- If your phone is off, there is no IMEI to capture
- If you need to make communications, pre-position a burner phone that is not associated with your identity and activate airplane mode immediately after use

### 5.2 Signal Metadata Considerations

Signal conceals message content, but:
- Your ISP and cell network can see that you are connecting to Signal's servers
- The times and frequency of these connections are metadata that builds a pattern-of-life picture
- Signal's "sealed sender" feature (see [Signal Guide](../digital-security/signal_guide.md)) conceals who is sending to whom from Signal's servers
- For maximum metadata protection, route Signal through Tor (using Orbot on Android, or configuring Signal's proxy settings)

### 5.3 Wi-Fi and Bluetooth Passive Surveillance

- Devices with Wi-Fi and Bluetooth enabled passively broadcast their MAC address to all nearby access points and Bluetooth receivers
- Modern devices use "randomized MAC addressing" which rotates the MAC address to prevent tracking — verify this is enabled on your device
- iOS: Settings → Wi-Fi → [Network] → Private Wi-Fi Address (enabled by default in iOS 14+)
- Android: Settings → Wi-Fi → [Network] → Advanced → Privacy → Use randomized MAC
- Bluetooth: disable entirely when not in use; active Bluetooth is a persistent tracking vector

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
