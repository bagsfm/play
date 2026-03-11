# Changelog

All notable changes to Bags Play CLI are documented here.

## v0.0.24

### Added
- New `bags art` command displays the Bags logo with neofetch-style system information.
- `login` and `whoami` now show specific error messages for 401 (invalid/revoked key) and 503 (service unavailable) responses.

### Changed
- Auth validation now calls the real Play API endpoint instead of returning a stub response.
- `login` success message shows the API key name; `whoami` output shows `Key` label instead of `Email`.
- Install script now downloads from the public repo, removing the `GITHUB_TOKEN` requirement.

### Fixed
- Forced `NODE_ENV=production` in CLI entrypoint to prevent pino-pretty worker threads from keeping the process alive in compiled binaries.
