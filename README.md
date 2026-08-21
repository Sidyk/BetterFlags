# Better Flags for LMU

A lightweight SimHub plugin that provides reliable, LED-ready flag states for **Le Mans Ultimate**.

**[Download BetterFlags.dll](https://github.com/Sidyk/BetterFlags/raw/refs/heads/main/BetterFlags.dll)**

Current version: **1.0.0**

## Why Better Flags?

The native LMU Yellow Flag can cover an entire sector or track. Better Flags detects confirmed local incidents physically ahead of the player and exposes consistent outputs for dashboards, LEDs and RGB Matrix profiles.

## Features

- Local Yellow incident detection ahead of the player
- Double Yellow for clustered incidents
- Slow-car White Flag detection
- Native Blue Flag integration
- Configurable Green at race start and after passing a local Yellow
- Automatic Private Qualifying detection through the local LMU REST API
- Built-in update notification
- Dark, responsive SimHub settings interface

## Installation

1. Download `BetterFlags.dll` using the link above.
2. Close SimHub.
3. Copy the DLL to `C:\Program Files (x86)\SimHub`.
4. If Windows blocks the downloaded file, open **Properties** for the DLL and select **Unblock**.
5. Start SimHub and enable **Better Flags for LMU** in **Settings > Plugins**.

If upgrading from an older build named `LMUFlags.dll`, remove that old DLL to avoid loading the plugin twice.

No additional libraries are required beyond a normal SimHub installation.

## SimHub properties

| Property | Values |
|---|---|
| `LMUFlags.Yellow` | `0` clear, `1` single incident, `2` double/clustered incident |
| `LMUFlags.Blue` | `0` inactive, `1` active |
| `LMUFlags.White` | `0` inactive, `1` active |
| `LMUFlags.Green` | `0` inactive, `1` active |

Runtime priority: **Yellow > White > Blue > Green**

Additional diagnostic properties are available under `LMUFlags.Debug.*`.

## Network access

The plugin performs read-only requests to:

- LMU's local REST API for Private Qualifying detection
- This GitHub repository's `version.json` once at plugin startup for update notifications

Network errors never prevent the flag detector from running.

## Support

Created by **Sidyk**.

[Support via PayPal](https://www.paypal.com/paypalme/MrSIdyk)
