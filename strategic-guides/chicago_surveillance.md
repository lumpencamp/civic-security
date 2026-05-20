# Chicago Surveillance Deep Dive: A Localized Threat Study

*Status: Level 3 Regional Analysis | Audience: Chicagoland Organizers and Direct Action Teams*

Chicago is arguably the most heavily surveilled city in the United States. The Chicago Police Department (CPD) has built a vast, integrated network of acoustic, visual, and cellular monitoring systems designed to track movement and association across Cook County. This brief details the exact mechanics of the municipal grid and how to mitigate exposure.

---

## 1. The Nerve Centers: Strategic Decision Support Centers (SDSCs)

**The Threat:** SDSCs are localized, high-tech intelligence hubs deployed in nearly every CPD district. They function as real-time fusion centers, ingesting data from thousands of sources and feeding it directly to patrol units and tactical teams.
**The Mechanics:** SDSCs integrate the Genetec Citigraf platform. This software pulls live feeds from POD cameras, private security cameras, ALPRs, and 911 calls, using predictive analytics to map "crime risk" and coordinate rapid response.
**Mitigation:** You cannot digitally "hack" an SDSC. Mitigation requires recognizing that *any* data point generated in public is instantly fused and analyzed. Do not rely on "getting lost in the crowd." Assume your movement timeline is being actively modeled if you are near an operational site.

## 2. The Visual Grid: POD Cameras and Genetec Clearview AI

**The Threat:** Police Observation Devices (PODs), known locally as "blue-light cameras," are ubiquitous. There are over 30,000 publicly and privately owned cameras linked into the CPD network.
**The Mechanics:** These cameras do not merely record; they are increasingly integrated with facial recognition systems like Clearview AI, which can map a face captured on a POD camera to social media profiles and state databases.
**Mitigation:**
*   **Physical:** CV Dazzle and asymmetrical makeup are largely ineffective against modern AI. High-quality, N95-style face masks combined with polarized sunglasses and low-profile hats are the only reliable defense against facial mapping.
*   **Behavioral:** Do not look up at blue-light boxes. Do not assemble or unmask directly beneath known POD locations. Use tools like the "Chicago POD Camera Map" (maintained by local activists) to plan routes that minimize exposure.

## 3. Acoustic Surveillance: The Post-ShotSpotter Era

**The Threat (Historical & Current):** In September 2024, Chicago decommissioned the controversial $50 million ShotSpotter acoustic array. However, acoustic surveillance has not ended.
**The Mechanics:** As of 2025, CPD is piloting Alarm.com’s Shooter Detection Systems in the 15th Ward. This system fuses acoustic sensors with **infrared cameras** to reduce the notorious false-positive rate of older systems.
**Mitigation:** The introduction of infrared means night operations are no longer shielded by darkness in the pilot zones. Thermal masking (specialized mylar-lined ponchos) is required if attempting to move undetected through the 15th Ward or areas where the pilot expands.

## 4. Vehicular Tracking: The ALPR Dragnet

**The Threat:** Automated License Plate Readers (ALPRs) are mounted on CPD cruisers, street sweepers, tow trucks, and stationary poles across the city.
**The Mechanics:** These cameras constantly scan plates, logging time, date, and GPS coordinates into databases accessible by the CPD and federal agencies. They create a massive, searchable history of your vehicle's movements.
**Mitigation:**
*   **Operational Transit:** Do not drive a vehicle registered to your true name or a known activist organization directly to an action.
*   **Parking Distancing:** Park at least a mile away from the target location in a dense, commercial parking structure (which confuses stationary ALPR algorithms) and transit the final mile via bicycle or the CTA.
*   **Transit Passes:** Buy CTA Ventra cards with **cash only**. Using a credit card links your transit movements directly to your financial identity.

## 5. Cellular Interception: Hailstorm and Stingray Deployment

**The Threat:** Covert IMSI-catchers (commonly known as Stingrays or the upgraded Hailstorm units) are actively deployed by CPD tactical units and federal partners during large-scale protests.
**The Mechanics:** These devices, often mounted in unmarked vans or small aircraft, mimic legitimate cell towers. Your phone connects to them, allowing the operator to harvest your IMSI (device identity), map your exact location, and potentially intercept unencrypted SMS/calls. They often force 4G/5G connections down to unencrypted 2G protocols.
**Mitigation:**
*   **The Baseline:** Turn off your personal phone and leave it at home. Use a cash-purchased burner phone for operational comms.
*   **The Technical Block:** On GrapheneOS or CalyxOS devices, navigate to Network settings and **Disable 2G connections**. This nullifies the most common downgrade attacks used by older Stingray models.
*   **The Faraday Fallback:** If you suspect an active IMSI-catcher in the area (e.g., sudden, massive battery drain or dropping to EDGE network), power down the device and place it in an RF-shielded Faraday bag. Do not rely solely on Airplane mode.

_Last Updated: 2026_
