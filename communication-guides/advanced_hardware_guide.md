# A Security Specialist's Guide to Activist Communication Hardware

This guide provides a curated list of hardware for activists, focusing on durability, security, and maintaining communication lines in challenging environments. The recommendations range from simple, off-the-shelf gear to advanced, custom-built solutions for experts.

---

## 1. Essential Off-the-Shelf Gear

This equipment is readily available, requires minimal setup, and forms the foundation of a reliable communication kit.

### Burner Phones (Feature Phones)

A 'burner phone' should be a simple, non-smart feature phone. The goal is to minimize the digital footprint—no GPS tracking (beyond cell tower triangulation), no app data, and no cloud accounts. Key features are extreme durability and multi-day battery life.

*   **Nokia 110 4G / Nokia 800 Tough:**
    *   **Description:** These are classic, robust feature phones. The Nokia 110 is a standard, reliable candy bar phone, while the 800 Tough is IP68 water/dust resistant and MIL-STD-810G compliant, making it nearly indestructible. Both offer exceptional battery life, often lasting over a week on standby.
    *   **Best For:** Voice calls and SMS text messages only. They are perfect for anonymous, temporary communication lines.

*   **CAT S22 Flip:**
    *   **Description:** A modern, ruggedized flip phone that runs a simplified version of Android (Android 11 Go). It's IP68 and MIL-STD-810G rated, meaning it can withstand drops, dust, and water. It features a physical keypad and a touchscreen.
    *   **Best For:** Users who need slightly more functionality, like basic encrypted messaging apps (e.g., Signal) from the app store, but in a much more durable and discreet form factor than a typical smartphone. Battery life is good for a day or two of use, but not as long as a true feature phone.

### Power Banks

In situations where power is unreliable, a high-capacity, durable power bank is non-negotiable. Look for a capacity of at least 20,000mAh, which can charge a typical phone 4-6 times.

*   **Anker PowerCore Series (e.g., PowerCore 20K):**
    *   **Description:** Anker is a highly reputable brand known for reliability. While not officially 'ruggedized', their power banks are built with high-quality materials and are known to withstand significant wear and tear. They offer excellent charging speeds and capacity for their size.
    *   **Best For:** A reliable, all-around choice for keeping multiple devices charged.

*   **BioLite Charge 80 PD:**
    *   **Description:** This 20,000mAh power bank is specifically designed for outdoor and rugged use. It features a durable, impact-resistant plastic shell that can handle drops and rough handling. Its distinctive yellow color also makes it easy to find in a bag.
    *   **Best For:** Activists operating in harsh outdoor environments where durability is the top priority.

---

## 2. Resilient Communication Hardware (Ready-to-Go)

When cellular networks are down or untrustworthy, these devices allow for independent, off-grid communication.

### Meshtastic Devices

*   **What is Meshtastic?**
    Meshtastic is an open-source project that uses inexpensive, low-power LoRa (Long Range) radio modules to create a decentralized, off-grid mesh network. Users can send encrypted text messages and share GPS location data with other devices in the mesh, completely independent of cellular service or the internet. Each device acts as a node, relaying messages for others to extend the network's range far beyond what a single device could achieve.

*   **Recommended Pre-built Devices:**
    *   **LILYGO T-Beam / T-Echo:** These are highly popular, all-in-one boards that come with a LoRa chip, a GPS module, a screen, and a battery holder. They are widely supported by the Meshtastic community and are designed to work out of the box with a simple firmware flash.
    *   **Heltec Wireless Stick Lite (V3):** A more compact and budget-friendly option. It includes the LoRa chip and a small OLED screen, making it a great entry-level device for building a portable, pocket-sized mesh communicator. It's one of the most common devices for getting started with Meshtastic.

---

## 3. Advanced Network Analysis Tools (for Defensive Auditing)

These tools are for technically-inclined users to audit their own security and detect potential threats in their environment. The focus here is strictly defensive: understanding attack vectors to better protect oneself and others.

### Flipper Zero

*   **What is it?**
    The Flipper Zero is a portable, multi-tool for pentesters and hardware enthusiasts. It can read, emulate, and analyze a wide range of wireless signals, including Sub-GHz radio (like key fobs), RFID, NFC, and Bluetooth.

*   **Defensive Uses:**
    *   **RFID/NFC Security Check:** An activist can use the Flipper Zero to test their own RFID/NFC access cards (e.g., for a co-working space or apartment building) to see if they use insecure, easily clonable protocols. This knowledge allows them to request a more secure card or take other precautions.
    *   **Understanding Physical Access Control:** By analyzing signals from their own car key fobs or garage door openers, they can learn to distinguish between insecure static codes and more secure rolling codes, raising their awareness of potential physical security vulnerabilities.

### Hak5 WiFi Pineapple

*   **What is it?**
    The WiFi Pineapple is a specialized Wi-Fi auditing tool designed for penetration testers. Its primary function is to create a 'rogue access point' to perform man-in-the-middle (MITM) attacks, capturing traffic from users who connect to it.

*   **Defensive Uses:**
    *   **Detecting 'Evil Twin' Attacks:** In a protest environment, adversaries may set up malicious Wi-Fi hotspots with inviting names (e.g., 'Free_Protest_WiFi') to intercept communications. By understanding how a Pineapple works, an activist can become highly suspicious of such networks. A user with a Pineapple can use its scanning features to get a clear picture of all nearby access points, helping to identify suspicious or spoofed network names and warn others not to connect.
    *   **Reinforcing Security Best Practices:** The sheer ease with which a Pineapple can intercept traffic underscores the critical importance of **always using a trusted VPN** on any Wi-Fi network that is not your own. It serves as a powerful educational tool on why one should never trust an unknown network.

---

## 4. DIY Custom Setups (Expert Level)

This project is for experts comfortable with hardware, Linux, and networking. It outlines a blueprint for a custom, long-range, low-power data link that is completely independent of existing infrastructure.

### Project Blueprint: Raspberry Pi with 802.11ah (Wi-Fi HaLow)

*   **Concept:**
    Wi-Fi HaLow (IEEE 802.11ah) is a new Wi-Fi standard that operates in the Sub-1GHz frequency band (around 900MHz). Unlike standard 2.4/5GHz Wi-Fi, its signals travel much farther (1km+) and penetrate obstacles more effectively. While the data rates are lower, it is perfect for creating a private, long-range network for sending small text messages, GPS coordinates, or data from sensors. This setup creates a point-to-point or small mesh data link that is not LoRa, not cellular, and not standard Wi-Fi, making it a unique and resilient communication channel.

*   **Components:**
    1.  **Raspberry Pi:** A Raspberry Pi 4 or 5 is recommended for its processing power and standard 40-pin GPIO header.
    2.  **Wi-Fi HaLow Module:** The **ALFA Network AHPI7292S** or the **AsiaRF MM610X-H06**. These are commercially available modules designed as a Raspberry Pi HAT (Hardware Attached on Top). They connect directly to the Pi's GPIO pins and provide the 802.11ah radio functionality.
    3.  **Battery Solution:** A **PiJuice HAT**. This is a battery and power management board that sits between the Pi and the HaLow HAT. It contains an onboard battery and can manage charging, providing a clean, uninterruptible power supply for field use.
    4.  **Rugged Case:** A weatherproof, IP65-rated project enclosure, such as the **Sixfab IP65 Outdoor Project Enclosure**. These cases are designed to house a Raspberry Pi with one or more HATs and provide protection from rain, dust, and impacts. They often include gaskets for antenna pass-throughs.

*   **Project Outline:**
    1.  Assemble the hardware stack: Raspberry Pi on the bottom, PiJuice HAT in the middle, and the Wi-Fi HaLow HAT on top.
    2.  Install the stack into the rugged enclosure, ensuring weatherproof seals for the antenna and any power cables.
    3.  Install Raspberry Pi OS and the necessary drivers and software for the HaLow HAT, provided by the manufacturer (e.g., ALFA Network, AsiaRF).
    4.  Configure two or more of these units to create an ad-hoc network. This will involve setting up static IP addresses and configuring the HaLow interface.
    5.  Develop or deploy simple, lightweight messaging or data transfer applications (e.g., using netcat, socat, or custom Python scripts) to communicate between the nodes over the private HaLow network.
