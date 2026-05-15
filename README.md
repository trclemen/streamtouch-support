# streamtouch-support
> Touch Music Control for SoundTouch via Music Assistant

---

## What is StreamTouch?

StreamTouch is an iOS app that lets you control your SoundTouch speaker through a self-hosted Music Assistant server, directly from your iPhone or iPad. Search and play music from your connected providers, save presets, and control playback — all from one simple interface.

---

## Requirements

Before using StreamTouch you will need:

- A **SoundTouch** speaker connected to your local network
- A running instance of **Music Assistant** server (open source, self-hosted)
- A valid **Music Assistant API bearer token**
- All devices on the **same local network**

---

## Getting Started

On first launch, StreamTouch will guide you through a step-by-step setup wizard to enter your:

- SoundTouch speaker IP address
- Music Assistant server IP address and port
- Music Assistant Player ID
- API bearer token

> You can find your bearer token in Music Assistant under **Settings → API Tokens**

---

## Frequently Asked Questions

### Where do I find my SoundTouch IP address?
Check your router's connected devices list. The speaker will typically appear as "SoundTouch" or similar.

> To assign a static IP to a SoundTouch speaker, use your router's management page to set up a DHCP reservation. The speaker itself does not have a menu for manual IP entry.

---

### Where do I get Music Assistant Server?
You can run the Music Assistant server without Home Assistant by using its official Docker container. The server is available on Docker Hub and can be installed on any system supporting Docker, such as Linux, NAS devices (Synology, QNAP), or a Raspberry Pi.

🔗 [Music Assistant Installation Guide](https://www.music-assistant.io/installation/)

---

### Where do I find my Music Assistant Player ID?
In Music Assistant go to **Settings → Players** and select your SoundTouch player. The Player ID will be shown in the player details and will look similar to `up689e19dada87`.

---

### Where do I generate a bearer token?
Navigate to **Settings → Users** in the Music Assistant web interface, select your user profile, and find the **Access Tokens** section to generate a new Long-Lived token. These tokens are required for API authentication and connecting external applications.

> ⚠️ **Note:** In some versions of Music Assistant, the copy button for API tokens may not behave as expected. Make sure to manually select the full token text and save it to a text file as a backup.
>
> 💡 **Tip:** To easily enter your token into StreamTouch, email it to yourself so you can copy and paste it directly on your phone.

---

### The app says connection failed during setup — what do I do?

- Check all IP addresses are correct
- Ensure your iPhone and all devices are on the same Wi-Fi network
- Confirm your Music Assistant server is running
- Check your bearer token is copied in full with no extra spaces

---

### Can I change my settings after setup?
Yes — tap the **gear icon** on the main dashboard at any time to update your settings.

---

### The app is not finding my speaker

- Confirm the SoundTouch speaker is powered on
- Verify the IP address in settings matches the speaker's current IP
- Consider assigning a static/reserved IP to your speaker in your router settings to prevent it changing

---

### Music Assistant is unreachable

- Confirm your Music Assistant server is running
- Check the IP address and port are correct (default port is `8095`)
- Ensure your bearer token has not expired

---

## ⚠️ Caveats, Known Issues & Limitations

**SoundTouch LED/OLED Display**
For SoundTouch systems with LED/OLED displays, artist and track info is reliably shown when individual tracks or radio stations are played. When playing albums from StreamTouch, the display may only show the first track — this is a known limitation within Music Assistant's SoundTouch player support when using DLNA/UPnP playback and Queue Flow Mode streaming.

**Album playback only plays first track**
If StreamTouch only plays the first song when **Play Album** is selected, ensure that **Queue Flow Mode** is enabled in Music Assistant under the SoundTouch Player **Advanced** settings.

---

## Resetting the App

If you need to start setup again from scratch, go to **Settings → Full Reset (Run Setup Again)**. This will clear all settings and return you to the setup wizard on next launch.

---

## Privacy

StreamTouch does not collect, store or transmit any personal data to external servers. All communication is exclusively between your iOS device and your local network devices. Your API bearer token is stored securely in the iOS Keychain.

---

## Contact & Support

If you are experiencing an issue not covered above, please get in touch:

📧 [streamtouch.support@gmail.com](mailto:streamtouch.support@gmail.com)

Please include:
- Your iOS version
- A brief description of the issue
- Any error messages shown in the app

---

*StreamTouch is an independent app and is not affiliated with Bose Corporation or the Music Assistant project.*
