# Git Commit Message

Generate a concise, natural, and accurate Git commit message from the current Git changes.
This skill ONLY generates the commit message.
It MUST NOT create, amend, or execute any Git commit.

## Scope

This skill is responsible only for:
- Inspecting the current Git changes.
- Understanding the intent of the changes.
- Reading the repository's Commitlint configuration.
- Generating a valid Conventional Commit message.
- Returning the commit message.

This skill MUST NOT:
- Run `git commit`.
- Run `git commit --amend`.
- Create or modify commits.
- Stage files with `git add`.
- Unstage files with `git reset`.
- Push commits.
- Create branches.
- Modify Git history.
- Modify source files.
- Modify configuration files.
- Automatically apply or execute the generated message.

The user is responsible for deciding whether and when to commit.

## Commitlint Configuration

The repository's Commitlint configuration is the source of truth.
Before generating a message, inspect available configuration such as:
- `commitlint.config.*`
- `.commitlintrc*`
- `package.json`
- Other Commitlint configuration referenced by the repository

If the repository extends `@commitlint/config-conventional`, follow its Conventional Commit rules.
If the repository defines additional rules or commit types, follow those rules.
For example, this repository allows the additional type: `merge` because its Commitlint configuration extends the conventional types with `merge`.

## Workflow

1. Inspect the current Git diff.
2. Prefer staged changes when staged changes are available.
3. If there are no staged changes, inspect the working-tree diff.
4. Inspect the repository's Commitlint configuration.
5. Understand the actual intent of the changes.
6. Determine the appropriate commit type.
7. Determine a meaningful scope when appropriate.
8. Generate a concise and natural commit description.
9. Validate the message against the repository's Commitlint rules.
10. Return ONLY the commit message.

Never execute a Git commit as part of this workflow.

## Commit Format

Use: `type(scope): description`
Scope is optional.

**Examples:**
- `feat(auth): add Google OAuth login`
- `fix(api): handle expired access tokens`
- `refactor(user): simplify profile validation`
- `docs(readme): clarify local development setup`
- `test(auth): add login failure cases`
- `chore(deps): update dependencies`

For merge commits:
- `merge: merge authentication branch`

## Type Selection

Choose the type based on the actual change:
- `feat` — adds a new user-facing capability
- `fix` — fixes incorrect or broken behavior
- `build` — changes build system or build dependencies
- `chore` — maintenance work
- `ci` — changes CI/CD configuration
- `docs` — documentation changes
- `perf` — performance improvements
- `refactor` — changes internal structure without changing intended behavior
- `revert` — reverts a previous commit
- `style` — formatting or style changes without changing behavior
- `test` — adds or modifies tests
- `merge` — represents a Git merge operation when applicable

Only use commit types allowed by the repository's Commitlint configuration.

## Description Rules

The description MUST:
- Be concise.
- Be natural.
- Clearly describe what changed.
- Make it obvious whether something was added, fixed, changed, removed, or refactored.
- Start with a lowercase letter.
- Avoid unnecessary implementation details.
- Avoid vague wording.
- Avoid ending with a period.

**Avoid:**
- `feat(auth): update authentication code`
- `fix(api): fix user issue`
- `chore: update stuff`

**Prefer:**
- `feat(auth): add password reset flow`
- `fix(api): return 404 when user is not found`
- `refactor(cart): extract price calculation`
- `chore(deps): update React dependencies`

## Accuracy

The message MUST be based on the actual diff.
Do not:
- Infer the change from filenames alone.
- Invent requirements or motivations.
- Claim a feature was added when the change is only a refactor.
- Claim a bug was fixed without evidence.
- Exaggerate the impact of a change.
- List every changed file.
- Describe implementation details when the resulting behavior is clearer.

Describe the primary intent of the changes.

## Scope

Use a scope when it provides useful context.
**Examples:** `auth`, `api`, `user`, `cart`, `database`, `ui`, `config`, `deps`

Do not invent a scope when the affected area is unclear.

## Breaking Changes

For breaking changes, use: `type!: description` or `type(scope)!: description`

**Example:**
`feat(api)!: change authentication response format`

Only use `!` when the change actually breaks existing consumers, APIs, behavior, or configuration.

## Unrelated Changes

If the changes contain unrelated concerns that cannot be accurately represented by a single commit message, ask the user to split the changes.
Do not fabricate a misleading message just to produce an answer.

## Output Rules

The output MUST contain ONLY the commit message.
Do NOT output:
- Markdown
- Code fences
- Comments
- Explanations
- Analysis
- Alternatives
- `Commit:`
- `Message:`
- `git commit`
- Any command
- Trailing punctuation

**Example valid output:**
`feat(auth): add password reset flow`

**Example invalid output:**
`Commit: feat(auth): add password reset flow`

**Example invalid output:**
`git commit -m "feat(auth): add password reset flow"`

The generated message is informational only. The user must explicitly perform the commit themselves.
