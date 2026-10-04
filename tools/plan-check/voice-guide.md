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
