---
theme: seriph
title: Les itérateurs (en JS)
info: |
  ## Les Itérateurs (en JS)

  [Sources](https://github.com/nlepage/iterators-talk)
routerMode: hash
lineNumbers: true

class: text-center
---

# Les itérateurs (en JS)

---

```ts
interface Iterator<T> {
    next(): Result<T>
}

interface Result<T> {
    done: boolean
    value: T
}
```

---

```js {monaco-run}
const set = new Set(['carotte', 'grignotte', 'cracotte']);

const iter = set.values();

console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
```

---

```js {*} twoslash
const arr = ['Astérix', 'Obélix', 'Pix'];

for (const value of arr) {
    console.log(value);
}

const copy = [...arr];
```

---

```js {monaco-run}
const arr = ['Astérix', 'Obélix', 'Pix'];

const iter = arr[Symbol.iterator]();

console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
```

---

```js {all|6,9,10,16,17|3,4,7,12,14,19} twoslash
const iter = Iterator.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

iter.every((n) => n > 0);
iter.some((n) => n > 0);

iter.filter((n) => n % 2 === 0);
iter.find((n) => n % 5 === 0);

iter.map((n) => n ** 2);
iter.flatMap((n) => new Array(n).fill(n));

iter.reduce((a, b) => a + b);

iter.forEach((n) => console.log(n));

iter.drop(2);
iter.take(5);

iter.toArray();
```

---

```js {monaco-run}
const iter = Iterator.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

const result = iter
    .map((n) => n * 2)
    .take(5)
    .map((n) => n * 3)
    .reduce((a, b) => a + b);

console.log(result);
```

---

```js {monaco-run} { autorun: false }
const iter = Iterator.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

iter
    .map((n) => debug('map1', n * 2))
    .take(4)
    .map((n) => debug('map2', n * 3))
    .reduce((a, b) => debug('reduce', a + b));

function debug(...args) {
    console.log(...args);
    return args.at(-1);
}
```

---

```js {monaco-run}
const iter = Iterator.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

// const squares = iter.map((n) => n ** 2);

console.log(iter.take(3).toArray());
// console.log(iter.take(3).toArray());
// console.log(iter.take(3).toArray());
// console.log(iter.take(3).toArray());
```

---

```js {monaco-run}
function* count() {
    let i = 0;
    while (true) yield i++;
}

const iter = count();

console.log(iter.take(10).toArray());
// console.log(iter.take(10).toArray());
```
