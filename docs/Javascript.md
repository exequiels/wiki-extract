# Javascript

## What is Javascript?

## JavaScript Array Methods

| Shortcut      | Method                                    | Description                                           | Example                                            |
| ------------- | ----------------------------------------- | ----------------------------------------------------- | -------------------------------------------------- |
| 🔄 `map`      | `array.map(fn)`                           | Iterates and transforms each element.                 | `[1, 2, 3].map(n => n * 2) // [2, 4, 6]`           |
| 🎯 `filter`   | `array.filter(fn)`                        | Filters elements based on a condition.                | `[1, 2, 3, 4].filter(n => n > 2) // [3, 4]`        |
| 🔍 `find`     | `array.find(fn)`                          | Finds the first element that matches the condition.   | `[{id:1}, {id:2}].find(e => e.id === 2) // {id:2}` |
| ➕ `reduce`   | `array.reduce(fn, init)`                  | Reduces an array to a single value.                   | `[1, 2, 3].reduce((a, b) => a + b, 0) // 6`        |
| ✅ `some`     | `array.some(fn)`                          | Checks if **some** elements match the condition.      | `[1, 2, 3].some(n => n > 2) // true`               |
| ✅ `every`    | `array.every(fn)`                         | Checks if **all** elements match the condition.       | `[1, 2, 3].every(n => n > 0) // true`              |
| 🔄 `forEach`  | `array.forEach(fn)`                       | Iterates over each element (no return value).         | `[1, 2, 3].forEach(n => console.log(n))`           |
| 📊 `sort`     | `array.sort(fn)`                          | Sorts elements (modifies the array).                  | `[3, 1, 2].sort() // [1, 2, 3]`                    |
| 🔄 `reverse`  | `array.reverse()`                         | Reverses the order of elements.                       | `[1, 2, 3].reverse() // [3, 2, 1]`                 |
| 🔢 `includes` | `array.includes(val)`                     | Checks if an element exists in the array.             | `[1, 2, 3].includes(2) // true`                    |
| 🔀 `concat`   | `array1.concat(array2)`                   | Merges two arrays into a new one.                     | `[1, 2].concat([3, 4]) // [1, 2, 3, 4]`            |
| 🔍 `indexOf`  | `array.indexOf(val)`                      | Returns the index of an element (-1 if not found).    | `[1, 2, 3].indexOf(2) // 1`                        |
| 🎭 `slice`    | `array.slice(start, end)`                 | Extracts a portion of the array (does not modify it). | `[1, 2, 3].slice(1, 2) // [2]`                     |
| ✂️ `splice`   | `array.splice(start, count, newItems...)` | Modifies the array (removes/replaces elements).       | `[1, 2, 3].splice(1, 1, 99) // [1, 99, 3]`         |
| ➕ `push`     | `array.push(val)`                         | Adds elements to the end of the array.                | `[1, 2].push(3) // [1, 2, 3]`                      |
| ➖ `pop`      | `array.pop()`                             | Removes the last element.                             | `[1, 2, 3].pop() // [1, 2]`                        |
| ➕ `unshift`  | `array.unshift(val)`                      | Adds elements to the beginning.                       | `[2, 3].unshift(1) // [1, 2, 3]`                   |
| ➖ `shift`    | `array.shift()`                           | Removes the first element.                            | `[1, 2, 3].shift() // [2, 3]`                      |
| 🏷️ `join`     | `array.join(sep)`                         | Joins elements into a string.                         | `['a', 'b'].join('-') // "a-b"`                    |
| 🔤 `split`    | `string.split(sep)`                       | Splits a string into an array.                        | `"a,b,c".split(',') // ['a', 'b', 'c']`            |

💡 **Tip:** Use `map()`, `filter()`, and `reduce()` instead of `for` loops for cleaner, more functional code.

---
