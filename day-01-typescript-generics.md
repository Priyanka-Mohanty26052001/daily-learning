# Day 01: TypeScript Generics

## 1. What Are Generics?

Generics allow us to write reusable, type-safe code that works with different data types without losing type information.

Instead of using `any`, we can use a type parameter such as `T` to preserve the relationship between input and output types.

### Why Use Generics?

- Write reusable functions and interfaces.
- Maintain compile-time type safety.
- Reduce code duplication.
- Build flexible utilities for real-world applications.

## 2. Basic Example: Generic Function

```typescript
function identity<T>(value: T): T {
  return value;
}

const name = identity("Priyanka");
const age = identity(25);
const isDeveloper = identity(true);

console.log(name);
console.log(age);
console.log(isDeveloper);
```

### Output

```text
Priyanka
25
true
```

**Explanation:** TypeScript infers the type of `T` from the argument. A string returns a string, a number returns a number, and a boolean returns a boolean.

## 3. Generics with Arrays

We can use generics to create functions that work with arrays of different types.

```typescript
function getFirstElement<T>(items: T[]): T | undefined {
  return items[0];
}

console.log(getFirstElement([10, 20, 30]));
console.log(getFirstElement(["Angular", "TypeScript"]));
console.log(getFirstElement([]));
```

### Output

```text
10
Angular
undefined
```

**Explanation:**

- `T[]` represents an array of elements of type `T`.
- `T | undefined` means the function returns an element of type `T` or `undefined`.
- An empty array returns `undefined` because it has no first element.

## 4. Generic Constraints

Sometimes a function should accept only values that satisfy a particular requirement. We can use `extends` to constrain a generic type.

```typescript
interface HasId {
  id: number;
}

function getEntityId<T extends HasId>(entity: T): number {
  return entity.id;
}

const user = {
  id: 101,
  name: "Priyanka"
};

console.log(getEntityId(user));
```

### Output

```text
101
```

**Explanation:** The constraint `T extends HasId` requires the argument to contain a numeric `id`. Additional properties, such as `name`, are allowed.

## 5. Real-World Example: API Response

Generics are useful for defining reusable API response structures in Angular and Node.js applications.

```typescript
interface ApiResponse<T> {
  data: T;
  success: boolean;
  message: string;
}

interface User {
  id: number;
  name: string;
}

const response: ApiResponse<User> = {
  data: {
    id: 101,
    name: "Priyanka"
  },
  success: true,
  message: "User fetched successfully"
};

console.log(response.data.name);
```

### Output

```text
Priyanka
```

The same `ApiResponse<T>` interface can represent different types of data without duplicating the interface definition.

## 6. Runnable Coding Exercise

**Problem:** Create a generic function named `getLastElement` that returns the last element of an array.

### Requirements

- Accept arrays containing different data types.
- Preserve the element's type.
- Return `undefined` for an empty array.

### Solution

```typescript
function getLastElement<T>(items: T[]): T | undefined {
  return items[items.length - 1];
}

console.log(getLastElement([10, 20, 30]));
console.log(getLastElement(["Angular", "TypeScript"]));
console.log(getLastElement([]));
```

### Expected Output

```text
30
TypeScript
undefined
```

### Run It Locally

Save the code in `generics.ts` and execute it using `tsx`:

```bash
npx tsx generics.ts
```

Install `tsx` first if necessary:

```bash
npm install -D tsx typescript
```

## 7. Common Mistakes to Avoid

- Using `any` when a generic type would preserve type safety.
- Forgetting to handle empty arrays.
- Adding unnecessary generic parameters when a specific type is clearer.
- Assuming generics validate external data at runtime; TypeScript types are primarily checked at compile time.

## 8. Key Takeaways

1. Generics make code reusable without sacrificing type safety.
2. `T` represents a type parameter that TypeScript can infer.
3. `extends` restricts which types a generic function accepts.
4. Generic interfaces are useful for reusable API response models.
5. Union types such as `T | undefined` help represent possible missing values.

## 9. Interview Question

**Q: What is the difference between `any` and generics in TypeScript?**

**Answer:** `any` disables most type checking for a value, while generics preserve type information and relationships between inputs and outputs. Generics help developers write reusable code while allowing TypeScript to catch type errors during compilation.

---

**Day 01 completed:** TypeScript Generics

**Next topic:** Day 02 — TypeScript Utility Types (`Partial`, `Pick`, `Omit`, and `Record`).
