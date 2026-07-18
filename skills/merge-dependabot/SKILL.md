---
name: merge-dependabot
description: Assess and safely merge Dependabot PRs in the current repo — merge bumps that green CI with a real test suite actually verifies, flag the rest with test or manual-verification guidance. Use when I ask to merge/triage Dependabot PRs, clear dependency bumps, or handle bot dependency updates in this repo.
---

Assess the current repo's open Dependabot PRs, merge the ones a real test suite actually verifies, and flag the rest with a way to make them safe.

Scope is the current repo only. `prioritize` finds *which* repos have bumps waiting; this handles *one* repo's bumps in depth — run it after you've cd'd into the target.

## Gather

Run these once for the repo (batch the independent ones):

- Open Dependabot PRs: `gh pr list --author 'app/dependabot' --state open --json number,title,body,headRefName,mergeable,isDraft,statusCheckRollup`. No results → say so and stop.
- Allowed merge method: `gh repo view --json squashMergeAllowed,mergeCommitAllowed,rebaseMergeAllowed`. Prefer squash → merge → rebase.
- **Does CI run a real test suite?** Read `.github/workflows/*.{yml,yaml}` and look for a genuine test-runner step (`npm test`, `pytest`, `jest`, `vitest`, `go test`, `cargo test`, `dotnet test`, `mvn test`, …) — *not* lint / typecheck / build / format alone. This is the load-bearing check: if no workflow runs tests, green CI proves nothing and **every** bump is flagged as unverified. Decide this once; it applies to all PRs.

## Classify

Per PR, in order — first match wins:

1. **CI not green** — any check FAILURE/ERROR/CANCELLED → `✗ red CI`. Name the failing check and a one-line excerpt (`gh run view <run-id> --log-failed`). A broken bump needs code changes, not tests — out of scope here; flag and move on.
2. **Checks still pending** → `⏳ pending` — skip this run, no verdict yet.
3. **No real test suite** (from Gather) → `⚠ unverified` — green CI is meaningless without tests.
4. **Not mergeable** (`mergeable == "CONFLICTING"`) → `⚠ needs rebase` — note `@dependabot rebase`; do not merge.
5. **Major bump** → `⚠ major` — breaking by design; tests rarely cover intentional breakage. Treat a PR as major if any bumped dependency crosses a major version, **or** crosses a pre-1.0 minor (`0.27 → 0.28`, `0.x → 1.0`) since pre-1.0 minors can break. For grouped PRs the highest-risk member decides (worst-member wins) — parse each `Updates \`x\` from A to B` line in the body, not just the title.
6. Otherwise (**green + real tests + patch/minor + mergeable**) → `✓ safe`.

## Present & merge

List safe PRs, then flagged PRs grouped by reason. Ask **once** to merge the safe batch. On confirmation, merge each with the repo's method and delete the branch: `gh pr merge <n> --squash --delete-branch` (swap `--squash` for `--merge`/`--rebase` per Gather). Never touch a flagged PR.

For each **flagged** PR, make it actionable — state the reason, then:

- **major / unverified:** grep the repo for the package's import/use sites (`rg <package>`), link the changelog/release notes from the PR body, and give a targeted manual-test suggestion for those sites plus what a covering test would assert. Do **not** write test files — this is guidance.
- **red CI:** the failing check + excerpt is enough; the fix is code, which you'd start deliberately.
- **needs rebase / pending:** the one-line note is enough.

Keep it dense — one verdict block per PR, no padding. Example:

```
✓ safe (3) — merge these?
  jest 29.6→29.7 · lodash 4.17.20→4.17.21 · npm group (2 minor)
⚠ major axios 0.27→1.0 — breaking by design
  used in: src/api/client.ts, src/auth.ts · changelog: <link>
  manual: exercise login + a GET; assert error shape (axios reworked errors)
  test gap: no test hits src/api/client.ts
✗ typescript 5.2→5.3 — CI red: `tsc`, 2 type errors in src/db.ts (excerpt) — needs code changes
```

Stop after merging the safe batch and reporting the flagged ones. Don't start fixing broken bumps or writing tests unless I ask.

---

This skill is not yet battle-tested: if any instruction above was ambiguous, wrong, or needed a workaround, say so briefly at the end of the run.
