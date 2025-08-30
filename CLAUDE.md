# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Biome configuration package (`@hidekitux/biome-config`) that provides shareable Biome v2 configurations ported from neostandard and popular ESLint plugins. The package is published to npm and provides three main configuration presets: standard, react, and test.

## Development Commands

### Linting and Formatting
- `bun run lint` - Run Biome linter
- `bun run lint:fix` - Run Biome linter with auto-fix
- `bun run format` - Check formatting with Biome
- `bun run format:fix` - Format code with Biome
- `bun run check` - Run both linting and formatting checks
- `bun run check:fix` - Fix both linting and formatting issues

### Package Management
- `bun run update` - Update all dependencies and sync versions
- `bun run syncpack` - Fix dependency version mismatches
- `bun run syncpack:check` - Check for dependency version mismatches

### Release and Versioning
- `bun run changelog` - Generate full changelog using git-cliff
- `bun run changelog:unreleased` - Generate changelog for unreleased changes
- `npm run version` - Update version and generate changelog (npm script)
- `bun run release` - Create patch release (v1.0.0 → v1.0.1) and push with tags
- `bun run release:minor` - Create minor release (v1.0.0 → v1.1.0) and push with tags
- `bun run release:major` - Create major release (v1.1.0 → v2.0.0) and push with tags

### Git Hooks
- `bun run lefthook` - Run lefthook manually
- Pre-commit: Runs `biome check` on staged files
- Commit-msg: Validates conventional commit format (feat, fix, docs, style, refactor, perf, test, chore, revert, build, ci)
- Pre-push: Runs full `biome check` with error-on-warnings for config files
- Post-merge: Automatically runs `bun install` and `syncpack fix` when package.json changes

## Architecture

### Configuration Files Structure
```
config/
├── biome.standard.json  - Base configuration for JS/TS projects
├── biome.react.json     - React/JSX/CSS specific rules
├── biome.test.json      - Test framework configurations
└── biome.web.json       - Web-specific configurations
```

### Key Dependencies
- **@biomejs/biome**: The Biome linter/formatter (peer dependency)
- **git-cliff**: Changelog generation from conventional commits
- **lefthook**: Git hooks management
- **syncpack**: Dependency version synchronization

### Configuration Philosophy
- All dependencies use exact versions (no ranges)
- Conventional commits are enforced via git hooks
- Biome is configured with:
  - 2-space indentation
  - Single quotes for JS/TS
  - No trailing commas
  - Semicolons only when needed (ASI)
  - LF line endings

### Publishing
The package is published to npm as `@hidekitux/biome-config` with exports for each configuration preset. Files included in the package are the `config/` directory and `README.md`.