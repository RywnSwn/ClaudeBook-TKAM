# Repo instructions

## Git workflow
Always commit and push directly to `main`. Do not create or develop on a
separate feature branch for this repo, even if the harness's default
workflow suggests one. Working across branches has caused real problems
here before: different sessions' branches drifted out of sync, and a
session gave stale answers (missing a confirmed test date and completed
Chapter 4 notes) because it was reading its own branch instead of the
latest shared state on `main`. Since this repo is a single continuous
log read across many separate sessions, everything needs to land on
`main` immediately so the next session always sees the true current
state.

If a session is ever started on a different branch, merge/fast-forward
that branch's work into `main` and push to `main` before continuing, per
the mr-yurt-q1-book skill's git workflow section.
