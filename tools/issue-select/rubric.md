# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Repo facts: last 5 default-branch commits, their authors, and maintainer first-response sample. Measure dates against the bundle capture date in eval mode. | Pass if at least 2 of the last 5 default-branch commits are human-authored and occurred within the last 90 days, OR the maintainer first-response sample contains a maintainer response within 30 days. Bot-only commits do not count unless the bot merged a human pull request. | required |
| repo-in-use | Repo facts: archived flag, latest release, and last push to any branch. Measure dates against the bundle capture date in eval mode. | Pass if the repository is not archived AND either its latest release is within the last 12 months OR its last push is within the last 90 days. | required |
| scope-fits | Issue title and body, comment thread, issue open date, opener author association, labels, and linked PR history in Repo facts. Count requested outcomes, not files, suspected causes, or implementation steps. | Pass when the issue asks for one concrete end result that could be delivered in one PR. Several files, documentation pages, suspected causes, or implementation steps still count as one outcome when they all serve the same result. A terse issue also passes when it names a concrete bug/change and is maintainer-filed or labeled `good first issue`; missing reproduction details alone do not fail it. Fail if any of these is true: (1) it is explicitly an umbrella, tracking, or megaissue containing independent changes; (2) it is only a usage/support question; (3) implementation requires an unresolved product/design choice or required asset marked TBD; (4) a maintainer explicitly says it requires a broad rewrite or major core-internal redesign; or (5) the issue is more than 12 months old and has at least 2 closed unmerged linked PRs, indicating repeated abandoned implementation attempts. | required |
| unclaimed | Repo facts: this issue's assignees and linked PR states; Comments section for PR mentions and claim comments such as "I'll take this", "can I work on this", or "working on this". | Pass only if there is no current assignee, no open PR attempting to resolve the issue, and no unwithdrawn claim comment from another contributor within the last 14 days. Closed unmerged PRs count as abandoned attempts, not active claims. | required |
| ai-policy-allows | Repo facts: contribution policy, including CONTRIBUTING.md, AI policy files, contributor docs, and PR templates when summarized in the bundle. | Pass if the policy is silent about AI use or allows AI-assisted contributions outright or with conditions such as disclosure, testing, understanding, or human review. Fail only if the repository explicitly bans AI-generated or AI-assisted contributions. | required |

## Verdict rule

Accept only if every required check passes. Preferred checks, if any are added later, may rank accepted issues but never change the verdict. Treat `unclear` on any required check as fail.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
