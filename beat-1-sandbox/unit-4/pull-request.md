# Unit 4 — Test and Submit

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/138

**Branch**

`fix/72-malformed-password-hash`

## Eval iterations

**Run history**

1. First full run: `agreement: 17/20 scored items` — below the 18/20 bar.
2. First targeted run: `agreement: 7/7 scored items`.
3. Second targeted run: `agreement: 3/3 scored items`.
4. Final full run: `agreement: 19/20 scored items` — PASS.

The final result matches the committed `eval-run.txt`.
All five scored categories met the required category floor.

**Package analysis**

I chose `pkg-19`, a clear-accept package about preserving indentation
in a single-quoted YAML scalar.

The instructor gold label was `accept`. My rubric initially returned
`reject` in the first full run, but returned `accept` in the targeted
run and in the final full run, matching the gold label.

The original version of my testing check was too strict about the
form of supporting test evidence. This package demonstrated the
specific fixed behavior with a byte-identical round-trip check:

```text
$ diff <(./yq . source.yml) source.yml && echo IDENTICAL
IDENTICAL
```

The package also states: "`go test ./...` passes (4108 tests)."

Those results support the intended fix. Requiring entire raw test logs
in addition to an observable reproduction would have rejected an
otherwise adequately evidenced contribution.

**Check rationale**

I revised the following check. This is the exact row from my
final `tools/pr-precheck/rubric.md`:

```markdown
| test-plan-and-repo-checks | The plan's named tests and control cases, the repository's stated test and validation requirements, and the candidate PR's recorded test results. | Pass when the central planned verification and applicable repository checks have identifiable outcomes across the PR description and test evidence. A specific report of a named regression test passing, a suite result with its command, or an explicitly verified control is acceptable supporting evidence when the actual issue-specific fix is already demonstrated. Full raw stdout for every supporting check is not required. Reject packages that test only an unrelated or easier scenario, give only generic success claims without meaningful issue-specific verification, conceal failures, or omit mandatory checks without explanation. | required |
```

I kept issue-specific verification mandatory while allowing concise
reports of supporting test-suite results. This prevents a review
from rejecting good PRs just because complete raw logs were not
copied into the description.

I rejected the alternative of accepting a generic "all tests pass"
statement without testing the original problem. The revised check
still requires meaningful issue-specific verification.

**Trade-offs**

The trade-off is that a named test result may be accepted without
its complete stdout. That saves unnecessary repetition but gives
less direct evidence about the supporting suite.

To check that the revision did not become too permissive, I re-ran
the negative canaries `pkg-07` and `pkg-14` (not-tested) and `pkg-01`
(standards-wall). All three remained correctly rejected.

I also tested `pkg-03` (silent-drift), `pkg-12` (unreviewable),
and `pkg-20` (standards-wall). All three remained correctly rejected.

The final full run scored 19/20. `pkg-16` remained a false rejection
even though it had passed in the targeted evaluation. I retained
the 19/20 result rather than weakening more requirements to chase
a perfect score.
