# Changelog

All notable changes to this repository are listed here, newest first, in the format of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.0.0]

### Changed (breaking)

- The workflow is now `.github/workflows/secret-scan.yml` (it was `gitleaks.yml`), and its job is named `full history`
  (it was `gitleaks`), so a caller's check is named for what it checks, not for the tool. A caller changes its `uses:`
  path to `.github/workflows/secret-scan.yml`, names its calling job `Secret scan`, and swaps its required check for
  `Secret scan / full history`. The inputs and the scan itself are unchanged.

### Added

- `.gitleaks.toml` carries `github-app-installation-token-stateless`, copied from engineering-practices, for GitHub App
  installation tokens in the stateless `ghs_APPID_JWT` form.

## [1.1.0]

### Added

- `gitleaks.yml` takes an optional `runs-on-json` input: a full `runs-on` value as JSON, such as a runner group with
  labels, used instead of `runner` when set.

## [1.0.1] - 2026-11-17

### Fixed

- `gitleaks.yml` removes the gitleaks action's leftover download before the scan, so a runner whose `/tmp` persists
  between jobs no longer fails with "Destination file path ... already exists".

## [1.0.0] - 2026-11-17

### Added

- The reusable workflow `gitleaks.yml`: a redacted full-history gitleaks scan of the calling repository with its own
  `.gitleaks.toml`, with an optional runner input.
- The default `SECURITY.md` and `CONTRIBUTING.md` for repositories that have none of their own.
