# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Biome configuration package (`@hidekitux/biome-config`) providing shareable Biome v2 configurations ported from neostandard and popular ESLint plugins. Published to GitHub Packages with four configuration presets.

## Development Commands

### Quality Checks
- `bun run check` - Run linting and formatting checks
- `bun run check:fix` - Auto-fix linting and formatting issues
- `bun run lint` / `bun run lint:fix` - Biome linter only
- `bun run format` / `bun run format:fix` - Biome formatter only

### Dependency Management
- `bun run update` - Update all dependencies, sync versions, and reinstall
- `bun run syncpack` - Fix dependency version mismatches
- `bun run syncpack:check` - Check for version mismatches
- `bunx knip` - Check for unused dependencies (CI only)

### Release Process
- `bun run release` - Create patch release (v1.1.1 → v1.1.2)
- `bun run release:minor` - Create minor release (v1.1.0 → v1.2.0)
- `bun run release:major` - Create major release (v1.0.0 → v2.0.0)

Release workflow:
1. Updates version in package.json
2. Generates CHANGELOG.md via git-cliff
3. Creates git tag (v*)
4. Pushes to GitHub
5. GitHub Actions publishes to GitHub Packages

### Testing Locally
- `act push -j quality` - Test CI quality job with act
- `act push -j test-configs --matrix name:standard` - Test config validation

## Architecture

### Configuration Hierarchy
```
config/
├── biome.standard.json  # Base - neostandard rules (single quotes, no semicolons)
├── biome.react.json     # Extends standard + React/JSX/CSS rules
├── biome.test.json      # Extends standard + test framework support
└── biome.web.json       # Extends standard + web-specific rules
```

**Usage Pattern:**
```json
{
  "extends": [
    "@hidekitux/biome-config/standard",
    "@hidekitux/biome-config/react"
  ]
}
```

### CI/CD Pipeline

**GitHub Actions:**
- `ci.yml` - On push/PR: Biome checks, dependency validation, config testing
- `release.yml` - On tag push: Publishes to GitHub Packages

**Git Hooks (via lefthook):**
- pre-commit: Biome check on staged files
- commit-msg: Enforces conventional commits via commitlint
- pre-push: Full Biome check with error-on-warnings
- post-merge: Auto-runs `bun install` and `syncpack fix`

### Key Configuration Decisions

**Formatting (standard base):**
- Indentation: 2 spaces
- Quotes: Single quotes for JS/TS
- Semicolons: Only when needed (ASI)
- Trailing commas: None
- Line endings: LF

**Dependencies:**
- Exact versions only (enforced by syncpack)
- Peer dependency: `@biomejs/biome` 2.2.2

**Testing:**
Test fixtures in `test/fixtures/` validate each config combination works correctly.

### Publishing Details

Published to GitHub Packages as `@hidekitux/biome-config`
- Registry: `https://npm.pkg.github.com`
- Access: Public
- Files: `config/` directory and `README.md`

Exports:
- `./standard` → `config/biome.standard.json`
- `./react` → `config/biome.react.json`
- `./test` → `config/biome.test.json`
- Note: `biome.web.json` exists but is not exported in package.json