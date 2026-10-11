# Evidence guide: where evidence lives in a PR package

This guide maps the evidence needed by rubric.md to its source.
Use only the practice bundle in eval mode. In live mode, use the
student's working copy and the relevant Path Review repository.

## Plan fidelity (harness category: silent-drift)

### Where it lives

In an eval package, compare:
- `Issue` and `Thread highlights`: the original problem,
  expected outcome, and any stated constraints.
- `Plan context`: the accepted diagnosis, in-scope and
  out-of-scope work, named files, implementation steps,
  and any recorded deviations.
- `Candidate PR > Diff`: every changed file and meaningful hunk.
- `Candidate PR > Commits`: what changes are included.
- `Candidate PR > Title` and `Description`: claims about
  what was implemented, omitted, or changed from the plan.

In live mode, compare:
- The actual GitHub issue and relevant thread comments.
- `plan.md`, including `## Scope`, `## Files to change`,
  `## Implementation approach`, and `## Deviations`.
- The committed branch diff from `git diff main...HEAD`.
- The proposed title and description in `pr_draft.md`.

### What good looks like

Each meaningful code change implements the agreed scope or a
specific, reasoned deviation. The implementation addresses the
issue's demonstrated failure boundary.

Planned work omitted intentionally is identified rather than
silently claimed as complete. A difference from the plan is
not automatically disqualifying if it is recorded honestly
and the delivered behavior is meaningful and verifiable.

Silent drift includes extra changes without explanation,
quietly missing planned work, or a description claiming an
implementation that the diff does not contain.

The description must match the actual code and evidence.
A claim of "implemented exactly as planned" does not pass
when the diff proves otherwise.

Rubric checks: plan-scope-fidelity, issue-outcome-alignment,
description-diff-truthfulness.

## Test evidence (harness category: not-tested)

### Where it lives

In an eval package, compare:
- `Plan context` and its reproduction evidence: original
  trigger, observed failure, and expected corrected behavior.
- `Plan context` test plan: expected checks and controls.
- `Candidate PR > Test evidence`: commands, observed results,
  before/after behavior, failures, and limitations.
- `Repo facts`: test commands or verification rules required
  by the repository.
- `Candidate PR > Description`: claims about testing.

In live mode, compare:
- The Unit 2 reproduction recorded on the GitHub issue.
- `plan.md`, especially its reproduction and test plan.
- `test_evidence.md` alongside `plan.md`.
- The repository's PR template and `docs/CONTRIBUTING.md`.
- Testing statements in `pr_draft.md`.

### What good looks like

Evidence identifies the original behavior and provides an
observable after-fix result that tests the same failure
boundary. The before result may come from a documented,
previously executed reproduction.

The evidence identifies the test or verification command
and its observed outcome, not only what the contributor
expected to happen.

Relevant planned tests, regression checks, and applicable
repository verification commands are accounted for.

A passing targeted test demonstrates a specific behavior;
a general suite may provide additional regression confidence.
Neither a proposed command nor an unsupported "tests pass"
statement is proof that verification occurred.

A failed or unavailable check must be reported accurately,
with its reason and impact. An honestly disclosed shortfall
is evaluated against the rubric rather than automatically
rejected. Missing meaningful evidence or fabricated test
claims cannot establish readiness.

Rubric checks: reproduction-evidence,
test-plan-and-repo-checks, description-diff-truthfulness.

## Diff quality (harness category: unreviewable)

### Where it lives

In an eval package, inspect:
- `Candidate PR > Diff`: all changed files, additions,
  deletions, and the actual implementation.
- `Candidate PR > Commits`: the commits being proposed.
- `Plan context`: planned files and permitted scope.
- Any documented deviations explaining extra changes.

In live mode, inspect:
- `git diff main...HEAD --stat` for the complete file list.
- `git diff main...HEAD` for every committed code change.
- `git log main..HEAD --oneline` for the branch commits.
- `plan.md` for scope and documented deviations.
- `pr_draft.md` for any stated limitations.

### What good looks like

The committed diff contains the intended fix and its
necessary supporting tests or documentation, without
unrelated changes that obscure the implementation.

The reviewer should be able to identify which changes
address the issue and why each changed file belongs.

Warning signs include debug prints, temporary files,
commented-out implementations, dead code, unrelated
refactoring, dependency upgrades without demonstrated
need, and large formatting-only changes.

Necessary supporting changes are acceptable. Merely
disclosing unrelated cleanup does not make unrelated
code appropriate for the pull request.

Assess the actual hunks, not the number of commits or
the length of the description. A small PR can still
contain an unrelated or misleading change.

Rubric checks: diff-reviewability,
plan-scope-fidelity, issue-outcome-alignment.

## Standards and comms (harness category: standards-wall)

### Where it lives

In an eval package, compare:
- `Repo facts`: PR-template requirements, checklist items,
  contribution instructions, and stated AI-use policy.
- `Thread highlights`: relevant maintainer directions.
- `Candidate PR > Title` and `Description`: how the
  contributor addresses those requirements.
- `Candidate PR > Test evidence`: support for checked
  testing claims when the template requires them.

In live mode, compare:
- `.github/PULL_REQUEST_TEMPLATE.md` in Path Review.
- `docs/CONTRIBUTING.md` and applicable repository policies.
- The actual GitHub issue thread.
- `pr_draft.md`, including all required PR sections.
- `test_evidence.md` for any testing claims.
- `scope.md` for Path Review's special house rules.
- `voice-guide.md` for outgoing writing guidance.

### What good looks like

All applicable required template sections contain specific
information, truthful checklist states, or an explained
N/A when an item does not apply.

The PR identifies the relevant issue and explains the
change and its verification clearly enough for review.

The contributor follows explicit maintainer instructions
and the repository's contribution and AI-use requirements.

For live Path Review PRs, the course requires an AI-use
disclosure in Notes for Reviewers even though the template
does not provide a dedicated AI-disclosure section.

In eval mode, apply only policies stated in the bundle.
Do not invent an AI policy or a missing template requirement.

A classmate's PR on the same Path Review issue is not
grounds for rejection under the course's house rules.

An unfilled template, a missing mandatory disclosure, or
an ignored stated requirement is a standards problem.
Whether factual claims match the diff is evaluated under
Plan fidelity instead of being reduced to writing style.

Rubric checks: template-compliance,
policy-and-thread-compliance.
