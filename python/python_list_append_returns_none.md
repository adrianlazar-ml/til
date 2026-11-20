# `list.append()` mutates in place and returns `None`

`list.append()` adds an element to the end of the original list (*in-place* mutation) without creating a new list. It always returns `None`, so writing `result = my_list.append(x)` or `return my_list.append(x)` leads to unexpected bugs.

```python
scores = [10, 20]
result = scores.append(30)

print(scores) # [10, 20, 30]
print(result) # None
```

**Alternative when preserving the original list:**
```python
new_scores = scores + [30]
```