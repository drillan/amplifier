# Claude Code Skills

Skills provide modular, on-demand context loading for Claude Code.

## What are Skills?

Instead of always loading all documentation into the context window, Skills allow you to load specific guidance only when needed. This dramatically reduces baseline context usage while preserving access to full documentation.

## Benefits

- **Reduced context usage**: ~60% reduction in always-loaded context
- **Better performance**: More room for complex tasks and sub-agents
- **Preserved documentation**: Full docs available via reference links
- **No breaking changes**: Existing workflows continue to work

## Available Skills

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| `design-philosophy` | Core design principles and decision framework | Design decisions, architecture reviews |
| `implementation-guide` | Implementation patterns and technical guidelines | Coding tasks, refactoring |
| `agent-usage` | Sub-agent optimization and parallel execution | Complex multi-step tasks |
| `discoveries` | Known issues, solutions, and patterns | Debugging, problem-solving |

## How Skills Work

1. **Core context** (AGENTS.md, CLAUDE.md) is always loaded
2. **Skills** are loaded on-demand when their expertise is needed
3. **Full documentation** (ai_context/*.md) available for deep dives via reference links

## Using Skills

Skills are automatically available in Claude Code. When you need specific guidance:

- For design decisions → the design-philosophy skill provides principles
- For implementation → the implementation-guide skill provides patterns
- For complex tasks → the agent-usage skill provides strategies
- For debugging → the discoveries skill provides known solutions

## Creating New Skills

1. Create directory: `.claude/skills/[skill-name]/`
2. Create `SKILL.md` with:
   - Purpose statement
   - When to use
   - Key content (200-250 lines max)
   - Reference links to full documentation

### Skill Template

```markdown
# [Skill Name] Skill

**Purpose**: [What this skill helps with]

**When to use**: [Situations where this skill is valuable]

---

[Main content - concise, actionable guidance]

---

## Reference for Deep Dive

[Links to full documentation for detailed information]
```

## Measured Results

From testing in a fork:

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Memory files | 34.6k tokens | 13.6k tokens | -60.7% |
| Free space | 75k tokens | 108k tokens | +44% |
| Context usage | 62% | 46% | -16% |
