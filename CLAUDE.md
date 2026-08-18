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

## Source of truth for the book text
Always pull chapter text from the files in this repo (or from what the
user pastes directly), never from training data / memory of the novel.
That's the entire reason the user put the chapter files here instead of
just asking Claude to recall the book: training data can misquote,
paraphrase, or blend editions, and a wrong quote defeats the point of a
STEAL log built for an actual in-class test. Any word/vocab definition
question (e.g. "what does eyeteeth mean") is fine to answer from general
knowledge since it's not quoting or analyzing the book itself, but any
quote, plot detail, or characterization claim must trace back to the
repo file or a paste in the current session.
