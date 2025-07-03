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

## 3. DIY Custom Setups (Expert Level)

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
    5.  Develop or deploy simple, lightweight messaging or data transfer applications to communicate between the nodes over the private HaLow network.

#### **Antenna Selection (900MHz Band)**

Choosing the right antenna is critical for maximizing the performance of your Wi-Fi HaLow link. The antenna system determines the range, reliability, and coverage pattern of your network. The recommended HaLow modules (ALFA Network AHPI7292SA and AsiaRF MM610X-H06) use a standard connector type, making antenna selection straightforward.

**Antenna Connector Type:**

The **ALFA Network AHPI7292SA** and the **AsiaRF MM610X-H06** both feature a **SMA-Female** connector. Therefore, you will need to purchase antennas equipped with a **SMA-Male** connector.

*Note: The base model ALFA Network AHPI7292S uses a smaller U.FL connector. To use the SMA antennas recommended below with this model, you will need a pigtail adapter cable (U.FL to SMA-Female).*

**Understanding Gain (dBi):**

Antenna gain, measured in decibels isotropic (dBi), indicates how well the antenna converts input power into radio waves in a specific direction. A higher dBi value means the signal is more focused, leading to longer range but in a narrower beam. There is always a trade-off between gain and coverage area.

*   **Low Gain (2-5 dBi):** Wider, less-focused signal (like a floodlight). Good for general coverage and mobile nodes.
*   **High Gain (9+ dBi):** Narrower, focused signal (like a spotlight). Excellent for long-distance, fixed links.

**Omnidirectional Antennas (For Base Stations & Mobile Nodes):**

These antennas radiate signal in a 360-degree horizontal pattern, ideal for situations where you need to connect with multiple devices in any direction, such as a central base station or a moving vehicle.

1.  **L-com HG905RD-SM (5 dBi):** A high-quality, flexible "rubber duck" style antenna. Its moderate gain provides a significant range boost over stock antennas while maintaining a wide coverage pattern. The tilt-and-swivel base is useful for optimizing signal orientation.
2.  **NOYITO 915MHz 5dBi Omni Antenna:** A cost-effective and widely available option. It provides similar gain to the L-com model and is a solid choice for general-purpose use.

**Directional Ant antennas (For Point-to-Point Links):**

Directional antennas, like Yagis or Panels, focus all their power in a single direction. They are essential for creating stable, long-distance links between two fixed points, such as connecting two buildings.

1.  **L-com HG909Y-SM (9 dBi):** A compact and high-performance Yagi antenna. It provides excellent gain for medium-to-long range links while being relatively easy to mount and aim.
2.  **Proxicast 9/11 dBi LPDA Yagi:** A versatile Log-Periodic Dipole Array (LPDA) Yagi that covers the 900MHz band. This type of antenna offers very consistent performance across its frequency range and is excellent for rejecting interference from outside its main beam.

#### **Software Stack & Applications**

Once the hardware is assembled and the HaLow link is established, the system functions as a standard IP network. You can use familiar networking tools and protocols to transmit data. Here’s how to build out the software stack.

**Base Layer: OS & Drivers**

As a foundation, your Raspberry Pi must be running **Raspberry Pi OS**. On top of this, you must install the specific kernel modules and drivers provided by the HaLow HAT manufacturer (e.g., ALFA Network or AsiaRF). These drivers create the wireless network interface (e.g., `wlan1`) that the rest of the software will use. After configuration (typically setting a static IP in an ad-hoc network), this interface will behave like a standard Ethernet connection.

**Transport Layer: Simple & Robust Data Pipes**

For simple, raw data transmission, classic Linux command-line tools are extremely effective and lightweight.

*   **Example: `netcat` (nc) for a one-way chat**
    `netcat` is the Swiss-army knife of networking. It's perfect for quick tests and simple data streams.

    On the **Listening Node** (IP: 192.168.100.1):
    ```bash
    # Listen for a connection on port 1234 and print any data received
    nc -l -p 1234
    ```

    On the **Sending Node**:
    ```bash
    # Connect to the listener on port 1234. Type a message and press Enter to send.
    nc 192.168.100.1 1234
    ```

*   **Example: `socat` for a resilient, bidirectional link**
    `socat` is a more advanced version of `netcat`. It can create a more stable, bidirectional link that automatically tries to reconnect if the connection drops—a useful feature for a wireless link.

    On **Node 1** (IP: 192.168.100.1):
    ```bash
    # Listen on port 5000 and fork a new process for each connection, allowing bidirectional communication
    socat TCP4-LISTEN:5000,fork,reuseaddr STDIO
    ```

    On **Node 2** (IP: 192.168.100.2):
    ```bash
    # Connect to Node 1 on port 5000. The 'retry' and 'forever' options ensure it keeps trying to connect.
    socat TCP4:192.168.100.1:5000,retry,forever STDIO
    ```
    Now, anything typed on one terminal will appear on the other, and vice-versa.

**Application Layer: Lightweight Messaging**

While `socat` is great, a dedicated chat application can offer a better user experience. `ncat`, a modern version of `netcat` included with the Nmap suite, has a built-in chat mode.

*   **Example: `ncat` for a terminal chat room**

    First, install Nmap: `sudo apt-get update && sudo apt-get install nmap`

    On the **Host/Server Node** (IP: 192.168.100.1):
    ```bash
    # Start a chat server on port 31337, allowing up to 5 users. --chat handles multiple clients.
    ncat -l --chat -p 31337 --max-conns 5
    ```

    On any **Client Node**:
    ```bash
    # Connect to the chat server. Add a username for clarity.
    ncat 192.168.100.1 31337 --user "Node2"
    ```

**Advanced Option: Decentralized Mesh over HaLow**

It is feasible to run a higher-level mesh protocol *over* the base HaLow ad-hoc network. This allows you to connect more than two nodes and have data automatically routed between them, even if they can't all see each other directly. A prime candidate for this is **Meshtastic**.

*   **Concept:** Meshtastic has an experimental **IP Tunnel** feature. Normally, Meshtastic uses LoRa radios. However, you can configure it to use an existing IP network (like the one your HaLow link provides) as its transport layer. Each node runs the Meshtastic daemon, which creates a virtual TUN network interface. The daemons on each node then communicate with each other over the HaLow Wi-Fi link, automatically routing IP packets between any device connected to the mesh. This effectively creates a resilient, multi-hop IP network on top of your long-range HaLow backbone.
