# Changelog

All notable changes to Bags Play CLI are documented here.

## v0.0.42

Internal improvements and bug fixes.

## v0.0.41

Internal improvements and bug fixes.

## v0.0.40

### Added
- **CLI**: `bags` commands now support `--json` machine-readable output, making scripting and CI automation easier.
- **CLI**: `bags init` now scaffolds projects against the shared `play-skills` library so generated guidance stays aligned with the latest Bags Play workflow.

### Changed
- **SDK**: App trigger and reference validation now align with the current manual, cron, webhook, and event trigger unions, giving earlier author-time feedback.

### Fixed
- **SDK**: Published npm packages now point TypeScript type exports at the built `dist` declarations, improving resolution for npm consumers.

## v0.0.39

### Fixed
- **SDK**: npm packaging for published packages — prepack/postpack steps and export maps so installs from npm resolve entry points and TypeScript declarations reliably when you depend on `@bagsfm/play-sdk` and related packages.

## v0.0.38

### Changed
- **CLI**: The `bags` standalone binary is built with bytecode, and the entrypoint avoids top-level `await` so compilation stays reliable across targets.
- **SDK**: Published npm packages now use a bundled JavaScript build with separate `.d.ts` emit (via the workspace npm build script), for more predictable installs when you depend on `@bagsfm/play-sdk` from npm.

## v0.0.37

Internal improvements and bug fixes.

## v0.0.36

### Added
- **SDK**: App DAG and expression validation aligned with the latest engine rules — catch structural and expression issues when authoring apps locally.
- **SDK**: New and expanded documentation — getting started, expressions, plugins, validation, and composition/presets (see package docs).
- **SDK**: Richer TSDoc across modules with improved type links and examples.

### Changed
- **CLI**: Fee amounts use clearer formatting in command output.
- **CLI**: `bags init --type plugin` scaffolds plugin templates that include the plugin runtime version field expected by the platform.

## v0.0.35

### Added
- `bags completion` command generates shell completions for bash, zsh, and fish — auto-configured during installation.
- `bags runs fees` command shows fee details for monetized app runs.
- `bags init` now verifies tool version compatibility before scaffolding.
- Custom `play_api` and `bags_api` URL overrides can be set in `bags.toml` for pointing the CLI at non-default API endpoints.
- Monetization-aware secrets: the CLI now handles integrated secrets for monetized plugin configurations.
- **SDK**: Plugin authors can declare per-action fee requirements using `fee()` in the action manifest builder.

### Changed
- Internal CLI metadata and constants centralized for consistency across all commands.

## v0.0.34

### Added
- **CLI**: Every command and subcommand now includes an "Examples:" section in `--help` output with practical, copy-paste usage examples.
- **CLI**: Parent command help pages (e.g. `bags deployments --help`, `bags runs --help`) now list their subcommands inline with argument signatures and descriptions — no more guessing what's available.
- **CLI**: `bags --help` root page now shows a curated "Examples:" section for the most common workflows.

### Changed
- **CLI**: Help output for nested subcommands now shows the full command path in the "Usage:" line (e.g. `bags deployments list [flags]` instead of just `list [flags]`).
- **CLI**: `--no-color` flag is honoured immediately on startup, before any color output is produced.

## v0.0.33

### Added
- **CLI**: `bags deployments` command group — list, get, pause, and unpause your deployments with rich table output.
- **CLI**: `bags runs` command group — list, get, trigger, cancel runs, and tail live logs directly from the terminal.
- **SDK**: `createOptionalPluginConfigAccessor` — new SDK helper for plugin authors. Use this when your plugin config is fully optional (all fields have defaults); it falls back to schema defaults when no deployment config is bound instead of failing.

### Fixed
- Zod v4 compatibility: env parsers now use `z.flattenError()` instead of the removed `result.error.flatten()` method.

## v0.0.32

Internal improvements and bug fixes.

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
