# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

**Verdict output**

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
  "checks": [
    {
      "name": "maintainer-alive",
      "grade": "pass",
      "evidence": "Last 5 default-branch commits (2026-08-24 through 2026-09-16) are all human-authored by Aburke225, within 90 days of capture date 2026-09-20."
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "Not archived; last push 2026-09-16, 4 days before today, well within 90 days."
    },
    {
      "name": "scope-fits",
      "grade": "pass",
      "evidence": "Issue asks for one concrete outcome — make verify_password fail closed on UnknownHashError and drop the covering test's xfail marker — labeled good first issue/tier-1, estimated 1–2 hours."
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "No assignees, no comments, and no open or mentioned PRs found referencing issue #72."
    },
    {
      "name": "ai-policy-allows",
      "grade": "pass",
      "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI restriction; repo history itself contains AI-assisted commits, consistent with silence/allowance."
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

My first attempted full run failed because Claude Code's OAuth session had expired, so all 20 issues errored and no score was produced. After logging in again, my first scored full run was 17/20.

I then used partial `--only` runs to revise the `scope-fits` check. One targeted run on issue-15, issue-19, and issue-20 scored 2/3. After another revision, issue-19 alone scored 1/1. My next full saved run scored 16/20, which showed the check was still inconsistent across the full set.

I revised `scope-fits` again and re-ran issue-01, issue-04, issue-15, issue-19, and issue-20, scoring 5/5. My final complete run scored 20/20 and passed every category.

**Issue analysis**

I analyzed `issue-19`. In an earlier run, my rubric rejected it while the gold label was `accept`. The rejection came from my `scope-fits` check because I interpreted the issue's multiple possible causes and implementation suggestions as evidence that the task was too broad.

After reviewing the issue more carefully, I realized that all of those possible causes were still aimed at one concrete outcome: fixing the UI freeze when selecting large subgraphs. I updated the check so it counts requested outcomes rather than the number of suspected causes, implementation steps, or files involved. With the final version of the rubric, `issue-19` was accepted, matching the gold label.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]


> | scope-fits | Issue title and body, comment thread, issue open date, opener author association, labels, and linked PR history in Repo facts. Count requested outcomes, not files, suspected causes, or implementation steps. | Pass when the issue asks for one concrete end result that could be delivered in one PR. Several files, documentation pages, suspected causes, or implementation steps still count as one outcome when they all serve the same result. A terse issue also passes when it names a concrete bug/change and is maintainer-filed or labeled `good first issue`; missing reproduction details alone do not fail it. Fail if any of these is true: (1) it is explicitly an umbrella, tracking, or megaissue containing independent changes; (2) it is only a usage/support question; (3) implementation requires an unresolved product/design choice or required asset marked TBD; (4) a maintainer explicitly says it requires a broad rewrite or major core-internal redesign; or (5) the issue is more than 12 months old and has at least 2 closed unmerged linked PRs, indicating repeated abandoned implementation attempts. | required |

I wrote the check this way because my earlier version was too subjective about what counted as “too broad.” I found that an issue can mention several files, causes, or implementation steps and still be one focused contribution if they all lead to the same end result. The final wording makes the grader count outcomes instead of complexity signals that can be misleading. It also gives explicit fail conditions for umbrella issues, unresolved design decisions, major rewrites, and older issues with repeated abandoned PR attempts, so the decision is based on observable evidence instead of whether the issue simply feels difficult.

**Trade-offs**

The `scope-fits` check gives up some flexibility in exchange for consistency. For example, an issue that is more than 12 months old with two closed unmerged PRs will fail even if the problem may now be easier because the codebase has changed. On the other hand, a newer issue may still be difficult even if it does not trigger any of those warning signs. I accepted that trade-off because the check gives the grader specific evidence and thresholds to apply instead of relying on a subjective judgment about whether an issue feels too hard.
---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
   Ans: Issue #72 fits my interests because it is related to backend development and security, especially how password verification should fail safely instead of raising an exception. It also fits the time available because the issue is small, points to the relevant implementation and test files, and is estimated at 1–2 hours.

2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   Ans: My rubric correctly identified that the repository is active, the issue is unclaimed, the scope is bounded, and the repository does not prohibit AI-assisted contributions. Outside of the rubric, I also considered whether the issue matched the kind of work I actually want to do. I preferred #72 because it involves Python, backend logic, testing, and security behavior, which are areas I am comfortable with and interested in.

3. The anticipated difficulty in claiming it.]
   Ans: I expect claiming the issue to be straightforward because it is still open and currently has no assignee. The Path Review house rules also say that classmates' claim activity does not block the issue, so I do not expect the claiming step in Unit 2 to be difficult.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
