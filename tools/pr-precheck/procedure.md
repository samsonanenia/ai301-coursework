# Procedure: how this tool grades a PR package

## Read order

1. Determine the mode before collecting evidence. In live mode,
   read `scope.md` first, verify the target Path Review repository,
   and apply its house rules. Refuse out-of-scope submissions or
   an unfilled scope placeholder. In eval mode, ignore scope.md
   and use only the supplied package bundle.

2. Read `rubric.md`. Record every check name, evidence source,
   pass condition, weight, and the verdict rule. Do not grade yet.

3. Read `references/evidence-guide.md` to locate the four evidence
   families: plan fidelity, test evidence, diff quality, and
   standards and communications.

4. Read the issue and thread, followed by repository requirements.
   In live mode, consult the actual issue, PR template, and
   docs/CONTRIBUTING.md. In eval mode, use the bundle's Issue,
   Thread highlights, and Repo facts sections. Record the requested
   behavior, constraints, template asks, and disclosure policy.

5. Read the accepted plan before the proposed PR. Record the
   diagnosis, scoped files, planned implementation, excluded
   changes, required tests, and any documented deviations.
   Note the original reproduction's trigger, observed failure,
   and expected corrected behavior.

6. Read the candidate commits and unified diff. In live mode,
   use `git diff main...HEAD` from the fork's working directory.
   Record the changed files and meaningful hunks, including
   deletions, supporting tests, and unexpected changes.

7. Read the candidate test evidence. Compare recorded tests
   and their observed results to the plan and original reproduction.

8. Read the proposed PR title and description last. In live mode,
   use pr_draft.md and read voice-guide.md. In eval mode, use
   only the Candidate PR title and description in the package.

9. This order prevents the description's claims from determining
   what the code or tests supposedly prove.

## Evidence gathering

1. For `plan-scope-fidelity`, create a side-by-side comparison
   of the plan's scoped work and each meaningful diff hunk.
   Record planned changes implemented, unexplained additions,
   missing planned work, and deviations documented in plan.md.

2. For `issue-outcome-alignment`, connect the issue's original
   failure boundary to the actual implementation in the diff.
   Record whether changed behavior plausibly addresses that
   demonstrated boundary without relying on unsupported claims.

3. For `description-diff-truthfulness`, compare each substantial
   claim in the title, summary, change list, testing section,
   and limitations against the diff and test evidence. Record
   unsupported claims, inaccurate descriptions, and omissions.

4. For `reproduction-evidence`, extract the original reproduction,
   its observed before state, the expected-after result, and
   the actual after-fix verification. Identify commands or
   actions and observed outputs. Do not treat a proposed test
   or an assertion of success as executed evidence.

5. For `test-plan-and-repo-checks`, map each applicable planned
   test and repository-required check to recorded evidence.
   Record commands, actual outcomes, failures, limitations,
   and justified omissions. Distinguish disclosed failures
   from missing verification or falsely claimed success.
   Do not invent a test result or assume that no output
   means the test passed.

6. For `diff-reviewability`, inspect all changed files and
   meaningful hunks for relevant implementation and tests.
   Identify debug output, temporary files, dead code,
   commented-out implementations, broad formatting churn,
   dependency changes, or unrelated cleanup. Compare each
   questionable change with the issue, plan, and deviations.

7. For `template-compliance`, extract the repository's actual
   required PR sections and checklist items. Compare them with
   the draft PR. Record fulfilled asks, meaningful N/A
   explanations, unchecked work, and unfilled boilerplate.

8. For `policy-and-thread-compliance`, collect applicable
   contribution rules, AI-use disclosure requirements, and
   explicit maintainer instructions. Compare them with the
   candidate PR. In live Path Review mode, require the
   course's AI-use disclosure even if the template lacks
   a dedicated section. Do not invent policies in eval mode.

9. Use `references/evidence-guide.md` for exact locations.
   In eval mode, never fetch live GitHub pages or fill missing
   bundle details with outside information. In live mode,
   cite the relevant file, command output, or repository source.

## Check execution

1. Execute all checks in the exact order listed in `rubric.md`:
   plan-scope-fidelity, issue-outcome-alignment,
   description-diff-truthfulness, reproduction-evidence,
   test-plan-and-repo-checks, diff-reviewability,
   template-compliance, policy-and-thread-compliance.

2. For each check, use the evidence gathered specifically
   for that check and apply its complete pass condition.

3. Grade `pass` only when the available evidence satisfies
   the stated pass condition. A concise artifact may pass
   when its observable evidence is sufficient.

4. Grade `fail` when the evidence establishes a violation.
   Examples include an unexplained out-of-scope change,
   unsupported test claims, unrelated diff debris, or a
   clearly violated mandatory repository policy.

5. Grade `unclear` when necessary evidence is missing or
   ambiguous and the check cannot be reliably decided.
   Never use unclear simply because a step was skipped.
   State exactly what evidence is missing.

6. Distinguish an honestly disclosed limitation from
   silent drift. A disclosed, justified omission can pass
   the fidelity check when the description is accurate.
   It does not excuse missing meaningful verification,
   unrelated edits, or a mandatory policy violation.

7. Evaluate tests by their demonstrated behavior and outcome,
   not by whether every command has a passing exit status.
   A disclosed failure with an explained impact is not an
   automatic rejection if the applicable pass condition holds.

8. Record a short evidence statement for every check, naming
   the decisive changed file, observed output, plan statement,
   missing evidence, or repository requirement.

9. Keep grades independent. A passing test cannot compensate
   for a materially misleading description, and a polished
   description cannot compensate for an unreviewable diff.

10. If a rubric or procedure instruction is missing, report
    the gap instead of inventing new criteria or steps.

## Verdict assembly

1. Complete every check before selecting the verdict.
   Keep each check's exact name, grade, and one-line evidence.

2. Apply `rubric.md`'s verdict rule. Accept only when every
   required check passes. Reject when any required check
   fails or is unclear. Treat unclear as fail for verdict
   purposes. Preferred checks never determine the verdict.

3. In a rejection, identify the first failed or unclear
   required check in rubric order as the primary blocker.
   Quote or state its decisive evidence in the readable
   summary. Report additional blockers separately.

4. For acceptance, state the strongest relevant observable
   support, including implementation fidelity and actual
   verification, without promising the code is defect-free.

5. In live mode, additionally report any voice-guide violations
   without changing the verdict unless the rubric requires it.

6. Before the JSON, provide a concise per-check summary,
   primary blocker if rejected, and actionable corrections.
   Report procedure gaps if encountered.

7. End with the exact JSON schema from SKILL.md containing
   the PR URL or bundle id, every check with pass/fail/unclear
   and one evidence line, and the final accept/reject verdict.
   Output nothing after the fenced JSON block.
