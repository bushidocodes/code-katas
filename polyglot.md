# Collections

|          | JavaScript                 | C     | C++           | Java  | Rust                      | Bash                |
| -------- | -------------------------- | ----- | ------------- | ----- | ------------------------- | ------------------- |
| Array    | Array Buffer / Typed Array | Array | Array         | Array | Array                     | N/A                 |
| Sequence | Array                      | DIY   | Vector        | List  | Vec, VecDeque, LinkedList | Array               |
| Maps     | Object, Map, Record(TS)    | DIY   | Map           | Map   | HashMap, BTreeMap         | Associative Array   |
| Sets     | Set                        | DIY   | Set, MultiSet | Map   | HashSet, BTreeSet         | Associative Array\* |

\* A bash associative array acts as a set if you only use keys and disregard the value

# Arrays - Indexed elements of static size/type contiguously laid out in memory

## JavaScript

JavaScript has not traditionally provided C-style arrays. However, due to WebAssembly, the language has added support for TypedArrays.

Array Buffer / Typed Arrays
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array

In many cases, modern JavaScript JIT compilers actually transform high-level JS Arrays into C-style Arrays.

Discussion of Performance: https://stackoverflow.com/questions/24853686/javascript-typedarray-performance

# Ordered Sequences

|                   | JavaScript            | C++                   | Java                               | Rust                               | Bash                    |
| ----------------- | --------------------- | --------------------- | ---------------------------------- | ---------------------------------- | ----------------------- |
| Get num elems     | arr.length            | vec.size()            | list.size()                        | vec.len()                          | ${#arr[@]}              |
| Get elem at idx   | arr[idx], arr.at(idx) | vec[idx], vec.at(idx) | list[idx], list.get(idx)           | vec[idx], vec.get(), vec.get_mut() | arr[idx]                |
| Get elem at -idx  | arr.at(-idx)          |                       |                                    |                                    | arr[-idx]               |
| Get front         |                       | vec.front()           |                                    | vec.first(), vec.first_mut()       | arr                     |
| Get back          |                       | vec.back()            |                                    | vec.last(), vec.last_mut()         |                         |
| Insert at idx     | arr.splice()          | vec.insert()          | list.add(idx, elem)                | vec.splice()                       | arr[idx] = elem         |
| Insert front      | arr.unshift()         |                       |                                    |                                    |                         |
| Insert back       | arr.push(elem)        | vec.push_back()       |                                    | vec.push(elem)                     | arr += (elem)           |
| Remove front      | arr.shift()           |                       |                                    |                                    |                         |
| Remove back       | arr.pop()             | vec.pop_back()        | list.remove()                      | vec.pop()                          |                         |
| Remove at idx     | arr.splice()          | vec.erase()           | list.remove()                      | vec.remove(), vec.swap_remove()    | unset arr[idx]          |
| find idx of elem  | arr.find()            | std::find             | list.indexOf(), list.lastIndexOf() | vec.binary_search()                |                         |
| test for elem     | arr1.includes(elem)   | std::any_of()         | list.contains()                    | vec.contains()                     |                         |
| Combine sequences | arr1.concat(arr2)     | std::merge()          | list.addAll()                      | vec1.append(vec2), vec.concat()    |                         |
| Sort elements     | arr.sort()            | std::sort()           | list.sort()                        | vec.sort()                         |                         |
| Reverse elements  | arr.reverse()         | std::reverse()        | java.util.reverse()                | vec.reverse()                      |                         |
| Shuffle elements  | None                  | std::random_shuffle() | java.util.shuffle()                |                                    |                         |
| Delete all        |                       | vec.clear()           | list.clear()                       | vec.clear()                        | unset arr               |
| Shallow Compare   | arr1 === arr2         |                       | list.equals()                      |                                    |                         |
| Join as string    | arr.join("")          |                       | String.join(delim, list)           |                                    | "${arr[*]}"             |
| Loop over elems   | for (let elem of arr) |                       | for (var elem: list)               |                                    | for elem in "${arr[@]}" |
| Map               | arr.map()             |                       | stream.map(), stream.mapToXX()     | iter.map()                         | None                    |
| Filter            | arr.filter()          |                       | stream.filter()                    | iter.filter()                      | None                    |
| Reduce            | arr.reduce()          | std::reduce           | stream.reduce()                    | iter.fold()                        | None                    |
| to stream         | automatic             |                       | .stream()                          | .iter()                            | None                    |
| from stream       | automatic             |                       | .collect(Collectors.toList())      | .collect()                         | None                    |

## JavaScript

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

## C

DIY

1. Create container struct that wraps buffer and has size and capacity fields
2. Automatically call realloc to resize buffer if needed

## C++

Backed by growable buffer
https://www.cplusplus.com/reference/vector/vector/

Efficient insertion at front, but elements are not necessarily packed in a single buffer
https://www.cplusplus.com/reference/deque/deque/

Singly Linked List
https://www.cplusplus.com/reference/forward_list/forward_list/

Doubly Linked List
https://www.cplusplus.com/reference/list/list/

## Java

https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/ArrayList.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collections.html

## Rust

https://doc.rust-lang.org/std/vec/struct.Vec.html

## Bash

https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Arrays

# Maps -

|                     | JS Obj           | JS Map        | C++                           | Java                                     | Rust                                              | Bash                   |
| ------------------- | ---------------- | ------------- | ----------------------------- | ---------------------------------------- | ------------------------------------------------- | ---------------------- |
| Get Size            |                  | map.size      | map.size()                    | map.size()                               | map.len()                                         | ${#aa[@]}              |
| Check if empty      |                  |               |                               | map.isEmpty()                            | map.is_empty()                                    |                        |
| Clear contents      |                  | map.clear()   | map.clear()                   | map.clear()                              | map.clear()                                       | unset aa (redeclare)   |
| Get V using K       | v = obj[k]       | map.get(k)    | map[k], map.at(k)             | map.get(k), map.getOrDefault(k, default) | map.get(k), map.get_mut(k)                        | ${aa[$k]}              |
| Get KV using K      |                  |               |                               |                                          | map.entry(k), map.get_key_value(k)                |                        |
| Test for K          | !!obj[k]         | map.has(k)    | map.contains(k)               | map.containsKey(k)                       | map.contains_key(k)                               | ${aa[$k]+\_}           |
| Test for V          |                  |               |                               | map.containsValue(k)                     |                                                   |                        |
| Set KV              | obj[k] = v       | map.set(k,v)  | map.insert(k,v)               | map.put(k,v), map.putIfAbsent(k,v)       | map.insert(k,v), map.try_insert(k,v)              | aa+=([k]=v), aa[k] = v |
| Get Keys            | Object.keys()    | map.keys()    |                               | map.keySet()                             | map.keys(), map.into_keys(),                      | keys=(“${!aa[@]}”)     |
| Get Values          | Object.values()  | map.values()  |                               | map.values()                             | map.values(), map.values_mut(), map.into_values() |                        |
| Get KV Pairs        | Object.entries() | map.entires() |                               |                                          | map.iter(), map.iter_mut()                        |                        |
| Iterate over keys   | for..in          | for..of       | for (const auto& [k,v] : map) |                                          | for key in map.keys()                             | for k in "${!aa[@]}"   |
| Iterate over values |                  |               | for (const auto& [k,v] : map) |                                          | for key in map.values()                           | for k in "${aa[@]}"    |
| forEach             |                  | map.forEach() |                               | map.forEach((k,v)->{})                   |                                                   |                        |
| Remove entry        |                  |               |                               |                                          | map.remove(k), map.remove_entry(k)                | unset aa[k]            |

## JavaScript

Objects
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object

Generally, prefer Map to object.

Keys are limited to symbols
for..in loops over keys provided by the prototype. Must use `Object.create(null)` to create an "empty object"
You can use for..of with Object.keys(obj)

Maps
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map

Record
https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type

## C

Use two arrays. The first array is of keys and the second array is of mapped values.
Find the idx of the key in the keys array and then use that to lookup the associated value

## C++

https://www.cplusplus.com/reference/map/map/
https://www.cplusplus.com/reference/map/multimap/
https://www.cplusplus.com/reference/unordered_map/unordered_map/
https://www.cplusplus.com/reference/unordered_map/unordered_multimap/

## Java

https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collections.html

## Rust

https://doc.rust-lang.org/std/collections/hash_map/struct.HashMap.html
https://doc.rust-lang.org/std/collections/struct.BTreeMap.html

## Bash

# Sets

|                  | JS            | C++ | Java | Rust | Bash |
| ---------------- | ------------- | --- | ---- | ---- | ---- |
| Check Membership | set.has(e)    |     |      |      |      |
| Add              | set.add(e)    |     |      |      |      |
| Remove           | set.delete(e) |     |      |      |      |
| Clear            | set.clear())  |     |      |      |      |
| Iterator         | set.values()) |     |      |      |      |

## JavaScript

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set

## C

TODO

## C++

https://www.cplusplus.com/reference/set/set/
https://www.cplusplus.com/reference/set/multiset/
https://www.cplusplus.com/reference/unordered_set/unordered_set/
https://www.cplusplus.com/reference/unordered_set/unordered_multiset/

## Java

https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashSet.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/TreeSet.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collections.html

## Rust

https://doc.rust-lang.org/std/collections/hash_set/struct.HashSet.html
https://doc.rust-lang.org/std/collections/struct.BTreeSet.html

## Bash

Bash does not have a set type.
You can get a collection that enforces uniqueness by using the keys of an associated array with arbitrary values

# Strings

|                       | JavaScript                        | C                    | C++ | Java | Rust                                         | Bash                      |
| --------------------- | --------------------------------- | -------------------- | --- | ---- | -------------------------------------------- | ------------------------- |
| To Uppercase          | str.toUpperCase()                 | toupper              | --- | ---- | str.to_uppercase()                           | ${str^^pattern}, local -u |
| To Lowercase          |                                   |                      | --- | ---- | str.to_lowercase()                           | ${str,,pattern}           |
| Compare for Equality  | ===                               | strncmp, strncasecmp | --- | ---- | ----                                         |                           |
| Copy string           | =, str.slice()                    | strncpy, strndup     | --- | ---- | str.clone()                                  |                           |
| Get length            | str.length                        | strnlen              | --- | ---- | str.len()                                    | ${#str}                   |
| Join strings          | +, tr1.concat(str2)               | strncat              | --- | ---- | str1 + str2                                  | str+="more"               |
| Get Slice             | str.substring(start, endExcl)     | deref+offset         |     |      | &str[0..5];                                  | ${str:idx:len}            |
| Trim                  | .trim(), .trimStart(), .trimEnd() | strncat+isspace      |     |      | str.trim(), str.trim_start(), str.trim_end() |                           |
| Pad                   | .padStart(), .padEnd()            | snprintf             |     |      | format!                                      |                           |
| Split into collection | .split(delim)                     | strtok               |     |      | str.split(delim)                             | IFS and don't quote       |
| Get char at idx       | .charAt()                         | str[idx]             |     |      |                                              |                           |
| Find Substring        | .indexOf, lastIndexOf             | strstr               |     |      |                                              |                           |
| Replace chars         |                                   |                      |     |      |                                              | ${str// /}                |
| Template String       | `${str} is a string`              | snprintf             |     |      |                                              | "${str} is a string"      |

TODO: Is JS string assignment value or ref?
