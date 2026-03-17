# Changelog

All notable changes to Bags Play CLI are documented here.

## v0.0.31

Internal improvements and bug fixes.

## v0.0.30

Internal improvements and bug fixes.

## v0.0.29

Internal improvements and bug fixes.

## v0.0.28

### Added
- **Plugin system**: Register, manage, and use third-party plugin packages in your automations. Plugins extend what your apps can do beyond the built-in actions.
- **Secrets management**: Store encrypted API keys and private values that plugins can access at runtime — never hardcode sensitive data in your app definitions.
- **`bags plugins` commands**: List, register, unregister, enable, and disable plugins from the CLI.
- **`bags secrets` commands**: Create, list, update, and delete encrypted secrets from the CLI.
- **`bags init --type plugin`**: Scaffold a new plugin package with typed action boilerplate, test harness, and tsconfig — ready to publish and register.
- **Typed action builders in SDK**: `createAction()` factory gives you IDE autocomplete when configuring actions in app definitions. `.config()` on `ActionNodeBuilder` now accepts typed values with full inference.
- **Plugin config helpers in SDK**: `createConfigAccessor()` for reading resolved plugin config in action handlers. `createPluginManifest()` for declaring your plugin's metadata and config requirements when registering.
- **`@bagsfm/play-core-plugin`**: Core actions (log, HTTP request, transform, set-variable, state, events) are now a standalone published package.
- **`@bagsfm/play-bags-plugin`**: Bags API actions (token info, holders, unclaimed fees, claim fees) are now a standalone published package.

### Changed
- Apps now validate that all referenced plugins exist and are enabled before a run begins — you get a clear error immediately rather than a mid-run failure.
- Deployments accept an optional `pluginConfig` binding that maps plugin IDs to config values or secret references, so each deployment can use different credentials for the same plugin.

## v0.0.27

### Fixed
- `bags init` scaffolded projects can now install dependencies successfully. Published SDK packages at 0.0.26 had incorrect internal dependency versions.

## v0.0.26

Internal improvements and bug fixes.

## v0.0.25

### Added
- **CLI**: All commands now use type-safe hono/client RPC — full end-to-end type inference from API route schemas, replacing the previous generic untyped HTTP client.
- **CLI**: `bags init` now includes an embedded template fallback so compiled binaries work correctly without filesystem access to template sources.
- **CLI**: `bags init` project scaffold now generates Cursor rules, skills, and MCP config; Claude rules, skills, and `CLAUDE.md`.
- **SDK**: New `./app-utils` sub-path export for lightweight consumers that need app validation/serialization without the full engine dependency.
- **npm**: `@bagsfm/play-shared`, `@bagsfm/play-engine`, `@bagsfm/play-sdk`, `@bagsfm/play-plugins`, and `@bagsfm/play-cli` are now published to the `@bagsfm` npm registry on each release.

### Changed
- **CLI**: Builder and loader utilities now import from `@bagsfm/play-sdk/app-utils` instead of the full SDK barrel, reducing compiled binary size.
- **CLI**: Template files renamed to `.tmpl` extension to prevent TypeScript from attempting to compile them as source files.

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
