# Bluetooth Trackers: Detection and Defense

*Status: Level 1 | Audience: All members who travel to sensitive locations*

Bluetooth tracking devices (Apple AirTags, Samsung SmartTags, Tile, and generic clones) are inexpensive, small, and can be covertly placed on vehicles, in bags, or on clothing. They use crowd-sourced networks of phones to report location data back to whoever placed them — creating persistent, low-effort tracking that does not require any dedicated surveillance team.

---

## 1. How Bluetooth Trackers Work

### 1.1 The Mechanics

Modern Bluetooth trackers broadcast a rotating Bluetooth Low Energy (BLE) signal. Every compatible smartphone within range automatically and silently detects these signals and uploads the tracker's location and time to the manufacturer's cloud servers. The tracker's owner can then query the cloud to see where the tracker has been.

**Apple AirTag network:**
- Over 1 billion iPhones participate in the "Find My" network
- Each iPhone passively, automatically scans for AirTag signals and reports location
- AirTag owners see location history through the Find My app
- **Accuracy:** Can be accurate to within a few meters in dense areas with many iPhones; less accurate in rural areas

**Samsung SmartTag, Tile, and similar devices:** Use similar crowd-sourced networks of Samsung devices, Tile app users, etc.

### 1.2 Anti-Stalking Features (and Their Limitations)

Apple, Samsung, and Tile have implemented anti-stalking features, but they are imperfect:

**Apple AirTag:**
- If an AirTag not registered to your Apple ID is traveling with you, your iPhone will alert you after 8–24 hours (iOS 14.5+ required)
- The AirTag also emits an audible beep after being separated from its registered device for an extended period (72 hours initially; this was extended to 8–24 hours after complaints from domestic violence advocates)
- **Limitation:** Android users do not receive automatic alerts. Apple released the Android "Tracker Detect" app, but it requires manual scanning — it does not run in the background automatically.
- **Limitation:** The anti-stalking alert only fires if the owner and you are separated. If you are being tracked at home and the owner drives by periodically, the timer resets.
- **Limitation:** AirTags can be modified to disable the speaker.

**Samsung/Tile:**
- Similar voluntary anti-stalking policies but with varying implementation quality
- Less reliable than Apple's system due to smaller device ecosystems

---

## 2. Detection Methods

### 2.1 iPhone Users: Find My Network Detection

*Settings → Privacy & Security → Location Services → Find My → Alerts about unknown devices*

iPhone automatically alerts you when an unknown tracker has been traveling with you. This runs in the background and requires no action from you. Keep this enabled.

### 2.2 Android Users: Manual Scanning

Android does not receive automatic background alerts. Use these apps to scan manually:

**AirGuard (TU Darmstadt — free, open source):**
- Available on Google Play
- Runs background scans periodically (by default every 4 hours — reduce to hourly for sensitive use)
- Alerts you to unknown Bluetooth trackers traveling with you
- More effective than Apple's official Tracker Detect app

**Apple Tracker Detect:**
- Available on Google Play
- Requires manual scanning — does not run in background
- Appropriate for manual pre-action sweeps

**Manual Bluetooth scan:**
- Settings → Bluetooth → scan for nearby devices
- Any unfamiliar device repeatedly appearing near you across different locations may be a tracker
- Trackers rotate their Bluetooth addresses (to prevent easy tracking of the tracker itself), so they may appear as "Unknown Accessory" or with rotating random identifiers

### 2.3 Physical Inspection

When you suspect tracker placement or before sensitive travel, physically inspect:

**On vehicles (highest risk placement points):**
- Under front and rear bumpers (most common: magnetic attachment)
- Inside all four wheel wells (run your hand around the inside of each)
- Under the vehicle along the frame rails (use a mirror on a stick or phone camera)
- Inside the trailer hitch receiver (if present)
- Behind license plates
- Under hood (near battery — some trackers use vehicle power)
- OBD-II port (inside the vehicle, under the dashboard — OBD dongles with cellular capability can be both tracker and data logger)

**On bags and personal items:**
- Check all pockets, including interior pockets
- Check inside laptop bags, zippers, and pouches
- Check jacket pockets, especially outer ones

**What to look for:**
- AirTag: coin-sized (38mm diameter) silver disk, about the thickness of four coins stacked
- Samsung SmartTag: rectangular, small plastic tag, about 36mm × 28mm
- Tile: various form factors; small square or rectangle
- Generic clones: vary widely; typically small plastic rectangles or discs

**RF detectors:** Handheld RF detectors ($30–100 range) can detect Bluetooth signals from active trackers even when they are not immediately visible. Sweep these around your vehicle before sensitive travel.

---

## 3. Response to Discovered Trackers

### 3.1 Do Not Immediately Destroy It

Resist the impulse to destroy a found tracker immediately. A tracker is evidence:
- Document its location with photos (note the time and location in your photo notes)
- Do not handle with bare hands if you intend to preserve fingerprints (use gloves or a bag)
- The tracker's serial number may help law enforcement or legal counsel identify who registered it

### 3.2 Consult Before Acting

- Contact your lawyer before taking any further action
- If law enforcement placed the tracker, destroying it could be evidence tampering
- If a private party placed it, you may have civil claims (stalking, harassment, trespass) that benefit from preserved evidence

### 3.3 If You Need to Disable It Immediately

If you are in immediate danger or the legal situation clearly permits:
- AirTag: Press and rotate the back cover counterclockwise; remove the CR2032 battery
- Samsung SmartTag: Remove battery or follow manufacturer's disable procedure
- Tile: Remove battery or power it off
- Generic clones: Remove visible battery

### 3.4 Document the Surveillance

Finding a tracker on your vehicle or belongings is significant evidence of surveillance and potentially of a crime:
- File a police report (ironic but creates a legal record)
- Contact the NLG or a civil rights attorney
- Document everything in writing with dates and times
- Coordinate with your organization's security team

---

## 4. Preventive Practices

### 4.1 Pre-Action Vehicle Sweeps

Before driving to any sensitive location (meeting, action, source meeting):
1. Sweep the vehicle using one of the detection apps while walking around it
2. Physically inspect the four highest-risk locations: front bumper, rear bumper, wheel wells, OBD port
3. Note the time — if you find a tracker later, the sweep timing establishes when it was placed

### 4.2 Varying Parking Locations

If your vehicle is tracked to a consistent parking location (home, organizational meeting location), adversaries can confirm associations:
- Vary where you park when traveling to sensitive locations
- Park far from the destination and walk the final distance
- Consider carpooling in vehicles not associated with your identity for the highest-sensitivity situations

### 4.3 Separating Vehicle and Activity Identity

- Do not park your personal vehicle at action locations if possible; use transit, ride-share dropped a distance away, or vehicles not linked to your identity
- ALPRs and Stingrays can both reveal vehicle location; a vehicle at the action location creates an identity link even without a tracker

---

*This guide does not constitute legal advice. Laws vary by jurisdiction. Detecting and removing a tracker placed by law enforcement may have legal implications — consult a lawyer.*

[← Back to Index](../index.md)
