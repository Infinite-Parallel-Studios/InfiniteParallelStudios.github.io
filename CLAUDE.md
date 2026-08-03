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
