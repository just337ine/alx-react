# 0x06. React Immutable

## Table of Contents

1. [Introduction](#introduction)
2. [Immutable Objects](#immutable-objects)
   - [Who, What, When, Where, and Why?](#who-what-when-where-and-why)
3. [Using Immutable.js](#using-immutablejs)
4. [Differences Between List and Map](#differences-between-list-and-map)
5. [Merge, Concat, and Deep Merging](#merge-concat-and-deep-merging)
6. [Lazy Seq](#lazy-seq)
7. [Resources](#resources)

## Introduction

This README provides an overview of immutability in JavaScript, focusing on the use of the Immutable.js library in React applications. Immutability is a key concept in functional programming and can greatly enhance the performance and predictability of your applications.

## Immutable Objects

### Who, What, When, Where, and Why?

**Who**:
Developers working on JavaScript applications, particularly those using React, benefit from using immutable objects. Functional programming enthusiasts also favor immutability.

**What**:
Immutable objects are objects whose state cannot be modified after creation. Instead of altering an object, new objects are created with the updated state.

**When**:
Use immutability when you want to ensure that objects remain unchanged throughout their lifecycle. This is particularly useful in complex applications where state management can become a challenge.

**Where**:
Immutability is commonly used in state management libraries (like Redux) and frameworks (like React) where predictable state management is crucial.

**Why**:

- **Predictability**: Immutable objects make state changes predictable.
- **Performance**: They can optimize rendering in React, as shallow comparison checks are easier.
- **Debugging**: Easier to track state changes, as new objects are created rather than modifying existing ones.
- **Concurrency**: Safer to use in concurrent programming as it prevents race conditions.

## Using Immutable.js

Immutable.js is a library that brings persistent immutable data structures to JavaScript. It provides several immutable data types like List, Map, Set, and others.

### Installation

To install Immutable.js, use npm or yarn:

```bash
npm install immutable
# or
yarn add immutable
```

### Basic Usage

```javascript
const { Map, List } = require("immutable");

const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set("b", 50);

console.log(map1.get("b")); // 2
console.log(map2.get("b")); // 50

const list1 = List([1, 2, 3]);
const list2 = list1.push(4);

console.log(list1.size); // 3
console.log(list2.size); // 4
```

## Differences Between List and Map

**List**:

- Ordered indexed collections, similar to arrays.
- Access elements via index.
- Supports methods like `push`, `pop`, `shift`, `unshift`.

**Map**:

- Collections of key-value pairs, similar to objects.
- Access elements via key.
- Supports methods like `set`, `get`, `delete`.

### Example

```javascript
const { List, Map } = require("immutable");

// List Example
const myList = List([1, 2, 3]);
const newList = myList.push(4);
console.log(newList.toArray()); // [1, 2, 3, 4]

// Map Example
const myMap = Map({ key1: "value1", key2: "value2" });
const newMap = myMap.set("key3", "value3");
console.log(newMap.toObject()); // { key1: 'value1', key2: 'value2', key3: 'value3' }
```

## Merge, Concat, and Deep Merging

### Merge

Combines properties from two maps, with the second map's properties overwriting the first's.

```javascript
const { Map } = require("immutable");

const map1 = Map({ a: 1, b: 2 });
const map2 = Map({ b: 3, c: 4 });

const mergedMap = map1.merge(map2);
console.log(mergedMap.toObject()); // { a: 1, b: 3, c: 4 }
```

### Concat

Combines two lists or arrays into one.

```javascript
const { List } = require("immutable");

const list1 = List([1, 2, 3]);
const list2 = List([4, 5, 6]);

const concatenatedList = list1.concat(list2);
console.log(concatenatedList.toArray()); // [1, 2, 3, 4, 5, 6]
```

### Deep Merging

Recursively merges nested structures.

```javascript
const { Map } = require("immutable");

const deepMap1 = Map({ a: Map({ b: 1 }) });
const deepMap2 = Map({ a: Map({ c: 2 }) });

const deepMergedMap = deepMap1.mergeDeep(deepMap2);
console.log(deepMergedMap.toObject()); // { a: { b: 1, c: 2 } }
```

## Lazy Seq

`Seq` is a lazy operation in Immutable.js. It allows for the creation of lazy sequences that do not compute values until required. This can optimize performance for large datasets or complex operations.

### Example

```javascript
const { Seq } = require("immutable");

const seq = Seq([1, 2, 3, 4, 5])
  .filter((x) => x % 2 === 0)
  .map((x) => x * 2);

console.log(seq.toArray()); // [4, 8]
```

Here, the filtering and mapping operations are performed only when `toArray` is called, demonstrating the laziness of `Seq`.

### Resources

- [Immutable Object concept](https://en.wikipedia.org/wiki/Immutable_object)
- [Immutabl.js Documentation](https://immutable-js.com/docs/v4.3.6/)
- [Immutable.js Github](https://github.com/immutable-js/immutable-js)
