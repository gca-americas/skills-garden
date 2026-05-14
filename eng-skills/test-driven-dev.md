---
name: test-driven-dev
description: Use this skill whenever the user is writing or has just written application code and wants tests around it. Trigger when the user says "write tests," "add tests," "test this," "TDD," "run the tests," or applies this skill explicitly. Also trigger automatically after generating a substantial implementation from an `engineering.md` or similar enginnering deisgn doc that includes a testing strategy section. Defines an auto-fix loop (write → run → fix → re-run, max 3 iterations), a scope contract (unit + simple integration only, no browser automation), and a regression rule (every human-caught bug becomes a new test). Specialized for Python (pytest) and Node/React (Jest or Vitest) stacks, but the methodology is language-agnostic.
---

# Test-Driven Dev

A lightweight TDD discipline for vibe-coded apps. Designed for beginners who shouldn't have to learn pytest or Jest deeply before they can ship something.

## The contract

**You will:**

1. Read the testing strategy section of `engineering.md` (if it exists) and use it as the source of truth for *what* to test.
2. Write tests that match the language and stack of the implementation. Default to **pytest** for Python and **Jest** (or **Vitest** for Vite-based apps) for Node/React.
3. Run the tests automatically. Do not stop after writing — execute them.
4. If tests fail, fix the **implementation code** (not the tests, unless the tests are clearly wrong) and re-run.
5. Loop a maximum of **3 times**. If tests are still failing after the third run, stop. Summarize what passed, what failed, and what you tried. Do not enter a fourth iteration.
6. When the human catches a bug in their app that the test suite missed, write a regression test that would have caught it, then fix the code so the test passes.

**You will not:**

- Write Playwright, Selenium, Cypress, or any browser-automation tests.
- Write exhaustive coverage. This is pragmatic testing, not academic testing.
- Mock the universe. Use real values where reasonable.
- Skip running the tests. "Writing them" is not the deliverable. "Passing tests" is.
- Modify tests to make them pass when the implementation is wrong. Fix the code.

## Scope: what counts as a test

**In scope:**

- **Unit tests** for pure functions, utility modules, data transformations, validators, and any function with clear inputs and outputs.
- **Simple integration tests** for: API endpoints (assert the HTTP response without spinning up a real browser), one happy-path flow per major feature, and database access if it's central to the app.

**Out of scope:**

- End-to-end browser tests (Playwright, Selenium, Cypress).
- Visual regression tests.
- Performance / load tests.
- Coverage targets. Do not optimize for a percentage. Optimize for "the test suite catches the dumb mistakes."

## The auto-fix loop

```
   Write tests from engineering.md strategy
                  │
                  ▼
            Run the tests
                  │
              ┌───┴───┐
              ▼       ▼
            PASS    FAIL
              │       │
              │       ▼
              │   Fix the implementation
              │       │
              │       ▼
              │   Re-run (iteration counter += 1)
              │       │
              │   ┌───┴───┐
              │   ▼       ▼
              │  PASS    FAIL
              │   │       │
              │   │       ▼
              │   │   iteration < 3? ──► loop back to fix
              │   │       │
              │   │      no
              │   │       │
              │   │       ▼
              │   │   Stop. Summarize.
              ▼   ▼
       Hand off to human for visual verification (Stage 6)
```

**Iteration counter starts at 1** (the first run after writing the tests). The third failed run is the cap. Do not silently retry past 3.

## When the cap is hit

If you reach the 3× cap without passing, **stop and report**. Do not "try one more thing." The report should include:

- Which tests passed (if any).
- Which tests failed, with the actual error output.
- What you tried in each iteration and why it didn't fix the issue.
- A hypothesis about what's wrong. Usually one of:
  - The testing strategy in `engineering.md` is asking for behavior the implementation doesn't actually provide (spec mismatch — update the doc).
  - The test is wrong about the expected behavior (rare — re-read the spec).
  - The architecture can't support what's being tested (structural problem — escalate to the human).

Then ask the human how to proceed. Do not loop further on your own.

## Stack-specific defaults

### Python

- **Runner:** `pytest`
- **Layout:** tests live in a `tests/` directory at the project root, mirroring the module structure. Each test file starts with `test_`.
- **Run command:** `pytest -v` from the project root.
- **Style:** simple `assert` statements. No `unittest.TestCase` boilerplate unless the project already uses it. Use `pytest` fixtures sparingly — only when setup is genuinely shared.
- **Imports:** prefer relative imports from the package; if the project has no package structure, add a `conftest.py` at the test root that handles path setup.

Example shape:

```python
# tests/test_calculator.py
from app.calculator import add, divide

def test_add_returns_sum():
    assert add(2, 3) == 5

def test_divide_by_zero_raises():
    import pytest
    with pytest.raises(ZeroDivisionError):
        divide(1, 0)
```

### Node / React

- **Runner:** **Vitest** if the project uses Vite (most React + Vite scaffolds); **Jest** otherwise. Detect by checking `package.json` and `vite.config.*`.
- **Layout:** colocate tests next to source as `*.test.js` / `*.test.ts` (or `.jsx` / `.tsx`), OR put them in a `__tests__/` directory. Match the project's existing convention if there is one.
- **Run command:** `npm test` if a script exists; otherwise `npx vitest run` or `npx jest`.
- **React component tests:** use `@testing-library/react` for rendering. Test behavior (what the user sees and clicks), not implementation details (state internals).
- **API route tests (Express, etc.):** use `supertest` for HTTP-level integration tests.

Example shape:

```javascript
// src/utils/format.test.js
import { formatPrice } from './format';

test('formats price with two decimals', () => {
  expect(formatPrice(1)).toBe('$1.00');
  expect(formatPrice(1.5)).toBe('$1.50');
});
```

```javascript
// src/components/Counter.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments when clicked', () => {
  render(<Counter />);
  fireEvent.click(screen.getByRole('button', { name: /increment/i }));
  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

### Other languages

If the project is in a language not covered above, pick the standard test runner for that ecosystem (e.g. `go test` for Go, `cargo test` for Rust, `rspec` or `minitest` for Ruby). The methodology stays identical — write, run, loop, cap at 3.

## Where to find the project-specific plan

This skill is the **methodology**. The **plan** lives in `engineering.md` under a heading like "Testing strategy" or "Tests." That section should tell you:

- Which modules / components / endpoints need unit tests
- Which user flows need an integration test (one happy path each)
- What is deliberately *not* being tested, and why

If `engineering.md` exists but has no testing strategy section, write tests for: (a) every exported function in the main module, and (b) the primary user flow. Then suggest the user add a testing strategy section to the doc.

If `engineering.md` doesn't exist, ask the user what they want tested before writing anything.

## Regression rule

Whenever a human reports a bug that the existing tests didn't catch:

1. Write a test that fails because of the bug.
2. Confirm the test fails by running it (this is the "red" step).
3. Fix the implementation.
4. Run the test again — it should pass (this is the "green" step).
5. Run the full suite to make sure nothing else broke.

This is the only way the test suite grows in a useful direction. Coverage that wasn't motivated by a real bug is theater.

## What you tell the user when you're done

After a successful run, give a short summary:

> Tests written: N unit, M integration.
> Tests passing: all.
> Iterations needed: K (where K is 1, 2, or 3).
> Ready for visual verification.

After hitting the cap without passing:

> Tests written: N unit, M integration.
> Tests passing: X of (N+M).
> Iterations attempted: 3.
> Suspected root cause: [one sentence].
> Next step: [update spec / re-read test / escalate to human — pick one].

Keep it brief. The human needs to know whether to proceed to visual verification or to fix the spec.
