# `zip()` silently truncates unequal-length iterables

`zip()` pairs elements from matching positions across two or more iterables, stopping automatically at the length of the shortest one. Remaining elements in longer iterables are dropped without raising an error (*silent failure*), which can produce incorrect results in calculations such as vector operations.

```python
a = [1, 2]
b = [10, 20, 30]

list(zip(a, b)) # [(1, 10), (2, 20)] — 30 is silently ignored
```

**How to prevent it:**
* Validate lengths explicitly beforehand and raise a `ValueError` on mismatch.
* Use `strict=True` (available in Python 3.10+):

```python
list(zip(a, b, strict=True)) # ValueError: zip() argument 2 is longer than argument 1
```