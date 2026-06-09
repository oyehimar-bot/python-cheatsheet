# 🐍 Python Cheat Sheet
> A beginner-friendly reference for core Python concepts — with explanations, gotchas, and tips.

**Author:** Oyelade Emmanuel | [GitHub](https://github.com/oyehimar-bot)

---

## Table of Contents
- [Variables](#variables)
- [If-Statements](#if-statements)
- [Loops](#loops)
- [Math](#math)
- [Arrays (Lists)](#arrays-lists)
- [Strings](#strings)
- [Queues](#queues)
- [HashSets](#hashsets)
- [HashMaps (Dicts)](#hashmaps-dicts)
- [Tuples](#tuples)
- [Heaps](#heaps)
- [Functions](#functions)
- [Classes](#classes)

---

## Variables

> Python variables are **dynamically typed** — you don't declare a type, Python figures it out.

```python
n = 0           # int
n = "abc"       # now a string — no error!
n = None        # None = null (no value)
```

**Multiple assignment in one line:**
```python
n, m = 0, "abc"            # n=0, m="abc"
n, m, z = 0.125, "abc", False
```

**Incrementing:**
```python
n = n + 1   # ✅ valid
n += 1      # ✅ shorthand
n++         # ❌ does NOT exist in Python
```

> 💡 `None` is Python's version of `null` — it represents the *absence* of a value.

---

## If-Statements

> No parentheses or curly braces needed — Python uses **indentation** to define blocks.

```python
n = 1
if n > 2:
    n -= 1
elif n == 2:
    n *= 2
else:
    n += 2
```

**Multi-line conditions** (parentheses required to span lines):
```python
n, m = 1, 2
if ((n > 2 and
     n != m) or n == m):
    n += 1
```

| Python | Other Languages |
|--------|----------------|
| `and`  | `&&`           |
| `or`   | `\|\|`          |
| `not`  | `!`            |

---

## Loops

> Python has `while` and `for` loops. `for` loops iterate over a **range or collection**.

**While loop:**
```python
n = 0
while n < 5:
    print(n)
    n += 1
```

**For loop with `range()`:**
```python
for i in range(5):        # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 6):     # 2, 3, 4, 5
    print(i)

for i in range(5, 1, -1): # 5, 4, 3, 2  (countdown)
    print(i)
```

> 💡 `range(start, stop, step)` — `stop` is **exclusive** (not included).

---

## Math

> Python handles math intuitively, but division and negative numbers have some **surprises**.

```python
5 / 2       # → 2.5   (always decimal)
5 // 2      # → 2     (floor division, rounds DOWN)
-3 // 2     # → -2    ⚠️ rounds DOWN, not toward zero!
int(-3 / 2) # → -1    ✅ workaround: convert float to int

10 % 3      # → 1     (modulo)
-10 % 3     # → 2     ⚠️ different from most languages
```

**Using the `math` module:**
```python
import math

math.fmod(-10, 3)   # → -1.0  (consistent with C/Java modulo)
math.floor(3 / 2)   # → 1
math.ceil(3 / 2)    # → 2
math.sqrt(2)        # → 1.414...
math.pow(2, 3)      # → 8.0

# Infinity
float("inf")        # +∞
float("-inf")       # -∞

math.pow(2, 200)               # Python handles huge numbers!
math.pow(2, 200) < float("inf") # → True
```

> 💡 Python integers have **no overflow** — they grow as large as needed.

---

## Arrays (Lists)

> Python calls arrays **lists**. They're ordered, mutable, and can hold mixed types.

**Basics:**
```python
arr = [1, 2, 3]
arr.append(4)       # add to end → [1, 2, 3, 4]
arr.pop()           # remove from end → [1, 2, 3]
arr.insert(1, 7)    # insert 7 at index 1 → [1, 7, 2, 3]
arr[0] = 0          # update by index
```

**Initializing:**
```python
arr = [1] * 5       # [1, 1, 1, 1, 1]
len(arr)            # → 5
```

**Negative indexing:**
```python
arr = [1, 2, 3]
arr[-1]   # → 3  (last element)
arr[-2]   # → 2  (second to last)
```

**Slicing `arr[start:stop]`** — stop is exclusive:
```python
arr = [1, 2, 3, 4]
arr[1:3]   # → [2, 3]
arr[0:4]   # → [1, 2, 3, 4]
arr[0:10]  # → [1, 2, 3, 4]  (no error if out of bounds)
```

**Unpacking:**
```python
a, b, c = [1, 2, 3]   # a=1, b=2, c=3
```

**Looping:**
```python
nums = [1, 2, 3]

for i in range(len(nums)):   # by index
    print(nums[i])

for n in nums:               # by value
    print(n)

for i, n in enumerate(nums): # index AND value
    print(i, n)

# Two lists at once
for n1, n2 in zip([1, 3, 5], [2, 4, 6]):
    print(n1, n2)
```

**Sorting:**
```python
arr = [5, 4, 7, 3, 8]
arr.sort()                        # ascending
arr.sort(reverse=True)            # descending
arr.sort(key=lambda x: len(x))    # custom: sort strings by length
```

**List comprehension** — concise way to build lists:
```python
arr = [i for i in range(5)]       # [0, 1, 2, 3, 4]

# 2D list (4x4 grid of zeros)
arr = [[0] * 4 for i in range(4)]

# ⚠️ Don't use this — all rows share the same reference!
# arr = [[0] * 4] * 4
```

---

## Strings

> Strings behave like lists of characters, but they are **immutable** (can't be changed in place).

```python
s = "abc"
s[0:2]      # → "ab"  (slicing works like lists)
# s[0] = "A"  ❌ immutable — this will throw an error

s += "def"  # ✅ creates a NEW string "abcdef"
```

**Type conversion:**
```python
int("123") + int("123")   # → 246  (string → int)
str(123) + str(123)       # → "123123"  (int → string)
```

**ASCII value:**
```python
ord("a")   # → 97
ord("b")   # → 98
```

**Joining strings:**
```python
strings = ["ab", "cd", "ef"]
"".join(strings)    # → "abcdef"
"-".join(strings)   # → "ab-cd-ef"
```

---

## Queues

> A **deque** (double-ended queue) lets you efficiently add/remove from **both ends** — unlike a list where removing from the front is slow.

```python
from collections import deque

queue = deque()
queue.append(1)      # add to right  → deque([1])
queue.append(2)      # add to right  → deque([1, 2])
queue.popleft()      # remove left   → deque([2])
queue.appendleft(1)  # add to left   → deque([1, 2])
queue.pop()          # remove right  → deque([1])
```

| Method          | Side    | Action  |
|-----------------|---------|---------|
| `append(x)`     | Right   | Add     |
| `appendleft(x)` | Left    | Add     |
| `pop()`         | Right   | Remove  |
| `popleft()`     | Left    | Remove  |

---

## HashSets

> A **set** stores **unique, unordered** values. Great for fast membership checks (`in`).

```python
mySet = set()
mySet.add(1)
mySet.add(2)
mySet.add(2)   # duplicate — ignored!

len(mySet)     # → 2
1 in mySet     # → True
3 in mySet     # → False
mySet.remove(2)

# Convert list to set (removes duplicates)
set([1, 2, 2, 3])   # → {1, 2, 3}

# Set comprehension
mySet = {i for i in range(5)}   # {0, 1, 2, 3, 4}
```

> 💡 Use a set when you need to check **"have I seen this before?"** — it's O(1) time.

---

## HashMaps (Dicts)

> A **dict** stores **key → value** pairs. Keys must be unique.

```python
myMap = {}
myMap["alice"] = 88
myMap["bob"] = 77
myMap["alice"] = 80   # overwrites previous value

len(myMap)            # → 2
myMap["alice"]        # → 80

"alice" in myMap      # → True  (key lookup)
myMap.pop("alice")    # removes key
"alice" in myMap      # → False
```

**Inline initialization:**
```python
myMap = {"alice": 90, "bob": 70}
```

**Dict comprehension:**
```python
myMap = {i: 2*i for i in range(3)}   # {0: 0, 1: 2, 2: 4}
```

**Looping:**
```python
for key in myMap:              # keys only
    print(key, myMap[key])

for val in myMap.values():     # values only
    print(val)

for key, val in myMap.items(): # both
    print(key, val)
```

---

## Tuples

> Tuples are like lists but **immutable**. Because they can't change, they can be used as **dictionary keys or set elements**.

```python
tup = (1, 2, 3)
tup[0]    # → 1
tup[-1]   # → 3
# tup[0] = 0  ❌ immutable

# Use as dict key (lists can't do this!)
myMap = {(1, 2): 3}
myMap[(1, 2)]   # → 3

# Use in a set
mySet = set()
mySet.add((1, 2))
(1, 2) in mySet   # → True

# myMap[[3, 4]] = 5  ❌ lists are NOT hashable
```

> 💡 Rule of thumb: use a **tuple** when data shouldn't change (coordinates, RGB values, etc.).

---

## Heaps

> A **heap** is a data structure that always gives you the **smallest (or largest) element first** in O(log n) time.

```python
import heapq

# Min-heap (smallest element at top)
minHeap = []
heapq.heappush(minHeap, 3)
heapq.heappush(minHeap, 2)
heapq.heappush(minHeap, 4)

minHeap[0]              # → 2  (peek at min, no removal)
heapq.heappop(minHeap)  # → 2  (remove and return min)
heapq.heappop(minHeap)  # → 3
heapq.heappop(minHeap)  # → 4
```

**Max-heap workaround** (negate values):
```python
# Python only has min-heap, so negate to simulate max-heap
maxHeap = []
heapq.heappush(maxHeap, -3)
heapq.heappush(maxHeap, -2)
heapq.heappush(maxHeap, -4)

-1 * maxHeap[0]              # → 4  (actual max)
-1 * heapq.heappop(maxHeap)  # → 4
-1 * heapq.heappop(maxHeap)  # → 3
-1 * heapq.heappop(maxHeap)  # → 2
```

**Build heap from existing list:**
```python
arr = [2, 1, 8, 4, 5]
heapq.heapify(arr)   # rearranges in-place to satisfy heap property
while arr:
    print(heapq.heappop(arr))   # prints: 1, 2, 4, 5, 8
```

| Operation       | Time Complexity |
|-----------------|-----------------|
| `heappush`      | O(log n)        |
| `heappop`       | O(log n)        |
| `heapify`       | O(n)            |
| Peek `heap[0]`  | O(1)            |

---

## Functions

> Functions are defined with `def`. Python supports **nested functions** and **closures**.

```python
def myFunc(n, m):
    return n * m

myFunc(3, 4)   # → 12
```

**Nested functions** (inner function can access outer variables):
```python
def outer(a, b):
    c = "c"
    def inner():
        return a + b + c   # accesses a, b, c from outer scope
    return inner()

outer("a", "b")   # → "abc"
```

**`nonlocal` keyword** — modify a variable from the enclosing scope:
```python
def double(arr, val):
    def helper():
        for i, n in enumerate(arr):
            arr[i] *= 2    # ✅ mutating a list works without nonlocal

        nonlocal val       # required to reassign (not just mutate)
        val *= 2
    helper()
    print(arr, val)

double([1, 2], 3)   # → [2, 4] 6
```

> 💡 You can **mutate** objects (like lists) without `nonlocal`, but you need `nonlocal` to **reassign** a variable.

---

## Classes

> Classes bundle **data** (attributes) and **behavior** (methods) together.

```python
class MyClass:
    # __init__ is the constructor — runs when you create an object
    def __init__(self, nums):
        self.nums = nums        # instance variable
        self.size = len(nums)   # instance variable

    # 'self' refers to the current instance (like 'this' in Java/C++)
    def getLength(self):
        return self.size

    def getDoubleLength(self):
        return 2 * self.getLength()   # can call other methods via self


myObj = MyClass([1, 2, 3])
myObj.getLength()        # → 3
myObj.getDoubleLength()  # → 6
```

| Concept         | Python          | Java/C++ equivalent |
|-----------------|-----------------|---------------------|
| Constructor     | `__init__`      | `ClassName()`       |
| Current instance| `self`          | `this`              |
| Member variable | `self.x = ...`  | `this.x = ...`      |

---

*Happy coding! 🚀*
