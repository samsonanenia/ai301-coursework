# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

### Where it lives

In an eval package, read:

- the `Issue` or issue-context section for the behavior the contributor is expected to address;
- the `Repro evidence` section for the exact trigger, observed behavior, expected behavior, and any limitation established during reproduction;
- the diagnosis or cause statement in the `Candidate plan`.

In live mode, use:

- the GitHub issue description and relevant thread comments;
- the contributor's own posted reproduction comment;
- the diagnosis written in `plan.md`.

### What good looks like

A good diagnosis explains the behavior actually demonstrated by the reproduction. It does not replace the evidence with speculation or claim a deeper root cause that was never established.

If the evidence supports only a failure boundary rather than a complete root cause, the plan should describe that boundary or label the deeper explanation as a hypothesis.

## Scope

### Where it lives

In an eval package, read:

- the issue request and any named relevant files;
- the candidate plan's change description;
- its in-scope and out-of-scope statements;
- the files or areas it says will be modified.

In live mode, compare the GitHub issue with the scope, file list, and exclusions in `plan.md`.

### What good looks like

Good scope is one bounded change that is sufficient to address the reproduced issue.

The plan should exclude unrelated cleanup, broad refactors, dependency upgrades, speculative improvements, or changes to neighboring systems unless the evidence shows they are necessary.

The files or areas named should make sense for the reproduced behavior and the proposed change.

## Executability

### Where it lives

In an eval package, read the candidate plan's:

- files or code areas to touch;
- implementation approach;
- sequence or description of the change.

In live mode, use those same parts of `plan.md`, checked against the relevant repository files when needed.

### What good looks like

A stranger familiar with the repository should be able to start implementing from the plan without asking which file, function, component, or behavior is supposed to change.

The plan does not need to contain code or exact line numbers, but it must describe the intended modification concretely enough that the next implementation step is clear.

## Test plan

### Where it lives

In an eval package, compare:

- the original steps and observed result in `Repro evidence`;
- any existing regression test mentioned by the issue;
- the verification steps and expected result in the candidate plan.

In live mode, compare the contributor's Unit 2 reproduction comment with the test plan in `plan.md`.

### What good looks like

A good test plan reuses or directly corresponds to the original reproduction trigger and names an observable before-and-after result.

Before the fix, the check should expose the reproduced failure or failing regression condition. After the fix, the same behavior should produce the intended result.

Running a general test suite can be useful additional regression coverage, but "run tests" alone is not enough. The plan must say what result demonstrates that this particular issue is fixed.

## Honesty

### Where it lives

In an eval package, read:

- the repro evidence's stated limitations;
- the candidate plan's diagnosis;
- its assumptions, risks, unknowns, and exclusions;
- any `Deviations` content if the package represents work already started.

In live mode, use the contributor's repro evidence plus the risks, unknowns, assumptions, and `## Deviations` section in `plan.md`.

### What good looks like

Good evidence distinguishes facts established by reproduction or code inspection from hypotheses about what may be happening.

A plan should not turn an unresolved question into certainty.

It is acceptable for a plan to have no major unknowns when the evidence genuinely resolves the relevant questions.

If the implementation later differs from the posted plan, the deviation should state what changed and why rather than silently rewriting the history.

## Comms

### Where it lives

In an eval package, read:

- `Thread highlights`;
- the `Repo facts` block;
- the `Candidate plan comment`;
- any stated contribution, template, or AI-assistance rules.

In live mode, use:

- the current GitHub issue thread;
- the repository's `CONTRIBUTING.md`, templates, and other applicable contribution instructions;
- `comment.md`;
- the Path Review house rules in `scope.md`.

### What good looks like

A good plan comment is the contributor's own plan and is consistent with the evidence from their own reproduction.

It responds to relevant maintainer or thread guidance and follows explicit repository requirements, including any required AI-use disclosure.

In Path Review, another student's plan on the same issue does not block the contributor. However, a comment that merely says "same as above" or copies another contributor's plan is not sufficient.

The comment should communicate the diagnosis, bounded change, and verification approach accurately enough that someone reading the issue thread understands what the contributor intends to build.
