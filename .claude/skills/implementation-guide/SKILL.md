# Implementation Guide Skill

**Purpose**: Understanding and applying implementation philosophy and modular design principles

**When to use**: Code implementation, architecture decisions, refactoring

---

## Core Philosophy

### Zen-like Minimalism

**Principles**:
- **Wabi-sabi philosophy**: Embrace simplicity and the essential
- **Occam's Razor**: As simple as possible, but no simpler
- **Trust in emergence**: Great systems emerge from simple, well-defined components
- **Present-moment focus**: Handle what's needed now, not every future scenario

**Quick Check**: Is this code really needed? Is there a simpler way?

---

## Three Core Principles

### 1. Ruthless Simplicity

**Practice**:
- **KISS principle**: Keep it as simple as possible
- **Minimize abstractions**: Every abstraction layer must justify its existence
- **Start minimal, grow as needed**: Begin with the simplest implementation
- **Avoid future-proofing**: Don't build for hypothetical requirements
- **Question everything**: Regularly challenge complexity in the codebase

**Questions to Ask**:
1. **Necessity**: "Do we actually need this right now?"
2. **Simplicity**: "What's the simplest way to solve this?"
3. **Directness**: "Can we solve this more directly?"
4. **Value**: "Does complexity add proportional value?"
5. **Maintenance**: "Will this be easy to understand and change later?"

---

### 2. Architectural Integrity with Minimal Implementation

**Practice**:
- **Preserve key architectural patterns**: MCP, SSE, separated I/O channels, etc.
- **Simplify implementations**: Maintain pattern benefits with dramatically simpler code
- **Scrappy but structured**: Lightweight implementations of solid foundations
- **End-to-end thinking**: Focus on complete flows over perfect components

**Quick Check**: Are we maintaining architectural benefits while keeping implementation simple?

---

### 3. Library vs Custom Code

**Evolution Pattern**:
1. **Start simple**: Custom code for basic needs (20 lines handles it)
2. **Growing complexity**: Switch to library when requirements expand
3. **Hitting limits**: Back to custom when you outgrow library capabilities

This isn't failure - it's natural evolution. Each stage was the right choice at that time.

**Custom Code Wins When**:
- Need is simple and well-understood
- You want code perfectly tuned to your exact requirements
- Libraries would require significant "hacking" or workarounds
- Problem is domain-specific
- You need full control over implementation

**Libraries Win When**:
- They solve complex problems you'd rather not tackle (auth, crypto, video encoding)
- They align well with your needs without major modifications
- Mature, battle-tested solutions exist
- Configuration alone can adapt them to your requirements
- Complexity they handle far exceeds integration cost

---

## Modular Design: Bricks & Studs

### The Brick Model

**Concept**: Software is built from small, clear modules (bricks)

**Key Points**:
- **Brick**: Self-contained module with one clear responsibility
- **Stud**: Public contract (function signatures, CLI, API schema)
- **Regeneratable**: Any brick can be regenerated from its spec

**The Loop**:
1. **Contract first**: Start with spec (purpose, inputs, outputs, side-effects, dependencies)
2. **Build in isolation**: Place code, tests, fixtures inside the brick
3. **Expose only contract**: Only public via `__all__` or interface file
4. **Verify behavior**: Focus on behavior at contract level
5. **Regenerate, don't patch**: When internal changes needed, rewrite entire brick from spec

---

## Technical Implementation Guidelines

### API Layer
- Implement only essential endpoints
- Minimal middleware with focused validation
- Clear error responses with useful messages

### Database & Storage
- Simple schema focused on current needs
- Use TEXT/JSON fields to avoid excessive normalization early
- Add indexes only when needed for performance

### Error Handling
- Handle common errors robustly
- Log detailed information for debugging
- Provide clear error messages to users
- Fail fast and visibly during development

---

## Development Approach

### Vertical Slices
- Implement complete end-to-end functionality slices
- Start with core user journeys
- Get data flowing through all layers early
- Add features horizontally only after core flows work

### Iterative Implementation
- **80/20 principle**: High-value, low-effort features first
- One working feature > multiple partial features
- Validate with real usage before enhancing
- Be willing to refactor early work as patterns emerge

### Testing Strategy
- Emphasis on integration and end-to-end tests
- Manual testability as a design goal
- Focus on critical path testing initially
- Add unit tests for complex logic and edge cases
- Testing pyramid: 60% unit, 30% integration, 10% end-to-end

---

## Areas to Embrace vs Simplify

### Embrace Complexity:
- **Security**: Never compromise on security fundamentals
- **Data integrity**: Ensure data consistency and reliability
- **Core UX**: Make primary user flows smooth and reliable
- **Error visibility**: Make problems obvious and diagnosable

### Aggressively Simplify:
- **Internal abstractions**: Minimize layers between components
- **Generic "future-proof" code**: Resist solving non-existent problems
- **Edge case handling**: Handle common cases well first
- **Framework usage**: Use only what you need from frameworks
- **State management**: Keep state simple and explicit

---

## Zero-BS Principle

**NEVER write** (without justification):
- `raise NotImplementedError` (except in abstract base classes)
- `TODO` comments without accompanying code
- `pass` as placeholder (except legitimate Python patterns)
- Mock/fake/dummy functions that don't work
- `return {}  # stub` or similar placeholder returns
- `...` as implementation

**Legitimate uses**:
- `@click.group()` with `pass` body (Click framework requires)
- `except: pass` for graceful degradation when errors expected
- `@abstractmethod` with `raise NotImplementedError` (Python ABC pattern)
- `pass` in protocol definitions or type stubs

**The Test**: "Does this code DO something useful right now?"
- Yes → Keep it
- No → Implement fully or remove

---

## Quick Decision Patterns

### Good Example: Simple SSE Implementation
```python
class SseManager:
    def __init__(self):
        self.connections = {}  # Simple dictionary tracking

    async def add_connection(self, resource_id, user_id):
        connection_id = str(uuid.uuid4())
        queue = asyncio.Queue()
        self.connections[connection_id] = {
            "resource_id": resource_id,
            "user_id": user_id,
            "queue": queue
        }
        return queue, connection_id
```

### Bad Example: Over-engineered SSE Implementation
```python
class ConnectionRegistry:
    def __init__(self, metrics_collector, cleanup_interval=60):
        self.connections_by_id = {}
        self.connections_by_resource = defaultdict(list)
        self.connections_by_user = defaultdict(list)
        self.metrics_collector = metrics_collector
        # [50+ lines of complex indexing and state management]
```

---

## Reference for Deep Dive

For detailed implementation guidelines:

- **Full Implementation Philosophy**: [@ai_context/IMPLEMENTATION_PHILOSOPHY.md](../../ai_context/IMPLEMENTATION_PHILOSOPHY.md)
- **Modular Design Details**: [@ai_context/MODULAR_DESIGN_PHILOSOPHY.md](../../ai_context/MODULAR_DESIGN_PHILOSOPHY.md)

---

**Remember**: It's easier to add complexity later than to remove it. Code you don't write has no bugs. Favor clarity over cleverness. The best code is often the simplest.
