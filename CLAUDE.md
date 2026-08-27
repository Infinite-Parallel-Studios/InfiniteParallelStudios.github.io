# InfiniteParallelStudios.github.io

<!-- ips-baseline:start — managed by infinite-forge/baseline. Edit there, not here. -->
## Merging pull requests

**You may merge your own PR once every required check is green. Everything still goes through a
PR.**

- **You may merge a PR you opened**, once all required checks have passed — not before, and not
  while one is still running.
- **You may enable auto-merge** on a PR you opened.
- **Never push directly to `main`.** Work goes on a branch and reaches `main` only through a PR.
- **Never merge a PR that touches `.github/workflows/**`, `baseline/**`, or
  `.github/scripts/**`.** Those are the pipeline itself — the thing that would be doing the
  merging. A pipeline change that merges itself has no reviewer. Open it, say what it does, and
  leave it for Joshua.
- **Never merge a PR that is not yours.** Yours means one this run opened.

This is enforced rather than only asked for: `claude.yml`'s `self-merge` job refuses on both
counts — by path class, and on any check that is pending, failed, or absent. **Zero check-runs
is a refusal too**, because "nothing failed" and "nothing ran" look identical from the outside
(infinite-forge#129). A check reporting `skipped` refuses as well, unless it is one of the named
few allowed to — today only `mark-not-ready` — so a check that skipped *because something went
wrong* can never read as approval. The merge is pinned to the exact commit the checks were read from, so
anything landing on the branch in between is rejected rather than merged unchecked.

**Enforcement is partial, and you should know which side of it you are on.** As of 2026-08-19 an
org ruleset is **Active on `infinite-media` only**, where `verify` is a required status check and
a failing `verify` genuinely blocks the merge. **Every other repo has no ruleset and no branch
protection on `main`** — a token with `contents: write` can push straight to it.

So in eight of nine repos the `self-merge` guard, not the platform, is what holds. Do not route
around it, and do not read a green check on a pipeline change as permission — the guard refuses
those by path regardless of how green they are. See infinite-cortex#342 for the rollout and
infinite-cortex#327 for what remains.

Everything up to and including the merge is yours for ordinary work: branch, commit, push, open
the PR, write a description saying what changed and how you verified it, label the issue, and
land it when the checks are green. The pipeline is not ordinary work.

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

## Accounting for the checklist: the `BOARD_ITEM` marker

`BOARD_STATUS` says how the run ended. `BOARD_ITEM` says what happened to each thing the
ticket asked for. They are different questions, and the second one is the one that caught
infinite-cortex#356 — a pull request that merged and closed a ticket it covered one eighth
of, because the report was prose and nothing compared what was asked for against what was
done.

**If the ticket body has checkbox items, the final comment must carry one line per item:**

```
- BOARD_ITEM: 1 | addressed | the extractor now reads the folded scalar (permissions-surface.sh:61)
- BOARD_ITEM: 2 | not-addressed | needs the token widened first; out of scope for this PR
- BOARD_ITEM: 3 | cannot-address | the API this asks for was removed in v4; see the comment below
```

`BOARD_ITEM: <n> | <verdict> | <evidence>`

- **`<n>`** is the item's position in the ticket body, counting **every** `- [ ]` or `- [x]`
  line in order, under any heading. Not just the ones under `## Acceptance`.
- **`<verdict>`** is exactly one of:

| Verdict | Use it when |
|---|---|
| `addressed` | this run did the thing the item asks for |
| `not-addressed` | this run did not do it — say why in the evidence field |
| `cannot-address` | it cannot be done as written; the item is wrong, obsolete, or contradicts something |

- **`<evidence>`** is one line a human can check. A file and line, a test name, or the reason.

Rules:

- **Every item, exactly once.** A missing item, a repeated item, or a verdict for an item the
  ticket does not have is a refusal — not a smaller pass.
- **`not-addressed` is an honest outcome, not a failure.** A run that gives an honest verdict
  for every item has accounted for the ticket, *even if that verdict is `not-addressed` on all
  of them*. Accounting is a claim about the report, not about how much got built. Deciding
  whether the amount of work is acceptable is a human's job, and it needs the list to be
  complete and true before it can be done at all.
- **Do not invent a verdict to look finished.** Saying `addressed` for something you did not do
  is worse than saying `not-addressed`, because it is the one thing here nobody can check
  cheaply.
- **Only these three words.** Anything else — `done`, `partial`, `already-satisfied` — is
  refused as unrecognised, deliberately: a vocabulary that grows on demand stops meaning
  anything.
- **A leading `-` or `*` is fine**, with or without a space, and indented is fine too. Write the
  list the way it reads best; the parser accepts both forms.
- **Markers inside a fenced code block are ignored**, bulleted or not, so quoting this section
  back, or showing an example, does not report anything.
- **A ticket with no checkbox items needs none of this.** There is nothing to account for, and
  the run is not held for the absence.

Until the org variable `SCOPE_ACCOUNTING_ENFORCE` is set to `true`, an unaccounted run is
reported beside a card that still moves. When it is set, the card is held at In Progress
instead of reaching Ready for Review.

## Task dependencies: `Blocked by #N`

Some tickets cannot be started until another one is finished. Say so in the issue **body**, on
its own line:

```
Blocked by #42
```

More than one is fine — separate lines, or one line:

```
Blocked by #42
Blocked by #43, #44 and #45
```

That is the whole vocabulary. It is read by the pipeline, not just by people:

- While **any** named issue is still open, the ticket carries the `blocked` label and its card
  sits in **Blocked**.
- **`@claude` will not start it.** The dispatcher checks before the agent runs and refuses,
  with a comment saying which issues it is waiting on. This is not advisory — the run does not
  happen.
- When the **last** blocker closes, the label comes off by itself and **`@claude` is summoned
  automatically** — the ticket starts building with nobody typing anything, and its card goes
  straight to **In Progress**. Closing one of three changes nothing; every blocker is
  re-checked each time.

The auto-summon happens **once per ticket, ever**, and only for a ticket that was genuinely
sitting in Blocked. If you would rather it not start on its own, take the `blocked` label off
by hand before the last blocker closes — that releases the card to Todo and leaves it there.

Rules worth knowing before you write one:

- **Same repo only.** `Blocked by owner/repo#12` is not supported; it is ignored and the run
  warns rather than quietly reading it as `#12` in this repo.
- **Only the blockers you name.** There is no transitive walk: if A is blocked by B and B is
  blocked by C, closing B releases A even though C is open. Name C too if you mean it.
- **A cycle is a real deadlock.** A blocked by B and B blocked by A leaves both stuck, visibly,
  until a human removes a line. Nothing spins.
- **Examples in fenced code blocks do not count**, which is why the ones above are safe to copy.
- **`Blocked by #N` in a comment does nothing.** It has to be in the issue body, because the
  body is the thing that gets re-read.

To override, remove the `blocked` label — that releases the card immediately.

**Filing a ticket that depends on another? Write the line.** Nothing infers it, and a
dependency you only mentioned in prose will not stop the agent from building the thing too
early.

## Tickets the agent must not build: `human-task`

Some tickets need a person: installing something on the homelab box, running an EAS build,
plugging in a phone, clicking through a console. Label those **`human-task`**.

The label is enforced, not advisory:

- **`@claude` will not start**, even if summoned by name. The gate refuses first, before it
  reads anything else, and comments saying why.
- **Auto-dispatch will never pick it up.** Every other refusal in that guard means "not ready
  yet"; this one means "never", so it outranks all of them.

Because it is enforced, a human task can safely carry `Blocked by #N` like anything else — the
dependency shows on the board and the ticket still will not be built. Before the label existed
the only defence was leaving `@claude` out of the body, which failed the first time someone
wrote a sentence *about* not summoning the agent.

Removing the label is how you overrule it.

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
