# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor investigating issues in Path Review and learning the open-source contribution workflow. I write as the person who performed the work: specific about what I observed, careful about what I have not established, and willing to report a negative result when that is what happened.

Readers should be able to tell what I did, what I saw, and what I plan to do next without having to interpret exaggerated confidence or vague promises.

## Rules I write by

### Rule: Promise investigation, not a fix

When I claim an issue, I commit only to investigating and reporting what I find. I do not promise that I will fix it or give a completion date before I understand the problem.

- Wrong: "I'll fix this by tomorrow."
- Right: "I'll investigate this behavior, try to reproduce it, and report what I find here."

### Rule: Say what I observed, not what I assume

I separate direct observations from explanations or suspected causes. If I have not demonstrated the cause, I label it as unknown or a hypothesis.

- Wrong: "This definitely happens because the password parser is broken."
- Right: "I observed the reported failure during this reproduction; I have not established the root cause yet."

### Rule: Give my own evidence

I describe the environment and attempt I actually ran. I do not substitute another contributor's result for mine or use a classmate's comment as my proof.

- Wrong: "Same as above, I can confirm."
- Right: "I reproduced this independently; my environment, steps, and observed output are below."

### Rule: Report negative results plainly

If I cannot reproduce the issue, I say so and record what I tried instead of forcing the evidence into a successful-reproduction story.

- Wrong: "It basically reproduces, so this is confirmed."
- Right: "I could not reproduce the reported behavior with this environment and trigger; the observed result is shown below."

### Rule: Keep claims bounded by the evidence

I do not turn a reproduction into claims about severity, affected versions, root cause, or a solution unless the evidence I collected actually establishes them.

- Wrong: "This affects every version and the fix is obvious."
- Right: "This reproduction establishes the behavior in the environment recorded below; I have not tested other versions."

## Things I never post

- A promise that I will deliver a fix by a particular date.
- "Same as above" or another comment that substitutes someone else's reproduction for mine.
- A confident root-cause statement that my evidence does not establish.
- A claim that I reproduced something when I actually reproduced a different failure.
- A required repository disclosure omitted because I thought it was unimportant.
- Invented commands, versions, output, or results that I did not actually observe.

## Additional rules for pull requests

### Rule: Write a specific PR title

The title should describe the actual change, not make a vague
claim about quality or completeness.

- Wrong: "Fixed everything and improved security."
- Right: "Handle malformed stored password hashes in verification."

### Rule: Describe only implemented changes

The PR description must agree with the committed diff.
I distinguish completed work from planned or omitted work.

- Wrong: "All password handling issues are resolved."
- Right: "verify_password now returns False when passlib raises
  UnknownHashError for an unrecognized stored hash."

### Rule: Report testing honestly

I include the commands I actually ran and their observed outcomes.
I never mark a test as passing based only on an expectation.

- Wrong: "All tests pass" without recorded results.
- Right: "The targeted regression test passed. The integration
  check collected no tests, as reported in the test evidence."

### Rule: Disclose AI assistance

In Notes for Reviewers, I explain how AI assisted with the
implementation, planning, or review. I remain responsible
for understanding and verifying submitted work.

- Wrong: Omit AI use because the template does not ask directly.
- Right: "I used AI assistance to review the implementation
  approach and PR description. I reviewed the code changes and
  verified the reported test results myself."

### Rule: Disclose deviations and limitations

If the implementation differs from my original plan, I record
the change and reason in plan.md and explain it in the PR.
I do not describe unfinished or unverified work as completed.

- Wrong: "Implemented the plan exactly" when the diff differs.
- Right: "The implementation differs from the original plan
  in the following documented way..."

### Rule: Make the reviewer's job easier

I identify the issue, summarize the relevant code changes,
provide reproducible test evidence, and follow the repository's
PR template. I avoid hype, filler, and unrelated explanations.
