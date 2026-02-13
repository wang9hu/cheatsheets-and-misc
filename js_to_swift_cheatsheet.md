# JS → Swift Cheatsheet

A quick, editable mapping from common JavaScript patterns/APIs to their Swift equivalents (Swift 5.9+/Swift Concurrency, Foundation).

## Table of Contents

- [JS → Swift Cheatsheet](#js--swift-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Swift Basics](#swift-basics)
    - [Variables and Types](#variables-and-types)
    - [Operators](#operators)
    - [Conditionals](#conditionals)
    - [Loops](#loops)
    - [Functions](#functions)
    - [Closures](#closures)
    - [Optionals](#optionals)
    - [Value vs Reference Types](#value-vs-reference-types)
    - [Access Control & Conventions](#access-control--conventions)
    - [Input / Output](#input--output)
    - [Comments & Documentation](#comments--documentation)
    - [Example: Factorial](#example-factorial)
    - [Pattern Matching & `switch`](#pattern-matching--switch)
    - [Error Handling](#error-handling)
    - [Files & Paths](#files--paths)
    - [Generics & Protocols](#generics--protocols)
    - [Type System Quick Wins](#type-system-quick-wins)
    - [Testing](#testing)
    - [Concurrency & Performance](#concurrency--performance)
  - [Strings](#strings)
  - [Arrays](#arrays)
  - [Objects-Dicts](#objects-dicts)
  - [Map-Set](#map-set)
  - [Tuples & Immutability](#tuples--immutability)
  - [Functional Patterns](#functional-patterns)
  - [Numbers & Math](#numbers--math)
  - [Dates & Time](#dates--time)
  - [Regex](#regex)
  - [Errors & Control Flow](#errors--control-flow)
  - [Modules & Imports](#modules--imports)
  - [Types: Structs, Classes, Enums](#types-structs-classes-enums)
  - [Async & Promises](#async--promises)
  - [Truthiness, Nullish-Coalescing](#truthiness-nullish-coalescing)
  - [Copying & Equality](#copying--equality)
  - [JSON & Codable](#json--codable)
  - [Common Helpers](#common-helpers)
  - [Dictionary Patterns You’ll Use Often](#dictionary-patterns-youll-use-often)
    - [Notes / Gotchas](#notes--gotchas)

---

## Swift Basics

### Variables and Types

```swift
let x: Int = 10              // immutable binding
var y: Double = 3.14         // mutable binding
let name: String = "Alice"
let isActive: Bool = true
let nums: [Int] = [1, 2, 3]
let dict: [String: Int] = ["a": 1]
```

- `let` = constant binding; `var` = variable binding.
- Swift is **statically typed**, but type inference is strong:
  ```swift
  let n = 42         // Int
  let pi = 3.14159   // Double
  ```

---

### Operators

| **Type**       | **JS**                        | **Swift**                                  | **Notes** |
| -------------- | ----------------------------- | ------------------------------------------ | --------- |
| Arithmetic     | `+ - * / % **`                | `+ - * / %`                                | No `**`; use `pow` from Foundation/Darwin |
| Comparison     | `== != > < >= <=`             | `== != > < >= <=`                          | Strong typing; no coercion |
| Logical        | `&& || !`                     | `&& || !`                                  | Short-circuits |
| Nullish        | `a ?? b`                      | `a ?? b`                                   | Same operator exists |
| Ternary        | `cond ? a : b`                | `cond ? a : b`                             | Same shape |
| Optional chain | `obj?.a?.b`                   | `obj?.a?.b`                                | Works with Optionals |
| Range          | -                             | `0..<n`, `0...n`                           | Half-open vs closed |
| Bitwise        | `& | ^ ~ << >>`               | `& | ^ ~ << >>`                            | Same symbols |
| Identity       | `Object.is` / reference checks| `===` / `!==`                              | Only for class instances |

---

### Conditionals

```swift
let x = 10

if x > 0 {
  print("positive")
} else if x == 0 {
  print("zero")
} else {
  print("negative")
}
```

---

### Loops

```swift
// for-in
for i in 0..<5 {
  print(i)
}

// iterate items
for item in nums {
  print(item)
}

// while
var n = 3
while n > 0 {
  n -= 1
}
```

**Everyday patterns**

```swift
for (i, item) in nums.enumerated() { ... } // i is Int
for (a, b) in zip([1,2,3], [4,5,6]) { ... } // (a,b) tuples
```

---

### Functions

```swift
func add(_ a: Int, _ b: Int = 0) -> Int {
  a + b
}

func greet(name: String) -> String {
  "Hello, \(name)"
}
```

- External parameter labels matter:
  ```swift
  func move(from start: Int, to end: Int) { ... }
  move(from: 1, to: 10)
  ```

---

### Closures

JS:
```js
const f = (x) => x * 2;
```

Swift:
```swift
let f: (Int) -> Int = { x in x * 2 }

// shorthand
let g: (Int) -> Int = { $0 * 2 }
```

Capturing variables is common:
```swift
var count = 0
let inc = { count += 1 }  // captures by reference for var in outer scope
```

---

### Optionals

Swift uses `Optional<T>` instead of `null/undefined`.

```swift
var maybeName: String? = nil
maybeName = "Ada"
```

- **Unwrap safely**
  ```swift
  if let name = maybeName {
    print(name)
  }
  ```
- **Guard**
  ```swift
  func printUpper(_ s: String?) {
    guard let s else { return }
    print(s.uppercased())
  }
  ```
- **Default value**
  ```swift
  let display = maybeName ?? "Anonymous"
  ```
- **Optional chaining**
  ```swift
  let length = maybeName?.count
  ```

---

### Value vs Reference Types

| Concept | JS | Swift |
|---|---|---|
| Value types | primitives | `struct`, `enum`, `String`, `Array`, `Dictionary`, `Set` |
| Reference types | objects/functions | `class`, `actor` |

- `Array`, `Dictionary`, `String` are **value types** with copy-on-write (efficient).
- Only `class` instances compare identity with `===`.

---

### Access Control & Conventions

| Element | Swift convention |
|---|---|
| Type names | `PascalCase` |
| Functions/vars | `camelCase` |
| Constants | `camelCase` (no enforced all-caps) |
| Access | `private`, `fileprivate`, `internal` (default), `public`, `open` |
| Files | one type per file when practical |
| Doc comments | `///` for symbols |

---

### Input / Output

Swift (command-line):

```swift
print("Name: ", terminator: "")
let name = readLine() ?? "Anonymous"
print("Hello, \(name)")
```

---

### Comments & Documentation

```swift
// single line
/*
 multi-line
 */
/// Doc comment for a symbol
```

---

### Example: Factorial

```swift
func factorial(_ n: Int) -> Int {
  guard n >= 0 else { return 0 }
  return (1...max(1, n)).reduce(1, *)
}

print(factorial(5)) // 120
```

---

### Pattern Matching & `switch`

```swift
let v = 3

switch v {
case 0:
  print("zero")
case 1...3:
  print("one to three")
default:
  print("other")
}
```

Tuples + `where`:
```swift
let point = (x: 2, y: -1)
switch point {
case let (x, y) where x == y:
  print("diagonal")
case (_, let y) where y < 0:
  print("below axis")
default:
  break
}
```

---

### Error Handling

```swift
enum ParseError: Error {
  case invalidNumber
}

func parseInt(_ s: String) throws -> Int {
  guard let n = Int(s) else { throw ParseError.invalidNumber }
  return n
}

do {
  let n = try parseInt("123")
  print(n)
} catch {
  print("Error:", error)
}
```

- `try?` turns errors into `nil`
- `try!` crashes if an error is thrown

---

### Files & Paths

```swift
import Foundation

let url = URL(fileURLWithPath: "/tmp/notes.txt")
try "hello\n".write(to: url, atomically: true, encoding: .utf8)

let text = try String(contentsOf: url, encoding: .utf8)
```

---

### Generics & Protocols

```swift
func first<T>(_ xs: [T]) -> T? { xs.first }

protocol Sized {
  var count: Int { get }
}
```

---

### Type System Quick Wins

```swift
// typealias
typealias UserID = String

// Result
func load() -> Result<Data, Error> { ... }
```

---

### Testing

Using XCTest:

```swift
import XCTest

final class MyTests: XCTestCase {
  func testAdd() {
    XCTAssertEqual(2 + 3, 5)
  }
}
```

---

### Concurrency & Performance

- `async/await` + `Task` for structured concurrency.
- Prefer value types; Swift collections are copy-on-write.
- Use `actor` for isolated mutable state.

```swift
func fetchThing() async throws -> String { "ok" }

Task {
  let v = try await fetchThing()
  print(v)
}
```

---

## Strings

| **Concept** | **JavaScript** | **Swift** | **Notes** |
|---|---|---|---|
| Length | `s.length` | `s.count` | `count` is grapheme-cluster aware (emoji, accents) |
| Contains | `s.includes(x)` | `s.contains(x)` | Case-sensitive by default |
| Starts/Ends | `startsWith`/`endsWith` | `hasPrefix`/`hasSuffix` |  |
| Index | `s[i]` | `s[s.index(...)]` | Swift strings are not integer-indexed |
| Slice | `s.slice(i,j)` | `String(s[start..<end])` | Use `String.Index` |
| Upper/lower | `toUpperCase()` | `uppercased()` | Locale-sensitive variants exist |
| Trim | `trim()` | `trimmingCharacters(in:)` | e.g., `.whitespacesAndNewlines` |
| Split | `s.split(',')` | `s.split(separator: ",")` | Returns `[Substring]` |
| Join | `arr.join(',')` | `arr.joined(separator: ",")` | For `[String]` |
| Replace | `replace`/`replaceAll` | `replacingOccurrences(of:with:)` | Regex replacement also possible |
| Template | `` `Hi ${x}` `` | `"Hi \(x)"` | String interpolation |
| To string | `String(x)` | `String(describing: x)` | Or `\(x)` |

**Indexing example**

```swift
let s = "Hello 👋"
let i = s.index(s.startIndex, offsetBy: 1)
print(s[i]) // "e"
```

---

## Arrays

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Literal / length | `[]` / `a.length` | `[]` / `a.count` |
| Push / Pop end | `a.push(x)` / `a.pop()` | `a.append(x)` / `a.popLast()` |
| Shift / Unshift | `a.shift()` / `a.unshift(x)` | `a.removeFirst()` / `a.insert(x, at: 0)` |
| Index access | `a[i]` | `a[i]` |
| Slice | `a.slice(i,j)` | `Array(a[i..<j])` |
| Splice | `a.splice(i,k,...xs)` | `a.replaceSubrange(i..<i+k, with: xs)` |
| Concat | `a.concat(b)` | `a + b` |
| Copy | `[...a]` | `Array(a)` |
| Includes | `a.includes(x)` | `a.contains(x)` |
| Find | `a.find(fn)` | `a.first(where: fn)` |
| FindIndex | `a.findIndex(fn)` | `a.firstIndex(where: fn)` |
| Filter / Map | `filter` / `map` | `filter` / `map` |
| Reduce | `reduce(fn, init)` | `reduce(init, fn)` |
| Some / Every | `some` / `every` | `contains(where:)` / `allSatisfy` |
| Sort | `a.sort()` | `a.sort()` / `a.sorted()` |
| Reverse | `a.reverse()` | `a.reverse()` / `a.reversed()` |
| Flat | `flat()` | `a.flatMap { $0 }` (when nested) |
| Unique | `Array.from(new Set(a))` | `Array(Set(a))` (order not guaranteed) |

Examples:

```swift
var a = [1, 2, 3]
a.append(4)                 // [1,2,3,4]
let b = a.filter { $0 % 2 == 0 } // [2,4]
let c = a.map { $0 * 10 }   // [10,20,30,40]
```

---

## Objects-Dicts

In Swift, dictionaries are `[Key: Value]`.

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Literal | `{ a: 1 }` | `["a": 1]` |
| Read | `o.k` / `o["k"]` | `d["k"]` |
| Safe read | `o?.k` | `d["k"]` returns `Value?` |
| Default | `o.k ?? def` | `d["k"] ?? def` |
| Existence | `"k" in o` | `d.keys.contains("k")` or `d["k"] != nil` |
| Keys/Values/Entries | `Object.keys` etc | `d.keys`, `d.values`, `d` (iterates pairs) |
| Merge | `{...a, ...b}` | `a.merging(b) { _, new in new }` |
| In-place merge | `Object.assign(a,b)` | `a.merge(b) { _, new in new }` |
| Delete | `delete o.k` | `d["k"] = nil` or `d.removeValue(forKey: "k")` |
| Iterate | `for (k,v) of Object.entries(o)` | `for (k,v) in d { ... }` |

Example:

```swift
var d = ["a": 1, "b": 2]
d["c"] = 3
let x = d["a"] ?? 0
d["b"] = nil
```

---

## Map-Set

Swift has `Set<T>` and `Dictionary<K,V>` (no separate Map type).

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Set literal | `new Set([1,2])` | `Set([1,2])` |
| Size | `s.size` | `s.count` |
| Add / Has / Delete | `add/has/delete` | `insert/contains/remove` |
| Union / Intersect | `s.union(t)` | `s.union(t)` / `s.intersection(t)` |
| Difference | manual | `s.subtracting(t)` |
| Symmetric diff | manual | `s.symmetricDifference(t)` |

Example:

```swift
var s: Set<Int> = [1,2,3]
s.insert(4)
s.contains(2) // true
s.remove(1)
```

---

## Tuples & Immutability

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Tuple/array destructure | `const [a,b] = arr` | `let (a,b) = tup` |
| Named fields | - | `let p = (x: 1, y: 2); p.x` |
| Swap | `[a,b]=[b,a]` | `swap(&a, &b)` or `(a,b)=(b,a)` |

---

## Functional Patterns

| **Pattern** | **JavaScript** | **Swift** |
|---|---|---|
| Map | `arr.map(f)` | `arr.map(f)` |
| Filter | `arr.filter(p)` | `arr.filter(p)` |
| Reduce | `arr.reduce(fn, init)` | `arr.reduce(init, fn)` |
| FlatMap | `arr.flatMap(f)` | `arr.flatMap(f)` |
| GroupBy | custom | `Dictionary(grouping: arr, by: keyFn)` |
| ForEach | `arr.forEach(f)` | `arr.forEach(f)` |
| Any/All | `some/every` | `contains(where:)` / `allSatisfy` |

Example GroupBy:

```swift
let words = ["a", "bb", "ccc", "dd"]
let grouped = Dictionary(grouping: words) { $0.count }
// [1: ["a"], 2: ["bb","dd"], 3: ["ccc"]]
```

---

## Numbers & Math

| **Concept** | **JavaScript** | **Swift** | **Notes** |
|---|---|---|---|
| Parse int | `parseInt(s, 10)` | `Int(s)` | Returns optional |
| Parse float | `parseFloat(s)` | `Double(s)` | Returns optional |
| NaN | `Number.isNaN(x)` | `x.isNaN` | Float/Double |
| Finite | `isFinite(x)` | `x.isFinite` | Float/Double |
| Random | `Math.random()` | `Double.random(in: 0..<1)` |  |
| Abs | `Math.abs(x)` | `abs(x)` |  |
| Min/Max | `Math.min/max` | `min` / `max` |  |
| Power | `x ** y` | `pow(x, y)` | `Foundation`/`Darwin` |

```swift
import Foundation
let p = pow(2.0, 10.0) // 1024
```

---

## Dates & Time

Foundation provides `Date`, `Calendar`, `DateComponents`, `DateFormatter`, `ISO8601DateFormatter`.

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Now | `Date.now()` | `Date()` |
| Millis timestamp | `Date.now()` | `Date().timeIntervalSince1970 * 1000` |
| Parse ISO | `new Date("2025-01-02T00:00:00Z")` | `ISO8601DateFormatter().date(from: s)` |
| Format | `toISOString()` | `ISO8601DateFormatter().string(from: date)` |
| Add days | `d + days` | `Calendar.current.date(byAdding: .day, value: n, to: d)` |

Example:

```swift
import Foundation
let iso = ISO8601DateFormatter()
let d = iso.date(from: "2025-01-02T12:34:56Z")!
let s = iso.string(from: d)
```

---

## Regex

Swift has `Regex` (modern, Swift 5.7+) and Foundation `NSRegularExpression`.

| **Concept** | **JavaScript** | **Swift (Regex)** |
|---|---|---|
| Compile | `/pat/i` | `let r = /pat/i` or `let r = try Regex("pat")` |
| Test | `re.test(s)` | `s.contains(r)` |
| First match | `re.exec(s)` | `s.firstMatch(of: r)` |
| Replace | `s.replace(re, repl)` | `s.replacing(r, with: "repl")` |

Example:

```swift
let s = "abc123"
if let m = s.firstMatch(of: /\d+/) {
  print(m.0) // "123"
}
```

---

## Errors & Control Flow

JS:
```js
try { ... } catch (e) { ... } finally { ... }
throw new Error("msg")
```

Swift:
```swift
do {
  try something()
} catch {
  print(error)
}
// no built-in finally; use `defer`
func f() throws {
  defer { print("cleanup") }
  try something()
}
```

Throwing:
```swift
enum MyError: Error { case bad }
throw MyError.bad
```

---

## Modules & Imports

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Import | `import x from "m"` | `import Foundation` / `import MyModule` |
| Export | `export ...` | `public` / `open` symbols in a module |
| Package mgr | npm/yarn/pnpm | Swift Package Manager (SPM) |

---

## Types: Structs, Classes, Enums

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Plain object | `{...}` | `struct` / `Dictionary` |
| Class | `class C {}` | `class C {}` |
| Interface/type | TS `interface` | `protocol` |
| Enum | `const X = {}` | `enum X { case a, b }` |
| Extension | prototype / mixins | `extension Type { ... }` |

Struct vs Class:

```swift
struct Point { var x: Int; var y: Int }  // value type
final class Person { var name: String; init(name: String){ self.name = name } } // ref
```

Enums with associated values:

```swift
enum Result<T> {
  case ok(T)
  case err(Error)
}
```

---

## Async & Promises

JS:
```js
const r = await fetch(url);
const json = await r.json();
```

Swift:
```swift
import Foundation

let (data, _) = try await URLSession.shared.data(from: url)
let obj = try JSONDecoder().decode(MyType.self, from: data)
```

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Promise | `Promise<T>` | `async` function returning `T` |
| Await | `await p` | `try await f()` |
| Sleep | `await new Promise(r=>setTimeout(r,ms))` | `try await Task.sleep(nanoseconds: ms * 1_000_000)` |
| Concurrent | `Promise.all([...])` | `async let` / `TaskGroup` |

Example concurrency:

```swift
async let a = fetchA()
async let b = fetchB()
let (va, vb) = try await (a, b)
```

---

## Truthiness, Nullish-Coalescing

Swift does **not** coerce types to Bool.

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Falsy | `false, 0, "", null, undefined, NaN` | No truthiness coercion |
| Boolean check | `if (x) ...` | `if x != 0 { ... }` / `if !s.isEmpty { ... }` |
| Nullish | `a ?? b` | `a ?? b` |

---

## Copying & Equality

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Value equality | `===` (primitives) | `==` (requires `Equatable`) |
| Reference identity | objects | `===` / `!==` (classes only) |
| Copy | `{...o}` / `structuredClone` | Value types copy by assignment (COW); classes need manual copy |
| Deep copy | library | implement `copy()` or use `Codable` roundtrip (when applicable) |

Example:

```swift
let a = [1,2,3]
var b = a
b.append(4)   // a unchanged (copy-on-write)
```

---

## JSON & Codable

JS:
```js
const s = JSON.stringify(obj);
const o = JSON.parse(s);
```

Swift:
```swift
import Foundation

struct User: Codable {
  let id: Int
  let name: String
}

let u = User(id: 1, name: "Ada")
let data = try JSONEncoder().encode(u)
let u2 = try JSONDecoder().decode(User.self, from: data)
```

---

## Common Helpers

| **Concept** | **JavaScript** | **Swift** |
|---|---|---|
| Range 0..n | `[...Array(n).keys()]` | `Array(0..<n)` |
| Repeat n times | `Array(n).fill(v)` | `Array(repeating: v, count: n)` |
| Sort by key | `arr.sort((a,b)=>a.k-b.k)` | `arr.sorted { $0.k < $1.k }` |
| Unique | `new Set(arr)` | `Set(arr)` |
| Count occurrences | reduce | `Dictionary(arr.map { ($0, 1) }, uniquingKeysWith: +)` |
| Safe array access | `arr?.[i]` | `arr.indices.contains(i) ? arr[i] : nil` |

---

## Dictionary Patterns You’ll Use Often

| **Pattern** | **Swift** |
|---|---|
| Safe read | `d[key]` returns `Value?` |
| Default | `d[key, default: 0] += 1` |
| Set if missing | `d[key] = d[key] ?? value` |
| Merge | `d.merge(other) { _, new in new }` |
| Pop/remove | `d.removeValue(forKey: key)` |

Example counting:

```swift
let xs = ["a","b","a"]
var counts: [String: Int] = [:]
for x in xs {
  counts[x, default: 0] += 1
}
```

---

### Notes / Gotchas

- Swift has **no implicit truthiness**: `if x` is invalid unless `x` is `Bool`.
- `String` indexing uses `String.Index`, not integer indices (Unicode-correct).
- Dictionary reads return an **optional** because the key may be missing.
- `Array.popLast()` returns optional; `removeLast()` traps on empty.
- Value types (Array/Dictionary/String) are copy-on-write; copying is usually cheap until mutation.
- `===` is only for `class` identity checks.
