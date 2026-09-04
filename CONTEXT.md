# spf13/cobra context
> refreshed 2026-09-04 | upstream default: main @ adbc881

## Identity & policies
- upstream: spf13/cobra, default branch `main`, primary language Go, English-first (yes — all docs/comments English)
- CLA/DCO: CLA required (CONTRIBUTING.md: "You will need to sign the CLA"); no DCO bot
- AI-assisted PR policy: unstated (no AI policy line found in CONTRIBUTING/.github)
- signed commits required: no (no branch protection `required_signatures`)
- PR template: none (`.github/` has only dependabot.yml, labeler.yml, workflows/) — use fallback 3-section body
- external tracker: github

## Conventions (verified from merged PRs)
- branch naming: mixed — `fix/...`, `feat/...`, `marck/...`, `main`, `patch-1`, `jfaer/opt`, `helpctx`. No strict convention; fall back to `fix/<kebab-description>`.
- commit style: Conventional Commits (`fix:`, `feat:`, `perf:`, `chore:`, `refactor:`)
- test command: `go test ./...` or `make test`
- lint/format: `make all` (gofmt + golangci-lint)
- CI: GitHub Actions (test, lint, codeql, dependency-review, pr-size-labeler)
- outside PRs get merged: yes — recent external merges (SudhanshuMatrix, takanuva15, ArturAronov, veeceey, dims, JeffFaer, htoyoda18, ssam18, anishathalye, n9v9, scop). Median time-to-merge varies; some fast (days), some slow.

## Maintainer picture
- active maintainers: marckhouzam (most active, reviews + merges), jpmcb, spf13, johnSchnake
- marckhouzam actively reviews completions/flag issues; jpmcb handles deps/CI
- in-flight maintainer PRs: marckhouzam `marck/fixLinter`, jpmcb dep bumps — avoid overlapping

## Issue-area health
- completions (bash/fish/zsh/powershell): high activity, many open PRs — contested
- flag parsing: active (required flags, path padding, suggestions) — many open PRs
- docs (site/): low activity; site content mostly lives in spf13/cobra.dev, NOT this repo
- man page generation (doc/): low activity, no open PRs — good area for a pick

## Gap ledger (dedupe — READ FIRST, never re-pick)
- `2026-09-04` self-found gap: man page generation strips angle brackets from UseLine (issue #2330) — status: in-progress (fix + test)

## Mined gaps (discovered, not yet attempted)
- `2026-09-04` docs/manpage: `doc/man_docs.go` manPreamble writes `cmd.UseLine()` raw into markdown fed to md2man; angle brackets like `[<remote>:]<instance>` are interpreted as HTML tags and stripped (repro: `GenMan` on a command with `Use: "incus [<remote>:]<instance>"` → SYNOPSIS shows `incus [:]`). Expected: `incus [<remote>:]<instance>`. Fix: escape `<`/`>` with backslash before writing. Dedupe: issue #2330 open, no open/closed/merged PR. — status: proposed
- `2026-09-04` self-found gap: man page generation strips angle brackets from UseLine (issue #2330) — outcome: pr-opened (https://github.com/olitreadwell/cobra/pull/2). Lesson: verified repro with GenMan, escaped `<`/`>` with backslash, added regression test. Fork CI not connected (0 workflow runs) — locally verified go test/vet/gofmt.
