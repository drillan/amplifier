# Design Philosophy Skill

**Purpose**: Understanding and applying the five pillars of design philosophy

**When to use**: Design decisions, component design, user experience design

---

## The Five Pillars

### 1. Purpose Drives Execution

**Principle**: Understand the "why" before perfecting the "how"

**Key Points**:
- Every component starts with purpose
- Ask not just how it looks, but why it's needed
- Avoid design without intention

**Quick Check**: Can you answer "Why does this component exist?"

---

### 2. Craft Embeds Care

**Principle**: Quality lives in the details. Refinement preserves care.

**Key Points**:
- 300ms timing (based on human perception)
- 4.5:1 contrast minimum (based on visual science)
- 44px touch targets (actual human finger size)
- Every decision has a reason

**Quick Check**: Is there evidence of care in the details?

---

### 3. Constraints Enable Creativity

**Principle**: Strategic constraints produce better solutions

**Structure**:
- **LOCKED**: Timing functions, animation durations, transform physics
- **CUSTOMIZABLE**: Colors, content, context
- **FLEXIBLE**: When to use, how to combine

**Quick Check**: "I can't change X, so what CAN I change?" → Usually leads to better solutions

---

### 4. Intentional Incompleteness

**Principle**: The best tools let users add themselves

**What We Complete** (requires expertise):
- Timing/easing
- Accessibility
- Performance
- Technical excellence

**What We Leave Open** (your expression):
- Content (your words, your voice)
- Colors (within validated ranges)
- Context (your values, your purpose)
- Combinations

**Quick Check**: Component is 95% complete (craft) + 5% addition (your intent) = 100% unique

---

### 5. Design for Humans

**Principle**: Design for people with diverse abilities, not just screens

**Physical Humans**:
- Touch targets (44px minimum)
- Contrast ratios (4.5:1, based on visual biology)
- Motion (respect vestibular system)

**Cognitive Humans**:
- Clear feedback for every interaction
- Predictable patterns
- Helpful error messages

**Diverse Humans**:
- Screen reader compatibility
- Keyboard navigation
- Color independence
- Multiple input methods

**Quick Check**: Could someone with low vision, motor impairment, or vestibular disorder use this?

---

## Daily Practice

**Ask before each task**:
1. **Why**: Why does this need to exist?
2. **Who**: Who will use this?
3. **What**: What problem does this solve?
4. **How**: How do we execute with care?

**While coding**:
- **Near**: Execute the implementation
- **Far**: Evaluate against purpose

**Before shipping**:
- [ ] Purpose is clear
- [ ] Craft shows care
- [ ] Constraints are respected
- [ ] Room for user contribution
- [ ] Accessible to diverse humans

---

## The AI Era Shift

**Traditional**: Design systems democratized "good design" through templates

**Amplified Design**: Amplifies individual human expression within quality guardrails

**The Difference**:
- Not removing effort, but directing it toward meaningful choices
- AI handles technical execution
- You provide sensibility, values, cultural meaning

**Result**: Design that's not just technically correct, but carries your human imprint

---

## Quick Reference

### The Decision Framework

When facing design decisions:
1. **Necessity**: "Do we actually need this right now?"
2. **Simplicity**: "What's the simplest way to solve this?"
3. **Directness**: "Can we solve this more directly?"
4. **Value**: "Does complexity add proportional value?"
5. **Maintenance**: "Will this be easy to understand and change later?"

### Areas to Embrace Complexity

- Security (never compromise)
- Data integrity
- Core user experience
- Error visibility

### Areas to Aggressively Simplify

- Internal abstractions
- Generic "future-proof" code
- Edge case handling (handle common cases well first)
- Framework usage (use only what you need)
- State management (keep simple and explicit)

---

## Reference for Deep Dive

For detailed theory, examples, and practices:

- **Full Philosophy**: [@ai_context/DESIGN-PHILOSOPHY.md](../../ai_context/DESIGN-PHILOSOPHY.md)
- **Daily Practice**: [@ai_context/DESIGN-PRINCIPLES.md](../../ai_context/DESIGN-PRINCIPLES.md)
- **Sensibility Framework**: [@ai_context/design/DESIGN-FRAMEWORK.md](../../ai_context/design/DESIGN-FRAMEWORK.md)
- **Product Vision**: [@ai_context/design/DESIGN-VISION.md](../../ai_context/design/DESIGN-VISION.md)

---

**Remember**: Artifacts are containers. Experience is the product. Values are the legacy. Impact is what matters.
