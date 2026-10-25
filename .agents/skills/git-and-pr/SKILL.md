---
name: git-and-pr
description: Defines the team's Git conventions: commit message format, branch naming, and pull request template. Use this skill whenever the user is committing code, creating or naming a branch, writing a commit message, opening or describing a pull request, or asking for a PR summary or changelog. Make sure to use it any time code changes are about to be saved to Git, even if the user does not mention commit or PR conventions explicitly.
---

# Git and PR Conventions

Keep history clean and reviews fast. Follow these rules every time you create
a branch, write a commit, or draft a pull request.

## Workflow

Follow these steps in order.

### Step 1: Create a branch

Name it `type/short-description` in lowercase with hyphens.

| Type | Use for | Example |
|---|---|---|
| `feature` | New functionality | `feature/claim-status-api` |
| `fix` | Bug fixes | `fix/login-token-expiry` |
| `refactor` | Restructuring without behavior change | `refactor/policy-service` |
| `docs` | Documentation only | `docs/api-readme` |
| `test` | Adding or fixing tests | `test/claims-endpoints` |
| `chore` | Tooling, dependencies, config | `chore/upgrade-fastapi` |

Rules:
- Max 5 words in the description.
- No spaces, uppercase letters, or personal names.
- If there is a ticket, put it first: `feature/INS-142-claim-status-api`.
- Never commit directly to `main`.

### Step 2: Make small, focused commits

One logical change per commit. If the summary needs the word "and", split it
into two commits. Before committing, check the staged changes with
`git diff --staged` and make sure no secrets, `.env` files, or debug code are
included.

### Step 3: Write the commit message

Format:

```
type(scope): short summary

Optional body explaining what and why (not how).

Optional footer: Closes #123
```

Rules:
- **Types**: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`.
- **Scope**: the area changed, such as `claims`, `auth`, `policy`, `db`.
- **Summary**: imperative mood ("add", not "added"), lowercase, no period,
  max 50 characters.
- **Body**: wrap at 72 characters. Explain why the change was needed.
- Breaking changes: add `!` after the scope, for example `feat(api)!: ...`,
  and explain in the body.

Good examples:
```
feat(claims): add claim status update endpoint
fix(auth): refresh expired tokens before retry
refactor(policy): extract premium calculation into service
test(claims): cover invalid status transitions
```

Bad examples (and why):
```
fixed stuff                -> no type, no meaning
Update code.               -> vague, capitalized, has a period
feat: added many things and fixed bugs   -> two changes, past tense
```

### Step 4: Prepare the pull request

Before opening the PR, confirm:
- [ ] Branch is up to date with `main` (rebase or merge)
- [ ] Tests pass locally
- [ ] No leftover debug code, commented-out blocks, or secrets
- [ ] The diff is small enough to review (aim for under 400 changed lines;
      split larger work)

### Step 5: Write the PR title and description

**Title**: same format as a commit, for example
`feat(claims): add claim status update endpoint`.

**Description template** (use exactly these headings):

```markdown
## What changed
<2-4 bullets describing the change>

## Why
<The problem or requirement this addresses. Link the ticket.>

## How to test
1. <exact step or command>
2. <expected result>

## Screenshots / sample output
<API response, logs, or UI screenshot if relevant. Remove if not needed.>

## Checklist
- [ ] Tests added or updated
- [ ] Docs updated if behavior changed
- [ ] No secrets or personal data included
- [ ] Reviewed my own diff

## Notes for reviewers
<Risky areas, trade-offs, or follow-up work. Remove if none.>
```

### Step 6: After review

- Address each comment with a commit or a reply explaining your reasoning.
- Do not force-push over a reviewer's work without telling them.
- Prefer squash merge so `main` keeps one clean commit per PR, using the PR
  title as the final commit message.
- Delete the branch after merging.

## Rules the AI must follow

- Always show the proposed branch name, commit message, or PR text for the
  developer to approve before running any git command that changes history.
- Never run `git push --force`, `git reset --hard`, or delete branches
  without explicit permission.
- Never commit secrets, API keys, `.env` files, or real customer data. If
  found in the diff, stop and warn the developer.
- If the changes mix several unrelated concerns, suggest splitting them into
  separate commits or PRs.
- Base the PR description on the actual diff, not on assumptions.

## Before every commit (required)

1. Run `git status` and `git diff --staged`.
2. Show the developer, in this exact format:
   - Branch: <name>
   - Files to be committed: <list>
   - Commit message: <message>
3. Ask: "Approve this commit? (yes / edit)"
4. Run `git commit` only after the developer replies yes.
5. After committing, run `git log -1` and show the result.