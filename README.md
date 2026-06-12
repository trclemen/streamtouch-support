# streamtouch-support
> Touch Music Control for SoundTouch via Music Assistant

---
## Contents

- [What is StreamTouch?](#what-is-streamtouch)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
- [Speaker Management](#speaker-management)
- [WiFi Reconnection Wizard](#wifi-reconnection-wizard)
- [Speaker Grouping](#speaker-grouping)
- [StreamTouch Local Cloud (SLC)](#streamtouch-local-cloud-slc)
  - [What is SLC?](#what-is-slc)
  - [Do I need SLC?](#do-i-need-slc)
  - [How SLC works](#how-slc-works)
  - [Where Does SLC Need to Be?](#where-does-slc-need-to-be)
  - [SLC Requirements](#slc-requirements)
  - [Where to run SLC](#where-to-run-slc)
  - [Installing SLC](#installing-slc)
  - [Platform-Specific Network Configuration](#platform-specific-network-configuration)
  - [Saving a radio station as a hardware preset](#saving-a-radio-station-as-a-hardware-preset)
  - [Hardware Preset Viewer](#hardware-preset-viewer)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Caveats, Known Issues and Limitations](#caveats-known-issues-and-limitations)
- [Resetting the App](#resetting-the-app)
- [Privacy](#privacy)
- [Contact and Support](#contact-and-support)

---

## What is StreamTouch?

StreamTouch is an iOS app that lets you control your SoundTouch
speaker through a self-hosted Music Assistant server, directly
from your iPhone or iPad. Search and play music from your
connected providers, save presets, control playback, reconnect
speakers to WiFi and save radio stations as hardware presets —
all from one simple interface.

---

## Requirements

Before using StreamTouch you will need:

- A **SoundTouch** compatible speaker connected to your
  local network
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
   and port or use Scan for Music Assistant
3. **Enter your API bearer token**
4. **Test connections** — StreamTouch verifies your speaker,
   server and player ID before launching

> You can find your bearer token in Music Assistant under
> **Settings → Users → Access Tokens**

---

## Speaker Management

StreamTouch supports multiple SoundTouch speakers.

### Adding a speaker

Go to **Settings → SoundTouch Speakers → Add**

| Method | When to use |
|--------|-------------|
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
appears at the top of the main dashboard. Swipe left or right
on the speaker chip to switch between speakers.

---

## WiFi Reconnection Wizard

StreamTouch includes a built-in WiFi reconnection wizard that
lets you reconnect a speaker to your home network or add a new
speaker — without needing any other app.

### When to use this

- After a factory reset
- When your WiFi network name or password has changed
- When setting up a new speaker for the first time

### How to use it

1. Go to **Settings → Advanced Settings → Add / Reconnect Speaker**
2. Put your speaker into setup mode by holding the WiFi or
   setup button until the LED turns amber
3. Go to **iPhone Settings → WiFi** and connect to the
   speaker's network (shown as Bose_xxxxx or similar)
4. Return to StreamTouch and tap
   **I'm Connected to Speaker WiFi**
5. Select your home WiFi network from the list
6. Enter your WiFi password and set a name for your speaker
7. StreamTouch will configure the speaker and reconnect it
   to your home network automatically

> ℹ️ After reconnecting, use **Advanced Settings →
> Configure Speaker for SLC** to re-enable hardware presets
> if you were using StreamTouch Local Cloud before the reset.

---

## Speaker Grouping

StreamTouch supports grouping multiple speakers to play the
same content across different rooms simultaneously.

### Creating a group

1. Tap the group icon on the main dashboard
2. Select which speakers to include
3. Choose which speaker will be the **master**
   (the master controls playback)
4. Tap **Create Group**

### Play All Speakers

Tap **Play All Speakers** to instantly group every speaker
in your home with the currently active speaker as master —
one tap to play everywhere.

### Group volume

When grouped, a **Group Volume** slider adjusts all speakers
together while preserving their relative levels. Individual
speaker sliders are also available for fine control.

### Dissolving a group

Tap the group icon on the dashboard and tap
**Dissolve Group**. Slave speakers will return to standby.

---

## StreamTouch Local Cloud (SLC)

### What is SLC?

StreamTouch Local Cloud is an optional self-hosted service
that unlocks hardware preset saving for radio stations.

When you play a radio station via Music Assistant, the audio
is delivered as a network stream — the speaker cannot store
it as a hardware preset directly. SLC bridges this gap by
acting as a local media server that the speaker can
communicate with to save and play radio streams as hardware
presets — independently of Music Assistant or the StreamTouch app.

**In plain terms:** SLC lets you save a radio station to
one of the 6 physical preset buttons on your speaker. Press
the button and it plays directly — no app required.

---

### Do I need SLC?

SLC is entirely optional. StreamTouch works fully without it.

| Feature | Without SLC | With SLC |
|---------|-------------|----------|
| Search and play music | ✅ | ✅ |
| Playback controls | ✅ | ✅ |
| In-app presets | ✅ | ✅ |
| Speaker grouping | ✅ | ✅ |
| Save radio to hardware preset | ❌ | ✅ |
| Play radio without Music Assistant | ❌ | ✅ |
| Physical preset buttons on speaker | ❌ | ✅ |

---

### How SLC works

SLC runs as a lightweight Python service inside a Docker
container on your local network. When you save a radio
station as a hardware preset in StreamTouch:

1. StreamTouch sends the station details to SLC
2. SLC registers the station as a Local Internet Radio
   source on your speaker
3. The speaker stores the station and can play it directly
   by pressing the preset button — even without StreamTouch
   or Music Assistant running

SLC also acts as a UPnP media server and handles the
speaker's account and streaming API calls, which is what
allows the hardware preset buttons to work correctly.

---

### Where Does SLC Need to Be?

SLC must be hosted on your **local home network** — the
same network your speaker is connected to. The speaker
communicates directly with SLC over your local network.

**SLC does not need to be:**
- Accessible from the internet
- On the same device as Music Assistant
- A powerful or dedicated machine

**SLC does need to be:**
- On the same local network as your speaker
- Reachable by your speaker at a fixed IP address and port
- Running whenever you want to save or play hardware presets

> 💡 The most common setup is to run SLC on the same
> device as Music Assistant — a Raspberry Pi, NAS or
> home server. They use different ports and do not
> conflict with each other.

#### Can SLC run on the same device as Music Assistant?

Yes — this is the most common setup. If you are already
running Music Assistant on a Raspberry Pi, NAS or home
server, you can run SLC on the same device. They use
different ports and do not conflict with each other.

#### Can SLC run on a different network or remotely?

No. SLC must be on the same local network as your speaker.
The speaker initiates a direct connection to SLC to play
radio streams — this connection cannot cross network
boundaries.

#### What about VLANs or network separation?

If your network uses VLANs or separates devices onto
different subnets, SLC must be either on the same
VLAN/subnet as your speaker, or your router/firewall
must allow traffic between the speaker's subnet and the
device running SLC on the required port (default 8300).

> ⚠️ This is an advanced network configuration. If you
> are unsure, place SLC on the same network segment as
> your speaker.

---

### SLC Requirements

| Requirement | Detail |
|-------------|--------|
| **Docker** | Any device that can run Docker |
| **Always on** | Device must remain powered on for presets to work |
| **Local network** | Must be on the same network as your speaker |
| **Fixed IP** | Device should have a static or reserved IP address |
| **Port 8300** | Default port — can be changed if needed |

---

### Where to run SLC

| Device | Suitable | Notes |
|--------|----------|-------|
| **Raspberry Pi** (3B+ or newer) | ✅ Ideal | Low power, always on |
| **Synology NAS** | ✅ Ideal | Use Container Manager |
| **QNAP NAS** | ✅ Ideal | Use Container Station |
| **Linux PC / server** | ✅ Ideal | Any distro with Docker |
| **Windows PC** | ✅ Supported | Requires Docker Desktop |
| **Mac** | ✅ Supported | Requires Docker Desktop |
| **Same device as Music Assistant** | ✅ Recommended | Runs alongside MA on same host |

> ⚠️ The device running SLC must remain powered on for
> hardware presets to work. Existing presets already saved
> to the speaker will continue to play even if SLC goes
> offline.

---

### Installing SLC

#### Step 1 — Download the SLC files

Download the StreamTouch Local Cloud package from:

[https://github.com/trclemen/streamtouch-slc/releases/latest](https://github.com/trclemen/streamtouch-slc/releases/latest)

The package contains:
- `shim.py` — the SLC service
- `requirements.txt` — Python dependencies
- `Dockerfile` — container build instructions
- `docker-compose.yml` — run configuration template
- `data/presets.json` — empty preset store

Save the files to a folder on your device, for example:
- **Raspberry Pi / Linux:** `/home/pi/streamtouch-slc/`
- **Synology NAS:** `/volume1/docker/streamtouch-slc/`
- **QNAP NAS:** `/share/CACHEDEV1_DATA/streamtouch-slc/`
- **Windows:** `C:\streamtouch-slc\`

---

#### Step 2 — Install Docker

If Docker is not already installed on your device:

[Get Docker](https://docs.docker.com/get-docker/)

- **Synology:** Open **Package Center** → install
  **Container Manager**
- **QNAP:** Open **App Center** → install
  **Container Station**
- **Raspberry Pi / Linux:** Run:
  
curl -fsSL https://get.docker.com | sh


---

#### Step 3 — Find the IP address of your SLC host

You need the local IP address of the device running SLC:

- **Raspberry Pi:** run `hostname -I` in terminal
- **Synology/QNAP:** check the NAS control panel
  network settings
- **Windows:** run `ipconfig` in Command Prompt
- **Mac:** check **System Settings → Network**

---

### SLC Network Configuration

#### Static IP vs DHCP — Why It Matters

When your device gets its IP address automatically (DHCP),
your router may assign it a different IP after a reboot.
If this happens, StreamTouch and your speaker can no longer
reach SLC at the old address.

**What happens if the SLC IP changes:**
- ✅ Existing hardware presets already saved to the speaker
  will continue to play normally
- ❌ Saving new presets will fail until the IP is updated
- ❌ The speaker will lose SLC registration and need
  to be reconfigured

**Recommendation:** Always assign a fixed IP to the device
running SLC — either via DHCP reservation in your router
or by setting a static IP on the device itself.

| Method | How | Best for |
|--------|-----|----------|
| **DHCP Reservation** | Tell your router to always give the same IP to the device based on its MAC address | Most users — done in router, no changes on device |
| **Static IP on device** | Configure the device itself to use a fixed IP | Advanced users |

#### Setting a DHCP Reservation

1. Log in to your router admin page
   (typically `192.168.0.1` or `192.168.1.1`)
2. Find the **DHCP** or **Connected Devices** section
3. Find the device running SLC in the list
4. Select **Reserve IP** or **Static Lease**
5. Save — the device will now always get the same IP

| Router | Admin URL | Section |
|--------|-----------|---------|
| BT Hub | `192.168.1.254` | Advanced → DHCP |
| Sky Router | `192.168.0.1` | Settings → DHCP |
| Virgin Media | `192.168.0.1` | Advanced → DHCP |
| Netgear | `routerlogin.net` | LAN Setup → Address Reservation |
| TP-Link | `192.168.0.1` | DHCP → Address Reservation |
| Asus | `router.asus.com` | LAN → DHCP Server → Manually Assigned |

> 💡 If your router is not listed, search for
> "DHCP reservation [your router model]" for
> specific instructions.

---

#### Step 4 — Configure and build SLC

#### Platform-Specific Network Configuration

The default docker-compose.yml uses standard port mapping which works on most platforms.  
However some NAS devices require additional network configuration to give the SLC container a fixed IP address directly on your local network.  

#### Why This Matters

Your speaker communicates directly with SLC over your local network. The key requirement is that SHIM_HOST must be set to whatever IP address 
the speaker will use to reach SLC — this differs depending on your platform and network setup.  

---

### Raspberry Pi / Linux / Windows / Mac  
The default docker-compose.yml works without any changes.  
Edit the `docker-compose.yml` file and set your values:

services:  
··streamtouch-slc:  
····build: .  
····container_name: streamtouch-slc  
····restart: unless-stopped. 
····ports:  
······- "8300:8300"  
····environment:  
······- SHIM_HOST=192.168.0.x········# IP of THIS container/device running SLC  
······- SHIM_PORT=8300  
······- MA_HOST=192.168.0.x··········# IP of your Music Assistant server   
······- MA_PORT=8095  
····volumes:  
······- ./data:/data  

On these platforms the container shares the host device IP address. Set SHIM_HOST to the IP address of the device running Docker  
— for example if your Raspberry Pi is at 192.168.0.100 then SHIM_HOST=192.168.0.100  

---

### QNAP NAS
QNAP uses its own virtual network driver called qnet. This gives each container its own dedicated IP address directly on your local network  
— completely separate from the NAS IP address itself.

For example:

QNAP NAS:                192.168.0.252  
Music Assistant container: 192.168.0.253  
SLC container:             192.168.0.254  

SHIM_HOST must be set to the container IP assigned via --ip not the NAS IP. The speaker connects to the container IP directly.
#### Step 1 — Find your QNAP network name

In QNAP Container Station go to Networks and note the name of your static network. It will look similar to:  
qnet-static-bond0-0fa2ce

The exact name varies by QNAP model and network configuration.
#### Step 2 — Choose a fixed IP for the SLC container
Pick an unused IP address on your local network for example 192.168.0.254. This will be the container IP — not the NAS IP. Reserve this in your router using DHCP reservation so nothing else takes it.

#### Step 3 — Build and run using docker run
QNAP Container Station docker compose support for custom networks can be unreliable. Use docker run directly instead:

cd /share/CACHEDEV1_DATA/streamtouch-slc  
docker build -t streamtouch-slc:latest .  
docker stop streamtouch-slc 2>/dev/null.   
docker rm streamtouch-slc 2>/dev/null  
docker run -d \  
  --name streamtouch-slc \
  --network qnet-static-bond0-0fa2ce \
  --ip 192.168.0.254 \
  -e MA_HOST=192.168.0.253 \
  -e MA_PORT=8095 \
  -e SHIM_HOST=192.168.0.254 \
  -e SHIM_PORT=8300 \
  -e SHIM_UUID=streamtouch-upnp-0000-0000-000000000001 \
  -v /share/CACHEDEV1_DATA/streamtouch-slc/data:/data \
  --restart unless-stopped \
  streamtouch-slc:latest

#### Important:

    --ip and SHIM_HOST must be the same value
    --ip is the container IP not the NAS IP
    MA_HOST is the IP of your Music Assistant server
    Replace qnet-static-bond0-0fa2ce with your actual QNAP network name

---

### Synology NAS

Synology NAS supports two approaches depending on your DSM version and network setup.
#### Option A — Bridge network with port mapping (simpler)
In Container Manager create the container using the standard docker-compose.yml with port mapping. This works on most Synology setups and is the recommended starting point.

On Synology with bridge networking the container shares the NAS IP address. Set SHIM_HOST to the IP address of the NAS itself:

environment:
  - SHIM_HOST=192.168.0.x
  - SHIM_PORT=8300
  - MA_HOST=192.168.0.x
  - MA_PORT=8095


  Where 192.168.0.x is your Synology NAS IP address.

#### Option B — Macvlan network with fixed container IP
If Option A does not work reliably create a macvlan network to give the container its own dedicated LAN IP — similar to how QNAP works.

In Synology Container Manager:

   1. Go to Network then Add
   2.  Select Macvlan
   3.  Choose your network interface for example eth0
   4.  Set a fixed IP for the container for example 192.168.0.254
   5.  Use this network in your container configuration

With macvlan the container gets its own IP separate from the NAS IP. Set SHIM_HOST to the container IP not the NAS IP:

environment:
  - SHIM_HOST=192.168.0.254


If you are unsure which option to use start with Option A. If the speaker cannot reach SLC after configuring in StreamTouch switch to Option B

| Platform | SHIM_HOST value |
|----------|----------------|
| Raspberry Pi / Linux | IP of the host device e.g. `192.168.0.100` |
| Windows / Mac | IP of the host device e.g. `192.168.0.100` |
| Synology NAS (bridge / port mapping) | IP of the NAS e.g. `192.168.0.252` |
| Synology NAS (macvlan) | IP assigned to the container e.g. `192.168.0.254` |
| QNAP NAS (qnet static network) | IP assigned to the container via `--ip` e.g. `192.168.0.254` |  

> **The rule:** SHIM_HOST must be the IP address your speaker
> will use to reach SLC. Verify by opening a browser on any
> device and going to `http://[SHIM_HOST]:8300/api/health`
> — if you see a JSON response the speaker can reach it too.

---

#### Step 5 — Verify SLC is reachable

Open a browser on any device on your network and go to:
http://[your-slc-ip]:8300/api/health

You should see a JSON response confirming the service
is running. You can also use **Test SLC Connection**
in StreamTouch Advanced Settings.

---

#### Step 6 — Configure StreamTouch

1. Open StreamTouch
2. Go to **Settings → Advanced Settings**
3. Under **StreamTouch Local Cloud** enter:
   - **IP address** — the IP of the device running SLC
   - **Port** — `8300` (or your custom port)
4. Tap **Test SLC Connection** to confirm

---

#### Step 7 — Configure your speaker for SLC

Each speaker needs to be individually pointed at SLC:

1. Go to **Settings → Advanced Settings**
2. Tap **Configure Speaker for SLC**
3. Select the speaker to configure
4. StreamTouch will configure the speaker automatically

> ⚠️ You will need to repeat this step after a factory
> reset or WiFi reconnection.

---

#### Changing the SLC Port

The default port is **8300**. To use a different port
update both values in `docker-compose.yml` to match:
ports:

    "9000:9000" environment:
    SHIM_PORT=9000

Then update the port in StreamTouch **Advanced Settings**
to match.

> ⚠️ Both values must be identical or SLC will not
> be reachable.

---

#### Updating the SLC IP in StreamTouch

If your SLC IP address changes:

1. Go to **Settings → Advanced Settings**
2. Update the IP under **StreamTouch Local Cloud**
3. Tap **Test SLC Connection**
4. Run **Configure Speaker for SLC** again for each speaker

> ⚠️ After an IP change you must re-run Configure Speaker
> for SLC — the speaker stores the SLC IP internally and
> will not automatically pick up the new address.

---

### Saving a radio station as a hardware preset

1. Play a radio station via StreamTouch
2. When playing, tap **Save to Hardware Preset** on the
   main dashboard
3. Choose which preset slot (1–6) to save to
4. The station is saved to that slot on the speaker and
   will appear on the physical preset buttons

> ℹ️ SLC must be running and the speaker must be
> configured for SLC for this to work.

---

### Hardware Preset Viewer

Go to **Settings → Advanced Settings → Hardware Presets**
to view all 6 preset slots for the active speaker and
clear individual slots.

---

## Frequently Asked Questions

### This all sounds very complicated, is it?  
It depends on what you already have running.
If you already have Music Assistant running — adding SLC 
is straightforward. You copy a few files to the same device, edit one
configuration file with your network details, and run two commands to 
build and start it. Most users have it working in under 30 minutes.

If you are starting from scratch — there is a bit more to do, Music Assistant
is well documented and has active communities. The most common setup is
a Raspberry Pi or a NAS device that you may already have running at home. 
If it can run Docker it can run both Music Assistant and StreamTouch SLC.

The honest answer — if you are comfortable logging in to your router to check
connected devices, or have ever set up a NAS or home server, you will find
this manageable. If those things sound unfamiliar it may take a bit more time
and reading..

**What you do not need:**
- Any cloud accounts or subscriptions
- A developer account or technical background
- Any changes to your speaker hardware

**What you do need:**
- A device on your home network that can run Docker and stays powered on
- a Raspberry Pi, NAS, or any always-on computer works well
- About 30 to 60 minutes for the initial setup

---

### How do I add content/music streaming sources?
You add your preferred music sources to Music Assistant Server.
Access your MA server vi http://**YourMAServerIP**:8095/#/settings.
Choose your music sources and these will all be available to search/browse
in StreamTouch.

---

### What about internet radio custom URLs?
Add custom URLs via http://**YourMAServerIP**:8095/#/radios.
Click the add/olus button top right and enter custom URL details.
This will then be avaialble in StreamTouch as a library item.
If you have SLC running you can save any of these custom URLs to
a hardware preset.

---

### Where do I find my speaker's IP address?

Check your router's connected devices list. The speaker
will typically appear as "SoundTouch" or similar.

> To assign a static IP, use your router's DHCP reservation
> feature. Alternatively enable **Auto IP (DHCP)** in
> StreamTouch speaker settings and the app will find your
> speaker automatically on each launch.

---

### Where do I get Music Assistant?

Music Assistant is a free, open source, self-hosted music
server. It can be installed as a Docker container on any
device supporting Docker, or as a Home Assistant add-on.

[Music Assistant Installation Guide](https://www.music-assistant.io/installation/)

---

### Where do I find my Music Assistant Player ID?

In Music Assistant go to **Settings → Players** and select
your SoundTouch player. The Player ID will look similar to
`up689e19dada87`.

> StreamTouch will attempt to detect this automatically.
> You can also use the **Auto Find** button in
> **Settings → SoundTouch Speakers → Edit Speaker**.

---

### What is a Music Assistant API Bearer Token?

A bearer token is a password that StreamTouch uses to 
prove to your Music Assistant server that it is allowed 
to control music playback. Without it, Music Assistant 
will refuse all requests from StreamTouch.

Think of it like a key card — Music Assistant issues the 
key card, and StreamTouch presents it every time it wants 
to search for music, play a track or control the queue.

**Key things to know:**

- The token is generated once in Music Assistant and 
  copied into StreamTouch during setup
- It does not expire unless you delete it in 
  Music Assistant
- It never leaves your local network — StreamTouch only 
  uses it to talk to your Music Assistant server
- It is stored securely in the iOS Keychain on your 
  iPhone, not in plain text

**Where to find it:**

1. Open the Music Assistant web interface in a browser
2. Go to **Settings → Users**
3. Select your user profile
4. Find the **Access Tokens** section
5. Click **Create Token** and give it a name 
   e.g. "StreamTouch"
6. Copy the token immediately — Music Assistant will 
   only show it once

> ⚠️ Copy the full token before closing the window.
> Music Assistant will not show it again after you 
> navigate away. If you lose it, delete it and 
> create a new one.
>
> 💡 Email the token to yourself before closing 
> the browser — this makes it easy to copy and 
> paste into StreamTouch on your iPhone.

---

### Where do I generate a bearer token?

Navigate to **Settings → Users** in the Music Assistant
web interface, select your user profile, and find the
**Access Tokens** section to generate a new Long-Lived
token.

> ⚠️ **Note:** In some versions of Music Assistant, the
> copy button for API tokens may not behave as expected.
> Manually select the full token text and save it
> somewhere safe.
>
> 💡 **Tip:** Email the token to yourself so you can
> copy and paste it directly on your iPhone.

---

### The app says connection failed — what do I do?

StreamTouch tests three things:

| Test | What to check if it fails |
|------|---------------------------|
| **Speaker** | Check IP address, confirm speaker is powered on and on the same network |
| **Music Assistant Server** | Check server IP, port (default 8095) and bearer token |
| **Music Assistant Player** | Check Player ID — use Auto Find in speaker settings |

---

### My speaker shows as Not Configured after a factory reset

After a factory reset you need to:

1. Use the **WiFi Reconnection Wizard** in Advanced
   Settings to reconnect the speaker to your network
2. Use **Configure Speaker for SLC** in Advanced Settings
   to re-enable hardware presets

Both steps are required to fully restore the speaker.

---

### Can I change my settings after setup?

Yes — tap the **gear icon** on the main dashboard at any
time to update settings, manage speakers or test
connections.

---

### The app is not finding my speaker

- Confirm the speaker is powered on and on the same network
- Try **Settings → SoundTouch Speakers → Add → Discover**
- Verify the IP address in speaker settings is correct
- Enable **Auto IP (DHCP)** to let StreamTouch find your
  speaker automatically
- Consider assigning a reserved IP in your router settings

---

### Music Assistant is unreachable

- Confirm your Music Assistant server is running
- Check the IP address and port (default `8095`)
- Ensure your bearer token is valid and has not expired
- Use **Settings → Test Connection** to diagnose

---

### SLC is not working

- Confirm the Docker container is running on your host device
- Check the IP address and port in
  **Settings → Advanced Settings → StreamTouch Local Cloud**
- Ensure the device running SLC is powered on and reachable
- Use **Test SLC Connection** in Advanced Settings to
  confirm connectivity
- Confirm the speaker has been configured for SLC using
  **Configure Speaker for SLC**

---

### Player ID not found or auto detection failed

1. Go to **Settings → SoundTouch Speakers**
2. Tap **edit** on your speaker
3. Tap **Auto Find** next to the Player ID field
4. If Auto Find fails, go to Music Assistant
   **Settings → Players**, find your player and copy
   the Player ID manually

---

## Caveats, Known Issues and Limitations

**SoundTouch LED/OLED Display**
For systems with LED/OLED displays, artist and track info
is reliably shown when playing individual tracks or radio
stations. When playing albums, the display may only show
the first track — this is a known limitation of the
SoundTouch player within Music Assistant when using
DLNA/UPnP playback.

**Album playback only plays first track**
If StreamTouch only plays the first song when Play Album
is selected, ensure that **Queue Flow Mode** is enabled
in Music Assistant under the SoundTouch Player
**Advanced** settings.

**Hardware presets require SLC to be running**
Hardware preset saving requires SLC to be reachable at
the time of saving. Existing presets already saved to the
speaker will continue to work even if SLC goes offline.

**WiFi reconnection — keep iPhone on speaker network**
During the WiFi reconnection wizard, keep your iPhone
connected to the speaker's temporary network for the full
duration. iOS may attempt to switch back to your home
network automatically — if this happens, return to
iPhone Settings → WiFi and reconnect to the speaker
network before retrying.

**Connection tests are successful — no playback**
Following WiFi reconnection or speaker being offline
the speaker maybe present but unavailable in Music Assistant
for several minutes before being 'seen' again by Music Assistant.
Some systems, particulary Wave pedestal systems may require more
time following WiFi reconnection or power cycle to become avaialble
to Music Assistant and resume playback via StreamTouch.

---

## Resetting the App

Go to **Settings → Full Reset (Run Setup Again)** to
clear all settings and return to the setup wizard on
next launch.

---

## Privacy

StreamTouch does not collect, store or transmit any
personal data to external servers. All communication
is exclusively between your iOS device and your local
network devices. Your API bearer token is stored
securely in the iOS Keychain.

---

## Contact and Support

streamtouch.support@gmail.com

Please include:
- Your iOS version
- Your StreamTouch version (shown in Settings)
- A brief description of the issue
- Any error messages shown in the app

---

*StreamTouch is an independent app and is not affiliated
with or endorsed by the makers of SoundTouch speakers or
the Music Assistant project.*
