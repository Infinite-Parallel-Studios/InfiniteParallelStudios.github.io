# InfiniteParallelStudios.github.io

<!-- ips-baseline:start — managed by infinite-forge/baseline. Edit there, not here. -->
## NEVER merge pull requests

**Joshua is the merge gate. Open the PR, then stop.**

This is a hard rule with no exceptions for convenience, urgency, or "the change is tiny":

- **Never merge a PR.** Not with `gh pr merge`, not through the API, not by pushing the
  branch's commits onto `main` yourself.
- **Never enable auto-merge**, and never set a PR to merge when checks pass.
- **Never push directly to `main`.** Work goes on a branch and reaches `main` only through a
  PR that Joshua merges.
- **This applies to test and verification runs too.** If confirming something genuinely
  requires a merge — verifying that a merged PR moves its board card to Done, say — **ask
  first and wait for an answer.** A task saying "verify X on merge" describes what to check,
  not permission to merge.

A merge is effectively irreversible and it ships code. Being asked to build something is not
the same as being cleared to release it. When in doubt, open the PR, say exactly what you
would have merged and why, and let Joshua decide.

Everything up to the merge is yours: branch, commit, push the branch, open the PR, write a
description that says what changed and how you verified it, and label the issue. The final
click is not.

## Before you build

Every ticket starts by reading, not writing. The repo almost always does more than the ticket
description implies, and the failure this prevents is a run that reimplements something already
present — a second, half-working copy of a working thing, which is worse than either extending
the original or doing nothing.

On **every** ticket, before the first edit:

**Read the code the ticket touches.** Find the files that already handle this area and read
them. What you build goes on top of the current implementation — its shapes, its helpers, its
conventions — not beside it. If you cannot say what the existing code does, you are not ready
to change it.

**Check what is already in flight.** Another run, or a human, may already be on this:

```bash
gh pr list --state open --search "<keywords>"      # open PRs touching this area
git branch -r --list 'origin/claude/issue-*'       # branches from other runs
gh issue list --state open --search "<keywords>"   # tickets covering the same ground
```

If something in flight touches the same area, build on that branch or say in your PR what you
are coordinating with. Do not open a second PR that changes the same files a different way:
two competing diffs for one problem is a conflict Joshua has to arbitrate, and it is avoidable
by looking first.

**Prefer the smallest change that extends what is there.** A large rewrite is a claim that the
existing design is wrong — make that claim out loud and let Joshua decide, rather than
smuggling it in as part of a feature. When most of the capability already exists, make the
minimal targeted addition and **say so in the PR body**: "this adds X to the existing Y in
`path/to/file`" tells a reviewer where to look far better than a diff that reads as though Y
were built from scratch.

**If the ticket duplicates functionality that already exists, say so instead of building it.**
Name what already covers it and where, and let Joshua decide — reroute the ticket, narrow it,
or confirm the duplicate is wanted anyway. End the run with `BOARD_STATUS: needs-context`,
because that is a question for Joshua rather than a dependency on other work. A redundant
implementation is not a neutral outcome: it is code that has to be maintained, and it competes
with the original for which one people are supposed to call.

## Board status model

Every issue is a card on **IPS Master Board**, and the column is meant to answer one question:
*what is the state of this ticket right now?*

| Column | Means |
|---|---|
| **Todo** | New. Nobody has started it. |
| **In Progress** | `@claude` is actively working this ticket. |
| **Needs Context** | `@claude` could not finish — it needs Joshua to answer something to proceed. |
| **Blocked** | Waiting on **another ticket or task** — a dependency, not a question. |
| **Ready for Review** | Work is done, a PR is open, awaiting merge. |
| **Done** | The PR was merged, **or** a non-code task (research, a question answered, a reply) is fully complete. |

**Done does not require closing the issue.** It is set on the card. A research or respond-only
task can be Done with its issue still open.

## Ending a run: the BOARD_STATUS marker

**Every `@claude` run must end its final comment with a marker on its own line**, so the board
can record the outcome instead of leaving the card stuck in In Progress:

```
BOARD_STATUS: done
BOARD_REASON: one line saying why
```

`BOARD_STATUS` must be exactly one of:

| Value | Use it when | Card goes to |
|---|---|---|
| `ready-for-review` | a PR is open for this issue | Ready for Review, **only if one really is** |
| `done` | the work is complete and there is no open question — a non-code task finished, a question answered, a reply written | Done |
| `needs-context` | you cannot proceed until **Joshua answers something**; say what you need in the same comment | Needs Context |
| `blocked` | you are waiting on **another ticket or task**; name it | Blocked |

Rules:

- The marker goes on **its own line**. A mention inside a sentence is ignored on purpose.
- `BOARD_REASON` is one line, and it is what a human reads first — write it for them.
- If you opened a PR, the PR wins regardless of the marker: an open PR is a fact, the marker is
  a self-report.
- **`ready-for-review` is checked, not believed.** If no open PR closes the issue, the card
  stays In Progress and the run says so. You cannot put a card in Ready for Review by claiming
  to be — that column means a human has something to review, and it has to be true.
- **No marker means the card stays In Progress**, and the run logs that it was missing. Nothing
  guesses an outcome on your behalf — a stalled run is supposed to look stalled.
- `needs-context` and `blocked` are different. A question for Joshua is `needs-context`. Waiting
  on other work is `blocked`.

## Board signals

Issues and pull requests in this repo are cards on the org GitHub Project **IPS Master
Board**. The card moves on its own as work progresses — `.github/workflows/board.yml` forwards
every relevant event to the shared lifecycle workflow in `infinite-forge`:

| Column | Moves there when |
|--------|------------------|
| **Todo** | the issue is opened (the card is added; the project built-in sets Todo) |
| **In Progress** | `@claude` is summoned on the issue, the issue is assigned, or the `in-progress` label is added |
| **Ready for Review** | a PR is opened — its own card *and* every issue it closes |
| **Needs Context** | the `needs-context` label is added |
| **Done** | the PR is merged or closed, or the issue is closed |

You control two of those transitions, and both are labels on the **issue** — never on the PR.

**At the START of every run → add `in-progress` to the issue you are working.** Do this before
you begin, not after. A card sitting in Todo while an agent is mid-run is the single most
misleading state on the board: it makes claimed work look unclaimed and invites a second run at
the same issue. (Being summoned with `@claude` also moves the card, but label anyway — it is
what a human reading the issue sees.)

**When you are blocked → add `needs-context` to the issue and comment explaining what you
need.** The label alone is not enough; a card in Needs Context with no explanation is a dead
end for whoever picks it up. In the comment state what you were trying to do, exactly what is
missing (a credential, a design decision, an API shape, a file that does not exist), and where
possible the options you see, so a human can reply with a choice rather than prose. Then stop
work on that issue rather than guessing.

**Ready for Review is not something you label.** Opening a PR whose body says `Closes #<n>`
(or `Fixes` / `Resolves`) moves that issue's card automatically — as does working on a
`claude/issue-<n>-…` branch. Always write the closing reference into the PR body: it is what
links the card to the diff *and* what advances the board. Adding the label without a PR does
nothing but log a warning; the label is a request for the status, not evidence of it.

**You do not have to open the PR yourself.** Push your `claude/issue-<n>-…` branch and the
pipeline's `open-pr` job opens it for you, with `Closes #<n>` in the body, and verifies it
exists. Opening one yourself is still fine — the job sees it and leaves it alone. What is no
longer possible is finishing with a pushed branch and no PR, which is how work used to get
stranded on a card that claimed to be waiting for review.

**Nothing in the pipeline merges.** It opens the PR; Joshua merges it.

Labels are additive — removing one does not move the card back.

## Branch convention

```
{area}/{feature-id}/{short-description}
```

Work on a branch, open a PR, let Joshua merge.
<!-- ips-baseline:end -->
