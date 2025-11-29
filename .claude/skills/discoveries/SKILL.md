# Discoveries Skill

**Purpose**: Recording and referencing non-obvious problems, solutions, and patterns

**When to use**: Before tackling complex problems, during debugging, when discovering new patterns

---

## Overview

This skill documents non-obvious problems, solutions, and patterns discovered during development. It prevents encountering the same issues repeatedly and helps benefit from past learnings.

---

## When to Consult DISCOVERIES.md

### Before Implementation

**Before solving complex problems**:
1. Check DISCOVERIES.md for similar problems already solved
2. Avoid past failure patterns
3. Leverage proven solutions

---

## When to Update DISCOVERIES.md

### Add Entry When You:

1. **Encounter non-obvious problems** - Requiring research or debugging
2. **Find conflicts between tools/libraries** - Unexpected interactions
3. **Discover framework-specific patterns** - Undocumented limitations
4. **Solve issues future developers might face** - Prevent repetition

---

## Common Discovery Categories

### Environment & Setup Issues

**DevContainer Problems**:
- Missing tools after container rebuild
- Environment variables not set in post-create scripts
- Permission issues with mounted volumes

**Solution Pattern**: Use official DevContainer features over custom scripts. Add logging for troubleshooting.

### Cloud Sync & File I/O

**OneDrive/Dropbox/iCloud Issues**:
- Intermittent I/O errors (OSError errno 5)
- Files not available locally ("cloud-only")
- Sync delays causing race conditions

**Solution Pattern**: Add retry logic with exponential backoff. Use "Always keep on device" settings. Create centralized file I/O utilities.

### LLM Response Handling

**Common Failures**:
- JSON parsing errors (markdown-wrapped, explanatory text)
- Context contamination (system instructions in output)
- Transient failures without retry

**Solution Pattern**: Use extraction over validation. Implement feedback loops for retries. Isolate context with clear delimiters.

### Tool Generation Patterns

**Predictable Failures**:
- Non-recursive file discovery (`*.md` vs `**/*.md`)
- No minimum input validation
- Silent failures without user feedback

**Solution Pattern**: Enforce standard patterns via templates. Always show what's being processed. Fail fast and loud.

---

## Entry Format

When adding new discoveries, follow this structure:

### [Title] ([Date])

**Issue**:
[Concise description of the problem]

**Root Cause**:
[Technical explanation of why it happened]

**Solution**:
[Implemented solution with code examples]

**Key Learnings**:
[Main insights for future reference]

**Prevention**:
[How to avoid this problem]

---

## Example Entry

### pnpm Global Bin Configuration (2025-10-23)

**Issue**: `make install` fails with `ERR_PNPM_NO_GLOBAL_BIN_DIR`

**Root Cause**: SHELL environment variable not set during DevContainer post-create script execution

**Solution**:
```bash
export SHELL="${SHELL:-/bin/bash}"
pnpm setup
export PNPM_HOME="/home/vscode/.local/share/pnpm"
export PATH="$PNPM_HOME:$PATH"
```

**Key Learnings**:
- SHELL not set in post-create context
- pnpm requires SHELL to modify correct config file
- Silent failures are dangerous - check logs

**Prevention**:
- Always set SHELL explicitly in post-create scripts
- Check post-create logs after rebuilding containers

---

## Best Practices

### Writing Discoveries

1. **Be specific**: Avoid vague descriptions
2. **Be actionable**: Include implementable solutions
3. **Provide context**: Explain why and under what conditions
4. **Show code examples**: Demonstrate actual solutions
5. **Extract learnings**: Identify key insights

### Maintaining Discoveries

**Regularly review and update**:
- Remove outdated entries
- Remove those replaced by better practices, code, or tools
- Update those where best practice has evolved

### Discovery Lifecycle

1. **Encounter**: Hit a non-obvious problem
2. **Investigate**: Find root cause
3. **Solve**: Implement and verify fix
4. **Document**: Add to DISCOVERIES.md
5. **Review**: Periodically check for staleness

---

## Quick Reference

### Before Starting Complex Work

```
1. Check DISCOVERIES.md for related issues
2. Search for similar patterns
3. Note any relevant solutions
4. Apply learnings proactively
```

### After Solving Non-Obvious Problems

```
1. Document the issue
2. Explain root cause
3. Show the solution
4. Extract key learnings
5. Add prevention steps
```

---

## Reference for Complete Details

For full discovery history and detailed implementations:

- **Complete DISCOVERIES**: [@DISCOVERIES.md](../../DISCOVERIES.md)

---

**Remember**: Learning from past mistakes is more efficient than repeating them. DISCOVERIES is collective memory.
