# Procedure: how this skill grades a plan package

## Read order

1. In live mode, read `scope.md` first and confirm that the issue belongs to the allowed Path Review repository. Note the Path Review house rules, especially that another student's plan does not block this contributor's own plan.

2. Read `rubric.md` and list every check, its required evidence, its pass condition, its weight, and the verdict rule before grading anything.

3. Read `references/evidence-guide.md` so each evidence family has a known location and standard before evidence is gathered.

4. Read the issue context and thread highlights before reading the candidate plan. Record the behavior the issue asks to change, any requested files or constraints, relevant maintainer guidance, and repository conventions.

5. Read the repro evidence next. Record the exact trigger, observed behavior, expected behavior, environment or revision when relevant, and any limitations or unresolved questions.

6. Read the candidate plan and candidate plan comment last. This order prevents the plan's explanation from replacing or reshaping what the issue and reproduction actually established.

## Evidence gathering

1. For `diagnosis-grounded`, locate the plan's diagnosis or cause statement and compare it directly with the issue context and reproduced evidence. Record the reproduced fact that supports or contradicts the diagnosis.

2. For `cause-target-aligned`, locate the proposed implementation change and compare it with the demonstrated failure boundary. Record whether the proposed change addresses that boundary or merely hides a symptom.

3. For `scope-bounded`, collect the plan's in-scope work, out-of-scope work, named files or areas, and any extra cleanup or improvements. Compare those items with what the issue actually requires.

4. For `executable-approach`, collect the files or areas to be touched, the implementation approach, and any stated sequence of work. Record whether a contributor could start without inventing a missing target or essential step.

5. For `test-plan-proves-fix`, collect the original repro command or actions, the before-fix observable result, the plan's proposed verification, the expected after-fix result, and any regression test named by the issue or plan.

6. For `uncertainty-honest`, collect claims about root cause, risks, assumptions, unknowns, and limitations. Compare certainty in the plan with what the issue and reproduction actually prove.

7. For `thread-and-repo-conventions`, read the candidate plan comment against thread highlights, repository facts, contribution instructions, templates, AI-use requirements, and Path Review house rules. Record any explicit requirement the comment satisfies or violates.

8. In live mode, use GitHub and the local drafts only for evidence locations named by the rubric and evidence guide. In eval mode, use only the supplied package; do not fetch outside evidence.

## Check execution

1. Grade the checks in the order they appear in `rubric.md`.

2. For each check, use only the evidence named for that check. Do not award a pass because the overall plan seems reasonable.

3. Grade `pass` when the available evidence satisfies the full pass condition.

4. Grade `fail` when the available evidence shows that the plan violates the pass condition.

5. Grade `unclear` only when evidence required to decide the check is genuinely missing or too ambiguous to apply the pass condition. `unclear` must not mean that the grader skipped looking.

6. Record one concise fact or quote that explains every grade. Prefer the smallest piece of evidence that actually decides the check.

7. Do not let strong performance on one check compensate for failure on another required check.

8. When a plan contains a hypothesis, distinguish between a clearly labeled hypothesis and a claim presented as proven fact. Apply the rubric's diagnosis and honesty checks separately.

9. When the proposed test only says to run tests, inspect whether it names an observable before-and-after behavior. If it does not demonstrate the original failure and intended corrected behavior, grade according to the test-plan pass condition rather than assuming the test is sufficient.

## Verdict assembly

1. After every check has a grade, apply the verdict rule from `rubric.md` exactly as written.

2. Treat every `unclear` required check as a failure because the rubric's verdict rule says `unclear` counts as fail.

3. Return `accept` only when every required check passes.

4. Return `reject` when any required check is `fail` or `unclear`.

5. Preferred checks, if added later, may be reported but never change the final verdict.

6. In the readable summary, identify the check or checks that caused a rejection and quote or state the evidence that decided them.

7. End with the required machine-readable JSON block containing the item, every check with its grade and one-line evidence, and the final `accept` or `reject` verdict.
