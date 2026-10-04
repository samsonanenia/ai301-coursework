# Plan for issue #72: fail closed on an unrecognized stored password hash

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

## Diagnosis

`verify_password()` in `core/security.py` passes the stored hash directly to `pwd_context.verify(...)` without handling the exception raised when passlib cannot recognize the stored hash format.

My Unit 2 reproduction established this failure at that boundary. With `"not_a_valid_bcrypt_hash"`, `passlib.exc.UnknownHashError` escapes instead of `verify_password()` returning `False`.

I am not claiming a broader passlib or bcrypt problem. My own reproduction establishes this specific unhandled exception.

## Reproduction evidence

My reproduction used commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088` with Python 3.13.5, passlib 1.7.4, and bcrypt 4.3.0.

I ran:

`.venv/bin/python -c 'from core.security import verify_password; print(verify_password("password", "not_a_valid_bcrypt_hash"))'`

Instead of returning a Boolean, it raised:

`passlib.exc.UnknownHashError: hash could not be identified`

The traceback showed the exception escaping from `core/security.py` at the call to `pwd_context.verify(...)`.

I also ran:

`.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv -rxX`

The test reported:

`XFAIL ... issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False`

Running the complete security test file before the fix produced:

`24 passed, 1 xfailed`

Expected behavior is for the malformed stored hash used by issue #72 to return `False`.

## Scope

In scope:

- Handle `passlib.exc.UnknownHashError` inside `verify_password()`.
- Return `False` for the unrecognized stored hash demonstrated in my reproduction.
- Remove the strict H-05 `xfail` marker from the existing regression test.
- Preserve normal verification behavior for valid bcrypt hashes.

Out of scope:

- Changes to `hash_password()`.
- JWT creation or decoding changes.
- Login-route changes.
- Dependency upgrades.
- Passlib or bcrypt configuration changes.
- Unrelated security refactoring.
- Broad exception handling not established by my reproduction.

The issue thread contains discussion of other malformed bcrypt-shaped values that may raise different `ValueError` cases. My own reproduction did not establish those cases, so I am not treating them as proven by my evidence. If implementation or testing shows the issue requires broader handling, I will record that as a deviation before proceeding.

## Files to change

### `core/security.py`

Import `UnknownHashError` from `passlib.exc`.

Wrap the existing `pwd_context.verify(...)` call so that `UnknownHashError` returns `False` instead of escaping.

### `tests/unit/test_security.py`

Remove the `@pytest.mark.xfail(...)` marker from `test_verify_with_wrong_hash_format`.

Keep the existing assertion that the malformed stored hash returns `False`.

## Implementation approach

1. Add the specific `UnknownHashError` import.
2. Keep `pwd_context.verify(...)` as the normal verification path.
3. Catch `UnknownHashError` and return `False`.
4. Remove the H-05 strict `xfail` marker.
5. Review the diff and confirm only the two issue-related files changed.

## Test plan

First, re-run my original reproduction:

`.venv/bin/python -c 'from core.security import verify_password; print(verify_password("password", "not_a_valid_bcrypt_hash"))'`

Before the fix, it raises `UnknownHashError`.

After the fix, I expect it to print:

`False`

Then run:

`.venv/bin/pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv`

After removing the `xfail` marker, I expect the test to report `PASSED`.

Finally run:

`.venv/bin/pytest tests/unit/test_security.py -vv`

Before the change this produced `24 passed, 1 xfailed`. After the change I expect all 25 tests to pass, including the existing correct-password and incorrect-password verification tests.

## Risks and unknowns

My reproduction establishes `UnknownHashError` for the exact malformed stored value used by issue #72 and its existing regression test.

I have not independently established the behavior of every malformed bcrypt-shaped value. I will therefore keep the initial implementation tied to the reproduced failure. If testing demonstrates that a broader exception boundary is required to satisfy the issue correctly, I will document the difference under `## Deviations` and re-run the plan check.

## Deviations

The implementation followed the plan without deviation.