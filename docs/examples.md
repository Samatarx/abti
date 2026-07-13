# Examples

These examples show the kind of concise, practical learning debrief Abti should produce. They are intentionally markdown, not screenshots.

## React

```md
# Abti Learning Debrief

## 1. What You Practised

- Moved stateful modal behaviour into a focused React hook.
- Kept rendering logic in the component while isolating escape-key and outside-click handling.
- Added tests for opening, closing, and focus restoration.

## 2. What The AI Helped With

- Suggested the hook boundary and drafted the first test cases.
- Helped spot that the event listener needed cleanup on unmount.

## 3. What You Should Understand Before Merging

- Why the hook owns side effects but not the modal markup.
- How the cleanup prevents duplicate listeners after re-renders.
- Which test proves focus returns to the trigger.
```

## TypeScript

```md
# Abti Learning Debrief

## 1. What You Practised

- Replaced loose API response types with a discriminated union.
- Narrowed success and error states before rendering.
- Removed non-null assertions from the page component.

## 2. What The AI Helped With

- Proposed the union shape and updated call sites.
- Helped identify a stale fixture that still used the old error format.

## 3. What You Should Understand Before Merging

- Which field discriminates success from failure.
- Why the UI no longer needs `!` assertions.
- How the fixture protects the error branch.
```

## Testing

```md
# Abti Learning Debrief

## 1. What You Practised

- Added regression coverage for a checkout retry path.
- Mocked the payment client at the boundary instead of mocking internal helpers.
- Verified both the user-facing message and the retry request payload.

## 2. What The AI Helped With

- Drafted the failing test from the bug description.
- Helped reduce brittle assertions around timestamps.

## 3. What You Should Understand Before Merging

- Why the mock lives at the payment-client boundary.
- What would break if the retry reused the original idempotency key.
- Which assertion proves the user can safely retry.
```

## API debugging

```md
# Abti Learning Debrief

## 1. What You Practised

- Traced a 500 response from route handler to service validation.
- Added a guard for missing account configuration.
- Returned a clear 400 response instead of leaking an internal error.

## 2. What The AI Helped With

- Suggested logging the normalized request payload.
- Helped compare the failing request against the expected schema.

## 3. What You Should Understand Before Merging

- Why this is a client error rather than a server error.
- Where the account configuration is loaded.
- Which test covers the missing-configuration branch.
```

## Refactoring

```md
# Abti Learning Debrief

## 1. What You Practised

- Split a large synchronization function into parse, validate, and persist steps.
- Preserved behaviour while making the failure paths easier to test.
- Removed duplicated normalization logic.

## 2. What The AI Helped With

- Proposed extraction points that matched existing responsibilities.
- Helped update tests without changing expected outcomes.

## 3. What You Should Understand Before Merging

- Which extracted function is pure and easiest to unit test.
- How the refactor preserves transaction boundaries.
- What would indicate a behaviour change in review.
```

## GitHub Actions

```md
# Abti Learning Debrief

## 1. What You Practised

- Updated a CI workflow to cache package-manager dependencies.
- Split lint and test jobs so failures are easier to diagnose.
- Limited workflow permissions to the minimum needed for checkout.

## 2. What The AI Helped With

- Drafted the cache key and restore-key pattern.
- Helped check that job dependencies did not serialize unrelated work.

## 3. What You Should Understand Before Merging

- What invalidates the cache.
- Which jobs can run in parallel.
- Why the permissions block is safer than the default.
```

## Accessibility

```md
# Abti Learning Debrief

## 1. What You Practised

- Improved keyboard navigation for a command menu.
- Added accessible labels for icon-only actions.
- Tested focus movement after filtering results.

## 2. What The AI Helped With

- Suggested the ARIA attributes to verify.
- Helped identify an icon button with no accessible name.

## 3. What You Should Understand Before Merging

- How a screen reader announces the active option.
- Why focus should stay inside the menu while it is open.
- Which test protects keyboard selection.
```

## Database migration

```md
# Abti Learning Debrief

## 1. What You Practised

- Added a nullable column before backfilling data.
- Wrote an idempotent backfill for existing records.
- Updated application code before making the field required.

## 2. What The AI Helped With

- Suggested a safer multi-step migration order.
- Helped check the rollback path for the schema change.

## 3. What You Should Understand Before Merging

- Why the migration avoids a table rewrite during deploy.
- What happens if the backfill runs twice.
- When it is safe to add the not-null constraint.
```

## Prompt engineering

```md
# Abti Learning Debrief

## 1. What You Practised

- Rewrote a coding-agent instruction to separate constraints from examples.
- Made consent and privacy behaviour explicit.
- Added expected behaviour for low-context sessions.

## 2. What The AI Helped With

- Suggested clearer trigger conditions.
- Helped remove wording that sounded like monitoring.

## 3. What You Should Understand Before Merging

- Which phrases tell the assistant to stay quiet during active work.
- How direct invocation differs from PR-time offering.
- Why the prompt says to store nothing.
```

## Hooks

```md
# Abti Learning Debrief

## 1. What You Practised

- Added a small optional hook that prints a reminder after recent git activity.
- Kept the hook limited to metadata checks instead of reading file contents.
- Documented that the reminder does not generate a debrief by itself.

## 2. What The AI Helped With

- Drafted a shell command that checks repository state quietly.
- Helped clarify the consent boundary in the documentation.

## 3. What You Should Understand Before Merging

- What git signals trigger the reminder.
- Why the hook must not inspect code or prompts.
- How the user can still decline the learning debrief.
```
