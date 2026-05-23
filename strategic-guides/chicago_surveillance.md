# Chicago Surveillance Deep Dive: A Localized Threat Study

*Status: Level 3 Regional Analysis | Audience: Chicagoland Organizers and Direct Action Teams*

Chicago is arguably the most heavily surveilled city in the United States. The Chicago Police Department (CPD) and the Office of Emergency Management and Communications (OEMC) have built a vast, integrated network of acoustic, visual, and cellular monitoring systems designed to aggregate private and public data into a single pane of glass. This brief details the exact mechanics of the municipal grid and how to mitigate exposure.

---

## 1. The Nerve Centers: Strategic Decision Support Centers (SDSCs)

**The Threat:** SDSCs are localized, district-level fusion centers. They function as real-time command hubs, pulling data from 911 calls, public cameras, plate readers, and predictive algorithms into real-time dashboards for dispatchers and commanders.
**The Mechanics:** SDSCs integrate platforms like Genetec Citigraf. This software allows operators to view disparate sensor data on a unified map, turning isolated data points into actionable, real-time intelligence.
**Mitigation:** You cannot digitally "hack" an SDSC. Mitigation requires recognizing that *any* data point generated in public is instantly fused and analyzed. Do not rely on "getting lost in the crowd." Assume your movement timeline is being actively modeled if you are near an operational site.

## 2. The Visual Grid: PODs and the Camera Integration Programs

The true power of Chicago's camera network is how the OEMC integrates private residential and commercial cameras into the public grid.

### The Real Camera Integration Programs
Chicago operates two distinct tracks for private camera data:
1.  **The Private Sector Camera Initiative (Direct Feed):** This is for commercial and institutional properties—businesses, high-rise apartment complexes, parking garages, and sister city agencies. They install enterprise-grade systems with direct public IP addresses and specific Video Management System (VMS) compatibility (such as Genetec). OEMC operators can access these exterior cameras **live** during emergencies.
2.  **The Camera Registration Program (No Live Feed):** This is where residential Ring and Nest cameras fall. Residents register the location of their cameras on a city map. OEMC and the police **do not** have direct, live access to these feeds. If an incident occurs, detectives check the map and send an automated request to the owner asking them to voluntarily share the footage. While Ring frequently partners with companies like Flock and Axon to streamline these requests, the homeowner still has to click "approve."

### Police Observation Devices (PODs)
**The Threat:** Known locally as "blue-light cameras," these are highly visible cameras mounted on utility poles. Many of these are equipped with Pan-Tilt-Zoom (PTZ) capabilities and can be actively driven by an operator in an SDSC fusion center.
**Mitigation:** Symmetrical disruption. A high-quality N95-style face mask combined with polarized sunglasses and low-profile hats is the only reliable defense against facial mapping. Do not assemble or unmask directly beneath known POD locations.

## 3. Acoustic Surveillance: The Post-ShotSpotter Era

**The Threat (Historical & Current):** In September 2024, Chicago decommissioned the controversial $50 million ShotSpotter acoustic array. However, acoustic surveillance has not ended.
**The Mechanics:** As of 2025, CPD is piloting Alarm.com’s Shooter Detection Systems in the 15th Ward. This system fuses acoustic sensors with **infrared cameras** to reduce the notorious false-positive rate of older systems.
**Mitigation:** Thermal masking (specialized mylar-lined ponchos) is required if attempting to move undetected through the 15th Ward or areas where the pilot expands.

## 4. Vehicular Tracking: The ALPR Dragnet

**The Threat:** Automated License Plate Readers (ALPRs) are mounted on fixed poles, PODs, street sweepers, tow trucks, and mobile patrol vehicles.
**The Mechanics:** They capture the plate, time, and GPS location of every passing vehicle. This allows analysts to easily establish "patterns of life" or track a target's physical movements backward in time.
**Mitigation:** Do not drive personal or organizational vehicles to operational zones. Park at least a mile away from the target location in a dense, commercial parking structure (which confuses stationary ALPR algorithms) and transit the final mile via bicycle or the CTA using cash-purchased transit passes.

## 5. Cellular Interception: Hailstorm and Stingray Deployment

**The Threat:** Covert IMSI-catchers (commonly known as Stingrays or the upgraded Hailstorm units) are deployed during specific operations or large gatherings.
**The Mechanics:** These devices spoof legitimate cell towers to force nearby mobile phones to connect to them. They capture IMSI/IMEI numbers and can be used to track device locations or identify who was in a specific area at a specific time. They often force 4G/5G connections down to unencrypted 2G protocols.

### Rayhunter: Detecting the Threat
The Electronic Frontier Foundation (EFF) developed **Rayhunter**, an open-source tool designed specifically to detect the presence of Cell-Site Simulators.
*   **How it Works:** Rayhunter runs on Android devices and scans the cellular environment for anomalies indicative of a Stingray attack, such as sudden downgrades to 2G networks, unusual broadcast parameters, or towers missing neighbor lists.
*   **Deployment:** You can install Rayhunter on an operational Android device. For installation instructions and source code, visit the [EFF Rayhunter GitHub](https://github.com/EFForg/rayhunter) or the [Installation Guide](https://efforg.github.io/rayhunter/installation.html).

### Mitigation
*   **The Baseline:** Turn off your personal phone and leave it at home. Use a cash-purchased burner phone for operational comms.
*   **The Technical Block:** On GrapheneOS or CalyxOS devices, navigate to Network settings and **Disable 2G connections**.
*   **The Faraday Fallback:** If Rayhunter alerts you to an anomaly, or you suspect an active IMSI-catcher, power down the device and place it in an RF-shielded Faraday bag.

---
**Key OpSec Takeaway:** The threat is not just an analyst watching a live Ring feed. The threat is retroactive data correlation. An adversary might use a cell-site simulator to get a device ID, use an ALPR to link that device to a vehicle, and then request commercial surveillance footage to identify the driver.

_Last Updated: 2026_
