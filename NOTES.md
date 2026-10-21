# Code Review Practice Notes

These notes are for practicing the pull-request review flow in a scratch
repository. The goal is to add a file, open a PR, and then review it the
way a real reviewer would, including leaving line-level comments on the diff.

## Review checklist
- Read the PR description first for context.
- Look at the diff before pulling the code locally.
- Leave line-level comments anchored to specific changes.
- Check that the PR is small and focused enough to review in one pass.

## A deliberate typo for practice
This line intentionally misspells the word "receive" as "recieve" so the
practice reviewer has something concrete to find and comment on.

## Notes to self
- Comment-only review: feedback without blocking the merge.
- Pending review: comments stay invisible until the review is submitted.
- Always re-read the review after submitting to verify it landed.