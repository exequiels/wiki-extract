# Javascript

## What is Javascript?

JavaScript is a powerful, high-level programming language mainly used to make websites interactive. While HTML structures a page and CSS styles it, JavaScript adds behavior — like responding to clicks, showing/hiding elements, loading data, or creating animations.

Originally designed for browsers, JavaScript now also runs on servers (using Node.js), making it a full-stack language. It's dynamic, versatile, and essential for modern web development.

---

## Truthy and Falsy

**Values with `!!` Conversion**

In JavaScript, **"truthy"** and **"falsy"** refer to how values behave when evaluated in a boolean context (like inside an `if` statement).

- A **truthy** value is any value that is **considered `true`** when evaluated in a boolean context.
- A **falsy** value is any value that is **considered `false`** in the same context.

### List of Falsy Values

There are only **seven** falsy values in JavaScript:

- `false`
- `0`
- `''` (empty string)
- `null`
- `undefined`
- `NaN`
- `document.all` (very rare)

All other values are **truthy**, including:

- Non-empty strings like `'hello'`
- Numbers other than `0` (e.g., `1`, `-5`)
- Arrays like `[]`
- Objects like `{}`

### Why Use `!!value`

Using `!!value` is a common trick to **convert any value into its boolean equivalent**, returning either `true` or `false`.

This is useful when you want to ensure a clean boolean result instead of potentially dealing with `null`, `undefined`, `0`, or other falsy values.

```js
const isLoggedIn = !!user
```

If user exists, isLoggedIn becomes true; otherwise, it becomes false.

### JavaScript Truthy and Falsy Values with `!!` Conversion

| Value       | Truthy or Falsy? | Result of `!!value` |
| ----------- | ---------------- | ------------------- |
| `true`      | truthy           | `true`              |
| `false`     | falsy            | `false`             |
| `1`         | truthy           | `true`              |
| `0`         | falsy            | `false`             |
| `'hello'`   | truthy           | `true`              |
| `''`        | falsy            | `false`             |
| `null`      | falsy            | `false`             |
| `undefined` | falsy            | `false`             |
| `[]`        | truthy           | `true`              |
| `{}`        | truthy           | `true`              |
| `NaN`       | falsy            | `false`             |

## Why Use `true` or `false` Instead of Just Truthy or Falsy?

JavaScript allows using truthy and falsy values in conditions, but sometimes it's better to convert them to a **clean boolean** (`true` or `false`) using `!!`.

### Reasons to Use `!!value`:

1. **Code Clarity**  
   It's clearer to read and understand when a variable is explicitly `true` or `false`.

2. **Avoid Logic Errors**  
   Falsy values like `''`, `0`, or `NaN` can accidentally cause `if` statements to fail when the value is technically valid.

3. **Stricter Validation**  
   When you need to return or store a strict boolean value:
   ```js
   return !!user.isActive
   ```

Examples:

```jsx
const user = {} // no id, no email

if (user) {
  console.log('✅ Logged in') // prints but shouln't
}
```

How to fix?

```jsx
const user = { id: '', name: '' }

// only if it has a valid id
const isLoggedIn = !!user.id

if (isLoggedIn) {
  console.log('User is logged in')
} else {
  console.log('User is not logged in')
}
```

---

## Minimal Early Return Example

📌 With Falsy Check

```jsx
useEffect(() => {
  const fetchData = async () => {
    if (!user) return // Exit early if user is falsy

    try {
      const data = await fetchSomeData(user.id)
      setData(data)
    } catch (error) {
      console.error('Failed to fetch data:', error)
      setData(null)
    }
  }

  fetchData()
}, [user])
```

✅ Key Points:

- if (!user) return ensures we only fetch data if user exists.
- Prevents unnecessary API calls and runtime errors.
- Makes the logic cleaner and safer.

---

## Function Declarations vs Function Expressions

### Function Declaration

```jsx
function greet() {
  console.log('Hello!')
}
```

#### Characteristics:

- Hoisted — You can call the function before it's defined.
- Named.
- Declared at the top level (or inside blocks).

**Example:**

```jsx
greet() // ✅ works
function greet() {
  console.log('Hello!')
}
```

### Function Expression

```jsx
const greet = function () {
  console.log('Hello!')
}
```

#### Characteristics:

- Not hoisted — You must define the function before calling it.
- Can be anonymous or named.
- Often assigned to a variable.
- Useful for callbacks, closures, and IIFEs.

**Example:**

```jsx
greet() // ❌ ReferenceError: Cannot access 'greet' before initialization

const greet = function () {
  console.log('Hello!')
}
```

### Side-by-Side Summary

| Feature                       | Function Declaration   | Function Expression              |
| ----------------------------- | ---------------------- | -------------------------------- |
| **Hoisting**                  | ✅ Yes                 | ❌ No                            |
| **Can be anonymous**          | ❌ No                  | ✅ Yes                           |
| **Callable before declared?** | ✅ Yes                 | ❌ No                            |
| **Syntax**                    | `function myFunc() {}` | `const myFunc = function() {}`   |
| **Common Use**                | General functions      | Callbacks, closures, short logic |

### Bonus: Arrow Function Expression

```jsx
const greet = () => {
  console.log('Hello!')
}
```

- Arrow functions are always expressions
- They do not bind their own this
- Great for short callbacks and functional programming

#### What Does “No this Binding” Mean?

Arrow functions do not bind their own this. Instead, they inherit this from the surrounding scope.

✅ Regular Function Binds Its Own this

```jsx
const person = {
  name: 'Exe',
  sayHi: function () {
    console.log("Hi, I'm " + this.name)
  },
}

person.sayHi() // ✅ "Hi, I'm Exe"
```

❌ Arrow Function Doesn't Bind this

```jsx
const person = {
  name: 'Exe',
  sayHi: () => {
    console.log("Hi, I'm " + this.name)
  },
}

person.sayHi() // ❌ "Hi, I'm undefined"
```

✅ When Arrow Functions Shine

```jsx
const numbers = [1, 2, 3]
const doubled = numbers.map((n) => n * 2) // ✅ Clean and concise
```

```jsx
class Timer {
  start() {
    setTimeout(() => {
      console.log('Timer done!', this) // ✅ `this` refers to Timer instance
    }, 1000)
  }
}
```

---

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
