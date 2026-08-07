# Contributing

_Adapted from `tdk`'s contributing guide (2026-08-04), which was the more evolved of the two existing versions found in `tdk`/`platform` - genericized as the org-wide default rather than written from scratch, since it already reflects real, working practice._

## Abstract

This document outlines the process for contributing to this project and provides guidance for both contributors and reviewers. It is a live document and will be updated as the project and team evolve. If you have any suggestions or feedback, please feel free to open an issue and a pull request.

## Guiding principles

- We are a small team and should be respectful of each other's time.
- We work on an enterprise product and try to be as nimble as possible for that context, keeping the coding process as lightweight as we can and removing unnecessary discussions and manual processes.
- Nimbleness is important, but so is quality. We should strive to maintain a balance between the two.
- There is no "my" code or "your" code. Once committed to the repository, the code is considered the entire team's liability, so we should be careful about what we commit.

## Branch naming

Please follow our branch naming rules:

**Allowed patterns:**
- `feature/{issue-number}-{description}` - new features (requires issue number)
- `fix/{issue-number}-{description}` - bug fixes (requires issue number)
- `chore/{description}` - non-code changes (CI, build, tooling, etc.)
- `renovate/{dependency-name}` - Renovate bot branches
- `experimental/{description}` - experimental or exploratory changes

**Examples:**

✅ `feature/1234-login-ui`
✅ `fix/5678-logout-bug`
✅ `chore/update-ci`
✅ `renovate/dependency-update`
✅ `experimental/new-cache-system`

❌ `feature/login-ui` (missing issue number)
❌ `fix/logout-bug` (missing issue number)
❌ `feat/login` (invalid prefix)
❌ `bugfix/error` (invalid prefix)

## PR titles (transition period)

Two formats are currently accepted while the org converges on one - see the PR-title-lint workflow:

- The existing format: `[#<issue-number>] <short description>` - e.g. `[#123] Fix flaky test`
- The target format: [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) with a Linear ticket ID immediately after the `type(scope):` prefix - e.g. `feat(ui): CLOUD-150 Add Button component`

Once the org picks one, this section (and the lint workflow) should drop the other.

## Guidelines

### General

- All code changes should be submitted via a pull request. There are exceptions (for example, a sudden flaky test appearing on the main branch), but they should be rare and justified separately.
- All pull requests should be reviewed by at least one other team member. The reviewer is assigned automatically according to the information in the `CODEOWNERS` file. If you feel that the reviewer is not the right person to review your code, please feel free to assign someone else.
- There should be an issue for each pull request. Hot fixes and certain small changes can be exceptions, but they should be rare and justified separately.
- All pull requests should have a clear title and description. The title should be concise and descriptive, and the description should provide enough context for the reviewer to understand the changes. The more extensive a code change is, the more detailed the description should be.
- The main branch is protected and does not allow direct pushes. We do not use admin privileges to circumvent branch protection, except in emergencies.
- PR review feedback is provided in the form of comments. Offline discussions can happen, but, aside from really minor changes, all feedback should be reflected in the PR comments.
- Both authors and reviewers should leave the next round of feedback (comments/approval or fixes) within 24 hours, unless agreed otherwise.
- There should be no major design discussions in the PR comments. All the design considerations related to a PR should be discussed beforehand (e.g. via an RFC or design doc). The PR description should then link to that discussion for easier navigation through the design choices.
- Everyone is welcome to leave comments on the PR, but the final decision on the PR approval is always made by the primary reviewer. Secondary reviewers should follow the same rules as the primary reviewer with regard to their comments - for example, it is their responsibility to timely mark their comments as resolved.
- The author is responsible for adding a changelog entry for the implemented functionality, where the project keeps one. The entry should be written with the user's perspective in mind. Purely internal changes that have no user-visible effect (e.g., refactorings, changes in tests) do not need an entry.

### Code quality

- The code style is ensured by automatic linters. So long as the linters pass, purely stylistic issues (formatting, imports, etc.) are considered acceptable and should not be a subject of review comments. Readability, naming, and API or design concerns are still in scope. However, reviewers are free to leave non-obligatory comments about the code style, marking them as `NIT`. Nit comments can be closed by the author without waiting for the reviewer to check that they are addressed.
- PRs should be as focused as possible and should not mix different types of changes. For example, a PR should not contain both a bug fix and a new feature, or a bug fix and a refactoring.
- Changes should include or update tests (unit, integration, or E2E as appropriate), or explicitly explain in the PR description why tests are not needed.
- Large or non-local refactorings should be done in separate PRs. The PR should be focused on a single change; small local cleanups (for example, extracting a helper method) are fine to include.

### Authors: rights and responsibilities

- The code author should make sure the PR template is correctly filled out and reflects the actual state of the PR.
- Before assigning reviewers, the author should make sure that the automatic checks pass against the PR at least once.
- It's the author's responsibility to update the PR branch with the latest changes on a reasonably regular basis.
- After the PR is published and has an assigned reviewer, the author should make their best effort not to commit any changes to the PR branch other than to fix review comments and update the PR branch with the main one. If substantial additional changes are needed, the PR should be converted to a draft until the necessary changes are put onto the PR branch.
- Every comment should be answered by the author, either by pushing a corrective change and a short reply (such as "fixed by <commit>") or replying more extensively with a reason why the comment will not be addressed. Comments from bots or automated tools can be resolved without a reply unless the disagreement is non-obvious.
- Once all the current review comments are addressed, the author should re-request a review from the reviewer.
- Comments concerning alternative ways to implement the same functionality are interpreted in favour of the author. Unless there are bugs in the current implementation or other significant reasons to make modifications, the author is free to stick to their original approach.
- After the PR is merged, the author should make sure that the corresponding build on the default branch passes.
- If the reviewer is not providing timely feedback, the author should reach out to the reviewer and, if necessary, assign a new reviewer.

### Reviewers: rights and responsibilities

- When comments are answered by the author, the reviewer should mark them as resolved.
- Comments should be published in batches (`Start a review` → leave comments → `Review changes` → `Approve / Comment / Request changes`), rather than one comment at a time.
- Once all comments are addressed, the reviewer should approve the PR explicitly.
- The reviewer can leave a provisional approval, noting in a comment that the author should address remaining points before merging - the author doesn't then need to wait for the reviewer to re-check.
- Comments regarding code comprehensibility are interpreted in favour of the reviewer. If the reviewer doesn't understand the code, it's the author's responsibility to make the code clearer.
- If the reviewer is unable to finish the review within a reasonable time frame, or finds they cannot review the PR for any reason, they should unassign themselves and let the author know why.

## Stale PRs

To keep the PR queue manageable, stale PRs are tracked automatically:

- A PR with no activity for **30 days** is automatically labeled `stale`.
- Once labeled stale, the PR enters a **7-day grace period**.
- If no activity occurs during the grace period, the PR is **automatically closed**.
- Any PR activity - a new commit, a comment, or a review - resets the inactivity timer and removes the `stale` label.

If a PR is closed due to inactivity and the work is still relevant, it can be reopened at any time.

## Before opening a PR

- Run `pre-commit run --all-files` locally
- Make sure CI checks pass

## Review

- At least one approval is required before merging
- Address all review comments, or explain why not, before merging
