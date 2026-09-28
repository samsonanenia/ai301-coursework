# Evidence guide: where proof lives in a reproduction package

## Environment

### Where it lives

In an eval bundle, read the issue context and repo-facts block first to determine the environment or versions the issue actually targets. Then read the repro report's environment record for the contributor's operating system, runtime, dependency/tool versions, repository revision or checkout state, configuration, and other issue-relevant setup.

In live mode, read the GitHub issue, repository setup documentation, dependency manifests or lockfiles when relevant, and the environment information written in the student's draft repro comment.

### What good looks like

The record identifies the versions and state that materially affect reproduction without demanding irrelevant machine details. A source revision is appropriate when the attempt uses a repository checkout; an identified released package, binary, CDN build, or similar artifact is sufficient when that is what was actually tested. If the contributor's environment differs from the issue's stated target in a way that may affect the result, that difference is stated rather than hidden.

## Steps

### Where it lives

In an eval bundle, read the issue's prerequisites and trigger description together with the repro report's setup instructions, commands, inputs, fixtures, and ordered steps.

In live mode, read the issue and repository setup instructions, then the commands and actions in the student's draft repro comment.

### What good looks like

A stranger can start from the recorded environment and reach the intended trigger without supplying an unstated prerequisite, command, value, input, fixture, or manual action. Issue-relevant inputs are shown exactly or referenced unambiguously. The sequence exercises the behavior described by the issue rather than a nearby workflow.

## Behavior shown

### Where it lives

In an eval bundle, read the output excerpts, stack traces, logs, screenshots, test output, return values, or other artifacts and compare them directly with the behavior described in the issue context.

In live mode, inspect the evidence included in or linked from the draft repro comment and compare it with the GitHub issue's reported trigger and behavior.

### What good looks like

For a successful reproduction, the artifact comes from the stated attempt and visibly demonstrates the specific behavior under investigation; an adjacent failure is not enough. For an evidenced cannot-reproduce, the report shows a concrete attempt aimed at the reported scenario, records what actually happened, and explicitly identifies any material trigger condition it could not recreate rather than presenting that gap as a successful test of the exact trigger.

## Honesty

### Where it lives

Read the repro report's conclusion, observations, limitations, and any explanation or suspected cause against the commands and artifacts from the same reproduction attempt.

### What good looks like

The conclusion does not claim more than the evidence demonstrates. "Reproduced," "partially reproduced," and "could not reproduce" are all acceptable when they match the evidence. Relevant uncertainty or environmental differences are disclosed. Observation is distinguished from inference, and a suspected root cause is not stated as proven unless the evidence actually establishes it.

## Comms

### Where it lives

In an eval bundle, read the claim comment and repro comment against the issue context and repo-facts block, including any contribution policy, issue template, comment convention, or AI-assistance disclosure requirement.

In live mode, read the GitHub issue thread, CONTRIBUTING documentation and applicable repository policies, then compare them with the student's draft claim or repro comment.

For Path Review specifically, also apply the house rules in `scope.md`: classmates' claims do not block another student, every student posts their own independently evidenced reproduction, and credit does not depend on being first.

### What good looks like

A claim names the specific issue behavior being investigated, states the next investigation step, and promises to report back without pretending reproduction already happened or promising a fix or date.

A repro comment reports the contributor's own environment, actions, evidence, and result rather than saying only "same as above" or relying on another student's work. Both comments obey explicit repository policies, including any required AI-assistance disclosure.
