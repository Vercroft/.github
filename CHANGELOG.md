# Changelog

All notable changes to this repository are listed here, newest first, in the format of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.1]

### Fixed

- `gitleaks.yml` removes the gitleaks action's leftover download before the scan, so a runner whose `/tmp` persists
  between jobs no longer fails with "Destination file path ... already exists".

## [1.0.0] - 2026-11-17

### Added

- The reusable workflow `gitleaks.yml`: a redacted full-history gitleaks scan of the calling repository with its own
  `.gitleaks.toml`, with an optional runner input.
- The default `SECURITY.md` and `CONTRIBUTING.md` for repositories that have none of their own.
