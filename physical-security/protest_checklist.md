# Tactical Field Deployment Checklist

*Status: Logistics & Field Readiness Manual | Audience: Direct Action Teams and Field Organizers*

Physical safety and digital security are inextricably linked during any direct action event. A failure in one domain instantly compromises the other. This checklist follows a strict chronological deployment schedule: **T-Minus 72 Hours**, **T-Minus 24 Hours**, **T-Minus 2 Hours**, **During the Action**, and **Post-Action**.

> **Mandatory prerequisite:** Before using this checklist, complete the [Threat Modeling Guide](../digital-security/threat_modeling_guide.md) for your specific action. The appropriate level of precaution scales with your threat tier.

---

## Phase 0: T-Minus 72 Hours — Planning and Coordination

### Organizational Preparation
- [ ] **Threat assessment complete:** Action-specific threat model reviewed by security team
- [ ] **Roles assigned:** Action lead, legal observer liaison, medic(s), jail support coordinator, communications coordinator, media contact (if applicable)
- [ ] **Affinity groups formed:** Groups of 4–7 people who will act together, stay together, and be responsible for each other
- [ ] **Decision-making protocol agreed:** What decisions require affinity group consensus vs. action lead authority? Under what conditions do affinity groups leave independently?
- [ ] **Legal support secured:** NLG or equivalent contacted, legal observers requested, emergency number distributed
- [ ] **Medical support secured:** Street medics invited or identified, first aid locations scouted
- [ ] **Communications plan established:** Primary channel (Signal), backup channel (Meshtastic or agreed alternate), out-of-band emergency contact

### Jail Support Setup
- [ ] **Jail support coordinator designated:** This person does NOT attend the action. They remain accessible by phone.
- [ ] **Participant information collected:** Full legal name, date of birth, any critical medical information (allergies, medications, conditions), emergency contact, for every person who might be arrested
- [ ] **Bail fund status confirmed:** Is the fund accessible? Who has authorization to disperse funds?
- [ ] **Arraignment monitoring plan:** Who will check court schedules if participants are held overnight?

---

## Phase 1: T-Minus 24 Hours — Preparation and Device Security

### Digital Preparation
- [ ] **Full device backup:** Back up your primary phone to a secure, offline, encrypted external drive. If your device is seized, this backup preserves your data.
- [ ] **Device decision made:** Are you bringing your primary phone, a burner, or no phone at all? This decision depends on your threat model.
  - **Low-risk actions** (permitted marches, community meetings): Primary phone acceptable with configurations below
  - **Medium-risk actions** (unpermitted actions, civil disobedience): Burner preferred; if primary phone, aggressive sanitization
  - **High-risk actions** (potential felony charges, T3/T4 threat environment): No personal phone. Burner or no device.
- [ ] **Biometric lockdown:** Disable Face ID and Touch ID. Set a strong alphanumeric passphrase (minimum 12 characters: mixed case, numbers, symbols). Record this passphrase somewhere secure you can access after release.
- [ ] **Data sanitization (if bringing primary phone):**
  - Delete all non-essential organizational data, photos, and messages
  - Empty "Recently Deleted" folders (photos and notes)
  - Clear browser history and cookies
  - Log out of sensitive apps (banking, work email)
  - Disable iCloud/Google Drive sync temporarily
  - Review and revoke unnecessary app permissions
- [ ] **Signal configuration:**
  - Enable disappearing messages in all chats (1 week or shorter for operational contacts)
  - Enable registration lock (Settings → Account → Registration Lock)
  - Enable Note to Self as a secure memo pad
  - Confirm your safety number with key contacts in person if possible
- [ ] **Emergency contact written:** NLG/FDLA number written on forearm in permanent marker
- [ ] **Lawyer number saved:** Stored in phone under a neutral name (in case phone is seized and browsed) AND memorized or written on body

### Burner Phone Procurement (if applicable)
- [ ] **Purchased with cash** at a physical store (not online — no shipping address link)
- [ ] **Purchased while not carrying your personal phone** (personal phone's location data would place you at the purchase location)
- [ ] **Purchased at a store without facial recognition** (large chain stores increasingly use it)
- [ ] **Prepaid SIM purchased with cash** at a separate location and time if possible
- [ ] **Device activated over a public Wi-Fi network** you do not regularly use, ideally with a VPN or Tor running
- [ ] **No Google/Apple accounts linked** — use without signing in, or create a new anonymous account over Tor
- [ ] **Only necessary apps installed:** Signal, a map downloaded offline (OsmAnd, Maps.me), NLG phone number saved

### Physical and Legal Preparation
- [ ] **Medical information written on body:** Blood type, critical allergies, and any conditions that emergency responders must know — written on inner forearm or thigh in permanent marker
- [ ] **Personal identification decision:** Know your state's laws. In Illinois, you must provide your name if lawfully detained. Consider whether to carry ID — it confirms your identity to police if detained, but also to hospitals if injured.
- [ ] **Legal briefing attended or reviewed:** Know the specific laws relevant to this action in this jurisdiction
- [ ] **Medical conditions disclosed:** To your affinity group and medics — not to your whole organization

---

## Phase 2: T-Minus 2 Hours — Staging and Final Lockdown

*This phase occurs at a secure staging area, away from the action zone, before transiting.*

### Physical Gear and PPE
- [ ] **Face concealment:**
  - N95 mask (highest efficacy against facial recognition and chemical irritants)
  - Polarized or dark lens sunglasses
  - Hat with a low brim (unbranded)
  - *Note:* Facial recognition systems analyze the geometry of the upper face — covering the nose and mouth while leaving the eyes visible is insufficient. Cover forehead-to-chin if concealment is your goal.
- [ ] **Clothing:**
  - Unbranded, solid-color, layered clothing. Distinctive logos, patterns, or colors create identifiable "markers" in surveillance video.
  - Layering allows you to change appearance quickly (outer jacket removal changes your profile in seconds)
  - Closed-toe, heavy-soled footwear
  - Weather-appropriate (hypothermia is a real medical risk at prolonged outdoor actions in winter)
- [ ] **First aid kit:** At minimum, for your affinity group:
  - Nitrile gloves
  - Gauze pads and medical tape
  - Antiseptic wipes
  - Eye wash (saline) — for pepper spray exposure
  - Mylar emergency blanket
  - Any personal medications (carry enough for 24 hours in case of extended detention)
- [ ] **Nutrition and hydration:**
  - Water (minimum 1 liter per person)
  - High-calorie food (nuts, energy bars — no perishables)
  - Medications, including psychiatric medications — missing a dose during detention is a real harm
- [ ] **Cash only:** No credit cards traceable to your identity. Cash for transportation, food, bail phone calls. Recommended minimum: $40.

### Device Final Configuration
- [ ] **Final device check:** Confirm biometrics disabled. Confirm passcode set.
- [ ] **Airplane mode decision:** At high-risk actions, consider enabling airplane mode on arrival (prevents Stingray capture of IMEI/IMSI, prevents real-time location tracking via cell towers). You can still use offline maps and take photos; you will lose cellular communication.
- [ ] **Faraday bag ready:** If you are not using the device at all, place it in the Faraday bag before entering the action zone.
- [ ] **Photo plan:** If documenting the action, use a separate dedicated camera (or burner) for photography. Metadata on photos (EXIF) includes time and GPS coordinates; scrub or disable GPS before taking photos.
- [ ] **Affinity group check-in completed:** Every member has confirmed: they have the jail support number, they know the dispersal plan, they know the medical protocol, they know the communications channel.

---

## Phase 3: During the Action

### Maintaining OPSEC in the Field
- [ ] **Stay with your affinity group** — do not fragment unless dispersal is ordered
- [ ] **Communicate only on secure channels** — no public social media about operational specifics in real time
- [ ] **Do not photograph faces** of other participants without explicit consent — even in public spaces, distributing photos can expose people who wanted anonymity
- [ ] **Do not livestream operational specifics** — livestreams are monitored in real time by law enforcement social media units
- [ ] **Witness and document police conduct** — note badge numbers, vehicle numbers, names of any officer making orders or using force

### Medical Protocol
- [ ] **Know the signs of chemical irritant exposure:**
  - Eyes: intense burning, involuntary closing, temporary vision loss — do not rub; flush immediately with water or saline
  - Respiratory: coughing, difficulty breathing — move upwind, fresh air
  - Skin: burning, redness — flush with large amounts of water; do NOT use milk (despite popular belief, milk is less effective than water and can introduce contamination)
- [ ] **Know the signs of concussion/head injury:** If struck in the head, do not continue to participate. Seek medical attention.
- [ ] **Know the location of the nearest predetermined safe location** (staging area or emergency medical point)

### If You Are Detained or Arrested
- [ ] Say clearly: *"I am invoking my right to remain silent and my right to an attorney."*
- [ ] Say nothing else. Do not explain. Do not negotiate. Do not try to talk your way out.
- [ ] Notify your affinity group that you are being detained (if safe to do so — a raised fist, a specific call word, or a text before your phone is taken)
- [ ] Your affinity group's responsibility: immediately contact jail support with your name and last known location

---

## Phase 4: Post-Action — 0 to 48 Hours After

### Immediate Post-Action (within 1 hour)
- [ ] **Check-in protocol:** All affinity group members check in with the communications coordinator. Any missing member triggers jail support protocol immediately.
- [ ] **Debrief with your affinity group** at a secure location away from the action zone. What happened? Who was detained? What did you observe about police tactics?
- [ ] **Report to jail support:** Confirm all check-ins or report unaccounted members with full identifying information.
- [ ] **Document police conduct:** While memory is fresh, write down officer names, badge numbers, vehicle numbers, any use of force witnessed, any orders heard.

### Digital Post-Action
- [ ] **Wipe the burner** if used: factory reset, remove the SIM, dispose of the device and SIM separately if you will not reuse it
- [ ] **Delete operational communications** that have served their purpose. Signal disappearing messages should have handled this; verify manually.
- [ ] **Change credentials** on any accounts that were accessed on the operational device, especially if the device status is uncertain
- [ ] **EXIF scrub all photos** before sharing. Use ExifTool, Scrambled EXIF (Android), or Photo Investigator (iOS) to verify photos contain no metadata before distribution.
- [ ] **Do not post photos of other participants without their consent** — even blurred images can be de-anonymized
- [ ] **Disable unnecessary cloud sync** — re-enable with caution

### Physical Post-Action
- [ ] **Preserve evidence of police misconduct:** Clothing with tear gas residue, injuries photographed, witness accounts documented
- [ ] **Medical follow-up:** Anyone exposed to chemical agents, struck by projectiles, or experiencing symptoms should seek medical evaluation
- [ ] **Psychological debrief:** Witnessing or experiencing police violence is traumatic. Normalize check-ins on emotional wellbeing. See [Mental Health & Psychological Security](./mental_security.md).

### Organizational Follow-Up
- [ ] **Full debrief meeting** (within 48 hours): What worked? What failed? What changed in the threat environment?
- [ ] **Update threat model** if new tactics, surveillance technologies, or legal developments were observed
- [ ] **Support arrested participants:** Legal defense, emotional support, covering missed work shifts
- [ ] **Review jail support contacts and bail fund** — replenish if used

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
