# Typescript

## What is Typescript?

TypeScript is like an improved version of JavaScript. It's almost the same, but it has something extras: it lets us specify what type of data we're going to use (for example, if a variable will be a number, a string, an array, etc.). This helps us avoid errors before our code runs.

## Interface & Type

Both interface and type are used to define the shape of objects, like props for React components.

### Interface

Good for describing objects and extending

```ts
interface User {
  name: string
  age: number
}
```

**Good for:**

- Object shapes
- React props
- Class definitions
- Extending/inheriting other interfaces

**_Supports Extension_**

```ts
interface Base {
  id: number
}

interface User extends Base {
  name: string
}
```

### Type

More flexible, supports unions and other types

```ts
type User = {
  name: string
  age: number
}
```

**Good for:**

- Objects
- Unions
- Primitives
- Tuples
- Intersections

```ts
type ID = string | number

type Todo =
  | {
      title: string
    }
  | {
      error: string
    }
```

#### Use Cases Summary

| I want to...                           | Use                   |
| -------------------------------------- | --------------------- |
| Describe an object or React props      | `interface` or `type` |
| Extend or merge types easily           | `interface`           |
| Create union or intersection types     | `type`                |
| Represent a primitive, tuple, or union | `type`                |
| Keep things flexible and composable    | `type`                |

**Final Notes**

- We can mix and combine type and interface, but lets be more consistent.

- interface is generally better for public APIs or libraries (because of declaration merging).

- type is more versatile for complex or functional types.

**What do we mean by merge in interface?**

In TypeScript, interfaces can be declared more than once, and TypeScript will automatically merge them into one.

```ts
interface User {
  name: string
}

interface User {
  age: number
}

// now "User" is:
const person: User = {
  name: 'Exequiel',
  age: 40,
}
```

- Why is this useful?

  - When extending third-party libraries

  - When working with global types

  - When splitting up large interfaces

**What do we mean by intersection**

- Intersection = combine types together (& operator)

```ts
type HasName = { name: string }
type HasAge = { age: number }

type Person = HasName & HasAge

// person must have both name and age
const p: Person = {
  name: 'Exequiel',
  age: 40,
}
```

**What is a tuple?**

- A tuple is an array with fixed number and types of elements.

```ts
const point: [number, number] = [10, 20]
```

**Represent a primitive?**

```ts
type ID = string
type Age = number
```

- We can’t do this with interface — it only works for objects.

**What do we mean by union?**

- A union allows a variable to be one of several types. Lets say:

“This can be A or B or C.”

- Basic example:

If we pass 'loading', the component shows a loading message. If we pass 'success', it shows the success message.
If we pass something that isn't allowed (like 'done'), TypeScript will give us an error at compile-time — it won't run that way.
If we want to show a fallback for unknown values, we can do that too, but only if we're not using strict types.

```ts
type Status = 'loading' | 'success' | 'error'

let current: Status

current = 'loading' // OK
current = 'error' // OK
current = 'done' // Error: "done" is not assignable to type Status
```

- Union with different types:

```ts
type ID = string | number

let userId: ID

userId = 'abc123' // string
userId = 42 // number
userId = true // Error
```

- Union with objects (Discriminated Union)

```ts
type Success = {
  status: 'success'
  data: string
}

type Error = {
  status: 'error'
  message: string
}

type Result = Success | Error

function handle(result: Result) {
  if (result.status === 'success') {
    console.log(result.data) // ts knows it's Success
  } else {
    console.log(result.message) // ts knows it's Error
  }
}
```
