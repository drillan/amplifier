# Agent Usage Skill

**Purpose**: Understanding effective sub-agent usage, parallel execution, and process patterns

**When to use**: Complex tasks, multi-step workflows, specialized work

---

## CRITICAL: Respect User Time

**User's time is the most valuable resource**

### Pre-Presentation Checklist

Before presenting work as "done":

1. ✅ **Test it yourself thoroughly** - Don't make the user your QA
2. ✅ **Fix obvious issues** - Syntax errors, import problems, broken logic
3. ✅ **Verify it actually works** - Run tests, check structure, validate logic
4. ✅ **Then present it** - "Ready for review" means YOU'VE already validated

### Role Division

**User's role**: Strategic decisions, design approval, business context, stakeholder judgment
**Your role**: Implementation, testing, debugging, fixing issues before engaging user

**Anti-pattern**: ❌ "I've implemented X, can you test it?"
**Correct pattern**: ✅ "I've implemented and tested X. Tests pass, structure verified, logic validated. Ready for your review. Here's how to verify."

---

## Sub-Agent Optimization Strategy

### Core Principle

**IMPORTANT**: Always proactively use sub-agents when their expertise matches the task. Don't wait to be asked.

### When to Use Sub-Agents

1. **Before starting work** - Consider if existing agents fit the task
2. **During challenges** - If struggling, propose a new specialized agent
3. **After completion** - Reflect on where an agent could have helped
4. **Agent creation is cheap** - Better to have specialized tools than struggle with generic ones

### Available Specialized Agents

**Development**:
- `zen-architect` - Code planning, architecture design, review
- `bug-hunter` - Bug finding and fixing specialist
- `test-coverage` - Test coverage analysis, test suggestions
- `modular-builder` - Module implementation from specifications
- `integration-specialist` - External services, APIs, MCP integration

**Knowledge Synthesis**:
- `concept-extractor` - Extract knowledge components from articles
- `insight-synthesizer` - Discover innovative connections between concepts
- `content-researcher` - Research and analyze content files

**Meta**:
- `subagent-architect` - Create new agents

### Usage Pattern

```
Task [agent-name]: "Clear, specific task description"
```

Examples:
```
Task zen-architect: "Analyze the architecture of this authentication system"
Task bug-hunter: "Systematically track down and fix this KeyError"
Task test-coverage: "Analyze if the synthesis pipeline has adequate test coverage"
```

---

## Parallel Execution Strategy

### CRITICAL Question

**Always ask yourself**: "What can I do in parallel here?"

**One message with multiple tool calls** - NOT multiple messages with single tool calls

### When to Parallelize

Parallelize when tasks:
- Don't depend on each other's output
- Perform similar operations on different targets
- Can be delegated to different agents
- Gather independent information

### Common Patterns

**Multiple File Edits**:
```
Single message with multiple Edit calls:
- Edit: Fix type error in src/auth.py
- Edit: Fix type error in src/database.py
- Edit: Fix type error in src/api.py
```

**Information Gathering**:
```
Parallel reads and searches:
- Grep: Search for existing patterns
- Read: Main implementation file
- Read: Test file
- Read: Related configuration
```

**Multiple Agent Analysis**:
```
Single message with multiple Task calls:
- Task zen-architect: "Design approach"
- Task bug-hunter: "Identify potential issues"
- Task test-coverage: "Suggest test cases"
```

### Anti-Patterns to Avoid

**❌ Don't do this**:
```
"Let me read the first file"
[Read file1.py]
"Now let me read the second file"
[Read file2.py]
```

**✅ Do this instead**:
```
"I'll examine these files in parallel"
[Single message: Read file1.py, Read file2.py, Read file3.py]
```

---

## Incremental Processing Pattern

### Batch Processing Principles

**Save progress after each item processed**:

- **Save continuously**: Write results after each item, not at intervals
- **Fixed filenames**: Consistent filenames that overwrite (e.g., `results.json`), not timestamps
- **Enable interruption**: Users can abort anytime without losing processed items
- **Support incremental updates**: Add new items without reprocessing existing ones

**Why**: Bottleneck is always processing (LLM APIs, network calls), never disk I/O

---

## Configuration Management

### Single Source of Truth Principle

**Every configuration setting should have exactly ONE authoritative location**

### Implementation

**Tool Configuration Hierarchy**:
- `pyproject.toml` - Python project settings (primary)
- `ruff.toml` - Ruff-specific settings only if not in pyproject.toml
- `.vscode/settings.json` - IDE settings that reference project config
- `Makefile` - Commands that use project config, not duplicate it

**Common Locations**:
- **Python dependencies**: `pyproject.toml` only (managed by uv)
- **Code exclusions**: `pyproject.toml` [tool.pyright] exclude
- **Formatting rules**: `ruff.toml` or `pyproject.toml` [tool.ruff]

**Benefits**:
- Changes propagate automatically
- Reduces maintenance burden
- Prevents configuration drift

---

## Decision Tracking System

### When to Consult

1. **Before proposing major changes** - Check if relevant decisions exist
2. **When questioning existing patterns** - Understand original rationale
3. **During architecture reviews** - Reference historical context
4. **When choosing between approaches** - Learn from past trade-offs

### When to Create

Create new decision record for:
- Architectural choices affecting system structure
- Selection between multiple viable approaches
- Adoption of new patterns, tools, or libraries
- Reversal or significant modification of previous decisions

### Location

`ai_working/decisions/` - See `ai_working/decisions/README.md` for template

---

## Quick Patterns

### DISCOVERIES.md Consultation

**Before solving complex problems**:
1. Check DISCOVERIES.md for similar problems already solved
2. Update DISCOVERIES.md when you:
   - Encounter non-obvious problems requiring research or debugging
   - Find conflicts between tools or libraries
   - Discover framework-specific patterns or limitations

### Git Commit Messages

Always insert at the end of commit messages:
```
🤖 Generated with [Amplifier](https://github.com/microsoft/amplifier)

Co-Authored-By: Amplifier <240397093+microsoft-amplifier@users.noreply.github.com>
```

---

## Reference for Deep Dive

For detailed patterns, examples, and anti-patterns:

- **Full Agent Guide**: [@AGENTS.md](../../AGENTS.md)
- **Agent Catalog**: [@.claude/AGENTS_CATALOG.md](../AGENTS_CATALOG.md) (if exists)

---

**Remember**:
- Parallel execution is the default, not an optimization
- Sequential execution needs justification (true dependencies)
- Respect user time = test before presenting
- Use sub-agents proactively
