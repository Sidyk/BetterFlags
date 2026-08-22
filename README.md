# Better Flags for LMU

A lightweight SimHub plugin that provides reliable, LED-ready flag states for **Le Mans Ultimate**.

**[Download BetterFlags.dll](https://raw.githubusercontent.com/Sidyk/BetterFlags/main/BetterFlags.dll?v=1.0.4)**

Current version: **1.0.4** — [changelog](CHANGELOG.md)

## Why Better Flags?

The native LMU Yellow Flag can cover an entire sector or track. Better Flags detects confirmed local incidents physically ahead of the player and exposes consistent outputs for dashboards, LEDs and RGB Matrix profiles.

## Features

- Local Yellow incident detection ahead of the player
- Double Yellow for clustered incidents
- Slow-car White Flag detection
- Configurable Green at race start and after passing a local Yellow
- Configurable Double Yellow and expert speed thresholds with safety lock and contextual help
- Verified `Update & Restart` flow with SHA-256 validation, rollback protection and automatic SimHub restart

## Installation

1. Download `BetterFlags.dll` using the link above.
2. Close SimHub.
3. Copy the DLL to `C:\Program Files (x86)\SimHub`.
4. If Windows blocks the downloaded file, open **Properties** for the DLL and select **Unblock**.
5. Start SimHub and enable **Better Flags for LMU** in **Settings > Plugins**.


No additional libraries are required beyond a normal SimHub installation.

Versions 1.0.2 and earlier require one final manual installation of v1.0.3. Starting with v1.0.3, future updates can be installed directly from the plugin using `Update & Restart`.

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

[Support via PayPal](https://www.paypal.com/paypalme/MrSIdyk)
