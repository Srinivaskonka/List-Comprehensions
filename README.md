# Python List Comprehensions — README

A concise, example‑rich guide to Python list comprehensions—plus dict/set comprehensions and generator expressions. Perfect for quick reference in projects and interviews.

---

## What is a List Comprehension?

A **list comprehension** is a compact way to create lists from iterables. It combines **looping**, **optional filtering**, and **optional transformation** in a single expression.

**Syntax**:

```python
[new_item  for item in iterable  if condition]
```

* `new_item` → how to transform each element
* `item in iterable` → the loop
* `if condition` → (optional) filter

**Example**:

```python
squares = [n*n for n in range(6)]  # [0, 1, 4, 9, 16, 25]
```

---

##  Quick Examples

### 1) Mapping (transform values)

```python
words = ["a", "list", "of", "words"]
lengths = [len(w) for w in words]  # [1, 4, 2, 5]
```

### 2) Filtering (keep some values)

```python
nums = list(range(10))
evens = [n for n in nums if n % 2 == 0]  # [0, 2, 4, 6, 8]
```

### 3) Map + Filter

```python
# squares of odd numbers only
odd_squares = [n*n for n in range(10) if n % 2]
```

### 4) Conditional Expression (if/else inside expression)

```python
labels = ["even" if n % 2 == 0 else "odd" for n in range(5)]
# ["even", "odd", "even", "odd", "even"]
```

### 5) Nested Loops (Cartesian product)

```python
pairs = [(x, y) for x in [1, 2, 3] for y in ["a", "b"]]
# [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]
```

### 6) Flatten a 2D List

```python
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [num for row in matrix for num in row]  # [1, 2, 3, 4, 5, 6]
```

### 7) Remove/Normalize Strings

```python
raw = ["  Alice\n", "Bob  ", "  ", "Charlie"]
clean = [s.strip() for s in raw if s.strip()]  # ["Alice", "Bob", "Charlie"]
```

---

##  Advanced Patterns

### Comprehension Order (read left → right)

```python
# for x in A
#   for y in B
#     if cond(x, y)
triples = [(x, y, x*y)
           for x in range(1, 4)
           for y in range(1, 4)
           if (x*y) % 2 == 0]
```

### Inline Unpacking

```python
pairs = [(1, "a"), (2, "b"), (3, "c")]
keys = [k for (k, _) in pairs]   # [1, 2, 3]
vals = [v for (_, v) in pairs]    # ["a", "b", "c"]
```

### Avoid Recomputing (bind a name)

```python
# Use a local name if a function is expensive
from math import sqrt
nums = range(1, 20)
root = sqrt
roots = [root(n) for n in nums if root(n).is_integer()]
```

---

##  Dict, Set, and Generator Variants

### Dict Comprehension

```python
names = ["alice", "bob", "carol"]
name_map = {n: n.title() for n in names}
# {"alice": "Alice", "bob": "Bob", "carol": "Carol"}
```

### Set Comprehension (unique results)

```python
vals = [1, 2, 2, 3, 3, 3]
uniq_squares = {v*v for v in vals}  # {1, 4, 9}
```

### Generator Expression (lazy; memory‑efficient)

```python
# Parentheses create a generator (iterates on demand)
sum_of_squares = sum(n*n for n in range(1, 1_000_001))
```

> **Tip:** Use a **generator** for large data to reduce memory; switch to a **list** if you need indexing or multiple passes.

---

##  Common Pitfalls

* **Nested If vs. If/Else:** `if` filters elements; `A if cond else B` chooses a value.
* **Readability:** If it’s too long or too nested, prefer a normal loop.
* **Side Effects:** Avoid I/O or mutation in comprehensions—keep them expression‑only.
* **Scope:** Loop variable is local to the comprehension (Py3+), it won’t leak outside.

---

##  Performance Notes

* Comprehensions are often **faster** than equivalent `for` loops in Python due to C‑level optimizations.
* Prefer `set` for membership tests when filtering (`if x in big_set`).
* For very large pipelines, consider **generator expressions** to lower memory usage.

---

##  Mini Exercises

1. Build `[n for n in range(50) if n % 7 == 0]`.
2. From `words = ["apple", "", "kiwi", "banana", " "]`, produce non‑empty, trimmed words.
3. Given `matrix = [[1,2,3],[4,5,6]]`, create column sums `[5,7,9]` using a comprehension.
4. From `text = "lorem ipsum dolor sit amet"`, create a dict of `{word: len(word)}`.
5. Make a set of unique lowercase letters from a sentence.

---

## 🔁 Loop vs. Comprehension (equivalence)

```python
# Loop
squares = []
for n in range(6):
    if n % 2 == 0:
        squares.append(n*n)

# List comprehension (same result)
squares = [n*n for n in range(6) if n % 2 == 0]
```

---

## Copy‑paste Snippets

```python
# Filter then map
[result(x) for x in xs if keep(x)]

# Flatten nested list
[y for row in grid for y in row]

# Dict from pairs
{k: f(v) for (k, v) in pairs}

# Unique transformed values
{g(x) for x in xs}

# Streaming aggregation
sum(h(x) for x in stream())
```
---

## 🤝 Contributing

PRs for new patterns, benchmarks, and edge cases are welcome!
