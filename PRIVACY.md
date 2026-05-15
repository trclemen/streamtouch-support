# StreamTouch — Privacy Policy

**Last Updated: May 15, 2026**

---

## Overview

StreamTouch ("the App") is an iOS controller for SoundTouch speakers 
operated via a self-hosted Music Assistant server. We respect your privacy 
and are committed to protecting it.

> **StreamTouch does not collect, store, or transmit any personal data 
> to external servers or to the App developer.**

---

## Information We Collect

StreamTouch collects no personal information. All configuration data is 
stored locally on your device only, including:

- SoundTouch speaker IP address
- Music Assistant server IP address, port and player ID
- API bearer token *(stored securely in the iOS Keychain — see below)*
- Saved presets and last played track metadata

None of this information is shared with the App developer or any third party.

---

## Network Communication

The App communicates exclusively with devices and services on your own 
local network:

| Destination | Purpose |
|---|---|
| Your SoundTouch speaker | Playback control and volume via local Wi-Fi |
| Your Music Assistant server | Search, playback commands and queue management via local Wi-Fi |
| Artwork image URLs | Album artwork served by your music providers (e.g. Spotify, Tidal, Plex) through your Music Assistant server |

No data is sent to the App developer, advertising networks, analytics 
services or any other third party.

---

## Local Network Access

iOS will prompt you to grant permission to access your local network when 
you first launch StreamTouch. This permission is required for the App to 
connect to your SoundTouch speaker and Music Assistant server.

This permission is used solely for those two local connections and for 
no other purpose.

---

## Data Storage

StreamTouch uses two secure on-device storage mechanisms:

| Storage | What is stored |
|---|---|
| **iOS Keychain** | API bearer token (encrypted, access-controlled by iOS) |
| **UserDefaults** | Server IP addresses, port, player ID, saved presets, last played track metadata |

### Deleting Your Data

You can remove all data stored by StreamTouch at any time by either:

- Deleting the App from your device, or
- Using **Settings → Full Reset (Run Setup Again)** within the App

---

## Third Party Services

StreamTouch does not integrate with any third party SDKs, analytics 
platforms, advertising networks or crash reporting services.

Artwork images displayed within the App are served directly from your 
own Music Assistant server, which in turn retrieves them from your 
connected music providers (such as Spotify, Tidal or Plex). StreamTouch 
does not interact with these providers directly.

---

## Security

Your API bearer token is stored exclusively in the iOS Keychain, which 
is encrypted and sandboxed by iOS. It is never logged, transmitted or 
exposed outside of your device.

All network communication occurs over your local Wi-Fi network. 
StreamTouch does not make any connections to the internet.

---

## Children's Privacy

StreamTouch is not directed at children under the age of 13. The App 
does not knowingly collect any data from any user, including children. 
As no data is collected, there is no specific risk to younger users 
beyond general iOS device usage.

---

## Your Rights

As StreamTouch does not collect or store any personal data on external 
servers, there is no personal data held by the App developer to access, 
correct or delete. All data is stored locally on your own device and 
remains entirely under your control.

---

## Changes to This Policy

We may update this Privacy Policy from time to time to reflect changes 
to the App or for other operational or legal reasons. Any changes will 
be reflected by an updated **Last Updated** date at the top of this page.

We encourage you to review this policy periodically. Continued use of 
the App following any changes constitutes acceptance of the updated policy.

---

## Contact

If you have any questions or concerns about this Privacy Policy or the 
App's data practices, please contact:

📧 [streamtouch.support@gmail.com](mailto:streamtouch.support@gmail.com)

---

*StreamTouch is an independent app and is not affiliated with 
Bose Corporation or the Music Assistant project.*
