# Day 01: TypeScript Generics

## What are Generics?

Generics allow us to write reusable, type-safe code that works with different data types.

## Example: Generic Function

typescript
function identity<T>(value: T): T {
  return value;
}

const name = identity("Priyanka");
const age = identity(25);

console.log(name);
console.log(age);

### Output

text
Priyanka
25


## Runnable Exercise

Write a generic function that returns the first element of an array.

typescript
function getFirstElement<T>(items: T[]): T | undefined {
  return items[0];
}

console.log(getFirstElement([10, 20, 30]));
console.log(getFirstElement(["Angular", "TypeScript"]));
console.log(getFirstElement([]));


### Key Takeaways

- Generics help create reusable functions.
- TypeScript preserves type information.
- `T | undefined` handles empty arrays safely.

**Next topic:** TypeScript Utility Types.
