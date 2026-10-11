---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Grade exactly one pull request package and answer one question:
is this ready to submit?

A PR package contains a proposed title and description, the
committed changes and diff, test evidence, and the implementation
plan, including documented deviations. Evaluate these artifacts
against the issue, the plan, and the repository's stated standards.

Do not implement the fix, invent missing evidence, or judge
readiness from confidence or presentation alone. Use rubric.md,
procedure.md, and references/evidence-guide.md to make the decision.

## Inputs and modes

Determine whether the request is live mode or eval mode.

**Live mode**

Read the following:
- The issue URL and its actual issue thread.
- The student's plan.md, including the Deviations section.
- The committed branch diff relative to main, produced with
  `git diff main...HEAD` from the fork's working copy.
- The proposed PR title and description in pr_draft.md.
- Actual test output and reproduction results in test_evidence.md.
- The repository's .github/PULL_REQUEST_TEMPLATE.md.
- The repository's docs/CONTRIBUTING.md and relevant policies.

Treat the full committed branch diff as the proposed change.
Do not silently include uncommitted edits as completed PR work.

Compare the implementation to the plan, the test output to the
test plan, and the PR description to the actual diff. Use the
issue thread and repository rules to verify scope and standards.

For a house-chain submission, use the supplied house plan,
house reproduction pack, and working branch instead of the
student's original issue artifacts. Apply the same checks.

**Eval mode**

Read only the provided practice package from eval/packages/.
Its issue context, plan, diff, test evidence, PR text, and
repository facts are the complete evidence set.

Do not fetch GitHub content, read local repository files outside
the bundle, or use outside knowledge to fill missing facts.
Grade every rubric check and apply the full verdict rule.

## The scope seam (live mode only)

Before reading any other live-mode evidence, read scope.md.

Confirm that the target repository matches its Repo line.
Follow the Path Review house rules stated there.

If Repo still contains the placeholder, stop without grading
and tell the student to replace it with the correct repository.
If the PR targets another repository, refuse to grade.
Never guess or silently change the allowed scope.

Ignore scope.md completely in eval mode.

## The voice seam (live mode only)

Read voice-guide.md and review the proposed PR title and
description against its writing and communication rules.

Report broken rules with specific examples and suggested
improvements in the readable summary.

A voice-guide violation alone does not change the final verdict
unless an explicit rubric check requires that rule.

Ignore voice-guide.md completely in eval mode.

## Component reads

Read rubric.md to determine exactly which checks exist,
what evidence each check requires, the passing conditions,
their required or preferred weights, and the verdict rule.

Read references/evidence-guide.md to locate each evidence
family in both live and evaluation packages.

Execute procedure.md exactly as written. It controls the
read order, evidence gathering, check execution, and verdict
assembly. Do not silently invent missing procedure steps.
Report any procedure gaps in the readable summary.

If rubric.md has no substantive checks or procedure.md has no
substantive operating steps, refuse to grade. Do not manufacture
checks or a procedure at runtime.

Do not confuse missing PR evidence with an empty skill: missing
evidence is graded according to the rubric, not automatically
treated as a reason to abandon the evaluation.

## Verdict and output

Use only two final verdicts:
- accept: the package satisfies the rubric and is ready to submit.
- reject: the package fails the rubric and must be held.

Grade each rubric check as pass, fail, or unclear. Include a
specific evidence line for each check. Follow rubric.md's
verdict rule without changing weights or inventing exceptions.

Before the JSON, provide a short readable per-check summary.
Include relevant live-mode voice-guide violations and procedure
gaps where applicable.

End every completed grading response with the following exact
JSON structure. Replace the placeholders with actual results.
Do not add, remove, or reorder fields. Nothing may follow it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: name the actual fact, quote, test result, or
  changed file supporting every grade. Never write "looks fine"
  as a substitute for evidence.
- Grade the actual PR, not its polish. A concise honest PR can
  pass; a detailed PR with unacknowledged drift must not.
- Compare claims against source evidence. A claimed passing test
  without corresponding observable output is not proof.
- Distinguish honestly disclosed limitations from hidden gaps.
  Apply the rubric's pass condition rather than automatically
  rejecting all incomplete work.
- The rubric decides the result. Never change a check's meaning
  during a grading run because a different answer feels better.
- The procedure decides how grading runs. Report missing steps
  rather than inventing a different process.
- Use unclear when evidence cannot establish a pass or failure.
  Apply the rubric's explicit unclear rule. If it is silent,
  treat unclear as fail.
- Complete all checks, including preferred checks, and report
  enough evidence for another reviewer to reproduce the verdict.
