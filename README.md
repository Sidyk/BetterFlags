# Better Flags for LMU

Better Flags is a lightweight SimHub plugin that provides reliable, LED-ready flag states for **Le Mans Ultimate**. It is designed for dashboards, flag displays, RGB matrices and other SimHub profiles that need clear `0/1` outputs instead of broad or inconsistent in-game warnings.

**[Download BetterFlags.dll](https://raw.githubusercontent.com/Sidyk/BetterFlags/main/BetterFlags.dll?v=1.1)**

Current version: **1.1** — [changelog](CHANGELOG.md)

## What it does

LMU's native Yellow Flag may warn for an entire sector or the whole track. Better Flags follows cars physically ahead of the player, confirms their movement over multiple samples and displays a local warning only when the incident is inside the configured range.

The plugin provides:

- **Yellow Flag** for a confirmed stopped or very slow car ahead
- **Double Yellow** when multiple confirmed incidents form a nearby cluster
- **Slow Car / White Flag (testing)** for a significantly slower moving car ahead
- **Blue Flag** from LMU's native signal, optionally extended by **Enhanced Blue Awareness (experimental)** for faster-class traffic approaching from behind
- **Green Flag** at the race start and optionally after passing a local Yellow incident
- **Last Lap (testing)** detection for timed races
- **Checkered Flag** near the finish of the player's final lap

All detection profiles, confirmation times, display distances and expert speed thresholds can be configured from the plugin's settings page.

## How flag detection works

Better Flags scans up to 30 cars in their physical order ahead on track. Pit and pit-lane cars are ignored. A single unusual telemetry sample is not enough to activate a flag: the plugin measures each car over time and requires repeated confirmation before creating an incident.

Default behavior:

- cars are scanned up to **1000 m** ahead
- Yellow is displayed within **400 m**
- White is displayed within **400 m**
- two Yellow incidents within **50 m** produce Double Yellow
- Yellow confirmation takes approximately **1 second**
- White confirmation takes approximately **4 seconds**
- Green after passing Yellow remains active for **3 seconds**

The runtime priority is:

**Yellow > White > Blue > Green > Clear**

Only the highest-priority color flag is exposed at a time. `LastLap` and `Checkered` are independent outputs and do not participate in this priority chain.

## Last Lap and Checkered

> **Testing:** Last Lap is still being validated across different timed-race formats and track lengths.

For timed Race sessions, Better Flags predicts whether the session timer will expire before the player's next start/finish crossing. `LMUFlags.LastLap` activates only when the final lap is actually about to begin, preventing the warning from appearing one lap too early.

Last Lap behavior:

- it can activate within **300 m** of the start/finish line
- it remains active until the player crosses the line to begin the final lap
- it stays active for another **4 seconds** after that crossing
- it cannot retrigger during the same final lap

`LMUFlags.Checkered` activates within **300 m** of the finish at the end of the final lap and remains active after the player crosses the line. For cars running behind the overall leader, the plugin tracks the leader by stable vehicle ID and uses LMU's finish status so the Checkered Flag can still appear at the player's correct next finish. It resets only after returning to the garage or changing/resetting the session.

## Features currently in testing

- **Slow Car / White Flag** detects a confirmed, significantly slower moving car ahead. Its confirmation and display thresholds can be tuned in the plugin settings.
- **Last Lap** predicts the final lap of timed races and may still need adjustment for unusual race formats.
- **Enhanced Blue Awareness (experimental)** supplements the official LMU Blue Flag during races. It warns when faster-class traffic on the same or fewer completed laps reaches approximately 0.8 seconds behind the player, then remains active until that car passes. The native Blue Flag continues to work normally.

## SimHub properties

| Property | Values | Meaning |
|---|---:|---|
| `LMUFlags.Yellow` | `0`, `1`, `2` | Clear, single Yellow, or Double Yellow |
| `LMUFlags.White` | `0`, `1` | Slow Car warning (testing) |
| `LMUFlags.Blue` | `0`, `1` | Native LMU Blue Flag or optional Enhanced Blue Awareness |
| `LMUFlags.Green` | `0`, `1` | Race-start Green or Green after passing Yellow |
| `LMUFlags.LastLap` | `0`, `1` | Final lap warning in a timed race (testing) |
| `LMUFlags.Checkered` | `0`, `1` | Checkered Flag at the end of the race |
| `LMUFlags.State` | text | `CLEAR`, `GREEN`, `BLUE`, `WHITE`, `YELLOW` or `DOUBLE YELLOW` |
| `LMUFlags.IncidentDistance` | metres | Distance to the currently displayed local incident |
| `LMUFlags.IncidentDriver` | text | Driver associated with the current local incident |

Additional troubleshooting values are available through the `LMUFlags.Debug.*` properties.

## Safe session handling

Flag outputs are enabled only while the player's car is directly controlled by the player. Lobby, observer, replay, AI control and unavailable control data clear the outputs.

Flags are also held clear during formation and before the session has genuinely started. In Private Qualifying, detected through LMU's local read-only REST API, opponent-based color flags are disabled and opponent scanning is skipped.

## Settings

The plugin includes three detection profiles:

- **Fast** — quicker confirmation
- **Balanced** — default behavior
- **Conservative** — slower, more cautious confirmation

Advanced settings expose Yellow and White sample intervals, required confirmations and track scanning distance. The Flag Display section controls when confirmed warnings appear and how long they remain visible. Expert settings unlock Double Yellow cluster distance and speed thresholds. Contextual `?` tooltips explain the effect of each option.

Green at race start can be disabled or shown for the first sector, half lap or complete first lap. Green after Yellow and experimental Enhanced Blue Awareness can be enabled or disabled separately.

## iFlag LED Profile

The plugin includes an installable **iFlag 8×8 RGB Matrix** profile with animated Green, Yellow, Double Yellow, Blue, Slow Car, Last Lap and Checkered displays. In LMU it uses Better Flags outputs; other games keep using their native SimHub flags.

The profile installer:

- installs and selects the profile without creating duplicates
- backs up the profile before replacement
- updates the installed profile automatically when its embedded definition changes
- preserves the user's Gear, native Flags and Spotter Overlay enable/disable choices
- can restore the previous backup or switch the profile to native SimHub flags only

## Installation

1. [Download `BetterFlags.dll`](https://raw.githubusercontent.com/Sidyk/BetterFlags/main/BetterFlags.dll?v=1.1).
2. Close SimHub.
3. Copy the DLL to `C:\Program Files (x86)\SimHub`.
4. If Windows blocks the file, open its **Properties** and select **Unblock**.
5. Start SimHub and enable **Better Flags for LMU** under **Settings > Plugins**.

No additional libraries are required beyond a normal SimHub installation.

## Updates and network access

The plugin checks this repository's `version.json` once at startup. When a verified update is available, **Update & Restart** downloads the DLL, validates its SHA-256 checksum and assembly version, installs it with rollback protection and restarts SimHub.

Better Flags performs only two types of network request:

- a read-only request to LMU's local REST API for Private Qualifying detection
- a request to this GitHub repository for update information

Network failures never stop flag detection from running.

## Support

[Support via PayPal](https://www.paypal.com/paypalme/MrSIdyk)
