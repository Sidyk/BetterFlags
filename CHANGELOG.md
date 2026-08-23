# Changelog

## 1.0.5

- Added `LMUFlags.LastLap` for timed races.
- Added `LMUFlags.Checkered` with persistent activation near the finish line.
- Added stable overall-leader finish tracking for cars behind the race leader.
- Prevented Last Lap from activating one lap too early when the timer is still positive at the next S/F crossing.
- Prevented transient telemetry dropouts from retriggering Last Lap or clearing Checkered.
- Added configurable Last Lap enablement and detailed diagnostics.

## 1.0.4

- Added immediate contextual help tooltips for Yellow and White sample intervals.
- Added help tooltips for required sample counts and estimated reaction times.
- Added help tooltips for track scan, Yellow display and White display distances.

## 1.0.3

- Replaced the manual Download action with `Update & Restart` when the update manifest includes SHA-256.
- Added asynchronous download and checksum/assembly-version verification before installation.
- Added an embedded elevated updater that closes SimHub, replaces the plugin with rollback protection, and restarts SimHub.
- Retained manual download as a safe fallback for manifests without a valid checksum.

## 1.0.2

- Expert-setting help tooltips now appear immediately on hover.
- Expanded the hover target to the complete `?` badge and added a help cursor.

## 1.0.1

- Added editable Double Yellow cluster distance.
- Added editable expert thresholds for Yellow and Slow Car detection.
- Added an `Unlock expert settings` safety checkbox; expert values remain locked by default.
- Added contextual `?` tooltips explaining every expert setting.
- Improved the alignment and label of the collapsible Advanced settings section.

## 1.0.0

- Initial public release of Better Flags for LMU.
