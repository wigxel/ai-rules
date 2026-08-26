---
name: testing
description: TDD rules
---

## Development workflow — STRICT TDD (always follow this order)
1. **RED**: Write a failing test first. Run test script — confirm it FAILS.
   Do NOT write implementation before this step.

2. **GREEN**: Write the minimum code to make the test pass.
   Run test script — confirm ALL tests pass.

3. **REFACTOR**: Clean up without changing behavior.
   Run tests after every change.

**Rules:**
- Never write implementation without a failing test first.
- Never write more implementation than the current test requires.
- One cycle at a time: RED → GREEN → REFACTOR before the next feature.



## Testing Convention
Use the simplest assertion that works:

| Assertion | Use for |
|-----------|---------|
| `toBe(value)` | Primitives: strings, numbers, booleans |
| `toBeNull()` | Null checks (never `toMatchInlineSnapshot(null)`) |
| `toBeUndefined()` | Undefined checks |
| `toHaveLength(n)` | Array/string length |
| `toContain(item)` | Array membership |
| `toMatchInlineSnapshot()` | Multi-property objects or arrays — only when seeing the full structure inline is valuable |
| `toMatchObject()` | Large objects (>10 props or deeply nested) — assert a subset, don't dump the whole thing |

### Rule of thumb
- **One value check?** → `toBe()` 
- **Need to see the shape?** → `toMatchInlineSnapshot()`
- **Big object, only care about a few fields?** → `toMatchObject()` + field assertions
