# Day 03: TypeScript Narrowing and Type Guards

## 1. What is Type Narrowing?

Type narrowing is a TypeScript feature that helps identify a more specific type of a variable within a particular block of code.

### Example: `typeof` Type Guard

```typescript
function printValue(value: string | number): void {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}

printValue("hello"); // HELLO
printValue(25.567);  // 25.57
```

**Explanation:** TypeScript narrows `value` to `string` or `number` based on the condition.

## 2. `instanceof` Type Guard

The `instanceof` operator checks whether an object belongs to a particular class.

```typescript
function printDate(value: Date | string): void {
  if (value instanceof Date) {
    console.log(value.toDateString());
  } else {
    console.log(value.toUpperCase());
  }
}

printDate(new Date());
printDate("monday");
```

## 3. Using the `in` Operator

The `in` operator checks whether a property exists on an object.

```typescript
type Developer = {
  name: string;
  skills: string[];
};

type Manager = {
  name: string;
  teamSize: number;
};

function displayInfo(person: Developer | Manager): void {
  if ("skills" in person) {
    console.log("Skills:", person.skills);
  } else {
    console.log("Team size:", person.teamSize);
  }
}

displayInfo({ name: "Priya", skills: ["Angular", "TypeScript"] });
displayInfo({ name: "Rahul", teamSize: 5 });
```

## 4. Custom Type Guards

A custom type guard is a function that checks a value's type and returns a boolean using a type predicate.

```typescript
type User = {
  id: number;
  name: string;
};

function isUser(value: unknown): value is User {
  if (typeof value !== "object" || value === null) {
    return false;
  }

  return (
    "id" in value &&
    typeof value.id === "number" &&
    "name" in value &&
    typeof value.name === "string"
  );
}

const data: unknown = {
  id: 1,
  name: "Priya"
};

if (isUser(data)) {
  console.log(data.name);
}
```

**Explanation:** The `value is User` predicate tells TypeScript that `value` is a `User` when the function returns `true`. The runtime checks validate the required properties.

## 5. Handling Union Types

Union types allow a variable to hold values of multiple possible types. Narrowing lets us safely handle each type.

```typescript
function getLength(value: string | string[]): number {
  if (typeof value === "string") {
    return value.length;
  }

  return value.length;
}

console.log(getLength("Angular")); // 7
console.log(getLength(["HTML", "CSS"])); // 2
```

## 6. Practice Exercises

Try solving these without looking at the examples.

1. Create a function that accepts `string | number` and returns a string representation of the value.
2. Write a function that accepts `Date | string` and prints the appropriate date or string value.
3. Create `Student` and `Teacher` types and use the `in` operator to distinguish them.
4. Write a custom type guard that validates an object with `id` and `email` properties.
5. Create a function that accepts `string | number | boolean` and handles all three types safely.

## 7. Key Takeaways

- Type narrowing makes code safer when working with union types.
- `typeof` checks primitive types.
- `instanceof` checks class instances.
- The `in` operator checks property existence.
- Custom type guards help validate and narrow complex values.
- Use `unknown` instead of `any` when a value's type is not yet known.

## Resources

- [TypeScript Handbook: Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- [TypeScript Handbook: Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
