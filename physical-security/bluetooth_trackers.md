# Detecting and Defeating Physical Trackers (AirTags)

Physical surveillance no longer requires an expensive, wired GPS tracker. Cheap, widely available Bluetooth trackers like Apple AirTags, Tile, and Samsung SmartTags are increasingly used by stalkers, counter-protesters, and law enforcement to track activists.

## The Threat Model

These devices do not have their own internet connection or GPS chips. Instead, they constantly broadcast a Bluetooth signal. If *any* smartphone (e.g., an iPhone for AirTags) passes nearby, that phone detects the signal and secretly reports the tracker's location to the cloud (Apple's "Find My" network).

Because there are hundreds of millions of smartphones in the world, these trackers provide near-real-time location data in urban environments.

*   **How they are used:** An adversary slips a tracker into your backpack, the pocket of your coat, or magnetically attaches it to the wheel well or undercarriage of your car during a protest.

## How to Detect Trackers

Both Apple and Google have built-in alerts for unwanted tracking, but they have limitations.

### On iPhone (iOS)
*   If an unknown AirTag is moving with you, your iPhone will eventually display a notification: **"AirTag Found Moving With You."**
*   **Limitation:** This alert is not immediate. It may take several hours or a change in location to trigger.

### On Android
*   Modern Android phones now have native "Unknown Tracker Alerts" built into the operating system.
*   Go to **Settings > Safety & emergency > Unknown tracker alerts**. Ensure this is toggled ON.
*   You can also manually scan your surroundings from this menu if you suspect you are being tracked.

### Third-Party Detection Apps
If you are using a de-Googled phone (like GrapheneOS) or an older device, you must manually install a detection app:
*   **AirGuard (Android):** Highly recommended. It runs in the background and scans for AirTags, Tiles, and other common trackers.
*   **Apple's Tracker Detect (Android):** Apple's official app for Android, but it requires you to *manually* initiate a scan. It does not scan in the background.

## What to do if you find a tracker

1.  **Do Not Go Home or to a Sensitive Location:** If you receive an alert or find a tracker, do not go to your house, your workplace, or an organizing space. Drive to a busy, public location.
2.  **Locate the Device:** Use the app to make the tracker play a sound. Search your bags, vehicle undercarriage, and pockets thoroughly.
3.  **To Disable or Not to Disable?**
    *   **If you want to stop tracking:** Most trackers can be disabled by simply removing the battery. For an AirTag, press down on the polished silver back cover and rotate counter-clockwise to remove the CR2032 battery.
    *   **If you want to gather evidence/mislead:** Leave the battery in, but place the tracker on a random public bus or a cross-country train to send the adversary on a wild goose chase, or turn it over to a trusted lawyer if you plan to file a police report (though be cautious involving law enforcement).

_Last Updated: 2026_
