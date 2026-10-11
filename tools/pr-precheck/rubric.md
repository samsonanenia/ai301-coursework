# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-scope-fidelity | The accepted plan's stated scope, named files, excluded work, and Deviations read against every changed file and meaningful hunk in the candidate PR diff. | Pass when the changes stay within the plan's scope or are covered by an explicit, reasoned deviation. Planned work that was intentionally omitted must be acknowledged rather than silently claimed as complete. Reject unexplained additions, omissions, or contradictions, including a claim of exact plan fidelity that the diff disproves. | required |
| issue-outcome-alignment | The issue's demonstrated problem and expected behavior, the plan's implementation approach, and the candidate PR's actual code changes. | Pass when the substantive changes address the issue's demonstrated failure boundary in a way consistent with the plan. The diff must show a relevant implementation, not merely describe or promise one. An honestly disclosed limitation is not automatically a failure if the implemented change still has a meaningful, verifiable outcome. | required |
| description-diff-truthfulness | The candidate PR's title, summary, change list, test claims, and limitations compared with its diff, commits, and actual test evidence. | Pass when the title and description accurately identify the issue, substantive change, and delivered outcome when read alongside the diff and test evidence. A high-level summary need not enumerate every hunk or repeat full test logs. Supporting evidence elsewhere in the PR package may substantiate concise claims. Reject materially false claims, fabricated verification, or omissions of important changes and deviations that mislead the reviewer. | required |
| reproduction-evidence | The plan-context reproduction and test plan compared with the candidate PR's test-evidence section, including commands, observed before/after behavior, and outcomes. | Pass when the issue or accepted reproduction establishes the original failure and the PR package records an actual post-change observation for the same relevant trigger. Evidence may appear in the description or Test evidence. A concrete before/after example, command output, or specific observed UI interaction is sufficient without full repeated transcripts. Reject generic assertions such as 'works now', tests of a different scenario, or expected outcomes presented as executed results. | required |
| test-plan-and-repo-checks | The plan's named tests and control cases, the repository's stated test and validation requirements, and the candidate PR's recorded test results. | Pass when the central planned verification and applicable repository checks have identifiable outcomes across the PR description and test evidence. A specific report of a named regression test passing, a suite result with its command, or an explicitly verified control is acceptable supporting evidence when the actual issue-specific fix is already demonstrated. Full raw stdout for every supporting check is not required. Reject packages that test only an unrelated or easier scenario, give only generic success claims without meaningful issue-specific verification, conceal failures, or omit mandatory checks without explanation. | required |
| diff-reviewability | The candidate PR's unified diff and commit list, compared with the issue, plan, and documented deviations. | Pass when the change is focused enough for a maintainer to review and contains no unrelated code, debug prints, temporary files, abandoned implementations, commented-out code, or unnecessary formatting churn. Necessary supporting tests, documentation, and generated changes are allowed when relevant. Explaining an unrelated edit does not automatically make it appropriate for this PR. | required |
| template-compliance | The repo-facts block's PR-template requirements or, in live mode, .github/PULL_REQUEST_TEMPLATE.md, compared with the candidate PR title and description. | Pass when all applicable required template sections and checklists are addressed with meaningful information, accurate statuses, or justified N/A explanations. Do not require a section or checklist that the repository does not ask for. Boilerplate left unfilled does not pass. | required |
| policy-and-thread-compliance | The repo-facts block's contribution policy and AI-use rules, the issue thread's applicable maintainer instructions, and the candidate PR description. In live mode also read docs/CONTRIBUTING.md and the relevant issue thread. | Pass when the submission meets applicable repository policies and explicit maintainer directions, including AI-use disclosure when required. If no AI disclosure policy exists, do not invent one. Path Review's course-required AI disclosure still applies in live mode. A classmate's work on the same Path Review issue is not by itself a violation. | required |

## Verdict rule

Grade every check as pass, fail, or unclear using its stated
evidence and pass condition.

Return `accept` only when every required check passes.

Return `reject` when any required check fails or is unclear.
Treat `unclear` as fail for the final verdict because missing
or unverifiable evidence cannot establish submission readiness.

Preferred checks, if added later, do not change the verdict.

Do not substitute overall confidence for individual grades.
Do not reject automatically because a disclosed limitation exists.
Evaluate whether the actual outcome satisfies each check.
Likewise, disclosure cannot excuse an unrelated diff, missing
meaningful verification, or a violated mandatory repository rule.

Each check must include a specific one-line evidence explanation.
The output must use the exact check names in this table.
