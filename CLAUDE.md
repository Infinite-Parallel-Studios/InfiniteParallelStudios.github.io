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
| `ready-for-review` | you opened a PR | Ready for Review |
| `done` | the work is complete and there is no open question — a non-code task finished, a question answered, a reply written | Done |
| `needs-context` | you cannot proceed until **Joshua answers something**; say what you need in the same comment | Needs Context |
| `blocked` | you are waiting on **another ticket or task**; name it | Blocked |

Rules:

- The marker goes on **its own line**. A mention inside a sentence is ignored on purpose.
- `BOARD_REASON` is one line, and it is what a human reads first — write it for them.
- If you opened a PR, the PR wins regardless of the marker: an open PR is a fact, the marker is
  a self-report.
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
links the card to the diff *and* what advances the board.

Labels are additive — removing one does not move the card back.

## Branch convention

```
{area}/{feature-id}/{short-description}
```

Work on a branch, open a PR, let Joshua merge.
<!-- ips-baseline:end -->
