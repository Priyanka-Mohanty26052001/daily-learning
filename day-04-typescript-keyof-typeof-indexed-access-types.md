# Day 04: TypeScript `keyof`, `typeof`, and Indexed Access Types

## 1. The `keyof` Operator

The `keyof` operator creates a union of an object's property names.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

type UserKeys = keyof User;
// "id" | "name" | "email"
```

### Real-world example

```typescript
function getProperty<T, K extends keyof T>(
  obj: T,
  key: K
): T[K] {
  return obj[key];
}

const user = {
  id: 1,
  name: "Priyanka",
  email: "priyanka@example.com"
};

console.log(getProperty(user, "name")); // Priyanka
console.log(getProperty(user, "id"));   // 1
```

`K extends keyof T` ensures that only valid property names can be passed.

## 2. The `typeof` Operator

In TypeScript, `typeof` can be used in a type position to derive a type from an existing variable.

```typescript
const user = {
  name: "Priyanka",
  age: 25
};

type User = typeof user;
```

The resulting `User` type contains the `name` and `age` properties with their inferred types.

## 3. Indexed Access Types

Indexed access types allow you to retrieve the type of a particular property.

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
}

type ProductName = Product["name"]; // string
type ProductPrice = Product["price"]; // number
type ProductValue = Product[keyof Product];
// string | number
```

## 4. Angular Use Case

These operators are useful when working with strongly typed objects, API responses, reusable components, and table column configurations.

```typescript
interface Employee {
  id: number;
  name: string;
  department: string;
}

type EmployeeKey = keyof Employee;

const displayedColumns: EmployeeKey[] = [
  "id",
  "name",
  "department"
];
```

This helps ensure that column names match the properties defined in the `Employee` interface.

## 5. Practice Exercises

1. Create an `Employee` interface and derive its keys using `keyof`.
2. Create a variable and derive its type using `typeof`.
3. Use indexed access types to extract the type of one property.
4. Write a generic `getProperty()` function that accepts only valid object keys.
5. Try passing an invalid property name and observe the TypeScript compiler error.

## Key Takeaways

- `keyof` extracts property names as a union of types.
- `typeof` derives a type from an existing value.
- Indexed access types retrieve the type of a selected property.
- Together, these features help build reusable and type-safe TypeScript code.
