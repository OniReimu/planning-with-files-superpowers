# Changelog

All notable changes to this project will be documented in this file.

## [2.0.0-superpowers] - 2026-01-09

### Added

- **Superpowers Integration**
  - Automatic detection of canonical plans in `docs/plans/...` when creating `task_plan.md`
  - User prompt to confirm if detected plan is the one to use
  - `task_plan.md` template includes canonical plan pointer section
  - Seamless handoff between Superpowers planning (Codex/GPT) and implementation (Claude Code)

- **Enhanced Workflow**
  - `task_plan.md` serves as execution tracker while `docs/plans/...` remains canonical
  - Support for multi-model workflows (GPT plans, Claude implements)
  - Maintains compatibility with original planning-with-files workflow

### Changed

- Plugin name changed to `planning-with-files-superpowers` to distinguish from original
- Repository URLs updated to reflect fork
- Installation instructions updated for fork

### Preserved

- All original v2.0.0 features and functionality
- Backward compatibility with existing planning-with-files workflows
- MIT License unchanged

## [2.0.1-superpowers] - 2026-01-09

### Fixed

- Removed duplicate legacy skill directory to prevent the fork from appearing to install “both” versions.
- Renamed the skill to `planning-with-files-superpowers` (unique skill name) to avoid collisions when the upstream `planning-with-files` plugin is also installed.
- Updated install docs to use marketplace install flow (`/plugin marketplace add ...` then `/plugin install ...`).

## [2.0.2-superpowers] - 2026-01-10

### Added

- **Checkpointed implementation** guidance (executing-plans compatible): review plan first, execute default batches of 3 tasks, report verification output, and wait for feedback.
- **Stop policy: checkpoints-allowed** to permit pausing between checkpoint batches without failing the Stop hook.
- **Batch Reports** section in `progress.md` template for clean handoff to reviewers (e.g. Codex/GPT-5.2).

## [2.0.0] - 2026-01-08

### Added

- **Hooks Integration** (Claude Code 2.1.0+)
  - `PreToolUse` hook: Automatically reads `task_plan.md` before Write/Edit/Bash operations
  - `Stop` hook: Verifies all phases are complete before stopping
  - Implements Manus "attention manipulation" principle automatically

- **Templates Directory**
  - `templates/task_plan.md` - Structured phase tracking template
  - `templates/findings.md` - Research and discovery storage template
  - `templates/progress.md` - Session logging with test results template

- **Scripts Directory**
  - `scripts/init-session.sh` - Initialize all planning files at once
  - `scripts/check-complete.sh` - Verify all phases are complete

- **New Documentation**
  - `CHANGELOG.md` - This file
  - `MIGRATION.md` - Guide for upgrading from v1.x

- **Enhanced SKILL.md**
  - The 2-Action Rule (save findings after every 2 view/browser operations)
  - The 3-Strike Error Protocol (structured error recovery)
  - Read vs Write Decision Matrix
  - The 5-Question Reboot Test

- **Expanded reference.md**
  - The 3 Context Engineering Strategies (Reduction, Isolation, Offloading)
  - The 7-Step Agent Loop diagram
  - Critical constraints section
  - Updated Manus statistics

### Changed

- SKILL.md restructured for progressive disclosure (<500 lines)
- Version bumped to 2.0.0 in all manifests
- README.md reorganized (Thank You section moved to top)
- Description updated to mention >5 tool calls threshold

### Preserved

- All v1.0.0 content available in `legacy` branch
- Original examples.md retained (proven patterns)
- Core 3-file pattern unchanged
- MIT License unchanged

## [1.0.0] - 2026-01-07

### Added

- Initial release
- SKILL.md with core workflow
- reference.md with 6 Manus principles
- examples.md with 4 real-world examples
- Plugin structure for Claude Code marketplace
- README.md with installation instructions

---

## Versioning

This project follows [Semantic Versioning](https://semver.org/):
- MAJOR: Breaking changes to skill behavior
- MINOR: New features, backward compatible
- PATCH: Bug fixes, documentation updates
