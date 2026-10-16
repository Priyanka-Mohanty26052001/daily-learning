# Day 02: TypeScript Utility Types

## 1. Introduction

TypeScript Utility Types help us transform existing types without rewriting them. They make code cleaner, reusable, and easier to maintain.

## 2. Example Interface

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;
  isActive: boolean;
}
```

## 3. Partial<T>

Makes all properties optional.

```typescript
type UpdateUser = Partial<User>;

const updateUser: UpdateUser = {
  name: "Priyanka"
};

console.log(updateUser);
```

**Use case:** Updating only selected fields of a user.

## 4. Required<T>

Makes all properties required, including optional properties.

```typescript
type CompleteUser = Required<User>;

const user: CompleteUser = {
  id: 1,
  name: "Priyanka",
  email: "priyanka@example.com",
  age: 25,
  isActive: true
};

console.log(user);
```

**Use case:** Ensuring all fields are provided before processing data.

## 5. Pick<T, Keys>

Selects specific properties from an existing type.

```typescript
type UserPreview = Pick<User, "id" | "name">;

const preview: UserPreview = {
  id: 1,
  name: "Priyanka"
};

console.log(preview);
```

**Use case:** Displaying only selected user information.

## 6. Omit<T, Keys>

Creates a type by excluding specific properties.

```typescript
type PublicUser = Omit<User, "email">;

const publicUser: PublicUser = {
  id: 1,
  name: "Priyanka",
  isActive: true
};

console.log(publicUser);
```

**Use case:** Excluding sensitive or unnecessary fields from a data structure. Note that TypeScript types alone do not remove properties at runtime.

## 7. Record<Keys, Type>

Creates an object type with specified keys and a common value type.

```typescript
type UserRoles = "admin" | "developer" | "tester";

const rolePermissions: Record<UserRoles, string[]> = {
  admin: ["create", "update", "delete"],
  developer: ["create", "update"],
  tester: ["read", "test"]
};

console.log(rolePermissions);
```

**Use case:** Defining role permissions, configuration objects, or lookup tables.

## 8. Practical Example: Updating a User

```typescript
interface Employee {
  id: number;
  name: string;
  department: string;
  salary: number;
}

function updateEmployee(
  employee: Employee,
  updates: Partial<Employee>
): Employee {
  return {
    ...employee,
    ...updates
  };
}

const employee: Employee = {
  id: 101,
  name: "Priyanka",
  department: "Development",
  salary: 30000
};

const updatedEmployee = updateEmployee(employee, {
  salary: 35000
});

console.log(updatedEmployee);
```

**Output:**

```text
{
  id: 101,
  name: "Priyanka",
  department: "Development",
  salary: 35000
}
```

## 9. Practice Exercises

1. Create a `Product` interface with `id`, `name`, `price`, and `description`.
2. Use `Partial<Product>` to update only the price.
3. Use `Pick<Product, "id" | "name">` to create a product summary.
4. Use `Omit<Product, "description">` to create a product listing type.
5. Use `Record` to map product categories to arrays of product names.
6. Create a function that accepts `Partial<Product>` and updates an existing product without changing unspecified fields.

## 10. Key Takeaways

- `Partial<T>` — makes every property optional.
- `Required<T>` — makes every property required.
- `Pick<T, K>` — selects properties.
- `Omit<T, K>` — excludes properties.
- `Record<K, T>` — maps keys to a value type.

These utility types are useful in Angular applications, API models, forms, and TypeScript-based backend development.
