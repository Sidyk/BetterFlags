# Changelog

## 1.0.3 — 2026-08-22

- Replaced the manual Download action with `Update & Restart` when the update manifest includes SHA-256.
- Added asynchronous download and checksum/assembly-version verification before installation.
- Added an embedded elevated updater that closes SimHub, replaces the plugin with rollback protection, and restarts SimHub.
- Retained manual download as a safe fallback for manifests without a valid checksum.

## 1.0.2 — 2026-08-22

- Expert-setting help tooltips now appear immediately on hover.
- Expanded the hover target to the complete `?` badge and added a help cursor.

## 1.0.1 — 2026-08-22

- Added editable Double Yellow cluster distance.
- Added editable expert thresholds for Yellow and Slow Car detection.
- Added an `Unlock expert settings` safety checkbox; expert values remain locked by default.
- Added contextual `?` tooltips explaining every expert setting.
- Improved the alignment and label of the collapsible Advanced settings section.

## 1.0.0 — 2026-08-21

- Initial public release of Better Flags for LMU.
