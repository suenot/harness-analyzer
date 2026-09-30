# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.4.6] - 2026-09-30

### Fixed

- Expose the open-source repository through GitHub icon links in the landing hero and footer.

## [0.4.5] - 2026-09-27

### Fixed

- Merge explicitly linked device identities after an OS reinstall, retaining unique historical sessions and preferring current analytics for duplicates.

## [0.4.4] - 2026-09-27

### Fixed

- Add GPT-6 and newer GLM cost estimates, correct Codex reasoning token totals, and use distinct green shades for GPT models.
- Recollect local caches so corrected estimates reach hosted analytics on the next sync.

## [0.4.3] - 2026-09-27

### Added

- Added an English project README with installation, sync, privacy, and development guidance plus a four-panel explanatory comic.

### Fixed

- Read model names from local transcripts without substituting GLM 5.2 for unknown or unpriced models.
- Recollect old caches and update hosted charts to preserve the recorded model labels.

## [0.4.2] - 2026-09-26

### Fixed

- Made the landing-page command visibly selectable and used the hero's right column for sync setup.

## [0.4.1] - 2026-09-26

### Fixed

- Made the landing-page privacy explanation explicit about session statistics, local conversation text, and opt-in history upload.

## [0.4.0] - 2026-09-26

### Added

- Added copyable landing-page setup steps for CLI login, initial sync, and automatic macOS sync.

### Fixed

- Made the landing-page installation command selectable and copyable.

## [0.3.3] - 2026-09-26

### Changed

- Renamed the source repository, workspace packages, and Git submodules to Harness Analyzer.
- Mounted the existing production cache data at the new `~/.harness-analyzer` path.

### Fixed

- Updated the reference submodule pin to a commit available from its upstream repository.

## [0.3.2] - 2026-08-16

### Fixed

- Prevented project card headings from clipping letter descenders.

## [0.3.1] - 2026-08-16

### Fixed

- Replaced full-width project rows with responsive square cards while preserving readable expanded breakdowns.

## [0.3.0] - 2026-08-16

### Added

- Added independent sharing controls and public routes for sanitized session and project analytics.

### Security

- Public session and project responses use explicit field allowlists and omit prompts, paths, session identifiers, files, and device metadata.

## [0.2.0] - 2026-08-16

### Added

- Added multi-device CLI synchronization with stable private device identities and fleet-wide aggregation.
- Added a private, range-aware device usage chart with USD, token and session metrics.

### Changed

- Replaced the duplicate landing-page hero logo with telemetry facts and clarified private device-label handling.

### Fixed

- Increased the installation command line height and vertical clearance so glyphs are not clipped.

### Security

- Updated resolved Hono and Nano ID dependencies to patched releases.

## [0.1.2] - 2026-08-16

### Fixed

- Made the landing-page CLI installation command a prominent full-width hero strip.

## [0.1.1] - 2026-08-16

### Fixed

- Exposed the Harness Analyzer CLI installation command on the public landing page.
- Corrected landing-page privacy copy for aggregate hosted synchronization.
