# Migration Guide

## v1.x to v2.0.0

## Overview

Version 2.0.0 adds hooks integration and enhanced templates while maintaining backward compatibility with existing workflows.

## v2.0.0 to v2.0.0-superpowers (This Fork)

### Overview

This fork adds Superpowers integration while maintaining full compatibility with the original v2.0.0 features.

### What's New

- **Canonical Plan Detection**: When creating `task_plan.md`, the skill now checks for existing plans in `docs/plans/...` and prompts you to link to them
- **Unified Workflow**: Designed for workflows where Superpowers generates canonical plans and this plugin maintains execution tracking
- **No Breaking Changes**: All existing workflows continue to work exactly as before

### Migration Steps

1. **Update the Plugin**
   ```text
   # If installed from original, uninstall first (optional)
   /plugin uninstall planning-with-files

   # Add your fork as a marketplace and install it
   /plugin marketplace add OniReimu/planning-with-files-superpowers
   /plugin install planning-with-files-superpowers@planning-with-files-superpowers
   ```

2. **Existing Files Continue Working**
   - Your existing `task_plan.md`, `findings.md`, and `progress.md` files will continue to work
   - No changes required to existing planning files

3. **Optional: Link to Superpowers Plans**
   - When creating new `task_plan.md` files, you'll be prompted if a canonical plan exists
   - You can choose to link to it or proceed with normal planning

### Benefits

- **Seamless Integration**: Works with Superpowers-generated plans in `docs/plans/...`
- **Better Handoff**: Clear separation between canonical plan (stable) and execution tracker (dynamic)
- **Multi-Model Support**: Designed for GPT planning + Claude implementation workflows

---

## v1.x to v2.0.0 (Original)

## What's New

### 1. Hooks (Automatic Behaviors)

v2.0.0 adds Claude Code hooks that automate key Manus principles:

| Hook | Trigger | Behavior |
|------|---------|----------|
| `PreToolUse` | Before Write/Edit/Bash | Reads `task_plan.md` to refresh goals |
| `Stop` | Before stopping | Verifies all phases are complete |

**Benefit:** You no longer need to manually remember to re-read your plan. The hook does it automatically.

### 2. Templates Directory

New templates provide structured starting points:

```
templates/
├── task_plan.md    # Phase tracking with status fields
├── findings.md     # Research storage with 2-action reminder
└── progress.md     # Session log with 5-question reboot test
```

### 3. Scripts Directory

Helper scripts for common operations:

```
scripts/
├── init-session.sh     # Creates all 3 planning files
└── check-complete.sh   # Verifies task completion
```

## Migration Steps

### Step 1: Update the Plugin

```bash
# If installed via marketplace
/plugin update planning-with-files

# If installed manually
cd .claude/plugins/planning-with-files
git pull origin master
```

### Step 2: Existing Files Continue Working

Your existing `task_plan.md` files will continue to work. The hooks look for this file and gracefully handle its absence.

### Step 3: Adopt New Templates (Optional)

To use the new structured templates, you can either:

1. **Start fresh** with `./scripts/init-session.sh`
2. **Copy templates** from `templates/` directory
3. **Keep your existing format** - it still works

### Step 4: Update Phase Status Format (Recommended)

v2.0.0 templates use a more structured status format:

**v1.x format:**
```markdown
- [x] Phase 1: Setup ✓
- [ ] Phase 2: Implementation (CURRENT)
```

**v2.0.0 format:**
```markdown
### Phase 1: Setup
- **Status:** complete

### Phase 2: Implementation
- **Status:** in_progress
```

The new format enables the `check-complete.sh` script to automatically verify completion.

## Breaking Changes

**None.** v2.0.0 is fully backward compatible.

If you prefer the v1.x behavior without hooks, use the `legacy` branch:

```bash
git checkout legacy
```

## New Features to Adopt

### The 2-Action Rule

After every 2 view/browser/search operations, save findings to files:

```
WebSearch → WebSearch → MUST Write findings.md
```

### The 3-Strike Error Protocol

Structured error recovery:

1. Diagnose & Fix
2. Alternative Approach
3. Broader Rethink
4. Escalate to User

### The 5-Question Reboot Test

Your planning files should answer:

1. Where am I? → Current phase
2. Where am I going? → Remaining phases
3. What's the goal? → Goal statement
4. What have I learned? → findings.md
5. What have I done? → progress.md

## Questions?

**For Superpowers integration:** Open an issue: https://github.com/OniReimu/planning-with-files-superpowers/issues

**For core planning-with-files:** Open an issue: https://github.com/OthmanAdi/planning-with-files/issues
