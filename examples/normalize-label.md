# Synthetic example: normalize a label

Use this example to practice the manual workflow without keys or private data. The patch is a format example; it does not come from a real MiMo call.

## Initial source

In an empty test project, create `labels.py` with exactly this content:

```python
def normalize_label(value):
    return value
```

## Task prepared by Codex

```text
Task ID: demo-label-01
Outcome: normalize_label accepts text and returns it without leading or trailing
whitespace and converted to lowercase.
Exclusions: no dependencies, new functions, or changes to other files.
Allowed source and output: existing labels.py, with these two lines:
def normalize_label(value):
    return value

Contract: the argument must be str. Any other type raises TypeError.
The empty string and strings containing only spaces return the empty string.
Internal spaces are preserved; use Python's lower conversion.
Do not convert None or numbers to text.

Acceptance: '  HELLO World  ' returns 'hello world'; '' returns '';
'   ' returns ''; None and 123 raise TypeError.
Codex will run these checks after reviewing and applying the patch.
Deliver only the unified patch for labels.py, without tools or wrapper text.
```

## Illustrative patch proposal

```diff
--- a/labels.py
+++ b/labels.py
@@ -1,2 +1,4 @@
 def normalize_label(value):
-    return value
+    if not isinstance(value, str):
+        raise TypeError("value must be a string")
+    return value.strip().lower()
```

## Independent check

Codex first checks that `labels.py` has not changed and that the patch touches only that output. After applying it, save the following as `check_labels.py` in the test project and run `python check_labels.py`, without `-O`:

```python
from labels import normalize_label

assert normalize_label("  HELLO World  ") == "hello world"
assert normalize_label("") == ""
assert normalize_label("   ") == ""
assert normalize_label(" A  B ") == "a  b"
for value in (None, 123):
    try:
        normalize_label(value)
    except TypeError:
        pass
    else:
        raise AssertionError("Expected TypeError")
print("6 checks passed")
```

If the source changes before integration, review the discrepancy before applying. Reject a patch that touches another path even if these tests pass. These checks validate the example, not MiMo's general quality or the behavior of any external adapter.
