# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

samsonanenia

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5860253621

Hi, I'd like to investigate #72, where `verify_password` crashes when the stored password hash is malformed.

I'll reproduce the reported behavior in my local Path Review setup, record the environment and exact trigger, and report what I observe here. If I can reproduce it, I'll use that evidence to narrow down where the exception is escaping before proposing any change.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5864757596

I reproduced the malformed stored-hash behavior from #72.

### Environment

- Repository: `codepath/pathreview-ai301-fa26-s3`
- Commit: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`
- macOS 27.0, arm64
- Python 3.13.5
- Passlib 1.7.4
- bcrypt 4.3.0
- Dependencies installed with `pip install -e ".[dev]"`

### Steps to reproduce

From a clean checkout, I created a virtual environment and installed the development dependencies:

```bash
python3 -m venv .venv
.venv/bin/python -m pip install --upgrade pip setuptools wheel
.venv/bin/pip install -e ".[dev]"
```

I then called `verify_password` directly with a malformed stored hash:

```bash
.venv/bin/python -c 'from core.security import verify_password; print(verify_password("password", "not_a_valid_bcrypt_hash"))'
```

### Observed behavior

The call does not return a Boolean. It raises:

```text
Traceback (most recent call last):
  ...
  File ".../core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
  ...
  File ".../passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
```

I also ran the existing regression test:

```bash
.venv/bin/pytest \
  tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format \
  -vv -rxX
```

It reports:

```text
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
- issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
```

### Expected behavior

For an unrecognized or malformed stored password hash, `verify_password` should handle the invalid hash and return `False` rather than allowing `passlib.exc.UnknownHashError` to escape.

### Result

Reproduced. The malformed stored hash reaches `pwd_context.verify(...)`, and the resulting `UnknownHashError` escapes from `verify_password` instead of the function returning `False`.

I have not investigated or established the fix yet; this report only confirms the current behavior.

## Eval iterations

**Run history**

1. **Run 1 — full eval:** 18/20 scored packages agreed with the gold labels. The run passed the 18/20 bar and every category floor. The disagreements were `pkg-07`, which my rubric rejected on `environment-target-match`, and `pkg-09`, which my rubric rejected on `behavior-target-match`.
2. **Run 2 — targeted partial rerun:** 2/2 agreement on `pkg-07` and `pkg-09` after revising those two checks. Both packages changed to `accept`, matching their gold labels.
3. **Run 3 — confirming full eval:** 19/20 scored packages agreed with the gold labels. Every category floor passed: clear-accept 7/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, and wrong-target 4/4. `pkg-03` was the only disagreement. This is the run saved in `eval-run.txt`.

**Package analysis**

I analyzed `pkg-09`. The gold label was `accept`, but my first rubric returned `reject` because `behavior-target-match` failed.

The package reported an honest cannot-reproduce result for the second `--exec-batch` ordering scenario. The contributor documented the environment, commands, repeated attempts, actual marker order, and the important limitation that their padding approach may not have caused the second command to hit the argument-size limit first.

My original check required a cannot-reproduce report to show that "the same trigger was exercised without the reported behavior." That wording was too strict because `pkg-09` explicitly documented that one issue-relevant trigger condition might not have been recreated. The report was still useful and honest evidence rather than a false claim of reproduction. I revised the check so a cannot-reproduce result can pass when it shows a concrete attempt aimed at the reported scenario, records what actually happened, and clearly identifies any trigger condition that could not be recreated.

**Check rationale**

My final check reads exactly:

> | behavior-target-match | The output excerpts, logs, screenshots, error text, or other artifacts read directly against the trigger and behavior described in the issue context. | Pass when a successful reproduction demonstrates the issue's specific reported behavior from the intended trigger. For a cannot-reproduce result, pass when the evidence shows a concrete attempt aimed at the reported scenario and records the observed result, while explicitly identifying any issue-relevant trigger condition the contributor could not recreate. An unrelated workflow, adjacent error, different bug, unsupported paraphrase, or negative result that hides a material trigger difference does not pass. | required |

I revised this check after `pkg-09`. My first version treated a cannot-reproduce result as valid only when the exact trigger had definitely been recreated. That rejected a report that honestly described both the attempt and the material condition it could not establish. The final wording keeps successful reproductions strict while allowing an evidenced negative result when its limitation is explicit. I kept the final rejection conditions so an adjacent symptom, different bug, or hidden trigger difference still fails.

**Trade-offs**

Loosening `behavior-target-match` makes the rubric more willing to accept an honest cannot-reproduce report even when one trigger condition could not be recreated. The trade-off is that a weak negative attempt could look acceptable if the rule were too permissive. I limited that risk by requiring a concrete attempt aimed at the reported scenario, the observed result, and explicit disclosure of any missing trigger condition, while still rejecting unrelated workflows and hidden material differences.

The revision changed `pkg-09` from reject to accept. In the confirming full run, all four `wrong-target` packages still matched their gold labels (`4/4`), while the overall agreement improved from 18/20 to 19/20. That gives me evidence that the change fixed the false rejection without making the wrong-target category broadly permissive.
