---
name: code-walkthrough
description: Explains what was just built so the developer truly understands it. Use this skill right after implementing, changing, or fixing anything: a feature, module, endpoint, service, bug fix, or refactor. Make sure to use it whenever code has just been written or modified, even if the user does not ask for an explanation, and whenever the user says "explain", "walk me through", "I don't understand this code", or "how does this work".
---

# Code Walkthrough

Never end an implementation with just "done". Finish every build with a
walkthrough so the developer can understand, test, and maintain the code
without needing the AI.

## Who you are explaining to

An early-career developer who can read code but was not present while it was
written. Be clear and direct. Define a term the first time it appears. Skip
basics the developer has already shown they know.

## Workflow

Follow these phases in order. Do not skip Phase 1.

### Phase 1: Size the change

Decide the depth before writing anything.

| Change size | Examples | Steps to include |
|---|---|---|
| Small | typo, config tweak, one-line bug fix | 1, 3, 7 |
| Medium | new endpoint, new function, single-file refactor | 1, 2, 3, 4, 7, 8 |
| Large | new module, multi-file feature, schema change | all 10 steps |

If the user says "explain deeply", use all 10 steps. If they say "quick
summary", use steps 1 and 7 only.

### Phase 2: Gather facts (do not guess)

Before explaining, re-check the actual code that was written:
- List every file created or changed.
- Note the entry point (route, function, or command) where execution starts.
- Note external things touched: database tables, APIs, environment variables.

Only explain what the code really does, not what it was intended to do.

### Phase 3: Write the walkthrough

Use this order. Each step has a clear goal.

1. **Summary** (2-3 sentences): What was built and what problem it solves.
2. **Big picture**: Show how the pieces connect as a short chain.
   Example: `Client -> router -> service -> repository -> database`
3. **File-by-file**: For each file, give its one-line job, the key
   functions or classes, and anything non-obvious (why this approach rather
   than the obvious one).
4. **Trace one real example**: Pick one input with sample data and follow it
   through the code step by step until the output.
5. **Concepts used**: Name the patterns or tools applied (dependency
   injection, Pydantic validation, async, transactions) with 1-2 sentences
   each.
6. **Decisions and trade-offs**: What was chosen, what was rejected, and why.
7. **How to test it**: Exact commands or sample requests with the expected
   result. These must be copy-pasteable.
8. **Edge cases and risks**: What could break, what is not handled yet, and
   known limitations.
9. **How to modify it**: Where to edit for likely future changes.
   Example: "To add a new status, change the enum in `models.py` and the
   transition map in `service.py`."
10. **Check understanding**: Ask 2-3 short questions about the code. Hide
    the answers until the developer asks for them.

### Phase 4: Quality check before sending

Confirm all of the following:
- [ ] Every file mentioned actually exists and was actually changed
- [ ] The traced example matches what the code would really do
- [ ] Test commands are exact and runnable
- [ ] Any shortcut, hack, TODO, or unhandled case is stated openly
- [ ] The length fits the size chosen in Phase 1

### Phase 5: Follow up

End by offering one next step, such as writing tests, a deeper explanation of
one concept, or a refactor. Then wait for the developer's reply.

## Style rules

- Explain the why, not just the what.
- Prefer short code excerpts over pasting whole files.
- Use short headings and short paragraphs so it is easy to scan.
- Use plain language first and jargon second.
- Never hide uncertainty. If something was not tested, say so.

## Output template

```
## Summary
<2-3 sentences>

## Big picture
<flow chain>

## Files
**path/to/file.py**: <one-line job>
- `function_name()`: <what it does and why>

## Example trace
<input> -> <step> -> <step> -> <output>

## How to test
<commands and expected result>

## Edge cases and risks
- <item>

## Check your understanding
1. <question>
2. <question>
```

## Example opening

"I added `POST /claims/{id}/status`. Flow: the router validates input with
`StatusUpdate`, `ClaimService.update_status` checks allowed transitions, then
the repository saves the change and logs it. Here is each piece..."
