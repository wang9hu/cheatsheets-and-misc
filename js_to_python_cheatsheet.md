# JS → Python Cheatsheet

A quick, editable mapping from common JavaScript methods to their Python equivalents.

## Table of Contents

- [JS → Python Cheatsheet](#js--python-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Python Basics](#python-basics)
    - [Variables and Types](#variables-and-types)
    - [Operators](#operators)
    - [Conditionals](#conditionals)
    - [Loops](#loops)
    - [Functions](#functions)
    - [Conventions (PEP 8 highlights)](#conventions-pep-8-highlights)
    - [Input / Output](#input--output)
    - [Comments \& Docstrings](#comments--docstrings)
    - [Example: Factorial](#example-factorial)
    - [Names \& Binding](#names--binding)
    - [Slicing](#slicing)
    - [Strings \& f-strings](#strings--f-strings)
    - [Scope (LEGB)](#scope-legb)
    - [Exceptions](#exceptions)
    - [Context Managers \& Files](#context-managers--files)
    - [Iterables \& `itertools`](#iterables--itertools)
    - [Data Classes \& Pattern Matching](#data-classes--pattern-matching)
    - [Type Hints](#type-hints)
    - [Standard Library Quick Wins](#standard-library-quick-wins)
    - [CLI, Environments, Testing](#cli-environments-testing)
    - [Concurrency \& Performance](#concurrency--performance)
  - [Strings](#strings)
  - [Arrays-Lists](#arrays-lists)
  - [Objects-Dicts](#objects-dicts)
  - [Map-Set](#map-set)
  - [Tuples-Immutability](#tuples-immutability)
  - [Comprehensions-Iterators](#comprehensions-iterators)
  - [Numbers-Math](#numbers-math)
  - [Dates-Time](#dates-time)
  - [Regex](#regex)
  - [Errors-Control Flow](#errors-control-flow)
  - [Modules-Imports](#modules-imports)
  - [Classes-Methods](#classes-methods)
  - [Async-Promises](#async-promises)
  - [Truthiness, Nullish-Coalescing](#truthiness-nullish-coalescing)
  - [Copying-Equality](#copying-equality)
  - [Common Built-in Helpers](#common-built-in-helpers)
  - [Dict Patterns You’ll Use Often](#dict-patterns-youll-use-often)
    - [Notes / Gotchas](#notes--gotchas)

---

## Python Basics

### Variables and Types

```python
x = 10              # int
y = 3.14            # float
name = "Alice"      # str
is_active = True    # bool
nums = [1, 2, 3]    # list
```

- **Dynamic typing:** no need to declare types explicitly.
- Use `type(x)` to inspect, `isinstance(x, int)` for type checking.

---

### Operators

| **Type**       | **Examples**                  | **Notes**                         |
| -------------- | ----------------------------- | --------------------------------- |
| **Arithmetic** | `+` `-` `*` `/` `//` `%` `**` | `//` floor-divides; `**` is power |
| **Comparison** | `==` `!=` `>` `<` `>=` `<=`   | Returns `bool`                    |
| **Logical**    | `and` `or` `not`              | No `&&` or `\|\|`; short-circuits |
| **Membership** | `in` `not in`                 | `'a' in 'cat'` → `True`           |
| **Identity**   | `is` `is not`                 | Object identity, not equality     |
| **Bitwise**    | `&` `\|` `^` `~` `<<` `>>`    | Bit operations                    |

**Truthiness (falsy):** `False, 0, 0.0, '', [], {}, set(), None`.

---

### Conditionals

```python
x = 10
if x > 0:
    print("positive")
elif x == 0:
    print("zero")
else:
    print("negative")
```

---

### Loops

```python
# For
for i in range(5):
    print(i)

# While
n = 3
while n:
    n -= 1

# Loop control with else
for x in data:
    if x == 0:
        continue
    if x < 0:
        break
else:
    print("completed without break")
```

**Everyday patterns**

```python
for i, item in enumerate(items, start=1): ...
for a, b in zip(xs, ys): ...
squares = [n*n for n in range(10) if n % 2 == 0]  # comprehension
```

---

### Functions

```python
def add(a, b=0):
    return a + b

def greet(name: str) -> str:
    return f"Hello, {name}"
```

- Default args & type hints are optional.
- Functions are first-class (can be passed or stored).

**Parameters in practice**

```python
def f(pos, /, a, b=0, *args, key, **kwargs):
    ...
```

- `/` = positional-only; `*` = keyword-only after it.

---

### Conventions (PEP 8 highlights)

| **Element**         | **Convention**            |
| ------------------- | ------------------------- |
| Variable / function | `snake_case`              |
| Class name          | `PascalCase`              |
| Constant            | `UPPER_CASE`              |
| Indentation         | 4 spaces                  |
| Imports             | one per line, at top      |
| Docstrings          | triple quotes `"""..."""` |
| Line length         | ≤ 79 chars (recommended)  |

---

### Input / Output

```python
name = input("Name: ")
print(f"Hello, {name}")
```

---

### Comments & Docstrings

```python
# single line
"""
This is a docstring.
It can span multiple lines.
"""
```

---

### Example: Factorial

```python
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

print(factorial(5))  # 120
```

---

### Names & Binding

- Names point to objects: `a = [1,2]; b = a` → same list.
- Copy when needed: `b = a[:]` / `list(a)`; deep copy with `copy.deepcopy`.

```python
x, y = 1, 2
x, y = y, x
head, *middle, tail = [1,2,3,4,5]
```

### Slicing

```python
a = [0,1,2,3,4,5]
a[1:4]; a[:3]; a[-3:]; a[::2]; a[::-1]
```

### Strings & f-strings

```python
s = "Pythonic"
s.upper(), s.split(), "-".join(["a","b"])
f"Hello {s.lower()}!"
x = 1234.567
f"{x:,.2f}"
```

### Scope (LEGB)

```python
x = 0
def outer():
    x = 1
    def inner():
        nonlocal x
        x += 1
    inner()
    return x
```

### Exceptions

```python
try:
    price = float(s)
except ValueError:
    price = 0.0
```

### Context Managers & Files

```python
from pathlib import Path
with Path("notes.txt").open("w", encoding="utf-8") as f:
    f.write("hello\n")
```

### Iterables & `itertools`

```python
from itertools import islice, count
list(islice(count(10,2), 5))  # [10,12,14,16,18]
```

### Data Classes & Pattern Matching

```python
from dataclasses import dataclass
@dataclass(slots=True)
class Point:
    x: int
    y: int
```

```python
def render(shape):
    match shape:
        case {"type":"circle","r": r}: return f"Circle r={r}"
        case [x, y, *_]: return f"Seq {x},{y}"
        case _: return "Unknown"
```

### Type Hints

```python
from typing import Iterable, TypedDict, Protocol

def take(n: int, xs: Iterable[int]) -> list[int]: ...

class User(TypedDict):
    id: int
    name: str

class Sized(Protocol):
    def __len__(self) -> int: ...
```

### Standard Library Quick Wins

```python
from collections import Counter, defaultdict, deque
from functools import lru_cache
```

### CLI, Environments, Testing

```bash
python -m venv .venv
```

```python
# pytest
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
```

### Concurrency & Performance

```python
import asyncio
async def hello():
    return "hi"
```

```python
# Mutable default pattern
def good(x, seen=None):
    seen = [] if seen is None else seen
```

---

## Strings

| **Concept**               | JavaScript                                                | Python                                                            |
| ------------------------- | --------------------------------------------------------- | ----------------------------------------------------------------- |
| **Length**                | `str.length`                                              | `len(s)`                                                          |
| **Contains**              | `str.includes(x)`                                         | `x in s`                                                          |
| **Index / Last index**    | `str.indexOf(x)` / `str.lastIndexOf(x)`                   | `s.find(x)` / `s.rfind(x)` _(−1 if not found)_                    |
| **Starts / Ends with**    | `str.startsWith(x)` / `str.endsWith(x)`                   | `s.startswith(x)` / `s.endswith(x)`                               |
| **Slice / Substring**     | `str.slice(i, j)` / `str.substring(i, j)`                 | `s[i:j]`; `s[-n:]`, `s[:n]`                                       |
| **Case**                  | `toUpperCase()` / `toLowerCase()` / `toLocaleUpperCase()` | `s.upper()` / `s.lower()` / `s.casefold()`                        |
| **Trim**                  | `trim()` / `trimStart()` / `trimEnd()`                    | `s.strip()` / `s.lstrip()` / `s.rstrip()`                         |
| **Split / Join**          | `s.split(',')` / `arr.join(',')`                          | `s.split(',')` / `','.join(arr)` _(all elements must be strings)_ |
| **Replace / Replace all** | `s.replace(a,b)` / `s.replaceAll(a,b)`                    | `s.replace(a, b, count)`; regex: `re.sub(pat, repl, s, count=0)`  |
| **Pad**                   | `padStart(n,ch)` / `padEnd(n,ch)`                         | `s.rjust(n, ch)` / `s.ljust(n, ch)`; zeros: `s.zfill(n)`          |
| **Repeat**                | `str.repeat(n)`                                           | `s * n`                                                           |
| **Regex match / test**    | `str.match(re)` / `re.test(s)`                            | `re.findall(p, s)` / `bool(re.search(p, s))`                      |
| **Template literal**      | ` `Hi ${x}` `                                             | `f"Hi {x}"`                                                       |
| **To string**             | `String(x)`                                               | `str(x)`                                                          |
| **Code point**            | `str.codePointAt(i)` / `String.fromCodePoint(n)`          | `ord(s[i])` / `chr(n)`                                            |

---

## Arrays-Lists

| **Concept**                 | JavaScript                             | Python                                                                                   |
| --------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Literal / Length**        | `[]` / `.length`                       | `[]` / `len(a)`                                                                          |
| **Push / Pop (end)**        | `a.push(x)` / `a.pop()`                | `a.append(x)` / `a.pop()`                                                                |
| **Shift / Unshift (front)** | `a.shift()` / `a.unshift(x)`           | `a.pop(0)` / `a.insert(0, x)` _(prefer `collections.deque` for heavy front ops)_         |
| **Random access / assign**  | `a[i]` / `a[i] = v`                    | same                                                                                     |
| **Slice / Splice**          | `a.slice(i,j)` / `a.splice(i,k,...xs)` | `a[i:j]` / `a[i:i+k] = xs`                                                               |
| **Concat / Extend**         | `a.concat(b)`                          | `a + b` or `a.extend(b)`                                                                 |
| **Copy (shallow)**          | `[...a]` / `Array.from(a)`             | `a[:]` or `list(a)` _(deep: `copy.deepcopy(a)`)_                                         |
| **Search / Includes**       | `a.indexOf(x)` / `a.includes(x)`       | `a.index(x)` _(raises `ValueError` if not found)_ / `x in a`                             |
| **Find / FindIndex**        | `arr.find(fn)` / `arr.findIndex(fn)`   | `next((x for x in a if fn(x), None))` / `next((i for i,x in enumerate(a) if fn(x)), -1)` |
| **Filter / Map**            | `arr.filter(fn)` / `arr.map(fn)`       | `[x for x in a if fn(x)]` / `[fn(x) for x in a]`                                         |
| **Reduce**                  | `reduce(fn, init)`                     | `functools.reduce(fn, a, init)` _(often `sum`, `any`, `all`)_                            |
| **Some / Every**            | `some(fn)` / `every(fn)`               | `any(fn(x) for x in a)` / `all(fn(x) for x in a)`                                        |
| **Sort**                    | `arr.sort()` / custom compare          | `a.sort(key=..., reverse=True)`; non‑mutating: `sorted(a, key=..., reverse=...)`         |
| **Reverse**                 | `arr.reverse()`                        | `a.reverse()`; non‑mutating: `a[::-1]`                                                   |
| **Flat / FlatMap**          | `arr.flat(d=1)` / `arr.flatMap(fn)`    | `itertools.chain.from_iterable(a)` / `[y for x in a for y in fn(x)]`                     |
| **Unique**                  | `Array.from(new Set(a))`               | `list(dict.fromkeys(a))` _(preserves order)_ or `list(set(a))`                           |
| **Fill**                    | `a.fill(v, i, j)`                      | `a[i:j] = [v] * (j-i)`                                                                   |
| **Repeat N times**          | `Array(n).fill(v)`                     | `[v] * n`                                                                                |

---

## Objects-Dicts

| **Concept**                     | JavaScript                                 | Python                                           |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------ |
| **Literal / Access**            | `{ a:1 }`, `o.k` / `o['k']`                | `{'a':1}`, `d['k']`                              |
| **Optional chaining / default** | `o?.k` / `o.k ?? def`                      | `d.get('k')` / `d.get('k', default)`             |
| **Existence**                   | `'k' in o` / `hasOwnProperty('k')`         | `'k' in d`                                       |
| **Keys / Values / Entries**     | `Object.keys/values/entries(o)`            | `d.keys()` / `d.values()` / `d.items()`          |
| **Merge**                       | `Object.assign({}, a, b)` / `{...a, ...b}` | `{**a, **b}`; in‑place: `d.update(other)`        |
| **Delete**                      | `delete o.k`                               | `del d['k']`                                     |
| **Get‑or‑set**                  | `o[k] ??= v`                               | `d.setdefault(k, v)`                             |
| **Deep get**                    | `o?.a?.b`                                  | `d.get('a', {}).get('b')`                        |
| **Iterate**                     | `for (k,v of Object.entries(o))`           | `for k, v in d.items():`                         |
| **Copy**                        | `{...d}`                                   | `d.copy()` _(shallow); deep: `copy.deepcopy(d)`_ |
| **From entries**                | `Object.fromEntries(pairs)`                | `dict(pairs)`                                    |
| **From keys**                   | -                                          | `dict.fromkeys(keys, value)`                     |
| **Unpack (spread)**             | `{...a, x:1}`                              | `{**a, 'x':1}`                                   |

---

## Map-Set

| **Concept**                        | JavaScript                                             | Python                                                                     |
| ---------------------------------- | ------------------------------------------------------ | -------------------------------------------------------------------------- |
| **Map literal / size**             | `new Map(iter)` / `m.size`                             | `dict(iter)` / `len(d)`                                                    |
| **Map get / set / has / delete**   | `m.get(k)` / `m.set(k,v)` / `m.has(k)` / `m.delete(k)` | `d.get(k)` / `d[k]=v` / `k in d` / `del d[k]`                              |
| **Map iterate**                    | `for (k,v) of m`                                       | `for k, v in d.items()`                                                    |
| **Set literal**                    | `new Set([1,2])`                                       | `set([1,2])` or `{1,2}`                                                    |
| **Set add / has / delete / clear** | `s.add(x)` / `s.has(x)` / `s.delete(x)` / `s.clear()`  | `s.add(x)` / `x in s` / `s.remove(x)` (safe: `s.discard(x)`) / `s.clear()` |
| **Set unions / intersections**     | `s.union(t)` / `s.intersection(t)`                     | `s \| t` / `s & t` (in-place: `\|=`, `&=`)                                 |
| **Set difference / symmetric**     | _(manual only)_                                        | `s - t` / `s ^ t` (in-place: `-=`, `^=`)                                   |
| **Subset / Superset**              | `s.isSubsetOf(t)` / `s.isSupersetOf(t)`                | `s <= t` / `s >= t`                                                        |
| **Frozen set**                     | -                                                      | `frozenset(iter)`                                                          |

---

## Tuples-Immutability

| **Concept**              | JavaScript           | Python        |
| ------------------------ | -------------------- | ------------- |
| **Python tuple literal** | -                    | `(a, b)`      |
| **Unpack**               | `const [x, y] = arr` | `x, y = tup`  |
| **Swap**                 | `[a, b] = [b, a]`    | `a, b = b, a` |

---

## Comprehensions-Iterators

| **Concept**          | JavaScript                                  | Python                                        |
| -------------------- | ------------------------------------------- | --------------------------------------------- |
| **Map**              | `arr.map(f)`                                | `[f(x) for x in a]`                           |
| **Filter**           | `arr.filter(p)`                             | `[x for x in a if p(x)]`                      |
| **FlatMap**          | `arr.flatMap(f)`                            | `[y for x in a for y in f(x)]`                |
| **Dict comp**        | `Object.fromEntries(arr.map(([k,v])=>...))` | `{k: f(v) for k, v in pairs}`                 |
| **Set comp**         | `new Set(arr.map(...))`                     | `{f(x) for x in a}`                           |
| **Generator (lazy)** | `function*(){...}`                          | `(f(x) for x in a)` or `def gen(): yield ...` |
| **Enumerate**        | `arr.entries()`                             | `enumerate(a)`                                |
| **Zip**              | -                                           | `zip(a, b)`                                   |

---

## Numbers-Math

| **Concept**              | JavaScript                                         | Python                                                  |
| ------------------------ | -------------------------------------------------- | ------------------------------------------------------- |
| **Round / Floor / Ceil** | `Math.round(x)` / `Math.floor(x)` / `Math.ceil(x)` | `round(x)` / `math.floor(x)` / `math.ceil(x)`           |
| **Abs / Sign**           | `Math.abs(x)` / `Math.sign(x)`                     | `abs(x)` / `(x>0)-(x<0)`                                |
| **Random / randint**     | `Math.random()`                                    | `random.random()` / `random.randint(a,b)` _(inclusive)_ |
| **Parse int / float**    | `parseInt(s, base)` / `parseFloat(s)`              | `int(s, base)` / `float(s)`                             |
| **NaN / finite**         | `Number.isNaN(x)` / `isFinite(x)`                  | `math.isnan(x)` / `math.isfinite(x)`                    |
| **BigInt**               | `123n`                                             | `int` _(arbitrary precision)_                           |
| **Format**               | `x.toFixed(2)` / `toExponential()`                 | `f"{x:.2f}"` / `f"{x:.2e}"`                             |

---

## Dates-Time

| **Concept**         | JavaScript                  | Python                                                                |
| ------------------- | --------------------------- | --------------------------------------------------------------------- |
| **Now / Construct** | `Date.now()` / `new Date()` | `time.time()` / `datetime.now()`                                      |
| **ISO**             | `d.toISOString()`           | `dt.astimezone(timezone.utc).isoformat()`                             |
| **Add / Subtract**  | `d ± days`                  | `dt ± timedelta(days=n)`                                              |
| **Parse**           | `new Date('2025-01-02')`    | `datetime.fromisoformat('2025-01-02')` / `datetime.strptime(s, fmt)`  |
| **Format**          | `d.toLocaleString()`        | `dt.strftime('%Y-%m-%d %H:%M:%S')`                                    |
| **Timezones**       | `Intl`                      | `zoneinfo` / `pytz`; `dt.astimezone(ZoneInfo('America/Los_Angeles'))` |

---

## Regex

| **Concept**         | JavaScript                  | Python                                      |
| ------------------- | --------------------------- | ------------------------------------------- |
| **Literal / flags** | `/pat/i`                    | `re.compile(r'pat', re.I)`                  |
| **Test / Exec**     | `re.test(s)` / `re.exec(s)` | `bool(re.search(p, s))` / `re.search(p, s)` |
| **Match all**       | `s.matchAll(re)`            | `re.finditer(p, s)`                         |
| **Replace**         | `s.replace(re, repl)`       | `re.sub(p, repl, s)`                        |
| **Groups**          | `m[1]` / named              | `m.group(1)` / `m.group('name')`            |

---

## Errors-Control Flow

```js
// JavaScript
try {
  /* ... */
} catch (e) {
  /* ... */
} finally {
  /* ... */
}
throw new Error('msg');
class MyError extends Error {}
```

```python
# Python
try:
    ...
except Exception as e:
    ...
finally:
    ...
raise Exception('msg')
class MyError(Exception):
    pass
```

---

## Modules-Imports

| **Concept**                | JavaScript                                       | Python                                                                                        |
| -------------------------- | ------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| **Import named / default** | `import {x as y} from 'm'` / `import x from 'm'` | `from m import x as y` / `import m`                                                           |
| **Export**                 | `export function f(){}` / `export default`       | define in module; import with `from mod import f` / `import mod`                              |
| **JSON**                   | `JSON.stringify(o)` / `JSON.parse(s)`            | `json.dumps(d)` / `json.loads(s)`                                                             |
| **File I/O**               | `fs.readFileSync(p, 'utf8')`                     | `open(p).read()`; write: `open(p,'w').write(txt)`; safe: `with open(p) as f: data = f.read()` |

---

## Classes-Methods

| **Concept**               | JavaScript                | Python                                                                |
| ------------------------- | ------------------------- | --------------------------------------------------------------------- |
| **Instance method**       | `obj.method()`            | `def m(self, x): ...`                                                 |
| **Static / Class method** | `static s(){}`            | `@staticmethod def s(...): ...` / `@classmethod def c(cls, ...): ...` |
| **Property**              | getters / setters         | `@property` / `@x.setter`                                             |
| **this / self**           | `this` bound at call time | `self` explicit argument                                              |

---

## Async-Promises

| **Concept**              | JavaScript                               | Python                          |
| ------------------------ | ---------------------------------------- | ------------------------------- |
| **Awaiting HTTP + JSON** | `await fetch(url).then(r=>r.json())`     | `aiohttp` with `await r.json()` |
| **Sleep**                | `await new Promise(r=>setTimeout(r,ms))` | `await asyncio.sleep(sec)`      |
| **Concurrent**           | `Promise.all([...])`                     | `await asyncio.gather(*coros)`  |

---

## Truthiness, Nullish-Coalescing

| **Concept**            | JavaScript                                   | Python                                               |
| ---------------------- | -------------------------------------------- | ---------------------------------------------------- |
| **Falsy values**       | `false, 0, '', null, undefined, NaN`         | `False, 0, 0.0, '', [], {}, set(), None`             |
| **Nullish coalescing** | `a ?? b`                                     | `a if a is not None else b`                          |
| **Or with truthiness** | `a                                   \|\| b` | `a or b` _(treats empty as False)_                   |
| **Optional chaining**  | `a?.b?.c`                                    | `getattr(a, 'b', None)` chaining / nested `dict.get` |

---

## Copying-Equality

| **Concept**             | JavaScript                                    | Python                              |
| ----------------------- | --------------------------------------------- | ----------------------------------- |
| **Shallow / Deep copy** | `Object.assign({}, o)` / `structuredClone(o)` | `copy.copy(o)` / `copy.deepcopy(o)` |
| **Equality**            | `==` (coercive), `===` (strict)               | `==` (value), `is` (identity)       |

---

## Common Built-in Helpers

| **Concept**              | JavaScript                 | Python                                                                             |
| ------------------------ | -------------------------- | ---------------------------------------------------------------------------------- |
| **Range / Times**        | `[...Array(n).keys()]`     | `list(range(n))`                                                                   |
| **Sort by key**          | `arr.sort((a,b)=>a.k-b.k)` | `a.sort(key=lambda x: x.k)`                                                        |
| **GroupBy**              | custom reduce              | `itertools.groupby(sorted(a, key=key), key=key)` / `collections.defaultdict(list)` |
| **Counters / Multisets** | -                          | `collections.Counter(iter)`                                                        |
| **Default dict**         | -                          | `collections.defaultdict(T)`                                                       |

---

## Dict Patterns You’ll Use Often

| **Concept**            | JavaScript | Python                                           |
| ---------------------- | ---------- | ------------------------------------------------ |
| **Safe read**          | -          | `d.get(k, default)`                              |
| **Set default once**   | -          | `d.setdefault(k, init)`                          |
| **Merge with compute** | -          | `for k, v in new.items(): d[k] = f(d.get(k), v)` |
| **Update many**        | -          | `d.update(other)`                                |
| **Pop with default**   | -          | `d.pop(k, default)`                              |

---

### Notes / Gotchas

- `list.index(x)` **raises** `ValueError` if not found (JS `indexOf` returns `-1`).
- Python sets: use `s.discard(x)` if you don’t want an error when the element is missing (JS `delete` is silent).
- Python strings are immutable like JS strings.
