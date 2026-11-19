# Changelog

All notable changes to this repository are listed here, newest first, in the format of
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.1.0]

### Changed

- `reusable-secret-scan.yml` installs gitleaks 8.30.1 from its release archive, checked against the SHA-256 for Linux
  x64, instead of through `gacts/gitleaks`, which checked no checksum and cached the binary between runs. Nothing is
  cached. Any other runner is refused with an error. The scan is gitleaks' own `git` command (which replaced `detect`)
  over the full history with the caller's `.gitleaks.toml`, redacted; a finding fails the check as before.

### Removed

- The step that removed the gitleaks action's leftover download: the archive now lives in the job's own temporary
  folder, which the runner empties at the start and end of every job.
- The SARIF report, which nothing read.

A caller changes only the commit SHA and the version comment.

## [2.0.0]

### Changed (breaking)

- The workflow is now `.github/workflows/reusable-secret-scan.yml` (it was `gitleaks.yml`), named `Reusable secret
  scan`; its job is `full-history`, named `Full history` (it was `scan`, named `gitleaks`), and its steps are named.
  A caller's check is named for what it checks, not for the tool.
- One input, `runs-on`, the job's `runs-on` value as JSON (default `'"ubuntu-latest"'`), replaces `runner` and
  `runs-on-json`.
- A caller changes its `uses:` path to `.github/workflows/reusable-secret-scan.yml`, its job id to `secret-scan` and
  name to `Secret scan`, its runner value, if any, to `runs-on` as JSON (a label `"ubuntu-latest"` in quotes, or a
  runner group with labels), and its required check to `Secret scan / Full history`. The scan itself is unchanged.

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
