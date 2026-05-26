# streamtouch-support
> Touch Music Control for SoundTouch via Music Assistant

---

## What is StreamTouch?

StreamTouch is an iOS app that lets you control your SoundTouch 
speaker through a self-hosted Music Assistant server, directly 
from your iPhone or iPad. Search and play music from your 
connected providers, save presets, and control playback — all 
from one simple interface.

---

## Requirements

Before using StreamTouch you will need:

- A **SoundTouch** speaker connected to your local network
- A running instance of **Music Assistant** server 
  (open source, self-hosted)
- A valid **Music Assistant API bearer token**
- All devices on the **same local network**

---

## Getting Started

On first launch, StreamTouch will guide you through a 
step-by-step setup wizard:

1. **Add your speaker** — scan your network automatically 
   or enter the IP address manually
2. **Enter Music Assistant server details** — IP address 
   and port
3. **Enter your API bearer token**
4. **Test connections** — StreamTouch verifies your speaker, 
   server and player ID before launching

> You can find your bearer token in Music Assistant under 
> **Settings → API Tokens**

---

## Speaker Management (v1.2.0)

StreamTouch now supports multiple SoundTouch speakers.

### Adding a speaker
Go to **Settings → SoundTouch Speakers → Add**

| Method | When to use |
|---|---|
| **Discover** | Automatically scans your network for SoundTouch speakers |
| **Manual** | Enter IP address directly if scan does not find your speaker |

### Auto IP (DHCP)
Enable this if your speaker uses a dynamic IP address. 
StreamTouch will automatically refresh the IP address on 
each app launch using network discovery.

### Player ID
StreamTouch will attempt to automatically detect the correct 
Music Assistant Player ID for each speaker. If auto detection 
fails, use the **Auto Find** button in the speaker edit screen, 
or enter it manually.

### Switching between speakers
When multiple speakers are configured, a speaker selector 
appears at the top of the main dashboard. Tap any speaker 
to switch playback target.

---

## Frequently Asked Questions

### Where do I find my SoundTouch IP address?
Check your router's connected devices list. The speaker will 
typically appear as "SoundTouch" or similar.

> To assign a static IP to a SoundTouch speaker, use your 
> router's management page to set up a DHCP reservation. 
> The speaker itself does not have a menu for manual IP entry.
> Alternatively enable **Auto IP (DHCP)** in StreamTouch and 
> the app will find your speaker automatically.

---

### Where do I get Music Assistant Server?
You can run the Music Assistant server without Home Assistant 
by using its official Docker container. The server is available 
on Docker Hub and can be installed on any system supporting 
Docker, such as Linux, NAS devices (Synology, QNAP), or a 
Raspberry Pi.

🔗 [Music Assistant Installation Guide](https://www.music-assistant.io/installation/)

---

### Where do I find my Music Assistant Player ID?
In Music Assistant go to **Settings → Players** and select 
your SoundTouch player. The Player ID will be shown in the 
player details and will look similar to `up689e19dada87`.

> From v1.2.0 StreamTouch will attempt to detect this 
> automatically. You can also use the **Auto Find** button 
> in **Settings → SoundTouch Speakers → Edit Speaker**.

---

### Where do I generate a bearer token?
Navigate to **Settings → Users** in the Music Assistant web 
interface, select your user profile, and find the 
**Access Tokens** section to generate a new Long-Lived token.

> ⚠️ **Note:** In some versions of Music Assistant, the copy 
> button for API tokens may not behave as expected. Make sure 
> to manually select the full token text and save it to a text 
> file as a backup.
>
> 💡 **Tip:** To easily enter your token into StreamTouch, 
> email it to yourself so you can copy and paste it directly 
> on your phone.

---

### The app says connection failed during setup — what do I do?

StreamTouch tests three things during setup:

| Test | What to check if it fails |
|---|---|
| **SoundTouch Speaker** | Check IP address, confirm speaker is powered on and on same network |
| **Music Assistant Server** | Check server IP, port (default 8095) and bearer token |
| **Music Assistant Player** | Check Player ID — use Auto Find in speaker settings |

---

### Can I change my settings after setup?
Yes — tap the **gear icon** on the main dashboard at any time 
to update your settings, manage speakers or test connections.

---

### The app is not finding my speaker

- Confirm the SoundTouch speaker is powered on
- Try **Settings → SoundTouch Speakers → Add → Discover** 
  to scan for your speaker automatically
- Verify the IP address in speaker settings matches the 
  speaker's current IP
- Consider enabling **Auto IP (DHCP)** to let StreamTouch 
  find your speaker automatically on each launch
- Consider assigning a static/reserved IP to your speaker 
  in your router settings to prevent the IP changing

---

### Music Assistant is unreachable

- Confirm your Music Assistant server is running
- Check the IP address and port are correct 
  (default port is `8095`)
- Ensure your bearer token has not expired
- Use **Settings → Test Connection** to diagnose the 
  specific failure

---

### Player ID not found or auto detection failed

- Go to **Settings → SoundTouch Speakers**
- Tap the **edit** icon on your speaker
- Tap **Auto Find** next to the Player ID field
- If Auto Find fails, go to Music Assistant 
  **Settings → Players**, find your SoundTouch player 
  and copy the Player ID manually

---

## ⚠️ Caveats, Known Issues & Limitations

**SoundTouch LED/OLED Display**
For SoundTouch systems with LED/OLED displays, artist and 
track info is reliably shown when individual tracks or radio 
stations are played. When playing albums from StreamTouch, 
the display may only show the first track — this is a known 
limitation within Music Assistant's SoundTouch player support 
when using DLNA/UPnP playback and Queue Flow Mode streaming.

**Album playback only plays first track**
If StreamTouch only plays the first song when **Play Album** 
is selected, ensure that **Queue Flow Mode** is enabled in 
Music Assistant under the SoundTouch Player **Advanced** 
settings.

---

## Resetting the App

If you need to start setup again from scratch, go to 
**Settings → Full Reset (Run Setup Again)**. This will clear 
all settings and return you to the setup wizard on next launch.

---

## Privacy

StreamTouch does not collect, store or transmit any personal 
data to external servers. All communication is exclusively 
between your iOS device and your local network devices. 
Your API bearer token is stored securely in the iOS Keychain.

---

## Contact & Support

If you are experiencing an issue not covered above, 
please get in touch:

📧 [streamtouch.support@gmail.com](mailto:streamtouch.support@gmail.com)

Please include:
- Your iOS version
- Your StreamTouch version
- A brief description of the issue
- Any error messages shown in the app

---

*StreamTouch is an independent app and is not affiliated 
with Bose Corporation or the Music Assistant project.*
