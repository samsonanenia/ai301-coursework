# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

---

## Posted upstream

**GitHub username**

samsonanenia

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5983052542

Plan for #72, based on my reproduction above at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

**Diagnosis:** my reproduction showed that `verify_password()` reaches `pwd_context.verify(...)` with `"not_a_valid_bcrypt_hash"`, and passlib's `UnknownHashError` escapes instead of the function returning `False`. The current function has no exception handling around that verification call.

**Change:** in `core/security.py`, I plan to handle `passlib.exc.UnknownHashError` at the `verify_password()` boundary and return `False`. In `tests/unit/test_security.py`, I will remove the H-05 strict `xfail` marker so the existing malformed-hash assertion becomes a normal regression test.

**Scope:** I am keeping this to those two files. I am not changing `hash_password`, JWT behavior, the login route, dependencies, or broadening the catch to exception types that my reproduction did not establish.

**Verification:** I will re-run my original direct reproduction and expect it to print `False` instead of raising `UnknownHashError`. I will then run `test_verify_with_wrong_hash_format` and expect a normal pass after removing the marker, followed by the full `tests/unit/test_security.py` file to check existing security behavior.

I used Claude to help draft this plan. The diagnosis and commands above are based on my own Unit 2 reproduction, and I reviewed the plan against that evidence.

---

## Your branch

**Branch**

`fix/72-malformed-password-hash`

**Evidence**

### Before the fix

Command:

` .venv/bin/python -c 'from core.security import verify_password; print(verify_password("password", "not_a_valid_bcrypt_hash"))' `

Output:

~~~text
Traceback (most recent call last):
  ...
  File "/Users/sami70/Documents/pathreview-ai301-fa26-s3/core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
  ...
  File ".../passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
~~~

Command:

` .venv/bin/pytest tests/unit/test_security.py -vv `

Output:

~~~text
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL
(issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False)

24 passed, 1 xfailed, 1 warning in 6.03s
~~~

### After the fix

Command:

` .venv/bin/python -c 'from core.security import verify_password; print(verify_password("password", "not_a_valid_bcrypt_hash"))' `

Output:

~~~text
False
~~~

Command:

` .venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv `

Output:

~~~text
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]

1 passed, 1 warning in 0.19s
~~~

Command:

` .venv/bin/pytest tests/unit/test_security.py -q `

Output:

~~~text
......................... [100%]

25 passed, 1 warning in 6.20s
~~~

## Eval iterations

**Run history**

Run 1 — full eval: **18/20 agreement**, meeting the 18/20 bar.

Category results:

- clear-accept: 5/7
- scope-creep: 4/4
- thread-convention: 2/2
- unbuildable: 3/3
- wrong-cause: 4/4

The two disagreements were `pkg-02` and `pkg-14`. This was my only full run and is the run saved in `eval-run.txt`.

**Package analysis**

I analyzed `pkg-03`.

My rubric verdict was **accept**, and the gold label was also **accept**.

The candidate plan says:

> "Change: in the command construction in `crates/cli/src/decompress.rs`, append `--` before the file path for every spawned decompression tool."

The package grounded its diagnosis directly in the reproduced behavior: a decompression tool receives a leading-dash filename in option position and interprets the filename as command-line options. The proposed change was bounded to adding the `--` end-of-options separator in `crates/cli/src/decompress.rs`, while explicitly excluding unrelated shell quoting, tool selection, and matching behavior.

The plan was executable because it named the exact code area and intended change. Its test plan also mapped directly to the reproduction: rerun `rg -z sometext`, require the dash-named compressed file to match with exit code 0, keep the normal-file control working, and add regression coverage. The candidate comment also acknowledged the existing PR and prior-art discussion in the thread and addressed the repository's AI-use policy. Those facts satisfied my required checks, so the rubric returned `accept`.

**Check rationale**

One check in my final `rubric.md` reads exactly:

> | test-plan-proves-fix | The plan's test plan read against the original repro steps, observed failure, expected behavior, and any existing regression test. | Pass when the proposed verification would fail or expose the original behavior before the fix and would show the intended behavior after the fix. It must name an observable result rather than only saying to run tests or confirm the fix, and it must include relevant regression coverage. | required |

I wrote the check this way because simply saying "run the tests" does not establish that a plan can prove the reported bug was fixed. I rejected that looser standard in favor of requiring a connection to the original reproduction plus an observable before-and-after result. The regression-coverage requirement also makes the plan show how the behavior will stay fixed rather than relying only on a one-time manual check.

**Trade-offs**

The `test-plan-proves-fix` check is intentionally strict. It can reject an otherwise reasonable plan whose author knows which test suite to run but does not state the issue-specific observable result or connect the test back to the original reproduction. I accept that trade-off because this skill is deciding whether another contributor could verify the fix from the written plan without having to infer what success means.

My first full run already reached the required 18/20 agreement with every category represented, so I did not loosen the check or spend additional course credit on targeted retries.
